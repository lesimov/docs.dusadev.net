---
icon: folder-arrow-down
---

# Configuration



## Config v1.3

```lua
----------------------------------------------------------------
----                   DUSADEV.TEBEX.IO                     ----
----------------------------------------------------------------
config = {}
config.debug = false -- For debugging purposes
config.error = true -- For debugging purposes, if you had a problem set this to true and open ticket

--- @param -- Check https://dusadev.gitbook.io/ for documentation


------------------------GENERAL OPTIONS------------------------
---------------------------------------------------------------
config.enableHudKeyInteraction = false -- If you set this true, it will open menu when desired key pushed. If you set false, it will only open menu when you type /hud
config.Voice = 'pma' -- mumble / pma / saltychat
config.defaultRefreshRate = "Medium" -- Default refresh rate for NUI Low / Medium / High / Real Time
config.mapWhileWalking = false -- Enable / disable show map while walking
config.canPassengerSeeSpeedo = true -- Enable / disable passenger can see speedometer
config.CustomMinimap = false -- Set this true if you using custom minimap

config.DefaultStatus = 5 -- Default status (1-10)
config.DefaultSpeedometer = 9 -- Default speedometer (1-10)
config.EnableInformations = true -- Enable top right corner player + server informations as default
config.DisableMinimapOption = false -- Disable minimap option from settings menu

-- In-game hour display
config.TimeFormat = '12h' -- 12h: Shows current time like 5:24 PM | 24h: Shows time like 17:24
config.TimeType = 'real' -- real: Shows real time | game: Shows game time


--------------------------HUD MENU-----------------------------
---------------------------------------------------------------
config.hudMenuCommand = 'hud'
config.hudMenuKey = 'I'
config.CursorHotkey = 'CAPITAL' -- Key list -> (https://docs.fivem.net/docs/game-references/input-mapper-parameter-ids/keyboard/)
config.CursorKeyLabel = 'CAPS'

config.MenuTabs = { -- If you want to disable any of the tabs, set to false
    ['media'] = true,
    ['vehicle'] = true,
    ['map'] = true,
}

----------------------------MONEY------------------------------
---------------------------------------------------------------
-- config.HideBlackMoney = false -- Hide black money from informations as default
-- config.HideCoin = false -- Hide special coin from informations as default


----------------------SERVER INFORMATIONS----------------------
---------------------------------------------------------------
config.Logo = "https://placehold.co/64x64/EEE/31343C" -- Logo URL [Has to be 1x1 ratio, or it will cause stretching]
config.ServerName = "Server Name" -- Server Name
config.Link = "dusadev.tebex.io" -- Server Link
config.EnableServerInfoOptions = {
    black_money = true,
    coin = true,
    user_money = true,
    server_logo = true,
    quick_info = true,
    cash_money = true,
}


-----------------------VEHICLE OPTIONS-------------------------
---------------------------------------------------------------
config.EnableRadio = true -- Enable / disable default GTA V car radio
config.CruiseControlCommand = 'cruise'
config.CruiseControlKey = "Y"

-- Engine control
config.EnableEngineControl = true -- Enable / disable engine control
config.ForceEngineOff = true -- Force engine off when player exit the vehicle
config.EngineCommand = 'engine' -- Command to toggle engine
config.EngineKey = 'X' -- Key to toggle engine
config.BrokenEngineThreshold = 985.0 -- Vehicle engine health threshold to mark as damaged at hud



----------------------GTA UI Management------------------------
---------------------------------------------------------------
-- Enabling this will increase resmon value by 0.03 - 0.05
config.EnableGTAUI = false -- Enable / disable default GTA V UI
config.HideDefaultUI = {
    vehicle_name = true, 
    area_name = true, 
    vehicle_class = true,
    street_name = true,
    cash = true,
    mp_cash = true,
    hud_components = true, 
    hud_weapons = true, 
    ammo = true,
}



---------------------------SEATBELT----------------------------
---------------------------------------------------------------
config.EnableSeatbelt = true
config.SeatbeltCommand = 'seatbelt'
config.SeatbeltKey = "K"
config.SeatbeltWarning = true
config.SeatbeltWarningSoundVolume = 0.5 -- a value between 0.0 and 1.0 
config.SeatbeltMinimumWarningSpeed = 30 -- if the value more than this value, it will run seatbelt warning sound
config.SeatbeltEjectSpeed = 120 -- Speed to eject player from vehicle (KMH)


-------------------------STRESS SYSTEM-------------------------
---------------------------------------------------------------
config.EnableStress = true
config.StressWhitelistJobs = { -- Add jobs you want to disable stress
    'police', 'ambulance'
}

config.WhitelistedWeaponStress = {
    `weapon_petrolcan`,
    `weapon_hazardcan`,
    `weapon_fireextinguisher`
}

config.RemoveStress = {
    ["eat"] = {
        min = 5,
        max = 10,
        enable = true,
        func = function()
            RegisterNetEvent('devcore_needs:client:StartEat')
            AddEventHandler('devcore_needs:client:StartEat', function()
                local val = math.random(config.RemoveStress["eat"].min, config.RemoveStress["eat"].max)
                TriggerServerEvent('hud:server:RelieveStress', val)
            end)
            RegisterNetEvent('esx_basicneeds:onEat')
            AddEventHandler('esx_basicneeds:onEat', function()
                local val = math.random(config.RemoveStress["eat"].min, config.RemoveStress["eat"].max)
                TriggerServerEvent('hud:server:RelieveStress', val)
            end) 
            RegisterNetEvent('consumables:client:Eat')
            AddEventHandler('consumables:client:Eat', function()
                local val = math.random(config.RemoveStress["eat"].min, config.RemoveStress["eat"].max)
                TriggerServerEvent('hud:server:RelieveStress', val)
            end) 
            RegisterNetEvent("esx_basicneeds:onUse")
            AddEventHandler("esx_basicneeds:onUse", function(type)
                if type == 'food' then
                    local val = math.random(config.RemoveStress["eat"].min, config.RemoveStress["eat"].max)
                    TriggerServerEvent('hud:server:RelieveStress', val)
                end
            end)
        end
    },
    ["drink"] = {
        min = 5,
        max = 10,
        enable = true,
        func = function()
            RegisterNetEvent('consumables:client:Drink')
            AddEventHandler('consumables:client:Drink', function()
                local val = math.random(config.RemoveStress["drink"].min, config.RemoveStress["drink"].max)
                TriggerServerEvent('hud:server:RelieveStress', val)
            end)
            RegisterNetEvent('consumables:client:DrinkAlcohol')
            AddEventHandler('consumables:client:DrinkAlcohol', function()
                local val = math.random(config.RemoveStress["drink"].min, config.RemoveStress["drink"].max)
                TriggerServerEvent('hud:server:RelieveStress', val)
            end) 
            RegisterNetEvent('devcore_needs:client:DrinkShot')
            AddEventHandler('devcore_needs:client:DrinkShot', function()
                local val = math.random(config.RemoveStress["drink"].min, config.RemoveStress["drink"].max)
                TriggerServerEvent('hud:server:RelieveStress', val)
            end) 
            RegisterNetEvent('devcore_needs:client:StartDrink')
            AddEventHandler('devcore_needs:client:StartDrink', function()
                local val = math.random(config.RemoveStress["drink"].min, config.RemoveStress["drink"].max)
                TriggerServerEvent('hud:server:RelieveStress', val)
            end) 
            RegisterNetEvent('esx_optionalneeds:onDrink')
            AddEventHandler('esx_optionalneeds:onDrink', function()
                local val = math.random(config.RemoveStress["drink"].min, config.RemoveStress["drink"].max)
                TriggerServerEvent('hud:server:RelieveStress', val)
            end) 
            RegisterNetEvent('esx_basicneeds:onDrink')
            AddEventHandler('esx_basicneeds:onDrink', function()
                local val = math.random(config.RemoveStress["drink"].min, config.RemoveStress["drink"].max)
                TriggerServerEvent('hud:server:RelieveStress', val)
            end) 
            RegisterNetEvent("esx_basicneeds:onUse")
            AddEventHandler("esx_basicneeds:onUse", function(type)
                if type == 'drink' then
                    local val = math.random(config.RemoveStress["drink"].min, config.RemoveStress["drink"].max)
                    TriggerServerEvent('hud:server:RelieveStress', val)
                end
            end)
        end
    },
    ["death"] = {
        enable = true,
        func = function()
            AddEventHandler('esx:onPlayerDeath', function() 
                TriggerServerEvent('hud:server:RelieveStress', 100)
            end)
            
            RegisterNetEvent('hospital:client:RespawnAtHospital')
            AddEventHandler('hospital:client:RespawnAtHospital', function() 
                TriggerServerEvent('hud:server:RelieveStress', 100)
            end)
        end
    },
    ["swim"] = {
        min = 5,
        max = 10,
        enable = true,
        func = function()
            CreateThread(function()
                while true do
                    local ped = PlayerPedId()
                    if IsPedSwimming(ped) then
                        local val = math.random(config.RemoveStress["swim"].min, config.RemoveStress["swim"].max)
                        TriggerServerEvent('hud:server:RelieveStress', val)
                    end
                    Wait(10000)

                end
            end)
        end
    },
    ["run"] = {
        min = 5,
        max = 10,
        enable = true,    
        func = function()
            CreateThread(function()
                while true do
                    local ped = PlayerPedId()
                    if IsPedRunning(ped) then
                        local val = math.random(config.RemoveStress["run"].min, config.RemoveStress["run"].max)
                        TriggerServerEvent('hud:server:RelieveStress', val)
                    end
                    Wait(10000)
                end
            end)
        end
    }
}

config.AddStress = {
    ["shoot"] = {
        min = 1, -- minimum amount to add stress
        max = 3, -- maximum amount to add stress
        enable = true,
        func = function()
            CreateThread(function()            
                while true do
                    local ped = PlayerPedId()
                    local weapon = GetSelectedPedWeapon(ped)
                    if weapon ~= `WEAPON_UNARMED` then
                        if IsPedShooting(ped) then
                            if math.random() < 0.15 and not IsWhitelistedWeaponStress(weapon) then
                                TriggerServerEvent('hud:server:GainStress', math.random(config.AddStress["shoot"].min, config.AddStress["shoot"].max))
                            end
                        end
                    else
                        Wait(1000)
                    end
                    Wait(20)
                end
            end)
        end
    },
    ["drive_fast"] = {
        min = 1, -- minimum amount to add stress
        max = 3, -- maximum amount to add stress
        enable = true,
        func = function()
            CreateThread(function()            
                while true do
                    local ped = PlayerPedId()
                    local vehicle = GetVehiclePedIsIn(ped, false)
                    if IsPedInAnyVehicle(ped, false) then
                        local speed = GetEntitySpeed(vehicle) * 3.6
                        local stressSpeed = 110 -- KMH value
                        if speed >= stressSpeed then
                            TriggerServerEvent('hud:server:GainStress', math.random(config.AddStress["drive_fast"].min, config.AddStress["drive_fast"].max))
                        end
                    end
                    Wait(10000)
                end
            end)
        end
    },
}
```

