# Exports

-----

## Server Exports

### GetVehicleOrderStatus

```lua
local ret = exports.dusa_mechanic:GetVehicleOrderStatus(vehicleNetId)
-- ret: 'pending' | 'in_progress' | 'completed' | nil
```

-----

### GetVehicleOrderStatuses

```lua
local ret = exports.dusa_mechanic:GetVehicleOrderStatuses()
-- ret: { [netId] = 'pending', [netId2] = 'completed', ... }
```

-----

### IsVehicleInAssembly

```lua
local ret = exports.dusa_mechanic:IsVehicleInAssembly(vehicleNetId)
-- ret: true | false
```

-----
