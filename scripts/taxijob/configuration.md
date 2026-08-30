# Configuration

All settings live in `config/shared.lua` under the `TaxiConfig` table.

## General

| Key             | Default    | Description                                                                                  |
| --------------- | ---------- | -------------------------------------------------------------------------------------------- |
| `debug`         | `false`    | Enables debug logging                                                                        |
| `locale`        | `'en'`     | UI language                                                                                  |
| `interaction`   | `'textui'` | How players interact with station points                                                     |
| `useMockData`   | `false`    | **Demo mode** — serves a bundled mock snapshot instead of live data. Keep off in production. |
| `currency`      | `'USD'`    | Currency label shown in the UI                                                               |
| `playerAccount` | `'bank'`   | Account used for station purchases                                                           |

## Commands

| Key                  | Default         | Description                                     |
| -------------------- | --------------- | ----------------------------------------------- |
| `managementCommand`  | `'taxiyonetim'` | Opens the station management panel for managers |
| `employeeCommand`    | `'taksimenu'`   | Opens the employee menu                         |
| `testMissionCommand` | `'testgorev'`   | Spawns a test mission (development only)        |

## Blips

| Key                | Default | Description                   |
| ------------------ | ------- | ----------------------------- |
| `blips.enabled`    | `true`  | Show station blips on the map |
| `blips.sprite`     | `198`   | Blip sprite ID                |
| `blips.color`      | `5`     | Blip color ID                 |
| `blips.scale`      | `0.8`   | Blip size                     |
| `blips.shortRange` | `true`  | Blip only visible when nearby |

## Economy

| Key                     | Default  | Description                               |
| ----------------------- | -------- | ----------------------------------------- |
| `economy.societyShare`  | `0.80`   | Station vault share of each fare (80%)    |
| `economy.driverShare`   | `0.20`   | Driver share of each fare (20%)           |
| `economy.driverAccount` | `'bank'` | Where driver payouts are sent             |
| `economy.tipAccount`    | `'cash'` | Where tips are sent                       |
| `economy.impoundFee`    | `2500`   | Fee to release an impounded fleet vehicle |

## Progression

Levels gate employee and vehicle capacity. Add or edit entries freely:

| Level | Required trips | Employee capacity | Vehicle capacity |
| ----- | -------------- | ----------------- | ---------------- |
| 1     | 0              | 3                 | 5                |
| 2     | 25             | 5                 | 5                |
| 3     | 75             | 10                | 10               |

## Taxi Meter

| Key                              | Default  | Description                                            |
| -------------------------------- | -------- | ------------------------------------------------------ |
| `meter.startKey`                 | `'B'`    | Key to open/control the meter                          |
| `meter.openingFare`              | `30.0`   | Base fare when the meter starts                        |
| `meter.ratePerUnit`              | `18.0`   | Price per distance unit                                |
| `meter.maxFare`                  | `1500.0` | Fare cap                                               |
| `meter.unit`                     | `'km'`   | `'km'` or `'mile'`                                     |
| `meter.priceIntervalMs`          | `4000`   | How often the fare ticks                               |
| `meter.maxSpeedMetersPerSecond`  | `70.0`   | Speed above which distance stops counting (anti-cheat) |
| `meter.manualIdleTimeoutSeconds` | `120`    | Idle timeout for manual meters                         |

## Missions

| Key                                                  | Default          | Description                                                                       |
| ---------------------------------------------------- | ---------------- | --------------------------------------------------------------------------------- |
| `missions.automaticAssignment`                       | `true`           | Auto-assign waiting missions to on-duty drivers (managers can toggle per station) |
| `missions.dispatchMinSeconds` / `dispatchMaxSeconds` | `180` / `300`    | Delay range before a new taxi call spawns                                         |
| `missions.offerTimeoutMinSeconds` / `MaxSeconds`     | `600` / `900`    | How long an offered mission waits for a decision                                  |
| `missions.pickupTimeoutSeconds`                      | `300`            | Time allowed to reach the passenger                                               |
| `missions.tripTimeoutSeconds`                        | `900`            | Time allowed to complete the trip                                                 |
| `missions.completionRadius`                          | `18.0`           | Distance to finish a trip                                                         |
| `missions.pickupRadius`                              | `28.0`           | Distance that counts as reaching the pickup                                       |
| `missions.tip.baseChance`                            | `0.25`           | Base chance the passenger tips                                                    |
| `missions.tip.fastPickupBonus`                       | `0.45`           | Extra tip chance for fast pickups                                                 |
| `missions.tip.minAmount` / `maxAmount`               | `25` / `90`      | Tip amount range                                                                  |
| `missions.passengerModels`                           | _(5 peds)_       | NPC passenger ped models                                                          |
| `missions.points`                                    | _(10 locations)_ | Pickup/destination points: `label`, `address`, `coords` (vector4)                 |

## Vehicles & Fuel/Keys

| Key                      | Default             | Description                                                                        |
| ------------------------ | ------------------- | ---------------------------------------------------------------------------------- |
| `vehicle.fuelSystem`     | `'ox_fuel'`         | Fuel resource integration                                                          |
| `vehicle.keySystem`      | `'auto'`            | `'auto'` detects the first supported key resource; set a resource name to override |
| `vehicle.spawnFuel`      | `100.0`             | Fuel level on spawn                                                                |
| `vehicle.shop`           | `taxi — $90,000`    | Purchasable fleet vehicles: `{ id, model, price }`                                 |
| `vehicle.blockedClasses` | _(classes 8,10–21)_ | Vehicle classes that cannot be registered to a fleet                               |

## Stations

Each entry in `TaxiConfig.stations` defines a buyable taxi station:

```lua
{
    id = 'downtown',                -- unique station id
    label = 'Downtown Cab Co.',     -- display name
    job = 'taxi_downtown',          -- the job this station is bound to
    bossGrade = 4,                  -- grade treated as manager (when managerUsesBossFlag)
    price = 1250000,                -- purchase price
    starterVehicles = { 'taxi', 'taxi' },  -- vehicles included with purchase
    blip = { name = '...', coords = vector3(...) },
    purchase   = { coords = vector3(...), size = vector3(...), rotation = 58.0 },  -- buy interaction zone
    management = { coords = ..., size = ..., rotation = ... },  -- management panel zone
    employee   = { coords = ..., size = ..., rotation = ... },  -- employee menu zone
    garage = {
        spawn = vector4(...),                       -- vehicle spawn point
        returnZone = { coords = ..., size = ..., rotation = ... },  -- where vehicles are returned
    },
},
```

| Key               | Description                                                           |
| ----------------- | --------------------------------------------------------------------- |
| `id`              | Unique identifier — also the `stationId` used across the API          |
| `job`             | Framework job name bound to the station. Employees must hold this job |
| `bossGrade`       | Minimum grade counted as manager (`permissions.managerUsesBossFlag`)  |
| `app.location`    | Location label shown in the companion app                             |
| `starterVehicles` | Models granted to the buyer on purchase                               |

> ⚠️ `permissions.managerUsesBossFlag = true` means manager permission comes from the job grade (`bossGrade`). Employees can never bypass server-side authorization regardless of client input.

## Recruitment

| Key                                | Default        | Description                            |
| ---------------------------------- | -------------- | -------------------------------------- |
| `recruitment.radius`               | `5.0`          | Max distance to invite a nearby player |
| `recruitment.inviteTimeoutSeconds` | `30`           | Invitation expiry                      |
| `employment.defaultJob`            | `'unemployed'` | Job check for recruitment candidates   |
