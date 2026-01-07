# Installation

Complete step-by-step installation guide for DUSA Mechanic.

## Prerequisites

Before installing DUSA Mechanic, ensure your server meets these requirements:

- **FiveM Server** - Artifact 5181 or higher
- **ox_lib** - Latest version installed and started
- **Database System** - MySQL or MariaDB
- **Supported Framework** - One of the following:
  - ESX Legacy (latest version)
  - QBCore (latest version)
  - QBox (latest version)

## Step 1: Download & Extract

1. Download the DUSA Mechanic package from your keymaster
2. Extract the ZIP file to a temporary location
3. You should have three folders:
   - `dusa_bridge`
   - `dusa_tablet`
   - `dusa_mechanicv2` (or `mechanic-spec`)

**File Structure:**
```
dusa_mechanic_package/
├── dusa_bridge/
│   ├── fxmanifest.lua
│   ├── bridge/
│   └── ...
├── dusa_tablet/
│   ├── fxmanifest.lua
│   ├── web/
│   └── ...
└── dusa_mechanicv2/
    ├── fxmanifest.lua
    ├── server/
    ├── client/
    └── ...
```

## Step 2: Resource Placement

Move the extracted folders to your server's resources directory:

1. Copy `dusa_bridge` to `resources/[dusa]/dusa_bridge`
2. Copy `dusa_tablet` to `resources/[dusa]/dusa_tablet`
3. Copy `dusa_mechanicv2` to `resources/[dusa]/dusa_mechanicv2`

**Recommended folder structure:**
```
resources/
└── [dusa]/
    ├── dusa_bridge/
    ├── dusa_tablet/
    └── dusa_mechanicv2/
```

**Note:** You can use any folder name instead of `[dusa]`, but ensure all three resources are together.

## Step 3: Database Setup

Database tables are created automatically on first start through the migration system.

**Automatic Migration:**
```lua
-- In dusa_mechanicv2/shared/config.lua (default setting)
MechanicConfig.Database = {
    AutoMigration = true  -- Migrations run automatically on first start
}
```

**Tables Created:**
- `mechanic_shops` - Shop locations and settings
- `mechanic_employees` - Employee records
- `shop_orders` - Work order tracking
- `mechanic_service_history` - Service history records
- `mechanic_zones` - Service/tuning zone definitions

**Manual Import (if needed):**
If automatic migration fails, manually import from `dusa_mechanicv2/sql/`:
```bash
mysql -u username -p database_name < dusa_mechanicv2/sql/migrations/001_initial_schema.sql
```

## Step 4: Framework Configuration

Configure the mechanic job in your framework.

### For ESX Legacy

Add mechanic job to your database:

```sql
INSERT INTO `jobs` (`name`, `label`, `whitelisted`) VALUES
    ('mechanic', 'Mechanic', 1);

INSERT INTO `job_grades` (`job_name`, `grade`, `name`, `label`, `salary`) VALUES
    ('mechanic', 0, 'trainee', 'Trainee', 200),
    ('mechanic', 1, 'mechanic', 'Mechanic', 400),
    ('mechanic', 2, 'senior', 'Senior Mechanic', 600),
    ('mechanic', 3, 'manager', 'Manager', 800),
    ('mechanic', 4, 'boss', 'Shop Owner', 1000);
```

Create society account:
```sql
INSERT INTO `addon_account` (`name`, `label`, `shared`) VALUES
    ('society_mechanic', 'Mechanic Shop', 1);
```

### For QBCore

Add to `qb-core/shared/jobs.lua`:

```lua
['mechanic'] = {
    label = 'Mechanic',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'Trainee', payment = 200 },
        ['1'] = { name = 'Mechanic', payment = 400 },
        ['2'] = { name = 'Senior Mechanic', payment = 600 },
        ['3'] = { name = 'Manager', payment = 800, isboss = false },
        ['4'] = { name = 'Shop Owner', payment = 1000, isboss = true },
    },
},
```

### For QBox

