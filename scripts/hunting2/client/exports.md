---
icon: function
---

# Client Exports

Client-side exports available for integration with other resources.

## Export List

<table><thead><tr><th width="220">Export</th><th width="180">Parameters</th><th width="100">Return</th><th>Description</th></tr></thead><tbody><tr><td>GetHuntingLevel</td><td>none</td><td><code>number</code></td><td>Returns player's current hunting level</td></tr><tr><td>GetHuntingXP</td><td>none</td><td><code>number</code></td><td>Returns player's current XP</td></tr><tr><td>GetHuntingData</td><td>none</td><td><code>table</code></td><td>Returns complete hunting stats</td></tr><tr><td>IsInHuntingZone</td><td>none</td><td><code>bool</code></td><td>Check if player is in hunting zone</td></tr><tr><td>OpenHuntingMenu</td><td>none</td><td>none</td><td>Opens the hunting menu UI</td></tr><tr><td>OpenHuntingShop</td><td>none</td><td>none</td><td>Opens nearest hunting shop</td></tr><tr><td>HasHuntingLicense</td><td>none</td><td><code>bool</code></td><td>Check if player has valid license</td></tr><tr><td>GetActiveQuests</td><td>none</td><td><code>table</code></td><td>Returns active quest data</td></tr><tr><td>PlaceTrap</td><td>none</td><td><code>bool</code></td><td>Triggers trap placement</td></tr><tr><td>PlaceBait</td><td>none</td><td><code>bool</code></td><td>Triggers bait placement</td></tr><tr><td>StartCooking</td><td>none</td><td>none</td><td>Opens cooking menu at campfire</td></tr><tr><td>DeployTent</td><td>none</td><td><code>bool</code></td><td>Deploy tent at current location</td></tr><tr><td>GetNearbyAnimals</td><td>radius: <code>number</code></td><td><code>table</code></td><td>Returns animals within radius</td></tr><tr><td>CanHuntAnimal</td><td>animalType: <code>string</code></td><td><code>bool</code></td><td>Check if animal can be hunted</td></tr><tr><td>GetTournamentData</td><td>none</td><td><code>table</code></td><td>Returns active tournament info</td></tr></tbody></table>

## Export Usage

### Basic Data Exports

#### GetHuntingLevel

Returns the player's current hunting level.

```lua
local level = exports['dusa_hunting']:GetHuntingLevel()
print('Your hunting level: ' .. level)
```

**Returns:**
- `number`: Current hunting level (1-20+)

---

#### GetHuntingXP

Returns the player's current hunting experience points.

```lua
local xp = exports['dusa_hunting']:GetHuntingXP()
print('Current XP: ' .. xp)
```

**Returns:**
- `number`: Current XP amount

---

#### GetHuntingData

Returns complete hunting statistics.

```lua
local data = exports['dusa_hunting']:GetHuntingData()
print('Level: ' .. data.level)
print('XP: ' .. data.xp .. '/' .. data.xpNeeded)
print('Total Kills: ' .. data.totalKills)
```

**Returns:**
```lua
{
    level = 10,
    xp = 1250,
    xpNeeded = 1500,
    totalKills = 245,
    perfectKills = 87,
    reputation = 520,
    questsCompleted = 12,
    tournamentsWon = 2
}
```

---

#### IsInHuntingZone

Check if player is currently in a hunting zone.

```lua
local inZone = exports['dusa_hunting']:IsInHuntingZone()
if inZone then
    print('You are in a hunting zone')
end
```

**Returns:**
- `boolean`: `true` if in zone, `false` otherwise

---

#### HasHuntingLicense

Check if player has a valid hunting license.

```lua
local hasLicense = exports['dusa_hunting']:HasHuntingLicense()
if not hasLicense then
    print('You need a hunting license!')
end
```

**Returns:**
- `boolean`: `true` if valid license, `false` otherwise

---

### Menu Exports

#### OpenHuntingMenu

Opens the main hunting menu UI.

```lua
-- Open hunting menu from custom command
RegisterCommand('huntmenu', function()
    exports['dusa_hunting']:OpenHuntingMenu()
end)
```

**Parameters:** None
**Returns:** None

---

#### OpenHuntingShop

Opens the nearest hunting shop interface.

```lua
-- Custom NPC interaction
RegisterNetEvent('myScript:openShop', function()
    exports['dusa_hunting']:OpenHuntingShop()
end)
```

**Parameters:** None
**Returns:** None

---

### Quest Exports

#### GetActiveQuests

Returns data for all active quests.

```lua
local quests = exports['dusa_hunting']:GetActiveQuests()
for _, quest in pairs(quests) do
    print('Quest: ' .. quest.title)
    print('Progress: ' .. quest.progress .. '/' .. quest.required)
end
```

**Returns:**
```lua
{
    {
        id = 'hunt_deer',
        title = 'Deer Hunter',
        description = 'Hunt 5 deer',
        progress = 3,
        required = 5,
        type = 'daily',
        timeRemaining = 18000, -- seconds
        rewards = {
            money = 1000,
            xp = 250,
            items = { ... }
        }
    },
    -- ... more quests
}
```

