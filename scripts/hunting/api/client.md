# Client-Side API

This page documents all client-side exports and events available in the Dusa Hunting System.

---

## Client Exports

### OpenMenu

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

**Use Cases**:
- Custom menu integration
- NPC interactions
- Custom keybinds
- Job-specific shop access

---

### UpdateQuestProgress

Updates quest progress for a specific quest type.

```lua
exports['dusa_hunting']:UpdateQuestProgress(questType, animalType, amount)
```

**Parameters**:
- `questType` (string) - Type of quest: `'hunt'`, `'trap'`, or `'cook'`
- `animalType` (string) - Animal type (e.g., `'deer'`, `'bear'`, `'rabbit'`)
  - Can be `nil` for cook quests
- `amount` (number) - Amount to add to progress

**Usage Examples**:
```lua
-- Update hunt quest progress
exports['dusa_hunting']:UpdateQuestProgress('hunt', 'deer', 1)

-- Update trap quest progress
exports['dusa_hunting']:UpdateQuestProgress('trap', 'rabbit', 1)

-- Update cook quest progress (no animal type needed)
exports['dusa_hunting']:UpdateQuestProgress('cook', nil, 5)
```

**Use Cases**:
- Custom hunting events
- Admin commands
- Special quest triggers
- Integration with other scripts

---

## Client Events

### hunting:client:OpenMenu

Triggers the hunting shop menu to open.

```lua
TriggerEvent('hunting:client:OpenMenu')
```

**Usage Example**:
```lua
-- Trigger from another script
TriggerEvent('hunting:client:OpenMenu')

-- From a NPC interaction
AddEventHandler('my-npc:openHuntingShop', function()
    TriggerEvent('hunting:client:OpenMenu')
end)
```

---

### hunting:client:PlaceTrap

Triggers the trap placement system.

```lua
TriggerEvent('hunting:client:PlaceTrap')
```

**Usage Example**:
```lua
-- Custom trap placement from another script
RegisterCommand('placetrap', function()
    TriggerEvent('hunting:client:PlaceTrap')
end, false)

-- From inventory item (already handled by script)
-- This is for custom integrations
```

**Note**: The script already handles trap placement when using the `hunting_trap` item. Use this event only for custom implementations.

---

### dusa_hunting:client:openBinocular

Opens the binocular view.

```lua
TriggerEvent('dusa_hunting:client:openBinocular')
```

**Usage Example**:
```lua
-- Open binoculars from custom keybind
RegisterCommand('usebinoculars', function()
    TriggerEvent('dusa_hunting:client:openBinocular')
end, false)
```

**Note**: Requires player to have `binocular` item in inventory.

---

### dusa_hunting:client:PlaceBait

Places hunting bait at the player's location.

```lua
TriggerEvent('dusa_hunting:client:PlaceBait')
```

**Usage Example**:
```lua
-- Custom bait placement
RegisterCommand('placebait', function()
    TriggerEvent('dusa_hunting:client:PlaceBait')
end, false)
```

**Note**: The script already handles bait placement when using the `hunting_bait` item. Use this event only for custom implementations.

---

### hunting:client:openLaptop

Opens the hunting laptop interface (if DUI laptop is enabled).

```lua
TriggerEvent('hunting:client:openLaptop')
```

**Usage Example**:
```lua
-- Open laptop from custom interaction
RegisterCommand('huntinglaptop', function()
    TriggerEvent('hunting:client:openLaptop')
end, false)
```

**Requirements**:
- `Shared.EnableDUILaptop = true` in config
- Player must have `hunting_laptop` item

---

### dusa_hunting:showHuntingLicense

Shows a hunting license to nearby players.

```lua
TriggerEvent('dusa_hunting:showHuntingLicense', targetPlayerId)
```

**Parameters**:
- `targetPlayerId` (number) - Server ID of the player to show the license to

**Usage Example**:
```lua
-- Show license to nearest player
local nearbyPlayers = GetNearbyPlayers(5.0)
if #nearbyPlayers > 0 then
    TriggerEvent('dusa_hunting:showHuntingLicense', nearbyPlayers[1].id)
end
```

**Note**: The script handles this automatically when using the `hunting_license` item.

---

## Integration Examples

### Example 1: Custom Menu Integration

