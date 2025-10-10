---
icon: gears
---

# Configuration

This guide covers all configuration options for the Hunting script. All config files are located in `dusa_hunting/configurations/`.

## Main Configuration Files

- **config_shared.lua** - Shared settings (client & server)
- **config_client.lua** - Client-only settings
- **config_server.lua** - Server-only settings

## Framework Setup

### Basic Framework Config

Located in `config_shared.lua`:

```lua
Config = {}

-- Framework selection
Config.Framework = 'esx' -- Options: 'esx', 'qb', 'qbox'

-- Target system
Config.Target = 'ox_target' -- Options: 'ox_target', 'qb-target', 'qtarget'

-- Inventory system
Config.Inventory = 'ox_inventory' -- Options: 'ox_inventory', 'qb-inventory', 'qs-inventory'
```

## Hunting Zones Configuration

Define where players can hunt animals.

```lua
Config.HuntingZones = {
    {
        name = 'Paleto Forest',
        coords = vector3(-1234.5, 4567.8, 90.2),
        radius = 500.0, -- Zone size in meters
        blip = {
            enabled = true,
            sprite = 442,
            color = 25,
            scale = 0.8,
            label = 'Hunting Zone'
        },
        requiredLevel = 0, -- Minimum hunting level
        animals = { -- Animals that spawn in this zone
            'deer',
            'rabbit',
            'coyote',
            'boar'
        }
    },
    {
        name = 'Mount Chiliad',
        coords = vector3(450.0, 5566.0, 795.0),
        radius = 800.0,
        blip = {
            enabled = true,
            sprite = 442,
            color = 1,
            scale = 0.9,
            label = 'Premium Hunting Zone'
        },
        requiredLevel = 10, -- High level zone
        animals = {
            'deer',
            'mountain_lion',
            'boar',
            'elk'
        }
    }
}
```

### Zone Settings Explained

| Setting | Type | Description |
|---------|------|-------------|
| `name` | string | Display name of the zone |
| `coords` | vector3 | Center point of the zone |
| `radius` | float | Size of zone in meters |
| `blip.enabled` | bool | Show zone on map |
| `blip.sprite` | int | Blip icon ID |
| `blip.color` | int | Blip color ID |
| `requiredLevel` | int | Minimum level to hunt here |
| `animals` | table | List of animals that spawn |

## Animal Configuration

Configure animal types, spawns, and rewards.

```lua
Config.Animals = {
    ['deer'] = {
        label = 'Deer',
        model = 'a_c_deer', -- Game model hash
        health = 100,
        spawnChance = 0.3, -- 30% chance
        maxSpawns = 5, -- Max in one zone
        respawnTime = 300, -- 5 minutes
        rewards = {
            items = {
                { item = 'deer_pelt', min = 1, max = 1, chance = 100 },
                { item = 'deer_meat', min = 2, max = 4, chance = 100 },
                { item = 'deer_antler', min = 0, max = 1, chance = 30 }
            },
            xp = 50,
            money = 0 -- Money directly earned
        },
        weaponMultipliers = {
            -- Weapon type affects quality
            ['WEAPON_RIFLE'] = 1.0, -- 100% quality
            ['WEAPON_SNIPERRIFLE'] = 1.0,
            ['WEAPON_BOW'] = 0.9, -- 90% quality
            ['WEAPON_PISTOL'] = 0.6, -- 60% quality (not recommended)
        },
        headshotBonus = 1.5, -- 50% quality boost for headshots
        illegal = false -- Not protected species
    },

    ['rabbit'] = {
        label = 'Rabbit',
        model = 'a_c_rabbit_01',
        health = 20,
        spawnChance = 0.5, -- Common
        maxSpawns = 8,
        respawnTime = 180, -- 3 minutes
        rewards = {
            items = {
                { item = 'rabbit_pelt', min = 1, max = 1, chance = 100 },
                { item = 'rabbit_meat', min = 1, max = 2, chance = 100 }
            },
            xp = 15,
            money = 0
        },
        weaponMultipliers = {
            ['WEAPON_RIFLE'] = 0.7, -- Overkill
            ['WEAPON_BOW'] = 1.0,
            ['WEAPON_PISTOL'] = 0.9
        },
        headshotBonus = 1.3,
        illegal = false
    },

    ['mountain_lion'] = {
        label = 'Mountain Lion',
        model = 'a_c_mtlion',
        health = 200,
        spawnChance = 0.1, -- Rare
        maxSpawns = 2,
        respawnTime = 600, -- 10 minutes
        rewards = {
            items = {
                { item = 'lion_pelt', min = 1, max = 1, chance = 100 },
                { item = 'lion_tooth', min = 1, max = 2, chance = 50 }
            },
            xp = 200,
            money = 500 -- Bonus cash
        },
        weaponMultipliers = {
            ['WEAPON_RIFLE'] = 1.0,
            ['WEAPON_SNIPERRIFLE'] = 1.0,
            ['WEAPON_BOW'] = 0.8
        },
        headshotBonus = 2.0,
        illegal = true, -- Protected species
        dangerAnimal = true -- Can attack players
    }
}
```

