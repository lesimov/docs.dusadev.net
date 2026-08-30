# Callbacks

**Direction:** client → server, via ox\_lib:

```lua
lib.callback('dusa_taxijob:server:bootstrap', false, function(result) ... end, payload)
```

> ⚠️ **Never include `source` in the payload.** The callback infrastructure provides it server-side; any identity or authorization claim inside the payload is ignored/untrusted. All authorization (manager, employee, duty, vehicle, distance) is enforced server-side and cannot be bypassed.

> 💡 Successful responses generally look like `{ ok = true, ... }`, failures like `{ ok = false, code = ErrorCode }`. For processing actions where `refresh ~= false`, the wrapper also attaches an up-to-date `snapshot`.
>
> `stationId` is filled from the client's open station when sent via NUI; for **external direct callback calls, send `stationId` explicitly**.

### Station & employment

| Callback                                       | Payload                                            | Success fields                          | Server behavior / auth                                                                                                                                |
| ---------------------------------------------- | -------------------------------------------------- | --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| `dusa_taxijob:server:bootstrap`                | `{ stationId?, panel? }`                           | `snapshot`                              | Initial state for a panel. `management` requires manager, `employee-menu` requires employee, `purchase-contract` requires an unpurchased station      |
| `dusa_taxijob:server:purchaseStation`          | `{ stationId, ... }`                               | Purchase result fields, `snapshot`      | Buys the station (server only uses `stationId`)                                                                                                       |
| `dusa_taxijob:server:setDuty`                  | `{ duty: boolean }`                                | `toggleClient`                          | Toggles the caller's duty. No snapshot. When `toggleClient` is true, the client syncs duty via the bridge                                             |
| `dusa_taxijob:server:dismissEmployee`          | `{ stationId?, employeeId }`                       | `snapshot`                              | Manager fires an employee. Target must belong to the caller's station; protected employees are rejected                                               |
| `dusa_taxijob:server:listNearbyPlayers`        | `{ playerSources: number[] }`                      | `players: [{ source, name, distance }]` | Manager-only filter of nearby candidates. Max 32 candidates; candidates can't be managers, can't share the job, must be physically close. No snapshot |
| `dusa_taxijob:server:employmentInvite`         | `{ targetSource }`                                 | —                                       | Manager invites a nearby eligible player. One active invite/candidate at a time. No snapshot                                                          |
| `dusa_taxijob:server:employmentInviteResponse` | `{ invitationId, decision: 'accept' \| 'reject' }` | `snapshot`                              | Invitee accepts/rejects. Expiry, manager validity, duty and proximity are re-validated                                                                |

### Fleet & vehicles

| Callback                                   | Payload                                             | Success fields                                                       | Server behavior / auth                                                                                                                           |
| ------------------------------------------ | --------------------------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `dusa_taxijob:server:fleetMap`             | `{ stationId? }`                                    | `employees`, `vehicles`                                              | Live fleet map data. Manager required. No snapshot                                                                                               |
| `dusa_taxijob:server:registerOwnedVehicle` | `{ stationId?, ownedId?, vehicleId?, id?, plate? }` | `vehicleId`, `snapshot`                                              | Registers a manager-owned vehicle into the fleet. At least one vehicle selector required; ownership list, model metadata and class are validated |
| `dusa_taxijob:server:purchaseVehicle`      | `{ stationId?, offerId?, id? }`                     | `vehicleId`, `plate`, `price`, `snapshot`                            | Manager buys from the configured vehicle shop; vault and fleet capacity validated server-side                                                    |
| `dusa_taxijob:server:deployVehicle`        | `{ stationId?, vehicleId?, id? }`                   | `vehicleId`, `networkId`, `plate`, `model`, `properties`, `snapshot` | On-duty employee spawns a garage/impound vehicle. Active vehicle, vehicle status, spawn point and (if needed) impound fee are validated          |
| `dusa_taxijob:server:payImpoundFee`        | `{ stationId?, vehicleId?, id? }`                   | `vehicleId`, `impoundFee`, `snapshot`                                | Employee pays the impound fee from the station vault to recover the vehicle                                                                      |

> ⚠️ **`returnVehicle` is declared in the contract but NOT registered in v1.0.1.** Calls currently fail with `invalid-request`. Do not build integrations on it until it is registered.

### Missions

| Callback                                     | Payload                                                     | Success fields                                | Server behavior / auth                                                                                 |
| -------------------------------------------- | ----------------------------------------------------------- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| `dusa_taxijob:server:assignMission`          | `{ stationId, missionId, driverIdentifier?, employeeId? }`  | `mission`, `missions`, `snapshot`             | Manager assigns a waiting mission. Rejected while automatic assignment is on                           |
| `dusa_taxijob:server:setAutomaticAssignment` | `{ stationId, enabled }`                                    | `automaticAssignment`, `missions`, `snapshot` | Manager toggles per-station auto-assignment                                                            |
| `dusa_taxijob:server:missionDecision`        | `{ missionId?, decision: 'accept' \| 'reject', waypoint? }` | `mission` (on accept)                         | On-duty employee accepts/rejects an offered mission. Without `missionId`, the first open offer is used |

### Taxi meter

| Callback                          | Payload               | Success fields                | Server behavior / auth                                                                                                   |
| --------------------------------- | --------------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `dusa_taxijob:server:meterOpen`   | —                     | `meter`                       | Opens a meter for the employee's active NPC mission, or a manual session for real passengers in the vehicle. No snapshot |
| `dusa_taxijob:server:meterStart`  | `{ missionId? }`      | `meter` (+ `mission` for NPC) | Requires the passenger on board (NPC) or at least one real passenger (manual). No snapshot                               |
| `dusa_taxijob:server:meterStop`   | —                     | `meter`                       | Completes the meter. Outside the mission destination radius → `destination-required`. No snapshot                        |
| `dusa_taxijob:server:meterReset`  | —                     | —                             | Deletes a manual meter or finishes a suitable NPC mission as driver cancellation. No snapshot                            |
| `dusa_taxijob:server:meterSettle` | `{ passengerSource }` | `invoiceId`                   | Sends a 120-second invoice to the registered nearby passenger for a completed **manual** meter. No snapshot              |

### Invoices & vault

| Callback                             | Payload                                                     | Success fields             | Server behavior / auth                                                                                                       |
| ------------------------------------ | ----------------------------------------------------------- | -------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `dusa_taxijob:server:invoiceApprove` | `{ invoiceId, account: 'bank' \| 'cash' }`                  | —                          | Passenger pays by choosing the account. Driver share and station vault split run in a single server transaction. No snapshot |
| `dusa_taxijob:server:invoiceReject`  | `{ invoiceId }`                                             | —                          | Passenger rejects the invoice. No snapshot                                                                                   |
| `dusa_taxijob:server:moveVaultFunds` | `{ stationId, direction: 'deposit' \| 'withdraw', amount }` | Economy result, `snapshot` | Moves funds between the employee's account and the station vault. Amount must be a positive money value                      |