Add to `qbx_core/shared/jobs.lua`:

```lua
['mechanic'] = {
    label = 'Mechanic',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'Trainee', payment = 200 },
        ['1'] = { name = 'Mechanic', payment = 400 },
        ['2'] = { name = 'Senior Mechanic', payment = 600 },
        ['3'] = { name = 'Manager', payment = 800 },
        ['4'] = { name = 'Shop Owner', payment = 1000, isboss = true },
    },
},
```

## Step 5: Inventory Items

Add mechanic items to your inventory system.

### For ox_inventory

Add to `ox_inventory/data/items.lua`:

```lua
['mechanic_tablet'] = {
    label = 'Mechanic Tablet',
    weight = 500,
    stack = false,
    close = true,
    description = 'Professional diagnostic tablet for mechanics',
    client = {
        image = 'mechanic_tablet.png'
    }
},

['repair_kit'] = {
    label = 'Repair Kit',
    weight = 1000,
    stack = true,
    close = true,
    description = 'Basic vehicle repair tools'
},

['engine_oil'] = {
    label = 'Engine Oil',
    weight = 200,
    stack = true,
    close = true,
    description = '5W-30 synthetic engine oil'
},
```

**Note:** See [Item Catalog](reference/item-catalog.md) for complete item list.

### For qb-inventory

Add to `qb-core/shared/items.lua`:

```lua
['mechanic_tablet'] = {
    name = 'mechanic_tablet',
    label = 'Mechanic Tablet',
    weight = 500,
    type = 'item',
    image = 'mechanic_tablet.png',
    unique = true,
    useable = true,
    shouldClose = true,
    description = 'Professional diagnostic tablet for mechanics'
},

-- Add other items...
```

## Step 6: Server Configuration

Add resources to `server.cfg` in the correct order:

```cfg
# Core dependencies
ensure oxmysql
ensure ox_lib

# DUSA Mechanic (order is important)
ensure dusa_bridge
ensure dusa_tablet
ensure dusa_mechanicv2
```

**Important:** Load order matters! `dusa_bridge` must start before `dusa_tablet` and `dusa_mechanicv2`.

## Step 7: First Start

1. Start your FiveM server
2. Watch console for startup messages:
   ```
   [dusa_bridge] Detected framework: ESX
   [dusa_tablet] Tablet system initialized
   [dusa_mechanicv2] Database migrations completed
   [dusa_mechanicv2] Mechanic system ready
   ```

3. Check for errors - there should be none if installation was successful

## Verification Checklist

Verify your installation is working correctly:

- [ ] No console errors on server start
- [ ] Database tables created (check with SQL client)
- [ ] Tablet opens with `/tablet` command or mechanic_tablet item
- [ ] Mechanic app visible in tablet app list
- [ ] Can navigate tablet interface without errors
- [ ] F8 console (client) shows no JavaScript errors

## Common Installation Issues

### Error: "ox_lib not found"
**Solution:** Ensure ox_lib is installed and started before DUSA resources in server.cfg

### Error: "Database connection failed"
**Solution:** Verify oxmysql is properly configured with correct database credentials

### Error: "Failed to verify protected resource"
**Solution:** Check keymaster.fivem.net to ensure your server IP is linked to your purchase

### Tablet doesn't open
**Solution:**
1. Check server console for errors
2. Verify `ensure dusa_tablet` in server.cfg
3. Check F8 client console for NUI errors

See [Troubleshooting Guide](troubleshooting.md) for more solutions.

## Next Steps

Now that installation is complete:

1. Follow the [Quick Start Guide](quick-start.md) to set up your first shop
2. Read [Configuration](configuration.md) to customize settings
3. Learn the [Tablet Interface](user-guide/tablet-basics.md)
4. Create your first [Work Order](user-guide/work-orders.md)

## Need Help?

If you encounter issues during installation:

- Check the [Troubleshooting Guide](troubleshooting.md)
- Review console logs for error messages
- Ensure all prerequisites are met
- Verify resource load order in server.cfg
