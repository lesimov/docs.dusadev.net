# Exports

These exports are registered in `server/public_api.lua` and must be called **from the server side** of other resources.

```lua
local stations = exports['dusa_taxijob']:GetPublicStations()
local station = exports['dusa_taxijob']:GetPublicStation(stationId)
```

| Export                             | Parameters          | Returns                                                                                                        | Purpose / access                                                                    |
| ---------------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `GetPublicStations()`              | None                | `{ ok = true, stations: PublicStation[] }`                                                                     | Public summary of all configured stations. No caller restriction.                   |
| `GetPublicStation(stationId)`      | `stationId: string` | `{ ok = true, station: PublicStation }` — or `invalid-request` / `station-not-found`                           | Single station including its employee list. No caller restriction.                  |
| `GetStationForMugshots(stationId)` | `stationId: string` | Same as `GetPublicStation` **plus** live employee `source` values — or `invalid-request` / `station-not-found` | ⚠️ **Restricted:** only succeeds when the calling resource is named `dusa_taxiapp`. |

### `PublicStation`

```ts
type PublicEmployee = {
  name: string;
  role: string;
  phoneNumber: string | null; // set when lb-phone is running and the employee is online
  dutyStatus: string;
  activityStatus: string;
  source?: number | null; // only present via GetStationForMugshots
};

type PublicStation = {
  id: string;
  name: string;
  location: string;
  locationCoords: { x: number; y: number; z: number } | null;
  company: string; // the station's job name
  purchased: boolean;
  employeeCount: number;
  onDutyCount: number;
  employees?: PublicEmployee[]; // absent in the list export, present in single-station exports
};
```

> 💡 Money values are numbers, coordinates are `{ x, y, z }` tables, and timestamps are Unix epoch seconds.
