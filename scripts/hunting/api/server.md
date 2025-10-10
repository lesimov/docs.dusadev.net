# Server-Side API

This page documents all server-side exports, callbacks, and events available in the Dusa Hunting System.

---

## Server Exports

### addExperience

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
        -- Send celebration notification
        TriggerClientEvent('hunting:levelUp', source, level)
    end
end
```

**Use Cases**:
- Custom quest rewards
- Admin commands
- Special events
- Integration with other systems

---

### UpdateQuestProgress

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

-- Update trap progress
exports['dusa_hunting']:UpdateQuestProgress(source, 'trap', 'rabbit', 1)
```

**Use Cases**:
- Custom hunting mechanics
- Admin quest completion
- Integration with other quest systems
- Special events

---

### reloadUITranslations

Reloads UI translations for all players.

```lua
exports['dusa_hunting']:reloadUITranslations()
```

**Usage Example**:
```lua
-- Reload translations after updating locale files
exports['dusa_hunting']:reloadUITranslations()

-- Use in admin command
RegisterCommand('reloadhuntinglang', function(source)
    exports['dusa_hunting']:reloadUITranslations()
    print('Hunting translations reloaded')
end, true)
```

**Note**: Useful when updating locale files without restarting the resource.

---

## Server Callbacks

All server callbacks use `lib.callback` from ox_lib.

### hunting:server:buyCart

Handles shop purchases.

```lua
local success = lib.callback.await('hunting:server:buyCart', false, cart, paymentMethod, totalPrice)
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

**Usage Example**:
```lua
-- Custom shop integration
local cart = {
    { item = 'hunting_bait', quantity = 10 },
    { item = 'campfire', quantity = 1 }
}

local success = lib.callback.await('hunting:server:buyCart', source, cart, 'cash', 550)

if success then
    print('Purchase successful')
end
```

---

### hunting:server:getSellList

Gets the player's sellable hunting items with quality-based pricing.

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
        basePrice = 45,
        qualityInfo = {
            hasQuality = true,
            quality = 2,
            qualityText = "Quality 2"
        }
    },
    {
        id = 2,
        item = 'hide',
        name = 'Hide',
        price = 25,
        quantity = 3,
        quality = 1,
        basePrice = 25,
        qualityInfo = {
            hasQuality = true,
            quality = 1,
            qualityText = "Quality 1"
        }
    }
}
```

**Usage Example**:
```lua
-- Get player's sellable items
local items = lib.callback.await('hunting:server:getSellList', source)

for _, item in ipairs(items) do
    print(string.format("%s x%d - $%d (Quality %d)",
        item.name, item.quantity, item.price, item.quality))
end
```

---

### hunting:server:sellItems

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
```lua
{
    success = true,
    totalEarnings = 226,
    soldItems = {
        { item = 'deer_beef', quantity = 3, totalPrice = 201, basePrice = 45, quality = 2 },
        { item = 'hide', quantity = 1, totalPrice = 25, basePrice = 25, quality = 1 }
    },
    xpGained = 4,
    xpDetails = {
        { item = 'deer_beef', quality = 2, quantity = 3, xp = 4 }
    }
}
```

**Usage Example**:
```lua
local itemsToSell = {
    { item = 'deer_beef', quantity = 5, quality = 3 },
    { item = 'deer_rib', quantity = 2, quality = 2 }
}

local result = lib.callback.await('hunting:server:sellItems', source, itemsToSell)

if result.success then
    print(string.format("Earned $%d and %d XP", result.totalEarnings, result.xpGained))
end
```

---

### hunting:server:processAnimalKill

Processes an animal kill and gives rewards.

```lua
local rewards = lib.callback.await('hunting:server:processAnimalKill', false, animalType, quality)
```

**Parameters**:
- `animalType` (string) - Type of animal (e.g., `'deer'`, `'bear'`)
- `quality` (number) - Quality level (1-3)

**Returns**: `table` - Array of rewards given

**Usage Example**:
```lua
-- Process a quality 3 deer kill
local rewards = lib.callback.await('hunting:server:processAnimalKill', source, 'deer', 3)

for _, reward in ipairs(rewards) do
    print(string.format("Gave %d x %s (%s)",
        reward.amount, reward.item, reward.type))
end
```

---

### hunting:server:getAnimalConfig

Gets the complete animal reward configuration.

```lua
local animalConfig = lib.callback.await('hunting:server:getAnimalConfig', false)
```

