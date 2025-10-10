# Installation Guide

This guide will walk you through the installation and setup of the Dusa Hunting System.

## Prerequisites

Before installing the hunting system, ensure you have the following:

1. **FiveM Server** - A running FiveM server (recommended: latest artifacts)
2. **Framework** - QBCore, ESX, or QBox
3. **Required Resources**:
   - [ox_lib](https://github.com/overextended/ox_lib) - Required library
   - [dusa_bridge](https://github.com/D-Development-FiveM/dusa_bridge) - Framework bridge

4. **Optional Resources**:
   - [MugShotBase64](https://github.com/BaziForYou/MugShotBase64) - For hunting license ID cards

## Step-by-Step Installation

### Step 1: Download the Resource

1. Download the `dusa_hunting` resource
2. Extract the archive to your server's `resources` folder
3. Ensure the folder name is `dusa_hunting` (without any version numbers)

### Step 2: Install Dependencies

1. **Install ox_lib**:
   - Download from: https://github.com/overextended/ox_lib/releases
   - Place in your `resources` folder
   - Add to `server.cfg`: `ensure ox_lib`

2. **Install dusa_bridge**:
   - Download from: https://github.com/D-Development-FiveM/dusa_bridge
   - Place in your `resources` folder
   - Add to `server.cfg`: `ensure dusa_bridge`

3. **(Optional) Install MugShotBase64**:
   - Download from: https://github.com/BaziForYou/MugShotBase64
   - Place in your `resources` folder
   - Add to `server.cfg`: `ensure MugShotBase64`

### Step 3: Database Setup

1. Import the SQL file to create necessary tables:
   ```sql
   -- The script will auto-create tables on first run
   -- Or manually import the provided SQL file
   ```

2. Tables created:
   - `hunting_data` - Player hunting progress and levels
   - `hunting_quests` - Player quest progress

### Step 4: Add Items to Your Inventory

Add the following items to your inventory system's item definitions:

#### Weapons
```lua
['WEAPON_DHR31'] = {
    label = 'Hunting Rifle',
    weight = 5000,
    type = 'weapon',
    ammotype = 'AMMO_SNIPER',
    image = 'WEAPON_DHR31.png',
    unique = true,
    useable = false,
    description = 'A powerful hunting rifle'
}
```

#### Ammunition
```lua
['ammo-heavysniper'] = {
    label = 'Heavy Sniper Ammo',
    weight = 100,
    type = 'item',
    image = 'ammo-heavysniper.png',
    unique = false,
    useable = true,
    description = 'Ammunition for hunting rifles'
}
```

#### Tools & Equipment
```lua
['hunting_license'] = {
    label = 'Hunting License',
    weight = 50,
    type = 'item',
    image = 'hunting_license.png',
    unique = true,
    useable = true,
    description = 'Official hunting license'
},

['hunting_bait'] = {
    label = 'Hunting Bait',
    weight = 100,
    type = 'item',
    image = 'hunting_bait.png',
    unique = false,
    useable = true,
    description = 'Bait to attract animals'
},

['hunting_trap'] = {
    label = 'Hunting Trap',
    weight = 500,
    type = 'item',
    image = 'hunting_trap.png',
    unique = false,
    useable = true,
    description = 'Trap for catching animals'
},

['binocular'] = {
    label = 'Binoculars',
    weight = 200,
    type = 'item',
    image = 'binocular.png',
    unique = false,
    useable = true,
    description = 'For scouting animals'
},

['hunting_laptop'] = {
    label = 'Hunting Laptop',
    weight = 1000,
    type = 'item',
    image = 'hunting_laptop.png',
    unique = false,
    useable = true,
    description = 'Laptop for environmental analysis'
},

['campfire'] = {
    label = 'Campfire',
    weight = 500,
    type = 'item',
    image = 'campfire.png',
    unique = false,
    useable = true,
    description = 'Portable campfire'
},

['primitive_grill'] = {
    label = 'Primitive Grill',
    weight = 800,
    type = 'item',
    image = 'primitive_grill.png',
    unique = false,
    useable = true,
    description = 'Basic cooking grill'
},

['advanced_grill'] = {
    label = 'Advanced Grill',
    weight = 1200,
    type = 'item',
    image = 'advanced_grill.png',
    unique = false,
    useable = true,
    description = 'Advanced cooking grill'
}
```

#### Animal Meats & Products

<details>
<summary>Deer Items</summary>

```lua
['deer_beef'] = {
    label = 'Deer Beef',
    weight = 200,
    type = 'item',
    image = 'deer_beef.png',
    unique = false,
    useable = false,
    description = 'Raw deer beef'
},
['deer_beef_cooked'] = {
    label = 'Cooked Deer Beef',
    weight = 200,
    type = 'item',
    image = 'deer_beef_cooked.png',
    unique = false,
    useable = true,
    description = 'Delicious cooked deer beef'
},
['deer_rib'] = {
    label = 'Deer Rib',
    weight = 150,
    type = 'item',
    image = 'deer_rib.png',
    unique = false,
    useable = false,
    description = 'Raw deer rib'
},
['deer_rib_cooked'] = {
    label = 'Cooked Deer Rib',
    weight = 150,
    type = 'item',
    image = 'deer_rib_cooked.png',
    unique = false,
    useable = true,
    description = 'Cooked deer rib'
},
['deer_leg'] = {
    label = 'Deer Leg',
    weight = 180,
    type = 'item',
    image = 'deer_leg.png',
    unique = false,
    useable = false,
    description = 'Raw deer leg'
},
['deer_leg_cooked'] = {
    label = 'Cooked Deer Leg',
    weight = 180,
    type = 'item',
    image = 'deer_leg_cooked.png',
    unique = false,
    useable = true,
    description = 'Cooked deer leg'
}
```
</details>

<details>
<summary>Bear Items</summary>

```lua
['bear_beef'] = {
    label = 'Bear Beef',
    weight = 300,
    type = 'item',
    image = 'bear_beef.png',
    unique = false,
    useable = false,
    description = 'Raw bear beef'
},
['bear_beef_cooked'] = {
    label = 'Cooked Bear Beef',
    weight = 300,
    type = 'item',
    image = 'bear_beef_cooked.png',
    unique = false,
    useable = true,
    description = 'Cooked bear beef'
},
['bear_rib'] = {
    label = 'Bear Rib',
    weight = 250,
    type = 'item',
    image = 'bear_rib.png',
    unique = false,
    useable = false,
    description = 'Raw bear rib'
},
['bear_rib_cooked'] = {
    label = 'Cooked Bear Rib',
    weight = 250,
    type = 'item',
    image = 'bear_rib_cooked.png',
    unique = false,
    useable = true,
    description = 'Cooked bear rib'
},
['bear_leg'] = {
    label = 'Bear Leg',
    weight = 280,
    type = 'item',
    image = 'bear_leg.png',
    unique = false,
    useable = false,
    description = 'Raw bear leg'
},
['bear_leg_cooked'] = {
    label = 'Cooked Bear Leg',
    weight = 280,
    type = 'item',
    image = 'bear_leg_cooked.png',
    unique = false,
    useable = true,
    description = 'Cooked bear leg'
}
```
</details>

<details>
<summary>Rabbit Items</summary>

```lua
['rabbit_body'] = {
    label = 'Rabbit Body',
    weight = 100,
    type = 'item',
    image = 'rabbit_body.png',
    unique = false,
    useable = false,
    description = 'Raw rabbit body'
},
['rabbit_body_cooked'] = {
    label = 'Cooked Rabbit Body',
    weight = 100,
    type = 'item',
    image = 'rabbit_body_cooked.png',
    unique = false,
    useable = true,
    description = 'Cooked rabbit body'
},
['rabbit_leg'] = {
    label = 'Rabbit Leg',
    weight = 80,
    type = 'item',
    image = 'rabbit_leg.png',
    unique = false,
    useable = false,
    description = 'Raw rabbit leg'
},
['rabbit_leg_cooked'] = {
    label = 'Cooked Rabbit Leg',
    weight = 80,
    type = 'item',
    image = 'rabbit_leg_cooked.png',
    unique = false,
    useable = true,
    description = 'Cooked rabbit leg'
},
['rabbit_beef'] = {
    label = 'Rabbit Beef',
    weight = 90,
    type = 'item',
    image = 'rabbit_beef.png',
    unique = false,
    useable = false,
    description = 'Raw rabbit beef'
},
['rabbit_beef_cooked'] = {
    label = 'Cooked Rabbit Beef',
    weight = 90,
    type = 'item',
    image = 'rabbit_beef_cooked.png',
    unique = false,
    useable = true,
    description = 'Cooked rabbit beef'
}
```
</details>

<details>
<summary>Other Animals (Boar, Coyote, Lion, Mountain Lion, Oryx, Antelope, Red Panda)</summary>

```lua
-- Boar
['boar_leg'] = { label = 'Boar Leg', weight = 200, type = 'item', image = 'boar_leg.png', unique = false, useable = false },
['boar_leg_cooked'] = { label = 'Cooked Boar Leg', weight = 200, type = 'item', image = 'boar_leg_cooked.png', unique = false, useable = true },
['boar_beef'] = { label = 'Boar Beef', weight = 220, type = 'item', image = 'boar_beef.png', unique = false, useable = false },
['boar_beef_cooked'] = { label = 'Cooked Boar Beef', weight = 220, type = 'item', image = 'boar_beef_cooked.png', unique = false, useable = true },
['boar_rib'] = { label = 'Boar Rib', weight = 180, type = 'item', image = 'boar_rib.png', unique = false, useable = false },
['boar_rib_cooked'] = { label = 'Cooked Boar Rib', weight = 180, type = 'item', image = 'boar_rib_cooked.png', unique = false, useable = true },

-- Coyote
['coyote_beef'] = { label = 'Coyote Beef', weight = 180, type = 'item', image = 'coyote_beef.png', unique = false, useable = false },
['coyote_beef_cooked'] = { label = 'Cooked Coyote Beef', weight = 180, type = 'item', image = 'coyote_beef_cooked.png', unique = false, useable = true },
['coyote_rib'] = { label = 'Coyote Rib', weight = 150, type = 'item', image = 'coyote_rib.png', unique = false, useable = false },
['coyote_rib_cooked'] = { label = 'Cooked Coyote Rib', weight = 150, type = 'item', image = 'coyote_rib_cooked.png', unique = false, useable = true },
['coyote_leg'] = { label = 'Coyote Leg', weight = 160, type = 'item', image = 'coyote_leg.png', unique = false, useable = false },
['coyote_leg_cooked'] = { label = 'Cooked Coyote Leg', weight = 160, type = 'item', image = 'coyote_leg_cooked.png', unique = false, useable = true },

-- Mountain Lion
['mtlion_beef'] = { label = 'Mountain Lion Beef', weight = 250, type = 'item', image = 'mtlion_beef.png', unique = false, useable = false },
['mtlion_beef_cooked'] = { label = 'Cooked Mountain Lion Beef', weight = 250, type = 'item', image = 'mtlion_beef_cooked.png', unique = false, useable = true },
['mtlion_rib'] = { label = 'Mountain Lion Rib', weight = 220, type = 'item', image = 'mtlion_rib.png', unique = false, useable = false },
['mtlion_rib_cooked'] = { label = 'Cooked Mountain Lion Rib', weight = 220, type = 'item', image = 'mtlion_rib_cooked.png', unique = false, useable = true },
['mtlion_leg'] = { label = 'Mountain Lion Leg', weight = 240, type = 'item', image = 'mtlion_leg.png', unique = false, useable = false },
['mtlion_leg_cooked'] = { label = 'Cooked Mountain Lion Leg', weight = 240, type = 'item', image = 'mtlion_leg_cooked.png', unique = false, useable = true },

-- Lion
['lion_beef'] = { label = 'Lion Beef', weight = 300, type = 'item', image = 'lion_beef.png', unique = false, useable = false },
['lion_beef_cooked'] = { label = 'Cooked Lion Beef', weight = 300, type = 'item', image = 'lion_beef_cooked.png', unique = false, useable = true },
['lion_rib'] = { label = 'Lion Rib', weight = 270, type = 'item', image = 'lion_rib.png', unique = false, useable = false },
['lion_rib_cooked'] = { label = 'Cooked Lion Rib', weight = 270, type = 'item', image = 'lion_rib_cooked.png', unique = false, useable = true },
['lion_leg'] = { label = 'Lion Leg', weight = 290, type = 'item', image = 'lion_leg.png', unique = false, useable = false },
['lion_leg_cooked'] = { label = 'Cooked Lion Leg', weight = 290, type = 'item', image = 'lion_leg_cooked.png', unique = false, useable = true },

-- Oryx
['oryx_beef'] = { label = 'Oryx Beef', weight = 210, type = 'item', image = 'oryx_beef.png', unique = false, useable = false },
['oryx_beef_cooked'] = { label = 'Cooked Oryx Beef', weight = 210, type = 'item', image = 'oryx_beef_cooked.png', unique = false, useable = true },
['oryx_rib'] = { label = 'Oryx Rib', weight = 180, type = 'item', image = 'oryx_rib.png', unique = false, useable = false },
['oryx_rib_cooked'] = { label = 'Cooked Oryx Rib', weight = 180, type = 'item', image = 'oryx_rib_cooked.png', unique = false, useable = true },
['oryx_leg'] = { label = 'Oryx Leg', weight = 200, type = 'item', image = 'oryx_leg.png', unique = false, useable = false },
['oryx_leg_cooked'] = { label = 'Cooked Oryx Leg', weight = 200, type = 'item', image = 'oryx_leg_cooked.png', unique = false, useable = true },

-- Antelope
['antelope_beef'] = { label = 'Antelope Beef', weight = 200, type = 'item', image = 'antelope_beef.png', unique = false, useable = false },
['antelope_beef_cooked'] = { label = 'Cooked Antelope Beef', weight = 200, type = 'item', image = 'antelope_beef_cooked.png', unique = false, useable = true },
['antelope_rib'] = { label = 'Antelope Rib', weight = 170, type = 'item', image = 'antelope_rib.png', unique = false, useable = false },
['antelope_rib_cooked'] = { label = 'Cooked Antelope Rib', weight = 170, type = 'item', image = 'antelope_rib_cooked.png', unique = false, useable = true },
['antelope_leg'] = { label = 'Antelope Leg', weight = 190, type = 'item', image = 'antelope_leg.png', unique = false, useable = false },
['antelope_leg_cooked'] = { label = 'Cooked Antelope Leg', weight = 190, type = 'item', image = 'antelope_leg_cooked.png', unique = false, useable = true },

-- Red Panda
['redpanda_body'] = { label = 'Red Panda Body', weight = 120, type = 'item', image = 'redpanda_body.png', unique = false, useable = false },
['redpanda_body_cooked'] = { label = 'Cooked Red Panda Body', weight = 120, type = 'item', image = 'redpanda_body_cooked.png', unique = false, useable = true },
['redpanda_leg'] = { label = 'Red Panda Leg', weight = 100, type = 'item', image = 'redpanda_leg.png', unique = false, useable = false },
['redpanda_leg_cooked'] = { label = 'Cooked Red Panda Leg', weight = 100, type = 'item', image = 'redpanda_leg_cooked.png', unique = false, useable = true },
['redpanda_beef'] = { label = 'Red Panda Beef', weight = 110, type = 'item', image = 'redpanda_beef.png', unique = false, useable = false },
['redpanda_beef_cooked'] = { label = 'Cooked Red Panda Beef', weight = 110, type = 'item', image = 'redpanda_beef_cooked.png', unique = false, useable = true },

-- Hide
['hide'] = {
    label = 'Animal Hide',
    weight = 150,
    type = 'item',
    image = 'hide.png',
    unique = false,
    useable = false,
    description = 'Animal hide that can be sold'
}
```
</details>

### Step 5: Server Configuration

Add to your `server.cfg`:

```cfg
# Make sure dependencies are started first
ensure ox_lib
ensure dusa_bridge

# Optional
# ensure MugShotBase64

# Start the hunting resource
ensure dusa_hunting
```

**Important**: The order matters! Dependencies must be started before `dusa_hunting`.

### Step 6: Configure the Script

1. Navigate to `resources/dusa_hunting/configurations/`
2. Edit the configuration files:
   - `config_shared.lua` - Shared configuration (species, shop, quests, etc.)
   - `config_client.lua` - Client-side configuration (hunting zones, areas, etc.)
   - `config_server.lua` - Server-side configuration (rewards, levels, etc.)

3. Configure hunting zones in `config_client.lua`:
   ```lua
   HuntingZones = {
       ['HuntingZone1'] = {
           name = 'Deer Zone',
           type = 'deer',
           coords = vec3(-575.706, 5460.014, 60.558),
           range = 250.0,
           animal = {
               model = 'a_c_deer',
               maxCount = 12,
               xp = 10,
               canAttack = false,
               isFleeing = false,
           }
       },
       -- Add more zones...
   }
   ```

4. Configure shop location in `config_shared.lua`:
   ```lua
   Shared.Shop = {
       Ped = {
           model = 'a_m_m_hillbilly_01',
           coords = vec4(-675.868, 5839.285, 17.320, 134.746),
           -- ...
       }
   }
   ```

### Step 7: Restart Your Server

1. Restart your FiveM server
2. Check the console for any errors
3. Join the server and test the hunting system

### Step 8: Verify Installation

1. **Check for hunting shop NPC** at the configured location
2. **Test buying hunting equipment**
3. **Visit a hunting zone** and verify animals spawn
4. **Hunt an animal** to test the complete workflow

## Post-Installation

### Optional: Customize Localization

Edit locale files in `resources/dusa_hunting/locales/`:
- `en.json` - English (default)
- `tr.json` - Turkish

Change locale in `config_shared.lua`:
```lua
Shared.Locale = 'en' -- or 'tr'
```

### Optional: Add Custom Animals

See the [Configuration Guide](configuration.md) for adding custom animal types.

### Optional: Vehicle Keys Integration

The script supports multiple vehicle key systems. If you use one, it will automatically integrate. Supported systems:
- dusa_vehiclekeys
- wasabi_carlock
- qb-vehiclekeys
- qs-vehiclekeys
- vehicles_keys
- ak47_vehiclekeys
- Renewed-Vehiclekeys

## Troubleshooting

If you encounter issues during installation, see the [Common Issues](common-issues.md) guide.

## Next Steps

- Review the [API Reference](api-reference.md) for integration with other scripts
- Check the [Configuration Guide](configuration.md) for customization options
- Join the support Discord for help and updates
