---
icon: folder-arrow-down
---

# Installation

## Prerequisites

Before installing the Hunting script, ensure you have the following:

- ✅ **Framework**: ESX Legacy, QBCore, or QBOX
- ✅ **dusa_bridge**: Required for framework compatibility
- ✅ **ox_lib**: Required for UI and callbacks
- ✅ **Target System**: ox_target, qb-target, or qtarget
- ✅ **Inventory**: Compatible with ox_inventory, qb-inventory, qs-inventory

## Download & Extract

1. Download the script from your Keymaster or Tebex
2. Extract the `dusa_hunting` folder to your server's `resources` directory
3. Extract `dusa_bridge` if you haven't already

## Script Start Order

The start order is crucial for proper functionality. Add these lines to your `server.cfg`:

### ESX Legacy

```cfg
ensure ox_lib
ensure dusa_bridge
ensure es_extended
ensure [esx_addons]  # Your ESX resources

ensure dusa_hunting
```

### QBCore

```cfg
ensure ox_lib
ensure dusa_bridge
ensure qb-core
ensure [qb]  # Your QBCore resources

ensure dusa_hunting
```

### QBOX

```cfg
ensure ox_lib
ensure dusa_bridge
ensure qbx_core
ensure [qbx]  # Your QBOX resources

ensure dusa_hunting
```

## Item Configuration

Add the following items to your framework's items database:

### For ox_inventory / qb-inventory

Add these items to your `items.lua` or items configuration:

```lua
-- Hunting Equipment
['hunting_license'] = {
    label = 'Hunting License',
    weight = 10,
    stack = false,
    close = true,
    description = 'Official hunting license'
},

['hunting_bait'] = {
    label = 'Animal Bait',
    weight = 50,
    stack = true,
    close = true,
    description = 'Bait to attract animals'
},

['hunting_trap'] = {
    label = 'Animal Trap',
    weight = 500,
    stack = true,
    close = true,
    description = 'Trap for catching small animals'
},

['tent'] = {
    label = 'Camping Tent',
    weight = 2000,
    stack = false,
    close = true,
    description = 'Portable tent for camping'
},

['campfire'] = {
    label = 'Campfire Kit',
    weight = 1000,
    stack = true,
    close = true,
    description = 'Everything needed to start a campfire'
},

-- Animal Products
['deer_pelt'] = {
    label = 'Deer Pelt',
    weight = 500,
    stack = true,
    close = true,
    description = 'High quality deer pelt'
},

['deer_meat'] = {
    label = 'Raw Deer Meat',
    weight = 300,
    stack = true,
    close = true,
    description = 'Fresh deer meat, needs cooking'
},

['cooked_meat'] = {
    label = 'Cooked Meat',
    weight = 250,
    stack = true,
    close = true,
    description = 'Delicious cooked meat',
    client = {
        status = { hunger = 200000 },
        usetime = 5000
    }
},

['rabbit_pelt'] = {
    label = 'Rabbit Pelt',
    weight = 100,
    stack = true,
    close = true,
    description = 'Soft rabbit pelt'
},

['boar_meat'] = {
    label = 'Raw Boar Meat',
    weight = 400,
    stack = true,
    close = true,
    description = 'Wild boar meat'
},

['coyote_pelt'] = {
    label = 'Coyote Pelt',
    weight = 300,
    stack = true,
    close = true,
    description = 'Coyote pelt'
},

-- Hunting Tools
['knife'] = {
    label = 'Hunting Knife',
    weight = 200,
    stack = false,
    close = true,
    description = 'Sharp knife for skinning animals'
},
```

## Database Setup

No SQL installation is required. The script uses statebags and server-side data management.

## Configuration

1. Navigate to `dusa_hunting/configurations/`
2. Open `config_shared.lua` and configure:
   - Framework type
   - Hunting zones
   - Animal spawns
   - Shop locations

3. Open `config_client.lua` and configure:
   - UI settings
   - Keybinds
   - Visual effects

## Verification Steps

After installation, verify everything works:

1. **Start Your Server**
   ```bash
   # Check console for errors
   # Look for: "dusa_hunting started successfully"
   ```

2. **In-Game Testing**
   - Join your server
   - Check for hunting shop blips on the map
   - Try purchasing a hunting license
   - Visit a hunting zone

3. **Check Framework Bridge**
   ```lua
   # In F8 console
   /testbridge
   ```

4. **Common Checks**
   - ✅ No errors in F8 console
   - ✅ Hunting shops appear on map
   - ✅ Can purchase items from shop
   - ✅ Animals spawn in hunting zones
   - ✅ Can harvest animals

## Troubleshooting

If you encounter issues:

- **Animals not spawning**: Check hunting zone coordinates in config
- **Shop not appearing**: Verify blip settings in config
- **Items not working**: Ensure items are added to your inventory system
- **Framework errors**: Confirm dusa_bridge is started before dusa_hunting

For more help, see [Common Issues](common-issues.md) or join our Discord:

{% embed url="https://discord.gg/dusa" %}

## Next Steps

Ready to start hunting? Check out the [Getting Started](getting-started.md) guide!