**Returns**: `table` - Complete animal rewards configuration

**Usage Example**:
```lua
-- Get config for custom processing
local config = lib.callback.await('hunting:server:getAnimalConfig', source)

if config['deer'] then
    print('Deer has ' .. #config['deer'].meat.parts .. ' meat parts')
end
```

---

### hunting:server:getPlayerLevel

Gets the player's current hunting level.

```lua
local level = lib.callback.await('hunting:server:getPlayerLevel', false)
```

**Returns**: `number` - Player's current hunting level (1-10)

**Usage Example**:
```lua
-- Check level for restrictions
local level = lib.callback.await('hunting:server:getPlayerLevel', source)

if level < 5 then
    TriggerClientEvent('chat:addMessage', source, {
        args = { 'Hunting', 'You need level 5 to hunt bears' }
    })
end
```

---

### hunting:server:getPlayerProfile

Gets the player's complete hunting profile.

```lua
local profile = lib.callback.await('hunting:server:getPlayerProfile', false)
```

**Returns**: `table` - Player profile data
```lua
{
    level = 5,
    experience = 250,
    title = 'apprentice',
    name = 'John Doe',
    -- Additional profile data
}
```

---

### hunting:server:GetLeaderBoard

Gets the hunting leaderboard.

```lua
local leaderboard = lib.callback.await('hunting:server:GetLeaderBoard', false)
```

**Returns**: `table` - Array of top hunters
```lua
{
    { name = 'Player1', level = 10, experience = 1000, title = 'master' },
    { name = 'Player2', level = 8, experience = 750, title = 'expert' },
    -- ...
}
```

---

### hunting:server:rentVehicle

Rents a hunting vehicle for the player.

```lua
local result = lib.callback.await('hunting:server:rentVehicle', false)
```

**Returns**: `table` - Result with success status and vehicle info
```lua
{
    success = true,
    message = 'Vehicle rented successfully',
    vehicle = {
        model = 'sandking',
        netId = 12345,
        entity = 98765,
        price = 1000
    }
}
```

**Note**: Money is refunded when vehicle is returned.

---

### hunting:server:returnVehicle

Returns a rented hunting vehicle.

```lua
local result = lib.callback.await('hunting:server:returnVehicle', false, vehicleNetId)
```

**Parameters**:
- `vehicleNetId` (number) - Network ID of the vehicle

**Returns**: `table` - Result with success status and refund amount
```lua
{
    success = true,
    message = 'Vehicle returned successfully',
    refundAmount = 1000
}
```

---

### hunting:server:checkVehicleOwnership

Checks if a player owns a specific rented vehicle.

```lua
local isOwner = lib.callback.await('hunting:server:checkVehicleOwnership', false, vehicleNetId)
```

**Parameters**:
- `vehicleNetId` (number) - Network ID of the vehicle

**Returns**: `boolean` - Ownership status

---

### hunting:server:addCookedItem

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

---

### hunting:server:removeRawItem

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

---

### hunting:server:getTraps

Gets all active traps on the server.

```lua
local traps = lib.callback.await('hunting:server:getTraps', false)
```

**Returns**: `table` - Array of active traps

---

### hunting:server:pickupTrap

Picks up a trap and returns it to inventory.

```lua
local success = lib.callback.await('hunting:server:pickupTrap', false, trapId)
```

**Parameters**:
- `trapId` (number) - ID of the trap

**Returns**: `boolean` - Success status

---

## Server Events

### hunting:server:addTrap

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

---

### hunting:server:resourceStarted

Triggered when a player loads into the server.

```lua
TriggerServerEvent('hunting:server:resourceStarted')
```

**Note**: Automatically triggered by the script. Use for custom initialization.

---

### dusa_hunting:requestUITranslations

Requests UI translations from the server.

```lua
TriggerServerEvent('dusa_hunting:requestUITranslations')
```

**Note**: Automatically handled by the script.

---

## Integration Examples

### Example 1: Custom Quest System

```lua
-- Award XP for custom hunting challenge
RegisterCommand('customhunt', function(source, args)
    local animalType = args[1] or 'deer'

    -- Update quest progress
    exports['dusa_hunting']:UpdateQuestProgress(source, 'hunt', animalType, 1)

    -- Give bonus XP
    local success, level, leveledUp = exports['dusa_hunting']:addExperience(source, 25)

    if leveledUp then
        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Hunting System', 'You leveled up to level ' .. level .. '!' }
        })
    end
end, false)
```

