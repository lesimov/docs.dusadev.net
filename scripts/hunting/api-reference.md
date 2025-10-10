# API Reference

This document provides a comprehensive reference for all exports, events, and callbacks available in the Dusa Hunting System for developers who want to integrate or extend the script.

## Table of Contents

- [Client-Side API](#client-side-api)
  - [Exports](#client-exports)
  - [Events](#client-events)
- [Server-Side API](#server-side-api)
  - [Exports](#server-exports)
  - [Callbacks](#server-callbacks)
  - [Events](#server-events)
- [Shared Functions](#shared-functions)

---

## Client-Side API

### Client Exports

#### OpenMenu
Opens the hunting shop menu.

```lua
exports['dusa_hunting']:OpenMenu()
```

**Usage Example**:
```lua
-- Open hunting shop from a custom command
RegisterCommand('openhuntingshop', function()
    exports['dusa_hunting']:OpenMenu()
end, false)
```

#### UpdateQuestProgress
Updates quest progress for a specific quest type.

```lua
exports['dusa_hunting']:UpdateQuestProgress(questType, animalType, amount)
```

**Parameters**:
- `questType` (string) - Type of quest: `'hunt'`, `'trap'`, or `'cook'`
- `animalType` (string) - Animal type (e.g., `'deer'`, `'bear'`, `'rabbit'`)
- `amount` (number) - Amount to add to progress

**Usage Example**:
```lua
-- Manually update hunt quest progress
exports['dusa_hunting']:UpdateQuestProgress('hunt', 'deer', 1)

-- Update trap quest progress
exports['dusa_hunting']:UpdateQuestProgress('trap', 'rabbit', 1)

-- Update cook quest progress (no animal type needed)
exports['dusa_hunting']:UpdateQuestProgress('cook', nil, 5)
```

---

### Client Events

#### hunting:client:OpenMenu
Triggered to open the hunting shop menu.

```lua
TriggerEvent('hunting:client:OpenMenu')
```

**Usage Example**:
```lua
-- Trigger from another script
TriggerEvent('hunting:client:OpenMenu')
```

#### hunting:client:PlaceTrap
Triggers the trap placement system.

```lua
TriggerEvent('hunting:client:PlaceTrap')
```

**Usage Example**:
```lua
-- Custom trap placement from another script
TriggerEvent('hunting:client:PlaceTrap')
```

#### dusa_hunting:client:openBinocular
Opens the binocular view.

```lua
TriggerEvent('dusa_hunting:client:openBinocular')
```

#### dusa_hunting:client:PlaceBait
Places hunting bait at the player's location.

```lua
TriggerEvent('dusa_hunting:client:PlaceBait')
```

#### hunting:client:openLaptop
Opens the hunting laptop interface (if DUI laptop is enabled).

```lua
TriggerEvent('hunting:client:openLaptop')
```

#### dusa_hunting:showHuntingLicense
Shows a hunting license to nearby players.

```lua
TriggerEvent('dusa_hunting:showHuntingLicense', targetPlayerId)
```

**Parameters**:
- `targetPlayerId` (number) - Server ID of the player to show the license to

---

## Server-Side API

### Server Exports

#### addExperience
Adds hunting experience to a player.

```lua
local success, newLevel, isLevelUp = exports['dusa_hunting']:addExperience(source, amount)
```

**Parameters**:
- `source` (number) - Player server ID
- `amount` (number) - Amount of XP to add

**Returns**:
- `success` (boolean) - Whether XP was added successfully
- `newLevel` (number) - Player's new level
- `isLevelUp` (boolean) - Whether the player leveled up

**Usage Example**:
```lua
-- Give 50 XP to a player
local success, level, leveledUp = exports['dusa_hunting']:addExperience(source, 50)

if success then
    print(string.format("Player is now level %d", level))

    if leveledUp then
        print("Player leveled up!")
    end
end
```

#### UpdateQuestProgress
Updates quest progress for a player.

```lua
exports['dusa_hunting']:UpdateQuestProgress(source, questType, animalType, amount)
```

**Parameters**:
- `source` (number) - Player server ID
- `questType` (string) - Type of quest: `'hunt'`, `'trap'`, or `'cook'`
- `animalType` (string) - Animal type (can be `nil` for cook quests)
- `amount` (number) - Amount to add to progress

**Usage Example**:
```lua
-- Update hunt progress from custom script
exports['dusa_hunting']:UpdateQuestProgress(source, 'hunt', 'bear', 1)

-- Update cooking progress
exports['dusa_hunting']:UpdateQuestProgress(source, 'cook', nil, 3)
```

#### reloadUITranslations
Reloads UI translations for all players.

```lua
exports['dusa_hunting']:reloadUITranslations()
```

**Usage Example**:
```lua
-- Reload translations after updating locale files
exports['dusa_hunting']:reloadUITranslations()
```

---

### Server Callbacks

All server callbacks use `lib.callback.register` from ox_lib.

#### hunting:server:buyCart
Handles shop purchases.

```lua
lib.callback.await('hunting:server:buyCart', false, cart, paymentMethod, totalPrice)
```

**Parameters**:
- `cart` (table) - Array of items to purchase
  ```lua
  {
      { item = 'hunting_bait', quantity = 5 },
      { item = 'hunting_trap', quantity = 2 }
  }
  ```
- `paymentMethod` (string) - Payment type: `'cash'` or `'bank'`
- `totalPrice` (number) - Total price to charge

**Returns**: `boolean` - Success status

#### hunting:server:getSellList
Gets the player's sellable hunting items.

```lua
local sellList = lib.callback.await('hunting:server:getSellList', false)
```

**Returns**: `table` - Array of sellable items with prices and quality

**Response Example**:
```lua
{
    {
        id = 1,
        item = 'deer_beef',
        name = 'Deer Beef',
        price = 67,  -- Base price * quality multiplier
        quantity = 5,
        quality = 2,
        qualityInfo = {
            hasQuality = true,
            quality = 2,
            qualityText = "Quality 2"
        }
    }
}
```

#### hunting:server:sellItems
Sells hunting items from the player's inventory.

```lua
local result = lib.callback.await('hunting:server:sellItems', false, itemsToSell)
```

**Parameters**:
- `itemsToSell` (table) - Array of items to sell
  ```lua
  {
      { item = 'deer_beef', quantity = 3, quality = 2 },
      { item = 'hide', quantity = 1, quality = 1 }
  }
  ```

**Returns**: `table` - Result with earnings and XP gained

#### hunting:server:processAnimalKill
Processes an animal kill and gives rewards.

```lua
local rewards = lib.callback.await('hunting:server:processAnimalKill', false, animalType, quality)
```

**Parameters**:
- `animalType` (string) - Type of animal (e.g., `'deer'`, `'bear'`)
- `quality` (number) - Quality level (1-3)

**Returns**: `table` - Array of rewards given

#### hunting:server:getAnimalConfig
Gets the animal reward configuration.

```lua
local animalConfig = lib.callback.await('hunting:server:getAnimalConfig', false)
```

**Returns**: `table` - Complete animal rewards configuration

#### hunting:server:getPlayerLevel
Gets the player's hunting level.

```lua
local level = lib.callback.await('hunting:server:getPlayerLevel', false)
```

**Returns**: `number` - Player's current hunting level

#### hunting:server:getPlayerProfile
Gets the player's hunting profile.

```lua
local profile = lib.callback.await('hunting:server:getPlayerProfile', false)
```

**Returns**: `table` - Player profile with level, XP, title, etc.

#### hunting:server:GetLeaderBoard
Gets the hunting leaderboard.

```lua
local leaderboard = lib.callback.await('hunting:server:GetLeaderBoard', false)
```

**Returns**: `table` - Array of top hunters

#### hunting:server:rentVehicle
Rents a hunting vehicle.

```lua
local result = lib.callback.await('hunting:server:rentVehicle', false)
```

**Returns**: `table` - Result with success status and vehicle info

#### hunting:server:returnVehicle
Returns a rented hunting vehicle.

```lua
local result = lib.callback.await('hunting:server:returnVehicle', false, vehicleNetId)
```

**Parameters**:
- `vehicleNetId` (number) - Network ID of the vehicle

**Returns**: `table` - Result with success status and refund amount

#### hunting:server:checkVehicleOwnership
Checks if a player owns a specific rented vehicle.

```lua
local isOwner = lib.callback.await('hunting:server:checkVehicleOwnership', false, vehicleNetId)
```

**Parameters**:
- `vehicleNetId` (number) - Network ID of the vehicle

**Returns**: `boolean` - Ownership status

#### hunting:server:addCookedItem
Adds a cooked item to the player's inventory.

```lua
local success = lib.callback.await('hunting:server:addCookedItem', false, data)
```

**Parameters**:
- `data` (table)
  ```lua
  {
      item = 'deer_beef',
      part = 'beef',
      count = 3
  }
  ```

**Returns**: `boolean` - Success status

#### hunting:server:removeRawItem
Removes raw items from the player's inventory.

```lua
local success = lib.callback.await('hunting:server:removeRawItem', false, data)
```

**Parameters**:
- `data` (table)
  ```lua
  {
      item = 'deer_beef',
      count = 3
  }
  ```

**Returns**: `boolean` - Success status

#### hunting:server:getTraps
Gets all active traps on the server.

```lua
local traps = lib.callback.await('hunting:server:getTraps', false)
```

**Returns**: `table` - Array of active traps

#### hunting:server:pickupTrap
Picks up a trap.

```lua
local success = lib.callback.await('hunting:server:pickupTrap', false, trapId)
```

**Parameters**:
- `trapId` (number) - ID of the trap

**Returns**: `boolean` - Success status

---

### Server Events

#### hunting:server:addTrap
Adds a new trap to the server.

```lua
TriggerServerEvent('hunting:server:addTrap', trapData)
```

**Parameters**:
- `trapData` (table)
  ```lua
  {
      coords = vector3(x, y, z),
      rotation = vector3(rx, ry, rz),
      heading = 180.0,
      triggered = false,
      placedBy = playerId
  }
  ```

#### hunting:server:resourceStarted
Triggered when a player loads into the server.

```lua
TriggerServerEvent('hunting:server:resourceStarted')
```

#### dusa_hunting:requestUITranslations
Requests UI translations from the server.

```lua
TriggerServerEvent('dusa_hunting:requestUITranslations')
```

---

## Shared Functions

### Functions.IsHuntingWeapon
Checks if a weapon is a hunting weapon.

```lua
local isHuntingWeapon = Functions.IsHuntingWeapon(weaponHash)
```

**Parameters**:
- `weaponHash` (string|number) - Weapon name or hash

**Returns**: `boolean`

**Usage Example**:
```lua
-- Check if current weapon is a hunting weapon
local currentWeapon = GetSelectedPedWeapon(PlayerPedId())
if Functions.IsHuntingWeapon(currentWeapon) then
    print("Holding a hunting weapon")
end
```

### Functions.GetInventoryImage
Gets the correct inventory image path for an item.

```lua
local imagePath = Functions.GetInventoryImage(itemName)
```

**Parameters**:
- `itemName` (string) - Item name

**Returns**: `string` - Full image path (nui://)

**Usage Example**:
```lua
local imagePath = Functions.GetInventoryImage('deer_beef')
-- Returns: "nui://ox_inventory/web/images/deer_beef.png"
```

### Functions.SpawnVehicle (Server-Side)
Spawns a vehicle on the server.

```lua
local netId, vehicle = Functions.SpawnVehicle(params)
```

**Parameters**:
- `params` (table)
  ```lua
  {
      model = 'sandking',
      spawnSource = vector4(x, y, z, heading),
      warp = playerId,  -- Optional: Warp player into vehicle
      props = {}  -- Optional: Vehicle properties
  }
  ```

**Returns**:
- `netId` (number) - Network ID of the vehicle
- `vehicle` (number) - Vehicle entity

**Usage Example**:
```lua
local netId, veh = Functions.SpawnVehicle({
    model = 'sandking',
    spawnSource = vector4(-677.869, 5826.417, 17.331, 134.575),
    warp = source
})

print("Spawned vehicle with netId: " .. netId)
```

### Functions.GiveVehicleKeys (Server-Side)
Gives vehicle keys to a player.

```lua
Functions.GiveVehicleKeys(source, vehicle, plate)
```

**Parameters**:
- `source` (number) - Player server ID
- `vehicle` (number) - Vehicle entity
- `plate` (string) - Vehicle plate

**Supported Key Systems**:
- dusa_vehiclekeys
- wasabi_carlock
- qb-vehiclekeys
- qs-vehiclekeys
- vehicles_keys
- ak47_vehiclekeys
- Renewed-Vehiclekeys

### Functions.RemoveVehicleKeys (Server-Side)
Removes vehicle keys from a player.

```lua
Functions.RemoveVehicleKeys(source, vehicle, plate)
```

**Parameters**:
- `source` (number) - Player server ID
- `vehicle` (number) - Vehicle entity
- `plate` (string) - Vehicle plate

---

## Integration Examples

### Example 1: Custom Quest Integration

```lua
-- Server-side: Award XP for custom hunting challenge
RegisterCommand('customhunt', function(source, args)
    local animalType = args[1] or 'deer'

    -- Update quest progress
    exports['dusa_hunting']:UpdateQuestProgress(source, 'hunt', animalType, 1)

    -- Give bonus XP
    local success, level, leveledUp = exports['dusa_hunting']:addExperience(source, 25)

    if leveledUp then
        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Hunting System', 'You leveled up!' }
        })
    end
end, false)
```

### Example 2: Custom Shop Integration

```lua
-- Client-side: Open hunting shop from custom menu
RegisterNetEvent('myCustomMenu:openHuntingShop', function()
    exports['dusa_hunting']:OpenMenu()
end)
```

### Example 3: Custom Vehicle Rental

```lua
-- Server-side: Custom vehicle rental with discount
RegisterCommand('renthuntingvehicle', function(source)
    local result = lib.callback.await('hunting:server:rentVehicle', source)

    if result.success then
        print(string.format("Player %d rented a hunting vehicle", source))
    end
end, false)
```

### Example 4: Checking Player Hunting Level

```lua
-- Server-side: Restrict area based on hunting level
RegisterNetEvent('checkHuntingLevel', function()
    local source = source
    local level = lib.callback.await('hunting:server:getPlayerLevel', source)

    if level >= 5 then
        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Hunting', 'Access granted to advanced hunting zone' }
        })
    else
        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Hunting', 'You need level 5+ to access this zone' }
        })
    end
end)
```

### Example 5: Custom Animal Reward Override

```lua
-- Server-side: Override animal rewards
AddEventHandler('hunting:server:processAnimalKill', function(animalType, quality)
    local source = source

    -- Custom logic for special animals
    if animalType == 'rare_deer' then
        -- Give custom rewards
        Framework.AddItem(source, 'rare_antler', 1)
        exports['dusa_hunting']:addExperience(source, 100)
    end
end)
```

---

## Notes for Developers

1. **Quality System**: All meat items support quality levels (1-3):
   - Quality 1: Body shot
   - Quality 2: Leg shot
   - Quality 3: Headshot or trap kill

2. **Quest Types**:
   - `'hunt'` - Hunting animals
   - `'trap'` - Trapping animals
   - `'cook'` - Cooking meat

3. **Animal Types**: The following animals are supported by default:
   - `deer`, `rabbit`, `bear`, `boar`, `coyote`, `mtlion`, `lion`, `oryx`, `antelope`, `redpanda`, `pig`

4. **Thread Safety**: All callbacks are thread-safe and can be called from any script.

5. **Error Handling**: All exports and callbacks include built-in error handling. Always check return values.

---

## Support

For additional API support or feature requests, please contact the script author or join the support Discord.