```lua
-- Add hunting shop to your custom F1 menu
RegisterNetEvent('myMenu:openHuntingShop', function()
    exports['dusa_hunting']:OpenMenu()
end)

-- Or use the event
RegisterNetEvent('myMenu:openHuntingShop', function()
    TriggerEvent('hunting:client:OpenMenu')
end)
```

### Example 2: Custom Quest Tracker

```lua
-- Track custom hunting challenges
RegisterNetEvent('customChallenge:complete', function(challengeType)
    if challengeType == 'deer_hunt' then
        exports['dusa_hunting']:UpdateQuestProgress('hunt', 'deer', 1)
    elseif challengeType == 'cooking' then
        exports['dusa_hunting']:UpdateQuestProgress('cook', nil, 5)
    end
end)
```

### Example 3: Custom Keybind System

```lua
-- Register custom keybinds for hunting tools
RegisterKeyMapping('openhuntingshop', 'Open Hunting Shop', 'keyboard', 'F7')
RegisterCommand('openhuntingshop', function()
    exports['dusa_hunting']:OpenMenu()
end, false)

RegisterKeyMapping('usebinoculars', 'Use Binoculars', 'keyboard', 'B')
RegisterCommand('usebinoculars', function()
    TriggerEvent('dusa_hunting:client:openBinocular')
end, false)
```

### Example 4: Job-Restricted Shop Access

```lua
-- Only allow hunters to open shop
RegisterCommand('huntshop', function()
    local playerJob = GetPlayerJob() -- Your framework function

    if playerJob == 'hunter' then
        exports['dusa_hunting']:OpenMenu()
    else
        Notify('You must be a hunter to access this shop', 'error')
    end
end, false)
```

### Example 5: Custom NPC Interaction

```lua
-- Custom NPC for hunting shop
exports['qb-target']:AddBoxZone("hunting_shop_npc", vector3(-675.87, 5839.29, 17.32), 1.5, 1.5, {
    name = "hunting_shop_npc",
    heading = 135,
    debugPoly = false,
    minZ = 16.32,
    maxZ = 18.32
}, {
    options = {
        {
            type = "client",
            event = "hunting:client:OpenMenu",
            icon = "fas fa-store",
            label = "Open Hunting Shop",
        },
    },
    distance = 2.5
})
```

---

## Event Flow

### Shop Opening Flow
```
Player triggers command/event
    ↓
hunting:client:OpenMenu OR exports['dusa_hunting']:OpenMenu()
    ↓
UI opens with shop data
    ↓
Player makes purchase
    ↓
Server validates and processes
    ↓
Items added to inventory
```

### Quest Progress Flow
```
Player performs action (hunt/trap/cook)
    ↓
Script or custom script triggers UpdateQuestProgress
    ↓
Progress sent to server
    ↓
Server updates database
    ↓
Player notified of progress
    ↓
Quest completion check
```

### Trap Placement Flow
```
Player uses trap item OR triggers event
    ↓
hunting:client:PlaceTrap
    ↓
Placement preview shown
    ↓
Player confirms location
    ↓
Trap spawned and synced to server
    ↓
Trap active and waiting for animals
```

---

## Best Practices

1. **Always check player state** before triggering events:
   ```lua
   if not IsPedInAnyVehicle(PlayerPedId()) then
       TriggerEvent('hunting:client:PlaceTrap')
   end
   ```

2. **Validate item possession** for item-related events:
   ```lua
   local hasBinoculars = HasItem('binocular')
   if hasBinoculars then
       TriggerEvent('dusa_hunting:client:openBinocular')
   end
   ```

3. **Use exports for cleaner code**:
   ```lua
   -- Preferred
   exports['dusa_hunting']:OpenMenu()

   -- Alternative (more verbose)
   TriggerEvent('hunting:client:OpenMenu')
   ```

4. **Handle errors gracefully**:
   ```lua
   local success = pcall(function()
       exports['dusa_hunting']:UpdateQuestProgress('hunt', 'deer', 1)
   end)

   if not success then
       print('Failed to update quest progress')
   end
   ```

---

## Notes

- All client events are **local** (use `TriggerEvent`, not `TriggerServerEvent`)
- Quest progress updates are automatically synced to server
- UI elements use NUI callbacks (handled internally)
- Some events require specific items in inventory
- Check configuration for enabled/disabled features (e.g., DUI laptop)

---

## Next Steps

- Review [Server-Side API](server.md) for server callbacks
- Check [Shared Functions](shared.md) for utility functions
- See [Configuration](../configuration/client.md) for client settings
