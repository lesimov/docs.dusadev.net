# Errors & Integration

Server callbacks fail with `{ ok = false, code = ErrorCode }`. These codes are **not player-facing text** — translate them in your locale/application layer.

| Category    | Codes                                                                                                                                                        |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Request     | `invalid-request`                                                                                                                                            |
| Employment  | `not-employee`, `not-manager`, `duty-required`, `employee-not-found`, `player-not-nearby`, `player-already-employed`, `employee-protected`, `job-set-failed` |
| Station     | `station-not-found`, `station-owned`, `already-owner`, `capacity-reached`                                                                                    |
| Invitations | `invitation-pending`, `invitation-not-found`, `invitation-expired`                                                                                           |
| Economy     | `insufficient-funds`                                                                                                                                         |
| Vehicles    | `vehicle-not-found`, `vehicle-unavailable`, `active-vehicle`                                                                                                 |
| Missions    | `mission-not-found`, `mission-unavailable`, `active-mission`, `no-passenger`, `destination-required`                                                         |
| Spawning    | `spawn-failed`, `spawn-point-blocked`                                                                                                                        |
| Bridge      | `bridge-unavailable`                                                                                                                                         |

### Integration rules

1. **Do not imitate management actions with `TriggerServerEvent`.** Use the documented callbacks and their payload validation.
2. **Treat `stateChanged`, mission, meter and invoice events as server truth.** Triggering them from your own resource creates race conditions and authorization violations.
3. **`GetStationForMugshots` is exclusive to `dusa_taxiapp`.** Any other resource must use `GetPublicStation`; the `source` field cannot be obtained without a source/export access change.
4. **`returnVehicle` is not registered in v1.0.1** (declared in the contract only). Calls fail with `invalid-request` — do not depend on it.

### Dependency touchpoints

| Dependency         | Side                            | Usage                                                                                                                          |
| ------------------ | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `dusa_bridge`      | Client + server                 | Player, job, duty, notification & money framework adaptation. Mandatory manifest dependency.                                   |
| `ox_lib`           | Client + server                 | Locales and callback transport. Mandatory manifest dependency.                                                                 |
| `oxmysql`          | Server                          | Persistent station/vehicle/economy data. Mandatory manifest dependency.                                                        |
| `lb-phone`         | Server, optional                | `GetEquippedPhoneNumber(source)` for public employee phone numbers                                                             |
| `MugShotBase64`    | Client, optional                | Player ped → data-URL avatar                                                                                                   |
| Key/fuel resources | Client/server, config-dependent | Adapted via `editable/vehicle.lua` and `server/vehicles.lua`. Their events/exports are **not** part of the Taxi Job public API |
