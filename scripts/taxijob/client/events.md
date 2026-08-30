# Events

> ⚠️ **These events are server-authoritative.** They are sent by the server via `TriggerClientEvent`. External resources must **never** trigger them — doing so creates race conditions and authorization violations. Treat incoming payloads as trusted server data.

| Event                                           | Payload                                   | Effect                                                                                               |
| ----------------------------------------------- | ----------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `dusa_taxijob:client:openPanel`                 | `panel: string, stationId?: string`       | Receives bootstrap data, broadcasts the snapshot, opens the NUI panel with focus                     |
| `dusa_taxijob:client:stateChanged`              | `snapshot: Snapshot`                      | Refreshes the full UI state of the open panel                                                        |
| `dusa_taxijob:client:employmentInviteReceived`  | `invitation: EmploymentInvitation`        | Opens the job-invite overlay                                                                         |
| `dusa_taxijob:client:employmentInviteCancelled` | `invitationId: string`                    | Closes the invite overlay                                                                            |
| `dusa_taxijob:client:employeeDismissed`         | —                                         | Clears local snapshot/station data and closes the open panel                                         |
| `dusa_taxijob:client:missionOffered`            | `mission: Mission`                        | Adds a mission offer for the employee                                                                |
| `dusa_taxijob:client:missionCancelled`          | `mission: Mission & { reason?: string }`  | Cancels an offer or active mission (`reason` may be `rejected`)                                      |
| `dusa_taxijob:client:missionAccepted`           | `mission: Mission`                        | Activates the mission and sets up pickup routing                                                     |
| `dusa_taxijob:client:missionPassenger`          | `mission: Mission`                        | Notifies the boarding stage of the NPC passenger                                                     |
| `dusa_taxijob:client:missionDestination`        | `mission: Mission`                        | Notifies the arrival stage and meter-open eligibility                                                |
| `dusa_taxijob:client:missionCompleted`          | `mission: Mission`                        | Completes the mission and clears routing/meter state                                                 |
| `dusa_taxijob:client:missionFailed`             | `mission: Mission & { reason?: string }`  | Fails the mission; an active meter enters error state                                                |
| `dusa_taxijob:client:meterChanged`              | `meter: Meter`                            | Updates the meter view for driver/passengers in the vehicle. `canControl` is `false` for non-drivers |
| `dusa_taxijob:client:invoiceReceived`           | `invoice: Invoice`                        | Opens the transaction form overlay on the passenger                                                  |
| `dusa_taxijob:client:invoicePaid`               | —                                         | Removes invoice-waiting state on the driver                                                          |
| `dusa_taxijob:client:invoiceDeclined`           | `reason?: string`                         | Removes invoice-waiting state; `expired` is parsed specially                                         |
| `dusa_taxijob:client:invoiceCancelled`          | `invoiceId: string, reason?: string`      | Closes the open transaction form on the passenger                                                    |
| `dusa_taxijob:client:vehicleSpawned`            | `payload: DeployPayload`                  | Applies properties to the network vehicle; runs fuel/key integrations                                |
| `dusa_taxijob:client:vehicleReturning`          | `{ vehicleId, networkId, plate, origin }` | Removes keys, exits the client from the vehicle and deletes it                                       |

#### Panel names

`openPanel` uses the following panel identifiers: `management`, `employee-menu`, `purchase-contract`, `employment-invitation`, `taxi-meter`, `transaction-form`.