---

### Action Exports

#### PlaceTrap

Triggers trap placement mode.

```lua
-- Custom trap placement from item use
RegisterNetEvent('myScript:useTrap', function()
    local success = exports['dusa_hunting']:PlaceTrap()
    if success then
        -- Trap placed successfully
    end
end)
```

**Returns:**
- `boolean`: `true` if placement started, `false` if failed

**Failure Reasons:**
- Not in hunting zone
- No trap in inventory
- Already at trap limit
- Invalid location

---

#### PlaceBait

Triggers bait placement mode.

```lua
local success = exports['dusa_hunting']:PlaceBait()
```

**Returns:**
- `boolean`: `true` if placement successful, `false` otherwise

---

#### StartCooking

Opens the cooking menu if near a campfire.

```lua
-- Custom cooking key bind
RegisterCommand('cook', function()
    exports['dusa_hunting']:StartCooking()
end)
```

**Parameters:** None
**Returns:** None

**Note:** Player must be near an active campfire

---

#### DeployTent

Deploys a tent at the player's current location.

```lua
local success = exports['dusa_hunting']:DeployTent()
if not success then
    print('Cannot deploy tent here')
end
```

**Returns:**
- `boolean`: `true` if deployed, `false` if failed

---

### Advanced Exports

#### GetNearbyAnimals

Returns all animals within specified radius.

```lua
local animals = exports['dusa_hunting']:GetNearbyAnimals(100.0)
for _, animal in pairs(animals) do
    print('Animal: ' .. animal.type .. ' at distance: ' .. animal.distance)
end
```

**Parameters:**
- `radius` (number): Search radius in meters

**Returns:**
```lua
{
    {
        entity = <entity handle>,
        type = 'deer',
        quality = 3,
        distance = 45.2,
        coords = vector3(x, y, z),
        isDead = false
    },
    -- ... more animals
}
```

---

#### CanHuntAnimal

Check if a specific animal type can be hunted by player.

```lua
local canHunt = exports['dusa_hunting']:CanHuntAnimal('mountain_lion')
if not canHunt then
    print('You need to be level 11 to hunt mountain lions')
end
```

**Parameters:**
- `animalType` (string): Animal type identifier

**Returns:**
- `boolean`: `true` if can hunt, `false` otherwise

---

#### GetTournamentData

Returns information about active tournament.

```lua
local tournament = exports['dusa_hunting']:GetTournamentData()
if tournament.active then
    print('Tournament Score: ' .. tournament.score)
    print('Current Rank: ' .. tournament.rank)
    print('Time Left: ' .. tournament.timeRemaining)
end
```

**Returns:**
```lua
{
    active = true,
    score = 1250,
    rank = 5,
    timeRemaining = 3600, -- seconds
    leaderboard = {
        { name = 'Player1', score = 2000 },
        { name = 'Player2', score = 1800 },
        -- ... top 10
    }
}
```

If no tournament active:
```lua
{
    active = false
}
```

---

## Integration Examples

### HUD Integration

```lua
-- Display hunting level in custom HUD
CreateThread(function()
    while true do
        local level = exports['dusa_hunting']:GetHuntingLevel()
        local data = exports['dusa_hunting']:GetHuntingData()

        -- Update your HUD elements
        SendNUIMessage({
            action = 'updateHunting',
            level = level,
            xp = data.xp,
            xpNeeded = data.xpNeeded
        })

        Wait(5000) -- Update every 5 seconds
    end
end)
```

### Custom Quest Display

```lua
-- Show quests in custom UI
RegisterCommand('myquests', function()
    local quests = exports['dusa_hunting']:GetActiveQuests()

    -- Send to NUI
    SendNUIMessage({
        action = 'showQuests',
        quests = quests
    })
    SetNuiFocus(true, true)
end)
```

### Zone Notification

```lua
-- Custom zone entry notification
local inZone = false
CreateThread(function()
    while true do
        local currentlyInZone = exports['dusa_hunting']:IsInHuntingZone()

        if currentlyInZone and not inZone then
            -- Entered zone
            TriggerEvent('myScript:showNotification', 'Entered hunting zone')
        elseif not currentlyInZone and inZone then
            -- Left zone
            TriggerEvent('myScript:showNotification', 'Left hunting zone')
        end

        inZone = currentlyInZone
        Wait(2000)
    end
end)
```

### Tournament Tracker

```lua
-- Display tournament info in custom UI
CreateThread(function()
    while true do
        local tournament = exports['dusa_hunting']:GetTournamentData()

        if tournament.active then
            -- Show tournament UI
            SendNUIMessage({
                action = 'showTournament',
                score = tournament.score,
                rank = tournament.rank,
                timeLeft = tournament.timeRemaining
            })
        end

        Wait(1000)
    end
end)
```

## See Also

- [Client Events](events.md) - Event handling
- [Server Exports](../server/exports.md) - Server-side functions
- [Integration Examples](../integration/examples.md) - Complete scenarios
