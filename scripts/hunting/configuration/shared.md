---
icon: circle-small
---

# Shared Configuration

File: `configurations/config_shared.lua`

This file contains configuration shared between client and server, including species definitions, shop settings, quests, and more.

***

## Basic Settings

```lua
Shared.TEST = false  -- Enable test mode
Shared.Debug = false  -- Enable debug logging
Shared.EnableDUILaptop = true  -- Enable/disable hunting laptop with DUI
```

**Note**: DUI laptop image quality may be low due to outdated FiveM DUI feature. You can disable it here.

***

## System Toggles

```lua
Shared.EnableTournamentSystem = true  -- Enable/disable tournament system
Shared.EnableShopSystem = true  -- Enable/disable shop system
```

Disable systems you don't want to use to improve performance.

***

## Language Settings

```lua
Shared.Locale = 'en'  -- Available: 'en', 'tr'
```

Supported languages:

* `'en'` - English
* `'tr'` - Turkish

Add more languages by creating locale files in `locales/` folder.

***

## Inventory Image Extension

```lua
Shared.InventoryImageExtension = nil  -- Options: nil (auto-detect), 'png', 'webp'
```

**Options**:

* `nil` - Auto-detect (checks webp first, then png)
* `'png'` - Force PNG extension for all images
* `'webp'` - Force WEBP extension for all images

***

## Vehicle Rental

```lua
Shared.Rent = {
    vehicle = 'sandking',  -- Vehicle model
    price = 1000,  -- Rental price (refunded on return)
    coords = vector3(-677.869, 5826.417, 17.331),  -- Spawn location
    heading = 134.575,  -- Spawn heading
}
```

**Configuration**:

* `vehicle` - Any valid vehicle model
* `price` - Rental deposit (returned when vehicle is returned)
* `coords` - Where the vehicle spawns
* `heading` - Vehicle spawn direction

***

## Keybinds

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

Players can rebind these in FiveM settings.

***

## Shop Configuration

### Shop Ped

```lua
Shared.Shop.Ped = {
    target = false,  -- Use target system instead of interaction
    model = 'a_m_m_hillbilly_01',  -- NPC model
    icon = "fa-solid fa-store",
    distance = 3.5,  -- Interaction distance
    coords = vec4(-675.868, 5839.285, 17.320, 134.746),
}
```

### Tournament Ped

```lua
Shared.Shop.Tournament = {
    target = false,
    model = 'a_m_m_salton_01',
    icon = "fa-solid fa-trophy",
    distance = 3.5,
    coords = vec4(-680.180, 5840.854, 17.320, 201.007),
}
```

### Blips

```lua
Shared.Shop.Blip = {
    Enabled = true,
    Sprite = 141,
    Color = 25,
    Scale = 0.8,
    Name = 'Hunting Shop',
    ShortRange = true,
    Coords = vec4(-675.868, 5839.285, 17.320, 134.746),
}

Shared.Shop.Butcher = {
    Enabled = true,
    Sprite = 273,
    Color = 25,
    Scale = 0.8,
    Name = 'Butchering Zone',
    ShortRange = true,
    Coords = vec4(-83.835, 6233.991, 31.091, 111.895),
}
```

***

## Shop Items

Items available for purchase:

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
    {
        item = 'campfire',
        price = 50,
    },
    {
        item = 'primitive_grill',
        price = 100,
    },
    {
        item = 'advanced_grill',
        price = 500,
    },
    {
        item = 'binocular',
        price = 50,
    },
    {
        item = 'hunting_trap',
        price = 250,
    },
    {
        item = 'hunting_laptop',
        price = 250,
    },
    {
        item = 'hunting_license',
        price = 250,
    },
}
```

Add more items as needed.

***

## Quality Multipliers

Affects selling prices based on item quality:

```lua
Shared.Shop.QualityMultipliers = {
    [1] = 1.0,    -- Quality 1: Normal price (100%)
    [2] = 1.5,    -- Quality 2: 50% increase (150%)
    [3] = 2.0,    -- Quality 3: 100% increase (200%)
}
```

**Example**:

* Deer beef base price: $45
* Quality 1: $45
* Quality 2: $67.5
* Quality 3: $90

***

## Sellable Items

Items that can be sold at the shop:

```lua
Shared.Shop.Sell = {
    -- Deer items
    {
        item = 'deer_beef',
        name = 'Deer Beef',
        price = 45
    },
    {
        item = 'deer_rib',
        name = 'Deer Rib',
        price = 35
    },
    {
        item = 'deer_leg',
        name = 'Deer Leg',
        price = 40
    },
    -- Add more sellable items...
}
```

Base prices are multiplied by quality multipliers when selling.

***

## Species Configuration

Define all huntable animals:

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
    ['bear'] = {
        name = 'Bear',
        type = 'bear',
        model = 'BrnBear',
        drag = {
            xPos = 0.0,
            yPos = 0.0,
            zPos = -0.25,
            xRot = -200.0,
            yRot = 0.0,
            zRot = 270.0
        }
    },
    -- Add more species...
}
```

**Drag Configuration**:

* `drag = false` - Carcass cannot be dragged (small animals)
* `drag = { ... }` - Defines how carcass attaches to player when dragging

***

## Pet System

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

**Quality Effects**:

* `'none'` - Pet doesn't affect meat quality
* `'decrease'` - Pet decreases quality by `Value`
* `'increase'` - Pet increases quality by `Value`

***

## Quest Configuration

Define quests for players:

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
        id = 'threedays_trap_rabbit',
        name = 'Rabbit Trapping',
        description = 'Trap 10 rabbits',
        type = 'trap',
        target_animal = 'rabbit',
        target_count = 10,
        renewal_period = 'threedays',
        rewards = {
            money = 2000,
            xp = 5
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

1. **Hunt Quests** (`type = 'hunt'`)
   * Requires `target_animal`
   * Completed by killing animals
2. **Trap Quests** (`type = 'trap'`)
   * Requires `target_animal`
   * Completed by trapping animals
3. **Cook Quests** (`type = 'cook'`)
   * No `target_animal` needed
   * Completed by cooking any meat

### Renewal Periods

* `'daily'` - Resets every 24 hours
* `'weekly'` - Resets every 7 days
* `'threedays'` - Resets every 3 days

***

## Next Steps

* Configure [Client Settings](client.md) for hunting zones
* Set up [Server Configuration](server.md) for rewards
* Review [API Reference](../api-reference.md) for integration
