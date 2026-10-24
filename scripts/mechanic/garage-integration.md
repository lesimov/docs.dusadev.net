# Garage Integration

Mechanic upgrades (stance, ECU tune, AWD, nitro color, illegal mods) are saved per plate by `dusa_mechanic`. Your garage only has to **restore** them when it spawns a vehicle. You do not need a "store" hook: every completed tuning order, assembly or stance save is committed automatically.

{% hint style="info" %}
Most "my stance / camber / tune resets after taking the car out of the garage" reports are a missing restore call. Follow the steps below once and the upgrades survive garage cycles, `/dv` and server restarts.
{% endhint %}

***

## What you need to add

{% stepper %}
{% step %}
### Find your garage's server-side spawn

Open your garage resource and find the **server** code that runs after the vehicle is spawned, its plate is set and its normal vehicle properties (colors, mods, wheels) are applied.

If your garage spawns vehicles only on the client, use the server event/callback your garage already calls after spawning. The restore exports are **server-only**.
{% endstep %}

{% step %}
### Restore stance (required)

Add this line **after** the vehicle properties are applied:

```lua
-- vehicle = server entity handle, plate = the vehicle's final plate
local netId = NetworkGetNetworkIdFromEntity(vehicle)

local result = exports.dusa_mechanic:RestoreVehicleStance(netId, plate)
if not result.success then
    print(('[garage] Stance restore failed for %s: %s'):format(plate, result.error))
end
```

This restores camber, wheel offset, wheel width and suspension height.
{% endstep %}

{% step %}
### Restore the rest of the mechanic layer (recommended)

To also bring back ECU tune, AWD/wheel power, nitro color and illegal mods, call this **before** `RestoreVehicleStance`:

```lua
exports.dusa_mechanic:ApplyStoredVehicleMods(netId, plate)
local result = exports.dusa_mechanic:RestoreVehicleStance(netId, plate)
```

{% hint style="warning" %}
`ApplyStoredVehicleMods` also restores the engine/body health and fuel level saved at the vehicle's last mechanic save. If your garage keeps its own damage and fuel, skip this call and use only `RestoreVehicleStance`.
{% endhint %}
{% endstep %}

{% step %}
### Restart and test

1. Restart your garage resource.
2. Apply stance or a tune at the mechanic and complete the order.
3. Store the vehicle, then take it out again. The upgrades should come back within about half a second.
{% endstep %}
{% endstepper %}

***

## Example: qbx\_garages

```lua
-- After qbx.spawnVehicle(...) returns netId and the vehicle props are applied
local netId, veh = qbx.spawnVehicle({ model = ..., spawnSource = ..., props = playerVehicle.props })

exports.dusa_mechanic:ApplyStoredVehicleMods(netId, playerVehicle.props.plate)
exports.dusa_mechanic:RestoreVehicleStance(netId, playerVehicle.props.plate)
```

***

## Call order

| Order | What runs                                                | Why                                                    |
| ----- | -------------------------------------------------------- | ------------------------------------------------------ |
| 1     | Garage spawns vehicle, sets plate, applies its own props | Mechanic upgrades are built on top of the normal props |
| 2     | `ApplyStoredVehicleMods(netId, plate)` (optional)        | ECU, AWD, nitro color, illegal mods                    |
| 3     | `RestoreVehicleStance(netId, plate)`                     | Stance always last, so nothing overwrites it           |

***

## Return values

### RestoreVehicleStance

| Result                              | Meaning                                                                                                                        |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `{ success = true, found = true }`  | Saved stance found and applied                                                                                                 |
| `{ success = true, found = false }` | Normal: this vehicle has no saved stance                                                                                       |
| `error = 'PLATE_MISMATCH'`          | Plate passed does not match the spawned vehicle, or the plate was set **after** the call. Call it after the final plate is set |
| `error = 'INVALID_ENTITY'`          | You passed an entity handle instead of a network ID                                                                            |
| `error = 'DATABASE_NOT_READY'`      | Mechanic database was still starting. Retry from your spawn flow a moment later                                                |
| `error = 'ENTITY_CHANGED'`          | The vehicle was deleted or replaced while restoring                                                                            |
| `error = 'LOAD_FAILED'`             | Database read failed. Check your server console for SQL errors                                                                 |
| `error = 'MODULE_DISABLED'`         | Both the `stance` and `tuning` modules are disabled in the mechanic config                                                     |

### ApplyStoredVehicleMods

| Result                                | Meaning                                                                         |
| ------------------------------------- | ------------------------------------------------------------------------------- |
| `{ success = true }`                  | Applied immediately                                                             |
| `{ success = true, deferred = true }` | Nobody is in the vehicle yet. It is applied automatically when a player gets in |
| `error = 'NOT_STORED'`                | Normal: no saved mechanic layer for this plate                                  |

***

## Common issues

<details>

<summary>Stance comes back, then resets after a few seconds</summary>

Another script is setting wheel offsets or camber after spawn. Make sure `RestoreVehicleStance` runs last, after every other script that changes the vehicle's wheels.

</details>

<details>

<summary>I get PLATE_MISMATCH on every spawn</summary>

Your garage sets the plate after the point where you added the call. Move the call below the line that sets the plate and applies the props.

</details>

<details>

<summary>Can I trigger the restore from a client event?</summary>

No. Both exports are server-only. Do not create a client event that calls them without checks. Call them from your garage's existing server spawn flow.

</details>

<details>

<summary>Do I need to change my database?</summary>

No. Mechanic stores its data in its own tables. No SQL migration and no changes to your framework's vehicle table are needed.

</details>

<details>

<summary>I was using RestoreVehicleProps before</summary>

`RestoreVehicleProps` is deprecated and no longer returns saved data. Replace it with the calls on this page.

</details>
