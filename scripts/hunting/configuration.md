# Configuration Guide

This guide explains all configuration options available in the Dusa Hunting System. Configuration files are located in the `configurations/` folder.

## Table of Contents

- [Shared Configuration](#shared-configuration)
- [Client Configuration](#client-configuration)
- [Server Configuration](#server-configuration)
- [Adding Custom Animals](#adding-custom-animals)
- [Quest Configuration](#quest-configuration)

---

## Shared Configuration

File: `configurations/config_shared.lua`

### Basic Settings

```lua
Shared.TEST = false  -- Enable test mode
Shared.Debug = false  -- Enable debug logging
Shared.EnableDUILaptop = true  -- Enable/disable hunting laptop with DUI
```

**Note**: DUI laptop image quality may be low due to outdated FiveM DUI feature. You can disable it here.

### System Toggles

```lua
Shared.EnableTournamentSystem = true  -- Enable/disable tournament system
Shared.EnableShopSystem = true  -- Enable/disable shop system
```

### Language Settings

```lua
Shared.Locale = 'en'  -- Available: 'en', 'tr'
```

### Inventory Image Extension

```lua
Shared.InventoryImageExtension = nil  -- Options: nil (auto-detect), 'png', 'webp'
```

- `nil` - Auto-detect (checks webp first, then png)
- `'png'` - Force PNG extension
- `'webp'` - Force WEBP extension

### Vehicle Rental

```lua
Shared.Rent = {
    vehicle = 'sandking',  -- Vehicle model
    price = 1000,  -- Rental price (refunded on return)
    coords = vector3(-677.869, 5826.417, 17.331),  -- Spawn location
    heading = 134.575,  -- Spawn heading
}
```

### Keybinds

```lua
Shared.Keybinds = {
    CancelCarcassAction = {
        name = 'cancel_carcass_action',
        description = 'Cancel carcass collection or carrying',
        defaultKey = 'X',
    },
    tournamentLeaderboard = {
        name = 'tournament_leaderboard',
        description = 'Open tournament leaderboard',
        defaultKey = 'TAB',
    },
    toggleCursor = {
        name = 'toggle_cursor',
        description = 'Toggle DUI cursor',
        defaultKey = 'G',
    },
    Visor = {
        name = 'visor',
        description = 'Open visor',
        defaultKey = 'TAB',
    },
}
```

### Shop Configuration

```lua
Shared.Shop = {
    Ped = {
        target = false,  -- Use target system instead of interaction
        model = 'a_m_m_hillbilly_01',  -- NPC model
        icon = "fa-solid fa-store",
        distance = 3.5,  -- Interaction distance
        coords = vec4(-675.868, 5839.285, 17.320, 134.746),
    },

    Tournament = {
        target = false,
        model = 'a_m_m_salton_01',
        icon = "fa-solid fa-trophy",
        distance = 3.5,
        coords = vec4(-680.180, 5840.854, 17.320, 201.007),
    },

    Blip = {
        Enabled = true,
        Sprite = 141,
        Color = 25,
        Scale = 0.8,
        Name = 'Hunting Shop',
        ShortRange = true,
        Coords = vec4(-675.868, 5839.285, 17.320, 134.746),
    },

    Butcher = {
        Enabled = true,
        Sprite = 273,
        Color = 25,
        Scale = 0.8,
        Name = 'Butchering Zone',
        ShortRange = true,
        Coords = vec4(-83.835, 6233.991, 31.091, 111.895),
    },
}
```

### Shop Items

```lua
Shared.Shop.Items = {
    {
        item = 'WEAPON_DHR31',
        price = 1000,
    },
    {
        item = 'ammo-heavysniper',
        price = 100,
    },
    {
        item = 'hunting_bait',
        price = 100,
    },
    -- Add more items...
}
```

### Quality Multipliers

```lua
Shared.Shop.QualityMultipliers = {
    [1] = 1.0,    -- Quality 1: Normal price (100%)
    [2] = 1.5,    -- Quality 2: 50% increase (150%)
    [3] = 2.0,    -- Quality 3: 100% increase (200%)
}
```

### Sell Items Configuration

```lua
Shared.Shop.Sell = {
    {
        item = 'deer_beef',
        name = 'Deer Beef',
        price = 45  -- Base price (modified by quality)
    },
    {
        item = 'deer_rib',
        name = 'Deer Rib',
        price = 35
    },
    -- Add more sellable items...
}
```

### Species Configuration

```lua
Shared.Species = {
    ['deer'] = {
        name = 'Deer',
        type = 'deer',
        model = 'a_c_deer',
        drag = {
            xPos = 0.0,
            yPos = 0.0,
            zPos = -0.25,
            xRot = -200.0,
            yRot = 0.0,
            zRot = 270.0
        }
    },
    ['rabbit'] = {
        name = 'Rabbit',
        type = 'rabbit',
        model = 'a_c_rabbit_01',
        drag = false,  -- Cannot be dragged
    },
    -- Add more species...
}
```

**Drag Configuration**:
- If `drag = false`, the carcass cannot be dragged
- If drag is a table, it defines attachment offsets and rotations

### Pet System

```lua
Shared.Pet = {
    Enabled = false,  -- Enable/disable pet system
    Price = 7500,  -- Purchase price
    WhistleAnimation = true,  -- Play whistle animation when calling
    Model = 'ft-btcoon',  -- Pet model
    MaxDistance = 30.0,  -- Max distance pet can follow
    MinGrade = 3,  -- Minimum hunting level required

    Shortcuts = {
        Enabled = true,
        Attack = { "LEFTSHIFT", "G" },  -- Attack command keybind
    },

    Fixskin = {
        Enabled = true,
        Component = 0,
        Drawable = 0,
    },

    Quality = {
        Effect = 'decrease',  -- Options: 'none', 'decrease', 'increase'
        Value = 1,  -- Amount to modify quality (1-5)
    }
}
```

---

## Client Configuration

File: `configurations/config_client.lua`

### General Settings

```lua
Config.TEST = false
Config.Currency = "$"
Config.CheckInterval = 1  -- Minutes between checks
Config.ObjectiveAlignment = "center-right"  -- Options: center-right, center-left, top-right, top-left, bottom-right, bottom-left
```

### Hunting Restrictions

```lua
Config.OnlyHuntByHuntingWeapons = true  -- Only hunting weapons can kill animals
Config.DisableHuntingRiflePVP = true  -- Disable hunting rifle PVP
Config.HuntingWeapons = {
    'WEAPON_DHR31',
    -- Add more hunting weapons...
}

Config.OnlyHunterCanCollect = true  -- Only the hunter can collect carcass
Config.RequireJob = false  -- Require specific job to hunt
Config.JobName = 'hunter'  -- Job name (if RequireJob is true)
```

### Target System

```lua
Config.UseTarget = false  -- Use target system instead of dusa_bridge interactions
```

### Trapping & Baiting

```lua
Config.TrapDamage = 50  -- Damage dealt to trapped animal
Config.BaitChance = 30  -- Chance (%) for bait to attract animals
```

### Hunting Zones

```lua
Config.HuntingZones = {
    ['HuntingZone1'] = {
        name = 'Deer Zone',
        type = 'deer',  -- Animal type to spawn
        coords = vec3(-575.706, 5460.014, 60.558),  -- Zone center
        range = 250.0,  -- Zone radius
        debug = false,  -- Show debug sphere
        animal = {
            model = 'a_c_deer',
            maxCount = 12,  -- Max animals in zone
            xp = 10,  -- XP per kill
            canAttack = false,  -- Can attack player
            isFleeing = false,  -- Flee when shot
        }
    },
    -- Add more zones...
}
```

**Important**: Do not set `maxCount` too high to avoid performance issues.

### Animal Wiki

```lua
Config.Wiki = {
    ['deer'] = {
        name = "Deer",
        info = "Get Information About",
        description = "A large, graceful herbivore found in forests and grasslands."
    },
    -- Add more wiki entries...
}
```

### Tournament Configuration

```lua
Config.Tournament = {
    AvailableSpecies = {
        'deer',
        'bear',
        'oryx',
        -- Add more species...
    },

    TournamentLimits = {
        RewardRange = {
            Minimum = 500,
            Maximum = 10000,
        },

        DurationRange = {
            Minimum = 5,  -- Minutes
            Maximum = 60,
        },

        Settings = {
            MaxPlayers = 10,
            MinPlayers = 2,
        }
    }
}
```

### Butchering Areas

```lua
Config.Areas = {
    ['butchering'] = {
        machine = {
            coords = vec3(-89.120, 6234.354, 31.061),
        }
    }
}
```

### Vehicle Carcass Attachment

```lua
Config.CarcassVehicleAttach = {
    -- Default settings for all animals
    default = {
        offset = vec3(0.0, 1.5, 1.0),
        rotation = vec3(0.0, 0.0, 0.0),
        alpha = 200,
    },

    -- Animal-specific settings
    deer = {
        offset = vec3(0.0, 1.5, 1.2),
        rotation = vec3(0.0, 0.0, 0.0),
        alpha = 200,
    },

    bear = {
        offset = vec3(0.0, 1.8, 1.3),
        rotation = vec3(0.0, 0.0, 0.0),
        alpha = 200,
    },

    -- Add more animal-specific configurations...
}
```

---

## Server Configuration

File: `configurations/config_server.lua`

### Level System

```lua
Config.MaximumLevel = 10

Config.Title = {
    beginner = 1,
    novice = 2,
    apprentice = 4,
    adept = 6,
    expert = 8,
    master = 10,
}
```

### Quality-Based Rewards

```lua
Config.IncreaseAmountByQuality = true  -- Enable quality-based bonus amounts
```

When enabled:
- Quality 1: +0 bonus items
- Quality 2: +1 bonus item
- Quality 3: +2 bonus items

### Animal Rewards

```lua
Config.AnimalRewards = {
    ['deer'] = {
        meat = {
            item = 'deer_meat',
            parts = {
                beef = {
                    amount = 3,  -- Base amount
                    model = 'propk_deer_beef_raw',
                    item = 'deer_beef',
                    cook = {
                        method = {'grill', 'stick'},  -- Cooking methods
                        cookingTime = 10,  -- Seconds
                        cookedModel = 'propk_deer_beef_cooked',
                        cookedItem = 'deer_beef_cooked'
                    }
                },
                rib = {
                    amount = 1,
                    model = 'propk_deer_rib_raw',
                    item = 'deer_rib',
                    cook = {
                        method = {'grill'},
                        cookingTime = 10,
                        cookedModel = 'propk_deer_rib_cooked',
                        cookedItem = 'deer_rib_cooked'
                    }
                },
                leg = {
                    amount = 4,
                    model = 'propk_deerleg_raw',
                    item = 'deer_leg',
                    cook = {
                        method = {'grill'},
                        cookingTime = 10,
                        cookedModel = 'propk_deerleg_cooked',
                        cookedItem = 'deer_leg_cooked'
                    }
                },
            },
        },
        hide = {
            amount = 1
        },
    },
    -- Add more animals...
}
```

**Cooking Methods**:
- `'grill'` - Can be cooked on grill
- `'stick'` - Can be cooked on stick
- Both can be specified in array

---

## Adding Custom Animals

### Step 1: Add to Species (Shared)

Edit `config_shared.lua`:

```lua
Shared.Species['wolf'] = {
    name = 'Wolf',
    type = 'wolf',
    model = 'a_c_wolf',  -- Make sure this model exists
    drag = {
        xPos = 0.0,
        yPos = 0.0,
        zPos = -0.25,
        xRot = -200.0,
        yRot = 0.0,
        zRot = 270.0
    }
}
```

### Step 2: Add Hunting Zone (Client)

Edit `config_client.lua`:

```lua
Config.HuntingZones['WolfZone'] = {
    name = 'Wolf Territory',
    type = 'wolf',
    coords = vec3(100.0, 200.0, 50.0),
    range = 300.0,
    debug = false,
    animal = {
        model = 'a_c_wolf',
        maxCount = 5,
        xp = 15,
        canAttack = true,
        isFleeing = false,
    }
}
```

### Step 3: Add Wiki Entry (Client)

Edit `config_client.lua`:

```lua
Config.Wiki['wolf'] = {
    name = "Wolf",
    info = "Get Information About",
    description = "A fierce predator that hunts in packs."
}
```

### Step 4: Add Rewards (Server)

Edit `config_server.lua`:

```lua
Config.AnimalRewards['wolf'] = {
    meat = {
        item = 'wolf_meat',
        parts = {
            beef = {
                amount = 4,
                model = 'propk_wolf_beef_raw',
                item = 'wolf_beef',
                cook = {
                    method = {'grill', 'stick'},
                    cookingTime = 12,
                    cookedModel = 'propk_wolf_beef_cooked',
                    cookedItem = 'wolf_beef_cooked'
                }
            },
            -- Add more parts...
        },
    },
    hide = {
        amount = 2
    },
}
```

### Step 5: Add Sellable Items (Shared)

Edit `config_shared.lua`:

```lua
table.insert(Shared.Shop.Sell, {
    item = 'wolf_beef',
    name = 'Wolf Beef',
    price = 80
})
```

### Step 6: Add Items to Inventory

Add wolf items to your inventory system (see Installation guide for format).

---

## Quest Configuration

Quests are defined in `config_shared.lua`:

```lua
Shared.Quests = {
    {
        id = 'daily_hunt_deer',
        name = 'Daily Deer Hunt',
        description = 'Hunt 1 deer today',
        type = 'hunt',  -- Options: 'hunt', 'trap', 'cook'
        target_animal = 'deer',  -- Required for hunt/trap quests
        target_count = 1,
        renewal_period = 'daily',  -- Options: 'daily', 'weekly', 'threedays'
        rewards = {
            money = 1000,
            xp = 2
        }
    },
    {
        id = 'weekly_hunt_bear',
        name = 'Weekly Bear Hunt',
        description = 'Hunt 3 bears this week',
        type = 'hunt',
        target_animal = 'bear',
        target_count = 3,
        renewal_period = 'weekly',
        rewards = {
            money = 5000,
            xp = 10
        }
    },
    {
        id = 'daily_cook_meat',
        name = 'Daily Cooking',
        description = 'Cook 15 pieces of meat',
        type = 'cook',
        target_count = 15,
        renewal_period = 'daily',
        rewards = {
            xp = 2
        }
    },
}
```

### Quest Types

1. **Hunt Quests**:
   - `type = 'hunt'`
   - Requires `target_animal`
   - Completed by killing animals

2. **Trap Quests**:
   - `type = 'trap'`
   - Requires `target_animal`
   - Completed by trapping animals

3. **Cook Quests**:
   - `type = 'cook'`
   - No `target_animal` needed
   - Completed by cooking any meat

### Renewal Periods

- `'daily'` - Resets every day
- `'weekly'` - Resets every week
- `'threedays'` - Resets every 3 days

---

## Advanced Configuration

### Custom Quality Calculation

The quality system is based on shot location:

- **Quality 3 (Best)**: Headshot (bone 99 or 98) or trap kill
- **Quality 2 (Good)**: Leg shot (bones 1-20)
- **Quality 1 (Normal)**: Body shot (other bones)

Level bonuses are also applied:
- Every 3 levels grants +1 quality (max quality 3)

This is calculated in `game/client/main.lua` in the `CheckHitAnimalQuality` function.

### Customizing Prices

All prices support quality multipliers. To change base prices, edit the sell configuration:

```lua
Shared.Shop.Sell = {
    {
        item = 'deer_beef',
        name = 'Deer Beef',
        price = 45  -- This will be 45 for Q1, 67.5 for Q2, 90 for Q3
    },
}
```

### Disabling Systems

You can disable entire systems:

```lua
-- Disable tournaments
Shared.EnableTournamentSystem = false

-- Disable shop
Shared.EnableShopSystem = false

-- Disable DUI laptop
Shared.EnableDUILaptop = false
```

---

## Best Practices

1. **Always backup** configuration files before making changes
2. **Test in TEST mode** first (`Shared.TEST = true`)
3. **Balance economy** carefully - consider server economy
4. **Limit animal counts** in zones to maintain performance
5. **Use debug mode** when adding new zones (`debug = true`)
6. **Restart server** after configuration changes

---

## Next Steps

- Check the [API Reference](api-reference.md) for integration options
- See [Common Issues](common-issues.md) if you encounter problems