### Example 2: Level-Based Restrictions

```lua
-- Restrict hunting based on level
RegisterNetEvent('hunting:checkLevel', function(animalType)
    local source = source
    local level = lib.callback.await('hunting:server:getPlayerLevel', source)

    local levelRequirements = {
        bear = 5,
        lion = 8,
        mtlion = 6
    }

    local required = levelRequirements[animalType]
    if required and level < required then
        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Hunting', string.format('You need level %d to hunt %s', required, animalType) }
        })
        return false
    end

    return true
end)
```

### Example 3: Custom Sell Bonus

```lua
-- Give bonus money for bulk sales
RegisterCommand('sellhunting', function(source)
    local sellList = lib.callback.await('hunting:server:getSellList', source)

    if #sellList == 0 then
        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Hunting', 'You have nothing to sell' }
        })
        return
    end

    -- Calculate bonus for selling everything
    local totalItems = 0
    for _, item in ipairs(sellList) do
        totalItems = totalItems + item.quantity
    end

    local result = lib.callback.await('hunting:server:sellItems', source, sellList)

    if result.success then
        -- Give 10% bonus for bulk sales
        if totalItems >= 20 then
            local bonus = math.floor(result.totalEarnings * 0.1)
            Framework.AddMoney(source, 'cash', bonus, 'bulk-hunting-bonus')

            TriggerClientEvent('chat:addMessage', source, {
                args = { 'Hunting', string.format('Bulk sale bonus: $%d', bonus) }
            })
        end
    end
end, false)
```

### Example 4: Admin Commands

```lua
-- Admin commands for hunting system
RegisterCommand('givehuntingxp', function(source, args)
    if not IsPlayerAdmin(source) then return end

    local targetId = tonumber(args[1])
    local amount = tonumber(args[2]) or 100

    if not targetId then
        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Admin', 'Usage: /givehuntingxp [playerid] [amount]' }
        })
        return
    end

    local success, level, leveledUp = exports['dusa_hunting']:addExperience(targetId, amount)

    if success then
        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Admin', string.format('Gave %d XP to player %d (now level %d)', amount, targetId, level) }
        })
    end
end, true)

RegisterCommand('sethuntinglevel', function(source, args)
    if not IsPlayerAdmin(source) then return end

    local targetId = tonumber(args[1])
    local level = tonumber(args[2])

    if not targetId or not level then
        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Admin', 'Usage: /sethuntinglevel [playerid] [level]' }
        })
        return
    end

    -- Custom implementation to set level directly
    -- You'll need to add this export to the hunting script
    exports['dusa_hunting']:setPlayerLevel(targetId, level)
end, true)
```

### Example 5: Custom Reward System

```lua
-- Override animal kill rewards
AddEventHandler('hunting:server:animalKilled', function(animalType, quality)
    local source = source

    -- Custom rewards for rare animals
    if animalType == 'lion' and quality == 3 then
        -- Give bonus items for perfect lion kill
        Framework.AddItem(source, 'rare_trophy', 1)
        exports['dusa_hunting']:addExperience(source, 100)

        TriggerClientEvent('chat:addMessage', source, {
            args = { 'Hunting', 'Perfect lion kill! You received a rare trophy!' }
        })
    end
end)
```

---

## Best Practices

1. **Always validate player data**:
   ```lua
   local Player = Framework.GetPlayer(source)
   if not Player then return end
   ```

2. **Check return values**:
   ```lua
   local success, level, leveledUp = exports['dusa_hunting']:addExperience(source, 50)
   if not success then
       print('Failed to add XP')
       return
   end
   ```

3. **Use callbacks for data retrieval**:
   ```lua
   -- Good
   local level = lib.callback.await('hunting:server:getPlayerLevel', source)

   -- Avoid storing level in global variables
   ```

4. **Handle edge cases**:
   ```lua
   local sellList = lib.callback.await('hunting:server:getSellList', source)
   if not sellList or #sellList == 0 then
       -- No items to sell
       return
   end
   ```

---

## Notes

- All callbacks require ox_lib
- Player must be online for callbacks to work
- Use `source` for the calling player in server events
- Check for player existence before processing
- Quality multipliers are configured in [Shared Config](../configuration/shared.md#quality-multipliers)

---

## Next Steps

- Review [Client-Side API](client.md) for client exports
- Check [Shared Functions](shared.md) for utility functions
- See [Configuration](../configuration/server.md) for server settings
