---
icon: question
---

# How to give keys to player? (e.g on dealerships)

If the gallery system or similar systems you use haven't provided an integration, you can easily perform the integration yourself by following the steps below.





### Client Side

```lua
function GiveVehicleKeys(plate, vehicle)
    exports.dusa_vehiclekeys:GiveKeys(plate)
end
```

If you need to embed it into

```lua
RegisterNetEvent('qb-vehicleshop:client:TestDrive', function()
    if not inTestDrive and ClosestVehicle ~= 0 then
        inTestDrive = true
        local prevCoords = GetEntityCoords(PlayerPedId())
        tempShop = insideShop -- temp hacky way of setting the shop because it changes after the callback has returned since you are outside the zone
        QBCore.Functions.TriggerCallback('qb-vehicleshop:server:spawnvehicle', function(netId, properties, vehPlate)
            local timeout = 5000
            local startTime = GetGameTimer()
            while not NetworkDoesNetworkIdExist(netId) do
                Wait(10)
                if GetGameTimer() - startTime > timeout then
                    return
                end
            end
            local veh = NetworkGetEntityFromNetworkId(netId)
            NetworkRequestControlOfEntity(veh)
            SetEntityAsMissionEntity(veh, true, true)
            Citizen.InvokeNative(0xAD738C3085FE7E11, veh, true, true)
            SetVehicleNumberPlateText(veh, vehPlate)
            exports['LegacyFuel']:SetFuel(veh, 100)
            
            -- HERE
            exports.dusa_vehiclekeys:GiveKeys(vehPlate)
            --

            TaskWarpPedIntoVehicle(PlayerPedId(), veh, -1)
            SetVehicleEngineOn(veh, true, true, false)
            testDriveVeh = netId
            QBCore.Functions.Notify(Lang:t('general.testdrive_timenoti', { testdrivetime = Config.Shops[tempShop]['TestDriveTimeLimit'] }), "success")
        end, 'TESTDRIVE', Config.Shops[tempShop]['ShowroomVehicles'][ClosestVehicle].chosenVehicle, Config.Shops[tempShop]['TestDriveSpawn'], true) 

        createTestDriveReturn()
        startTestDriveTimer(Config.Shops[tempShop]['TestDriveTimeLimit'] * 60, prevCoords)
    else
        QBCore.Functions.Notify(Lang:t('error.testdrive_alreadyin'), 'error')
    end
end)
```



### Server Side

Actually, there is no change on the server side, only the player's ID should be sent (source)

```lua
function GiveVehicleKeys(source, plate, vehicle)
    local src = source
    exports.dusa_vehiclekeys:GiveKeys(src, plate)
end
```