### Animal Settings Explained

| Setting | Description | Impact |
|---------|-------------|---------|
| `health` | Animal HP | Affects shots needed to kill |
| `spawnChance` | Spawn probability (0.0-1.0) | Rarity of animal |
| `maxSpawns` | Max animals per zone | Server performance |
| `respawnTime` | Seconds until respawn | Economy balance |
| `weaponMultipliers` | Quality modifier per weapon | Encourages proper weapon choice |
| `headshotBonus` | Quality bonus for headshots | Skill reward |
| `illegal` | Protected species flag | Creates wanted level |
| `dangerAnimal` | Can attack players | Adds challenge |

## Shop Configuration

Configure hunting shops and their inventory.

```lua
Config.Shops = {
    {
        name = 'Paleto Hunting Shop',
        coords = vector3(-1234.5, 4567.8, 90.2),
        blip = {
            enabled = true,
            sprite = 141,
            color = 25,
            scale = 0.8,
            label = 'Hunting Shop'
        },
        ped = {
            model = 'csb_cletus',
            coords = vector4(-1234.5, 4567.8, 90.2, 90.0),
            scenario = 'WORLD_HUMAN_SMOKING' -- Idle animation
        },
        items = {
            -- Items for sale
            { item = 'hunting_license', price = 5000, label = 'Hunting License' },
            { item = 'hunting_bait', price = 50, label = 'Animal Bait' },
            { item = 'hunting_trap', price = 250, label = 'Animal Trap' },
            { item = 'tent', price = 1500, label = 'Camping Tent' },
            { item = 'campfire', price = 500, label = 'Campfire Kit' },
            { item = 'knife', price = 300, label = 'Hunting Knife' },
            { item = 'WEAPON_BOW', price = 2500, label = 'Hunting Bow' }
        },
        buyback = {
            -- Items shop buys from players
            { item = 'deer_pelt', price = 150 },
            { item = 'deer_meat', price = 25 },
            { item = 'rabbit_pelt', price = 50 },
            { item = 'boar_meat', price = 30 },
            { item = 'coyote_pelt', price = 100 }
        }
    }
}
```

## Progression System

Configure leveling and experience.

```lua
Config.Progression = {
    enabled = true,

    -- XP required per level
    xpPerLevel = function(level)
        return 100 + (level * 50) -- Increases with each level
    end,

    -- Level rewards
    levelRewards = {
        [5] = {
            money = 1000,
            items = { { item = 'hunting_bait', amount = 10 } },
            notification = 'You unlocked new hunting areas!'
        },
        [10] = {
            money = 2500,
            items = { { item = 'advanced_scope', amount = 1 } },
            notification = 'You can now hunt rare animals!'
        },
        [15] = {
            money = 5000,
            items = { { item = 'legendary_bait', amount = 5 } },
            notification = 'Legendary animals are now available!'
        }
    },

    -- Zone unlock levels
    zoneUnlocks = {
        ['Paleto Forest'] = 0,
        ['Mount Chiliad'] = 10,
        ['Legendary Valley'] = 15
    }
}
```

## Quest System Configuration

```lua
Config.Quests = {
    enabled = true,

    -- Quest refresh times
    dailyResetHour = 6, -- 6 AM server time
    weeklyResetDay = 1, -- Monday (1-7)

    -- Max active quests
    maxDailyQuests = 3,
    maxWeeklyQuests = 1,

    -- Quest types
    questPool = {
        {
            id = 'hunt_deer',
            type = 'daily',
            title = 'Deer Hunter',
            description = 'Hunt 5 deer',
            objectives = {
                { type = 'kill', animal = 'deer', count = 5 }
            },
            rewards = {
                xp = 250,
                money = 1000,
                items = { { item = 'hunting_bait', amount = 5 } }
            }
        },
        {
            id = 'perfect_pelts',
            type = 'weekly',
            title = 'Perfectionist',
            description = 'Obtain 10 perfect quality pelts',
            objectives = {
                { type = 'quality_pelts', quality = 3, count = 10 }
            },
            rewards = {
                xp = 1000,
                money = 5000,
                items = { { item = 'legendary_bait', amount = 3 } }
            }
        }
    }
}
```

