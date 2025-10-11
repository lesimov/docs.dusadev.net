---
icon: circle-small
---

# Shared Functions

This page documents shared utility functions available in both client and server contexts.

***

## Weapon Functions

### Functions.IsHuntingWeapon

Checks if a weapon is registered as a hunting weapon.

```lua
local isHuntingWeapon = Functions.IsHuntingWeapon(weaponHash)
```

**Parameters**:

* `weaponHash` (string|number) - Weapon name or hash

**Returns**: `boolean` - Whether the weapon is a hunting weapon

**Usage Examples**:

**Client-Side**:

```lua
-- Check if player is holding a hunting weapon
local currentWeapon = GetSelectedPedWeapon(PlayerPedId())
if Functions.IsHuntingWeapon(currentWeapon) then
    print("Holding a hunting weapon")
end

-- Check by weapon name
if Functions.IsHuntingWeapon('WEAPON_DHR31') then
    print("DHR31 is a hunting weapon")
end
```

**Server-Side**:

```lua
-- Validate weapon before processing hunt
RegisterNetEvent('hunting:validateKill', function(weaponUsed)
    if Functions.IsHuntingWeapon(weaponUsed) then
        -- Process the kill
    else
        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Hunting', 'You must use a hunting weapon!' }
        })
    end
end)
```

