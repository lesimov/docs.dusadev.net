---
icon: equals
---

# Events



## Event Triggers



### vehiclekeys:client:setOwner

Determines the owner of the vehicle with the specified license plate and gives the key to player

```lua
TriggerClientEvent('vehiclekeys:client:SetOwner', playerId, plate)
```

* playerId: `number`
* plate: `string`&#x20;



### dusa\_vehiclekeys:client:GiveKeys

The player gives the key of the nearest vehicle they own to the person next to them

```lua
TriggerClientEvent('dusa_vehiclekeys:client:GiveKeys', playerId)
```

* playerId: `number`



### dusa\_vehiclekeys:client:RemoveKeys

Removes the specified license plate from the player's list of owned keys.

```lua
TriggerClientEvent('dusa_vehiclekeys:client:RemoveKeys', playerId, plate)
```

* playerId: `number`
* plate: `string`&#x20;



### dusa\_vehiclekeys:client:ToggleEngine

If the player is inside a vehicle, they turn the vehicle's engine on or off.

```lua
TriggerClientEvent('dusa_vehiclekeys:client:ToggleEngine', playerId)
```

* playerId: `number`&#x20;



