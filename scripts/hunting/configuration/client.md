---
icon: circle-small
---

# Client Configuration

File: `configurations/config_client.lua`

This file contains client-side configuration including hunting zones, animal AI, tournament settings, and more.

***

## General Settings

```lua
Config.TEST = false
Config.Currency = "$"
Config.CheckInterval = 1  -- Minutes between checks
Config.ObjectiveAlignment = "center-right"  -- UI objective alignment
```

**ObjectiveAlignment Options**:

* `"center-right"`
* `"center-left"`
* `"top-right"`
* `"top-left"`
* `"bottom-right"`
* `"bottom-left"`

***

## Hunting Restrictions

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

**Important Notes**:

* `OnlyHuntByHuntingWeapons` - When true, only weapons in `HuntingWeapons` table can kill animals
* `DisableHuntingRiflePVP` - Prevents hunting rifles from being used against players
* `OnlyHunterCanCollect` - Only the player who killed the animal can collect the carcass
* `RequireJob` - Set to true if you want only specific job to hunt

***

## Target System

```lua
Config.UseTarget = false  -- Use target system instead of dusa_bridge interactions
```

Set to `true` if you're using a target system (ox\_target, qb-target, etc.) instead of the default interaction system.

***

## Trapping & Baiting

```lua
Config.TrapDamage = 50  -- Damage dealt to trapped animal
Config.BaitChance = 30  -- Chance (%) for bait to attract animals
```

**Configuration**:

* `TrapDamage` - How much damage traps deal (animals have 100 HP)
* `BaitChance` - Percentage chance for bait to successfully attract animals (default: 30%)

***

## Hunting Zones

Define areas where animals spawn:

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
    ['HuntingZone2'] = {
        name = 'Rabbit Zone',
        type = 'rabbit',
        coords = vec3(-716.885, 5310.257, 72.257),
        range = 370.0,
        debug = false,
        animal = {
            model = 'a_c_rabbit_01',
            maxCount = 17,
            xp = 10,
            canAttack = false,
            isFleeing = false,
        }
    },
    ['HuntingZone3'] = {
        name = 'Bear Zone',
        type = 'bear',
        coords = vec3(-117.283, 1435.516, 294.283),
        range = 300.0,
        debug = false,
        animal = {
            model = 'BrnBear',
            maxCount = 5,
            xp = 10,
            canAttack = true,  -- Bears can attack players
            isFleeing = false,
        }
    },
    -- Add more zones...
}
```

**Zone Configuration**:

* `name` - Display name for the zone
* `type` - Must match a species type from `Shared.Species`
* `coords` - Center point of the zone
* `range` - Radius of the zone in meters
* `debug` - Set to `true` to see zone sphere for testing

**Animal Configuration**:

* `model` - Ped model to spawn (must match species model)
* `maxCount` - Maximum number of animals in this zone
  * **⚠️ WARNING**: Don't set too high (causes performance issues)
  * Recommended: 5-15 animals per zone
* `xp` - Experience points awarded per kill
* `canAttack` - Whether animal can attack players (bears, lions, etc.)
* `isFleeing` - Whether animal runs away when shot

***

## Adding Custom Animals

To add a new animal to the hunting system:

### Step 1: Add to Species (Shared Config)

In `config_shared.lua`:

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

### Step 2: Add Hunting Zone (Client Config)

In `config_client.lua`:

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

### Step 3: Add Wiki Entry (Client Config)

In `config_client.lua`:

```lua
Config.Wiki['wolf'] = {
    name = "Wolf",
    info = "Get Information About",
    description = "A fierce predator that hunts in packs."
}
```

### Step 4: Add Rewards (Server Config)

See [Server Configuration](server.md#animal-rewards) for reward configuration.

### Step 5: Add Sellable Items (Shared Config)

In `config_shared.lua`:

```lua
table.insert(Shared.Shop.Sell, {
    item = 'wolf_beef',
    name = 'Wolf Beef',
    price = 80
})
```

### Step 6: Add Items to Inventory

Add wolf items to your inventory system (see [Installation Guide](../installation.md) for item format).

***

## Animal Wiki

Information shown in the hunting laptop/wiki:

```lua
Config.Wiki = {
    ['deer'] = {
        name = "Deer",
        info = "Get Information About",
        description = "A large, graceful herbivore found in forests and grasslands."
    },
    ['rabbit'] = {
        name = "Rabbit",
        info = "Get Information About",
        description = "A small, fast mammal known for its long ears and quick movements."
    },
    ['bear'] = {
        name = "Bear",
        info = "Get Information About",
        description = "A large, powerful mammal known for its strength and hibernation habits."
    },
    -- Add more wiki entries...
}
```

***

## Tournament Configuration

```lua
Config.Tournament = {
    AvailableSpecies = {
        'deer',
        'bear',
        'oryx',
        'boar',
        'coyote',
        'mtlion',
        'redpanda',
        'lion',
        'pig',
        'rabbit',
        'antelope',
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

**Configuration**:

* `AvailableSpecies` - Animals that can be used in tournaments
* `RewardRange` - Min/max reward money for tournaments
* `DurationRange` - Min/max duration in minutes
* `MaxPlayers` - Maximum players per tournament
* `MinPlayers` - Minimum players to start tournament

***

## Butchering Areas

Define butchering machine locations:

```lua
Config.Areas = {
    ['butchering'] = {
        machine = {
            coords = vec3(-89.120, 6234.354, 31.061),
        }
    }
}
```

Add more butchering locations if needed.

***

## Vehicle Carcass Attachment

Configure how carcasses attach to vehicles:

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

    boar = {
        offset = vec3(0.0, 1.4, 1.0),
        rotation = vec3(0.0, 0.0, 0.0),
        alpha = 200,
    },

    rabbit = {
        offset = vec3(0.0, 1.2, 0.8),
        rotation = vec3(0.0, 0.0, 0.0),
        alpha = 200,
    },

    -- Add more animal-specific configurations...
}
```

**Configuration**:

* `offset` - Position offset from vehicle center (x, y, z)
* `rotation` - Rotation angles (x, y, z)
* `alpha` - Transparency (0-255, 255 = fully visible)

If an animal doesn't have specific settings, `default` is used.

***

## Performance Tips

1. **Limit maxCount**: Keep animal count per zone between 5-15
2. **Zone range**: Smaller zones = better performance
3. **Debug mode**: Always disable in production (`debug = false`)
4. **CheckInterval**: Increase to reduce checks (e.g., 5 minutes instead of 1)

***

## Next Steps

* Configure [Server Settings](server.md) for rewards and levels
* Review [Shared Configuration](shared.md) for shop and quests
* Check [Common Issues](../common-issues.md) for troubleshooting
