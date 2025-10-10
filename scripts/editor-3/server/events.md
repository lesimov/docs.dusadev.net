---
icon: equals
---

# Events



## Event Triggers



### dusa\_vehiclekeys:server:AcquireVehicleKeys

Enables the player to drive the defined plate vehicle

```lua
TriggerServerEvent('dusa_vehiclekeys:server:AcquireVehicleKeys', plate)
```

* plate: `string`&#x20;



### dusa\_vehiclekeys:server:GiveKeys

Give the player the key for the defined plate

```lua
TriggerServerEvent('dusa_vehiclekeys:server:GiveKeys', plate)
```

* plate: `string`&#x20;



### dusa\_vehiclekeys:server:RemoveKeys

Removes the specified license plate from the list of keys owned by player

```lua
TriggerServerEvent('dusa_vehiclekeys:server:RemoveKeys', plate)
```

* plate: `string`&#x20;