**Configuration**: Hunting weapons are defined in [Client Config](../configuration/client.md#hunting-restrictions):

```lua
Config.HuntingWeapons = {
    'WEAPON_DHR31',
    -- Add more weapons...
}
```

**Use Cases**:

* Validating kills
* UI indicators
* Permission checks
* Custom mechanics

***

## Inventory Functions

### Functions.GetInventoryImage

Gets the correct inventory image path for an item with automatic webp/png detection.

```lua
local imagePath = Functions.GetInventoryImage(itemName)
```

**Parameters**:

* `itemName` (string) - Item name (e.g., `'deer_beef'`)

**Returns**: `string` - Full NUI image path

**Usage Examples**:

**Client-Side**:

```lua
-- Get image for UI
local imagePath = Functions.GetInventoryImage('deer_beef')
-- Returns: "nui://ox_inventory/web/images/deer_beef.png"

-- Use in custom UI
SendNUIMessage({
    action = 'showItem',
    image = Functions.GetInventoryImage('hunting_bait')
})
```

**Server-Side**:

```lua
-- Send item data to client with images
local items = {
    { name = 'deer_beef', image = Functions.GetInventoryImage('deer_beef') },
    { name = 'hide', image = Functions.GetInventoryImage('hide') }
}

TriggerClientEvent('myResource:showItems', source, items)
```

**Configuration**: Image extension can be forced in [Shared Config](../configuration/shared.md#inventory-image-extension):

```lua
Shared.InventoryImageExtension = nil  -- Auto-detect
-- OR
Shared.InventoryImageExtension = 'png'  -- Force PNG
-- OR
Shared.InventoryImageExtension = 'webp'  -- Force WEBP
```

**How It Works**:

1. Checks `Shared.InventoryImageExtension` for forced extension
2. If nil, auto-detects (tries webp first, then png)
3. Returns full nui:// path

**Use Cases**:

* Custom UIs
* Item displays
* Inventory integration
* Shop systems

***

## Vehicle Functions (Server-Side)

### Functions.SpawnVehicle

Spawns a vehicle on the server with proper networking.

```lua
local netId, vehicle = Functions.SpawnVehicle(params)
```

**Parameters**:

*   `params` (table) - Vehicle spawn parameters

    ```lua
    {
        model = 'sandking',  -- Vehicle model
        spawnSource = vector4(x, y, z, heading),  -- Spawn location
        warp = playerId,  -- Optional: Player ID to warp into vehicle
        plate = 'PLATE123',  -- Optional: Custom plate
        props = {}  -- Optional: Vehicle properties
    }
    ```

**Returns**:

* `netId` (number) - Network ID of the vehicle
* `vehicle` (number) - Vehicle entity handle

**Usage Examples**:

```lua
-- Basic spawn
local netId, veh = Functions.SpawnVehicle({
    model = 'sandking',
    spawnSource = vector4(-677.869, 5826.417, 17.331, 134.575)
})
print("Spawned vehicle with netId: " .. netId)

-- Spawn and warp player
local netId, veh = Functions.SpawnVehicle({
    model = 'sandking',
    spawnSource = vector4(-677.869, 5826.417, 17.331, 134.575),
    warp = source  -- Warps player into driver seat
})

-- Spawn with custom plate
local netId, veh = Functions.SpawnVehicle({
    model = 'sandking',
    spawnSource = vector4(-677.869, 5826.417, 17.331, 134.575),
    plate = 'HUNT001'
})

-- Spawn with properties
local netId, veh = Functions.SpawnVehicle({
    model = 'sandking',
    spawnSource = vector4(-677.869, 5826.417, 17.331, 134.575),
    props = {
        plate = 'HUNT001',
        color1 = 0,
        color2 = 0
    }
})
```

**Advanced Example**:

```lua
-- Custom hunting vehicle rental
RegisterCommand('customrent', function(source)
    local Player = Framework.GetPlayer(source)
    if not Player then return end

    -- Spawn vehicle
    local netId, veh = Functions.SpawnVehicle({
        model = 'sandking',
        spawnSource = vector4(-677.869, 5826.417, 17.331, 134.575),
        warp = source
    })

    -- Give keys
    local plate = GetVehicleNumberPlateText(veh)
    Functions.GiveVehicleKeys(source, veh, plate)

    -- Mark as rental
    Entity(veh).state:set('customRental', true, true)
    Entity(veh).state:set('rentalOwner', source, true)

    TriggerClientEvent('chat:addMessage', source, {
        args = { 'Rental', 'Vehicle spawned!' }
    })
end, false)
```

**Notes**:

* Automatically handles entity ownership
* Supports vehicle properties
* Includes timeout handling
* Works with all vehicle models

***

### Functions.GiveVehicleKeys

Gives vehicle keys to a player (multi-script support).

```lua
Functions.GiveVehicleKeys(source, vehicle, plate)
```

**Parameters**:

* `source` (number) - Player server ID
* `vehicle` (number) - Vehicle entity handle
* `plate` (string) - Vehicle plate number

**Supported Key Systems**:

* dusa\_vehiclekeys
* wasabi\_carlock
* qb-vehiclekeys
* qs-vehiclekeys
* vehicles\_keys
* ak47\_vehiclekeys
* Renewed-Vehiclekeys

**Usage Example**:

```lua
-- After spawning vehicle
local netId, veh = Functions.SpawnVehicle({
    model = 'sandking',
    spawnSource = vector4(x, y, z, heading)
})

local plate = GetVehicleNumberPlateText(veh)
Functions.GiveVehicleKeys(source, veh, plate)
```

**How It Works**:

1. Detects installed key system
2. Calls appropriate export
3. Automatically handles different formats
4. Silently fails if no key system installed

***

### Functions.RemoveVehicleKeys

Removes vehicle keys from a player.

```lua
Functions.RemoveVehicleKeys(source, vehicle, plate)
```

**Parameters**:

* `source` (number) - Player server ID
* `vehicle` (number) - Vehicle entity handle
* `plate` (string) - Vehicle plate number

**Supported Systems**: Currently supports:

* Renewed-Vehiclekeys

**Usage Example**:

```lua
-- When returning rental vehicle
local plate = GetVehicleNumberPlateText(vehicle)
Functions.RemoveVehicleKeys(source, vehicle, plate)
DeleteEntity(vehicle)
```

**Note**: Add your key system integration in `game/opensource/functions.lua`

***

## Debug Functions

### DebugLog

Prints debug messages when debug mode is enabled.

```lua
DebugLog(message, type)
```

**Parameters**:

* `message` (string) - Debug message
* `type` (string) - Debug type (for filtering)

**Debug Types**:

```lua
local debugTypes = {
    ['createPed'] = true,
    ['cleanedUpAnimal'] = false,
    ['requestModel'] = false,
    ['weaponAim'] = true,
    ['removeAnimal'] = true
}
```

**Usage Example**:

```lua
DebugLog('Animal spawned: deer', 'createPed')
DebugLog('Weapon aimed at target', 'weaponAim')
```

**Enable Debug Mode**:

```lua
Shared.Debug = true
```

***

## Utility Functions

### Functions.HasLicense

Checks if player has a hunting license.

```lua
local hasLicense = Functions.HasLicense()
```

**Returns**: `boolean` - Always returns true (for customization)

**Customization**: Edit in `game/opensource/functions.lua` to add license checks:

```lua
function Functions.HasLicense()
    -- Add your license check logic
    local Player = Framework.GetPlayer(source)
    return Player.hasItem('hunting_license')
end
```

***

### Functions.GetCustomTitle

Gets custom title for player (for integration with other systems).

```lua
local customTitle = Functions.GetCustomTitle()
```

**Returns**: `string|boolean` - Custom title or false

**Customization**:

```lua
function Functions.GetCustomTitle()
    -- Integrate with your rank/title system
    local Player = Framework.GetPlayer(source)
    return Player.getCustomRank() or false
end
```

***

### Functions.randomFromTable

Gets a random element from a table.

```lua
local element, index = Functions.randomFromTable(table)
```

**Parameters**:

* `table` (table) - Table to select from

**Returns**:

* `element` - Random element
* `index` (number) - Index of selected element

**Usage Example**:

```lua
local scenarios = {
    'WORLD_HUMAN_AA_COFFEE',
    'WORLD_HUMAN_AA_SMOKE',
    'WORLD_HUMAN_SMOKING'
}

local randomScenario = Functions.randomFromTable(scenarios)
TaskStartScenarioInPlace(ped, randomScenario)
```

***

## Integration Examples

### Example 1: Custom Weapon Validation

```lua
-- Only allow hunting weapons in hunting zones
CreateThread(function()
    while true do
        Wait(1000)

        local playerPed = PlayerPedId()
        local weapon = GetSelectedPedWeapon(playerPed)

        if IsPlayerInHuntingZone() then
            if not Functions.IsHuntingWeapon(weapon) then
                -- Remove non-hunting weapons
                SetCurrentPedWeapon(playerPed, `WEAPON_UNARMED`, true)
                Notify('Only hunting weapons allowed in this zone', 'error')
            end
        end
    end
end)
```

### Example 2: Custom Vehicle Spawn System

```lua
-- Server-side: Advanced vehicle rental
RegisterCommand('advancedrent', function(source, args)
    local vehicleModel = args[1] or 'sandking'
    local Player = Framework.GetPlayer(source)

    if not Player then return end

    -- Charge rental fee
    if not Player.RemoveMoney('bank', 1000) then
        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Rental', 'Insufficient funds' }
        })
        return
    end

    -- Spawn vehicle
    local netId, veh = Functions.SpawnVehicle({
        model = vehicleModel,
        spawnSource = GetEntityCoords(GetPlayerPed(source)) + vector3(3, 0, 0),
        warp = source
    })

    -- Give keys
    local plate = GetVehicleNumberPlateText(veh)
    Functions.GiveVehicleKeys(source, veh, plate)

    -- Track rental
    rentals[source] = { vehicle = veh, netId = netId, plate = plate }

    TriggerClientEvent('chat:addMessage', source, {
        args = { 'Rental', 'Vehicle rented successfully' }
    })
end, false)
```

### Example 3: Custom Inventory UI

```lua
-- Client-side: Custom hunting inventory
RegisterNUICallback('getHuntingItems', function(data, cb)
    local items = {}

    for _, itemName in ipairs(huntingItems) do
        table.insert(items, {
            name = itemName,
            image = Functions.GetInventoryImage(itemName),
            label = GetItemLabel(itemName),
            count = GetItemCount(itemName)
        })
    end

    cb(items)
end)
```

***

## Best Practices

1.  **Use shared functions for consistency**:

    ```lua
    -- Good
    if Functions.IsHuntingWeapon(weapon) then
        -- Process
    end

    -- Avoid
    local isHunting = weapon == 'WEAPON_DHR31' or weapon == 'WEAPON_MUSKET'
    ```
2.  **Always check return values**:

    ```lua
    local netId, veh = Functions.SpawnVehicle(params)
    if not veh or not DoesEntityExist(veh) then
        print('Vehicle spawn failed')
        return
    end
    ```
3.  **Handle missing key systems gracefully**:

    ```lua
    -- GiveVehicleKeys silently fails if no system installed
    Functions.GiveVehicleKeys(source, veh, plate)
    -- No need to check if key system exists
    ```
4.  **Use debug logging for development**:

    ```lua
    DebugLog('Processing animal kill: ' .. animalType, 'hunting')
    ```

***

## Customization

All shared functions can be customized in `game/opensource/functions.lua`:

```lua
-- Example: Custom license check
function Functions.HasLicense()
    local Player = Framework.GetPlayer(source)
    return Player.hasItem('hunting_license') or Player.job == 'hunter'
end

-- Example: Custom title system
function Functions.GetCustomTitle()
    local Player = Framework.GetPlayer(source)
    return Player.metadata.customTitle or false
end
```

***

## Notes

* Shared functions work in both client and server contexts
* Vehicle functions are **server-side only**
* Debug functions respect `Shared.Debug` setting
* Key system integration auto-detects installed systems
* Image paths use NUI protocol

***

## Next Steps

* Review [Client API](client.md) for client-specific functions
* Check [Server API](server.md) for server-specific functions
* See [Configuration](../configuration/shared.md) for shared settings