## Tournament Configuration

```lua
Config.Tournaments = {
    enabled = true,

    -- Tournament schedule
    schedule = {
        { day = 6, hour = 18, duration = 120 }, -- Saturday 6 PM, 2 hours
        { day = 7, hour = 14, duration = 120 }  -- Sunday 2 PM, 2 hours
    },

    -- Scoring system
    scoring = {
        ['deer'] = 100,
        ['boar'] = 150,
        ['mountain_lion'] = 500,
        qualityMultiplier = {
            [1] = 1.0, -- Poor
            [2] = 1.5, -- Good
            [3] = 2.0  -- Perfect
        }
    },

    -- Rewards
    prizes = {
        [1] = { -- First place
            money = 10000,
            items = { { item = 'trophy_gold', amount = 1 } }
        },
        [2] = { -- Second place
            money = 5000,
            items = { { item = 'trophy_silver', amount = 1 } }
        },
        [3] = { -- Third place
            money = 2500,
            items = { { item = 'trophy_bronze', amount = 1 } }
        }
    }
}
```

## Cooking System Configuration

```lua
Config.Cooking = {
    enabled = true,

    -- Cooking recipes
    recipes = {
        {
            name = 'Cooked Meat',
            input = { item = 'deer_meat', amount = 1 },
            output = { item = 'cooked_meat', amount = 1 },
            cookTime = 10, -- seconds
            xp = 5
        },
        {
            name = 'Grilled Rabbit',
            input = { item = 'rabbit_meat', amount = 2 },
            output = { item = 'grilled_rabbit', amount = 1 },
            cookTime = 8,
            xp = 5
        },
        {
            name = 'Boar Steak',
            input = { item = 'boar_meat', amount = 1 },
            output = { item = 'boar_steak', amount = 1 },
            cookTime = 15,
            xp = 10
        }
    },

    -- Campfire duration
    campfireDuration = 600, -- 10 minutes before it burns out

    -- Cooking XP multiplier
    xpMultiplier = 1.0
}
```

## Trapping System Configuration

```lua
Config.Traps = {
    enabled = true,

    -- Trap settings
    maxTrapsPerPlayer = 5,
    trapCheckTime = 300, -- 5 minutes minimum between checks
    trapDuration = 3600, -- 1 hour before trap despawns

    -- Catch chances
    catchChances = {
        withBait = 0.6, -- 60% with bait
        withoutBait = 0.3 -- 30% without bait
    },

    -- Trappable animals
    trappableAnimals = {
        'rabbit',
        'coyote',
        'fox',
        'raccoon'
    }
}
```

## Performance Settings

```lua
Config.Performance = {
    -- Animal spawn distance
    spawnDistance = 150.0, -- Meters from player
    despawnDistance = 200.0,

    -- Update intervals
    animalUpdateRate = 1000, -- ms
    playerCheckRate = 5000, -- ms

    -- Max animals per zone
    maxAnimalsPerZone = 10,

    -- Entity cleanup
    cleanupDeadAnimals = true,
    cleanupTime = 300 -- 5 minutes
}
```

## Notification Settings

```lua
Config.Notifications = {
    type = 'ox_lib', -- Options: 'ox_lib', 'esx', 'qb', 'custom'

    -- Notification durations (ms)
    duration = {
        short = 2500,
        medium = 5000,
        long = 7500
    },

    -- Enable/disable specific notifications
    showZoneEntry = true,
    showLevelUp = true,
    showQuestComplete = true,
    showIllegalHunting = true
}
```

## Debug Settings

```lua
Config.Debug = false -- Enable debug prints
Config.DrawZones = false -- Draw zone boundaries (dev only)
Config.ShowAnimalHealth = false -- Show animal HP bars
```

## Best Practices

⚙️ **Economy Balance**
- Start with conservative prices
- Monitor server economy
- Adjust based on player feedback
- Balance hunting vs other income sources

⚙️ **Performance Optimization**
- Don't spawn too many animals
- Use appropriate spawn distances
- Enable cleanup systems
- Test with full server population

⚙️ **Zone Design**
- Place zones away from cities
- Consider terrain and access
- Balance zone sizes
- Create progression through zones

⚙️ **Reward Tuning**
- Make rare animals more rewarding
- Encourage quality over quantity
- Balance XP gains
- Make quests worthwhile

## Next Steps

- 🎮 Learn about [Hunting Mechanics](features/hunting-basics.md)
- 🔧 Check [Integration Examples](integration/examples.md)
- 🐛 Troubleshoot with [Common Issues](common-issues.md)
