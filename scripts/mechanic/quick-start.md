# Quick Start Guide

Get your first mechanic shop operational in under 5 minutes.

## Prerequisites

- Completed [Installation](installation.md)
- Server running without errors
- Mechanic tablet item available in inventory

## Step 1: Create Your First Shop (30 seconds)

Open `dusa_mechanicv2/shared/config.lua` and add your shop configuration:

```lua
Config.Shops = {
    {
        name = "bennys",
        label = "Benny's Motorworks",
        coords = vector3(-212.0, -1324.0, 31.0),
        blip = {
            enabled = true,
            sprite = 446,
            color = 5,
            scale = 0.8,
            label = "Benny's Motorworks"
        },
        employees = {},  -- Auto-populated from database
        zones = {
            {
                type = "sphere",
                coords = vector3(-212.0, -1324.0, 31.0),
                radius = 20.0
            }
        }
    }
}
```

**Save the file** and restart the resource:
```
ensure dusa_mechanicv2
```

## Step 2: Add Yourself as Employee (30 seconds)

Use the admin command to add yourself as shop owner:

```bash
/mechanicadmin addemp [playerId] bennys 4
```

- `[playerId]` - Your player ID (find with `/id` command)
- `bennys` - Shop name from config
- `4` - Rank 4 (Owner with full permissions)

**Rank levels:**
- 0 = Trainee (view only)
- 1 = Mechanic (create orders, tune)
- 2 = Senior Mechanic (assign orders)
- 3 = Manager (inventory, employees)
- 4 = Owner (full access, finances)

## Step 3: Open the Tablet (15 seconds)

1. Give yourself the mechanic tablet item:
   ```bash
   /giveitem mechanic_tablet 1
   ```

2. Open your inventory and **use** the mechanic_tablet item

3. The tablet interface should open showing the app list

4. Click on the **Mechanic** app (wrench icon)

5. You should see the Benny's Motorworks dashboard

**If tablet doesn't open:** Check F8 console for errors and verify dusa_tablet is running.

## Step 4: Create a Test Work Order (2 minutes)

Let's create your first work order:

1. In the Mechanic app, click **"New Work Order"** button

2. Fill in the form:
   - **Vehicle Plate**: Enter any plate (e.g., "ABC123")
   - **Customer Name**: Enter test customer name
   - **Vehicle Model**: Optional (auto-detected if near vehicle)
   - **Description**: "Oil change and brake inspection"

3. Add a service:
   - Click **"Add Service"**
   - Service name: "Oil Change"
   - Price: $500

4. Click **"Create Work Order"**

5. You should see a success message and the order in your dashboard

**Congratulations!** You've created your first work order.

## Step 5: Test Vehicle Tuning (2 minutes)

Now let's test the tuning system:

1. Spawn a vehicle and get in as driver

2. Drive to your shop location (within the zone radius)

3. Open the tablet → Mechanic app → **Tuning** tab

4. The tuning menu should open showing categories:
   - Performance
   - Cosmetic
   - Stance
   - Engine Swaps

5. Navigate to **Cosmetic** → **Front Bumper**

6. Select a different bumper option

7. You should see the vehicle update in real-time (preview mode)

8. Click **"Apply"** to purchase and permanently apply the mod

**Note:** Tuning requires sufficient funds in your bank account. Prices are configurable in `config.lua`.

## You're Done! 🎉

Your mechanic shop is now fully operational! You've successfully:

- ✅ Created a mechanic shop
- ✅ Added yourself as shop owner
- ✅ Opened the tablet interface
- ✅ Created a work order
- ✅ Tested vehicle tuning

## Next Steps

Now that your shop is running, explore these features:

### Learn the System
- [Tablet Basics](user-guide/tablet-basics.md) - Master the tablet interface
- [Work Orders](user-guide/work-orders.md) - Complete work order workflow
- [Vehicle Tuning](user-guide/vehicle-tuning.md) - All tuning options explained
- [Parts Management](user-guide/parts-management.md) - Inventory system
- [Shop Management](user-guide/shop-management.md) - Boss menu features

### Customize Your Setup
- [Configuration](configuration.md) - Customize prices, settings, and features
- [First Shop Setup](guides/first-shop-setup.md) - Detailed shop configuration guide
- [Adding Vehicle Mods](guides/adding-vehicle-mods.md) - Add custom modifications
- [Multi-Shop Setup](guides/multi-shop-setup.md) - Run multiple locations

### Hire Your Team
Use the tablet's Management section to:
1. Hire employees (must be nearby)
2. Assign ranks and permissions
3. Track employee performance
4. Manage shop finances

### Common Actions

**Give someone the mechanic job:**
```bash
# ESX
/setjob [playerId] mechanic 4

# QBCore
/job mechanic 4

# Or use tablet Management → Hire Employee
```

**Create additional shops:**
Add more entries to `Config.Shops` in `config.lua` and restart the resource.

**Adjust tuning prices:**
Edit `MechanicConfig.Tuning.Prices` in `config.lua`:
```lua
MechanicConfig.Tuning.Prices = {
    cosmetic = 500,      -- Base price for cosmetic mods
    performance = 2000,  -- Base price for performance parts
    stance = 1500,       -- Base price for stance adjustments
    engine_swap = 50000  -- Base price for engine swaps
}
```

## Troubleshooting

### Tablet won't open
- Check F8 console for errors
- Verify dusa_tablet is running: `ensure dusa_tablet`
- Try relogging to the server

### Mechanic app not showing
- Ensure dusa_mechanicv2 is running: `ensure dusa_mechanicv2`
- Check server console for errors
- Verify resource load order in server.cfg

### Tuning menu won't open
- Ensure you're in the driver seat
- Verify vehicle is within the tuning zone radius
- Check that you have mechanic job

### Can't create work orders
- Verify you have sufficient job rank (minimum rank 1)
- Check database connection
- Review server console for validation errors

For more solutions, see the [Troubleshooting Guide](troubleshooting.md).

## Need More Help?

- **Full Documentation**: Start with [User Guide](user-guide/)
- **Configuration Reference**: [Configuration](configuration.md)
- **Developer Docs**: [Developer Documentation](developer/)
- **Common Issues**: [Troubleshooting](troubleshooting.md)

Happy mechanic work! 🔧
