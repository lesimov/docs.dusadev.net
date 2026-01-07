# Troubleshooting & FAQ

## Common Issues

### Installation Problems

#### Error: "Database connection failed"

**Symptom**: Console shows database connection errors on server start.

**Causes**:
- Incorrect database credentials
- Database server not running
- oxmysql not installed or not started

**Solution**:
```cfg
# Check server.cfg for correct database connection
set mysql_connection_string "mysql://user:password@localhost/database"

# Ensure oxmysql is started before mechanic resources
ensure oxmysql
ensure dusa_bridge
ensure dusa_mechanicv2
```

Verify database server is running and credentials are correct.

#### Error: "Failed to verify protected resource"

**Symptom**: Escrow verification fails when starting the resource.

**Causes**:
- Keymaster not linked to your server
- Wrong Cfx.re account
- License expired or not purchased

**Solution**:
1. Visit [keymaster.fivem.net](https://keymaster.fivem.net)
2. Verify your purchase shows as active
3. Ensure your server IP is linked to the correct keymaster account
4. Restart server completely after linking

#### Error: "ox_lib not found"

**Symptom**: Resource fails to start with ox_lib dependency error.

**Solution**:
```cfg
# Ensure ox_lib is started BEFORE dusa resources in server.cfg
ensure ox_lib
ensure dusa_bridge
ensure dusa_tablet
ensure dusa_mechanicv2
```

Download ox_lib from [GitHub](https://github.com/overextended/ox_lib) if not installed.

---

### Tablet Issues

#### Tablet won't open

**Symptom**: Using mechanic_tablet item does nothing.

**Causes**:
- dusa_tablet resource not started
- NUI errors in F8 console
- Permission issues
- Item not configured in inventory

**Solutions**:

1. **Check server console for errors**
   ```
   ensure dusa_tablet
   ```

2. **Verify resource is running**
   ```
   restart dusa_tablet
   ```

3. **Check F8 client console** for JavaScript errors

4. **Verify inventory item exists** in `ox_inventory/data/items.lua`:
   ```lua
   ['mechanic_tablet'] = {
       label = 'Mechanic Tablet',
       weight = 500,
       stack = false,
       close = true,
       description = 'Professional diagnostic tablet for mechanics'
   }
   ```

5. **Check player has mechanic job**:
   ```bash
   # ESX
   /setjob [id] mechanic 1

   # QBCore
   /job mechanic 1
   ```

#### Mechanic app not showing in tablet

**Symptom**: Tablet opens but mechanic app is missing from app list.

**Causes**:
- App registration failed
- dusa_mechanicv2 not started
- Resource load order incorrect

**Solutions**:

1. **Verify correct load order** in `server.cfg`:
   ```cfg
   ensure ox_lib
   ensure dusa_bridge
   ensure dusa_tablet        # Tablet MUST load before mechanic
   ensure dusa_mechanicv2    # Mechanic loads last
   ```

2. **Check server console** for app registration messages:
   ```
   [dusa_mechanicv2] Registering mechanic app with tablet...
   [dusa_tablet] App registered: mechanic
   ```

3. **Restart both resources** in order:
   ```
   restart dusa_tablet
   restart dusa_mechanicv2
   ```

#### Tablet UI is blank or broken

**Symptom**: Tablet opens but shows blank screen or broken interface.

**Causes**:
- NUI build not compiled
- Web files missing
- Cache issues

**Solutions**:

1. **Rebuild NUI** (if you have access to source):
   ```bash
   cd dusa_tablet/web
   npm install
   npm run build
   ```

2. **Clear FiveM cache**:
   - Close FiveM completely
   - Navigate to `%localappdata%/FiveM/FiveM Application Data/cache`
   - Delete cache folder
   - Restart FiveM

3. **Check F8 console** for 404 errors or missing file warnings

---

### Work Order Issues

#### Can't create work orders

**Symptom**: "Permission denied" or "Failed to create order" errors.

**Causes**:
- Insufficient job permissions
- Database table missing
- Validation error in submitted data

**Solutions**:

1. **Check player job and rank**:
   ```lua
   -- Minimum rank 1 required to create orders
   -- Verify with: /job or check database
   ```

2. **Verify database tables exist**:
   ```sql
   SHOW TABLES LIKE 'shop_orders';
   SHOW TABLES LIKE 'mechanic_employees';
   ```

3. **Check server console** for validation errors showing which fields are invalid

4. **Verify shop exists** in `config.lua` and employee is assigned to that shop

#### Work orders not syncing between players

**Symptom**: Other mechanics don't see newly created orders.

**Causes**:
- Real-time events not configured
- NUI callbacks failing
- Client not refreshing data

**Solutions**:

1. **Check server console** for event errors
2. **Refresh tablet** by closing and reopening
3. **Restart mechanic resource**:
   ```
   restart dusa_mechanicv2
   ```
4. **Verify both players** are assigned to same shop

#### Can't complete work orders

**Symptom**: "Complete" button doesn't work or shows error.

**Causes**:
- Insufficient permissions
- Payment processing failure
- Database update error

**Solutions**:

1. **Verify rank** (rank 1+ required to complete orders)
2. **Check server console** for payment errors
3. **Verify customer** has sufficient funds if payment is required
4. **Check database** for locked transactions or connection issues

---

### Tuning Problems

#### Tuning menu won't open

**Symptom**: Tuning button does nothing or shows "Not in tuning zone" error.

**Causes**:
- Vehicle not in tuning zone
- Player not in vehicle
- Player not driver (passenger)
- Zone configuration error

**Solutions**:

1. **Verify vehicle is within tuning zone** bounds defined in config:
   ```lua
   zones = {
       {
           type = "sphere",
           coords = vector3(-212.0, -1324.0, 31.0),
           radius = 20.0  -- Check this radius
       }
   }
   ```

2. **Ensure player is in driver seat** (not passenger)

3. **Check player has mechanic job**

4. **Increase zone radius** if needed in `config.lua`

5. **Test zone detection** with debug mode:
   ```lua
   MechanicConfig.Debug = true
   ```

#### Mods applied but vehicle doesn't change

**Symptom**: Money deducted but no visual change on vehicle.

**Causes**:
- Client-server desync
- Network ownership issue
- Invalid mod configuration for specific vehicle
- Vehicle model doesn't support selected mod

**Solutions**:

1. **Exit and re-enter vehicle** to force sync

2. **Restart the resource** with vehicle spawned:
   ```
   restart dusa_mechanicv2
   ```

3. **Check mod configuration** in `config.mods.lua` for vehicle class compatibility

4. **Verify vehicle model supports the mod** type (some vehicles can't have certain bumpers, spoilers, etc.)

5. **Check server console** for mod application errors

#### Vehicle slower/worse after engine swap

**Symptom**: Performance degraded after upgrading engine.

**Causes**:
- Handling configuration issue
- Incorrect engine stats in config
- Missing performance multipliers

**Solutions**:

1. **Review handling values** in `config.mods.lua`:
   ```lua
   ['v8_engine'] = {
       fDriveInertia = 1.0,
       fInitialDriveMaxFlatVel = 150.0,
       fInitialDriveForce = 0.35,
       -- Ensure values are correct
   }
   ```

2. **Check engine multipliers** are properly applied

3. **Test with stock engine** to verify base handling is correct

4. **Consult** [Vehicle Tuning Guide](user-guide/vehicle-tuning.md#engine-swaps)

#### Tuning price too high/low

**Symptom**: Tuning costs don't match expectations.

**Solution**:

Adjust prices in `config.lua`:
```lua
MechanicConfig.Tuning.Prices = {
    cosmetic = 500,      -- Base cosmetic mod price
    performance = 2000,  -- Base performance part price
    stance = 1500,       -- Base stance adjustment price
    engine_swap = 50000  -- Base engine swap price
}
```

Individual mod prices can be set in `config.mods.lua`.

---

### Framework Integration

#### ESX: Job not detected

**Symptom**: "You are not a mechanic" despite having the job.

**Causes**:
- Job not in ESX database
- Bridge not detecting ESX
- Player data not loaded

**Solutions**:

1. **Verify job exists** in database:
   ```sql
   SELECT * FROM jobs WHERE name = 'mechanic';
   ```

2. **Add job** if missing:
   ```sql
   INSERT INTO `jobs` (`name`, `label`, `whitelisted`) VALUES
       ('mechanic', 'Mechanic', 1);
   ```

3. **Check bridge detection** in server console:
   ```
   [dusa_bridge] Detected framework: ESX
   ```

4. **Verify player is loaded** before checking job

5. **Restart ESX** and mechanic resources:
   ```
   restart es_extended
   restart dusa_bridge
   restart dusa_mechanicv2
   ```

#### QBCore: Society funds not working

**Symptom**: Can't withdraw/deposit to shop account.

**Causes**:
- Management system not configured
- Society account missing

**Solutions**:

1. **Ensure qb-management** is installed and started

2. **Create society account** in management system

3. **Verify boss grade** is configured correctly in `qb-core/shared/jobs.lua`:
   ```lua
   ['4'] = {
       name = 'Shop Owner',
       payment = 1000,
       isboss = true  -- Required for society access
   }
   ```

#### QBox: Compatibility issues

**Symptom**: Features not working with QBox framework.

**Solution**:

QBox is supported through dusa_bridge. Ensure you're using latest versions:
- QBox core (latest)
- dusa_bridge (latest)

Check server console for framework detection:
```
[dusa_bridge] Detected framework: QBox
```

---

### Performance Issues

#### Server lag when opening tablet

**Symptom**: Noticeable server performance drop when multiple players open tablet.

**Causes**:
- Database queries not optimized
- Too many simultaneous queries
- No caching enabled

**Solutions**:

1. **Enable caching** in `config.lua`:
   ```lua
   MechanicConfig.Cache = {
       enabled = true,
       duration = 300  -- Cache duration in seconds (5 minutes)
   }
   ```

2. **Optimize database queries** by adding indexes:
   ```sql
   CREATE INDEX idx_shop_id ON shop_orders(shop_id);
   CREATE INDEX idx_status ON shop_orders(status);
   CREATE INDEX idx_identifier ON mechanic_employees(identifier);
   ```

3. **Reduce query frequency** in config if real-time sync is not critical

4. **Monitor server performance** with profiler to identify bottlenecks

#### High memory usage

**Symptom**: Resource using excessive memory.

**Solutions**:

1. **Clear old work orders** from database periodically:
   ```sql
   DELETE FROM shop_orders
   WHERE completed_at < DATE_SUB(NOW(), INTERVAL 30 DAY);
   ```

2. **Disable debug logging** if enabled:
   ```lua
   MechanicConfig.Debug = false
   ```

3. **Restart resource periodically** if running 24/7 server

---

## Frequently Asked Questions

### General

#### Q: Which frameworks are supported?
**A:** DUSA Mechanic supports ESX Legacy, QBCore, and QBox out of the box through the dusa_bridge abstraction layer. No code modifications needed.

#### Q: Is this compatible with [inventory system]?
**A:** Yes, supports ox_inventory, qb-inventory, qs-inventory, and other popular inventory systems via dusa_bridge auto-detection.

#### Q: Can I have multiple mechanic shops?
**A:** Yes! Configure multiple shops in `config.lua`. Each shop can have separate employees, inventories, and financial accounts.

#### Q: Does this work with other garage scripts?
**A:** Yes, especially dusa_modulargarages. The system is designed to integrate with most garage/vehicle scripts. See [Garage Integration](integrations/garage-integration.md).

#### Q: Is source code available?
**A:** Partially. Some modules use FiveM escrow protection for security. Core logic is escrow-protected while configuration and integration points are open source. See [Architecture](developer/architecture.md).

### Configuration

#### Q: How do I change tuning prices?
**A:** Edit `MechanicConfig.Tuning.Prices` in `config.lua`:
```lua
MechanicConfig.Tuning.Prices = {
    cosmetic = 500,      -- Cosmetic mods
    performance = 2000,  -- Performance parts
    stance = 1500,       -- Stance adjustments
    engine_swap = 50000  -- Engine swaps
}
```

#### Q: Can I disable certain tuning categories?
**A:** Yes, set `enabled = false` for specific categories in `config.mods.lua`:
```lua
Config.ModCategories = {
    performance = { enabled = true },
    cosmetic = { enabled = true },
    stance = { enabled = false },  -- Disable stance
    engine_swaps = { enabled = true }
}
```

#### Q: How do I add custom vehicle mods?
**A:** See the detailed guide: [Adding Vehicle Mods](guides/adding-vehicle-mods.md)

#### Q: Can I customize the tablet interface?
**A:** Visual customization requires NUI modifications. Color schemes and icons can be adjusted in tablet configuration. For custom apps, see [Creating Tablet Apps](developer/creating-tablet-apps.md).

### Permissions

#### Q: What are the default job ranks?
**A:** Default rank structure:
- **Rank 0**: Trainee - View orders only
- **Rank 1**: Mechanic - Create orders, perform tuning
- **Rank 2**: Senior Mechanic - Assign orders to others
- **Rank 3**: Manager - Manage inventory, hire employees
- **Rank 4**: Owner - Full access, financial management

#### Q: Can I customize rank permissions?
**A:** Yes, edit `MechanicConfig.Permissions` in `config.lua`:
```lua
MechanicConfig.Permissions = {
    create_order = 1,    -- Minimum rank to create orders
    assign_order = 2,    -- Minimum rank to assign orders
    manage_inventory = 3, -- Minimum rank to manage parts
    hire_employees = 3,   -- Minimum rank to hire
    manage_finances = 4   -- Minimum rank for financial access
}
```

#### Q: How do I give someone mechanic job?
**A:** Depends on your framework:
```bash
# ESX
/setjob [playerId] mechanic [rank]

# QBCore
/job mechanic [rank]

# Or use in-game tablet Management → Hire Employee
```

### Economy

#### Q: Where does money go when work order is completed?
**A:** Configurable in `config.lua`:
- Option 1: All to shop society/management account
- Option 2: Split between employee (commission) and shop
- Option 3: Directly to employee (no shop cut)

```lua
MechanicConfig.Economy = {
    payment_mode = 'society',  -- 'society', 'split', or 'employee'
    employee_commission = 0.3   -- If split, 30% to employee
}
```

#### Q: Can customers refuse to pay?
**A:** By default, payment is automatic on order completion. Can be made optional:
```lua
MechanicConfig.WorkOrders = {
    require_customer_approval = true  -- Customer must approve/pay
}
```

#### Q: How do I withdraw shop funds?
**A:** Shop owners (rank 4) use tablet:
1. Open Mechanic app
2. Navigate to Management → Finances
3. Click "Withdraw Funds"
4. Enter amount
5. Confirm

Money goes to personal bank account.

### Development

#### Q: Can I create custom tablet apps?
**A:** Yes! The tablet platform supports custom apps. See [Creating Tablet Apps](developer/creating-tablet-apps.md) for complete tutorial.

#### Q: How do I integrate with other scripts?
**A:** Use the mechanic API callbacks and exports. See [Mechanic API](developer/mechanic-api.md) for available endpoints.

#### Q: Is there a debug mode?
**A:** Yes, enable in `config.lua`:
```lua
MechanicConfig.Debug = true
```

This enables detailed console logging. See [Debugging Guide](developer/debugging.md).

#### Q: Can I contribute to development?
**A:** Community contributions are welcome for open-source modules, documentation improvements, and translations. Contact via GitHub or Discord.

---

## Still Need Help?

### Before Asking for Help

1. ✅ Check console (F8 client + server) for errors
2. ✅ Review this troubleshooting guide
3. ✅ Ensure all resources are up to date
4. ✅ Test with minimal resource configuration
5. ✅ Verify all prerequisites are met

### Providing Debug Information

When asking for help, include:
- **FiveM server version** (artifact number)
- **Framework** (ESX/QBCore/QBox) and version
- **DUSA Mechanic version**
- **Console errors** (both server and client F8)
- **Steps to reproduce** the issue
- **Config.lua settings** (if relevant)
- **Screenshots or video** (if visual issue)

### Support Channels

- **Documentation**: [Full Documentation](README.md)
- **GitHub Issues**: Report bugs and feature requests
- **Discord**: Community support and discussions
- **Updates**: Check for latest versions and patches

### Emergency Fixes

#### Complete resource reset:
```bash
# Stop resource
stop dusa_mechanicv2

# Clear cache
# (Delete FiveM cache folder)

# Restart dependencies
restart oxmysql
restart ox_lib
restart dusa_bridge
restart dusa_tablet

# Start mechanic
ensure dusa_mechanicv2
```

#### Database reset (⚠️ WARNING: Deletes all data):
```sql
DROP TABLE IF EXISTS shop_orders;
DROP TABLE IF EXISTS mechanic_employees;
DROP TABLE IF EXISTS mechanic_shops;
DROP TABLE IF EXISTS mechanic_service_history;
DROP TABLE IF EXISTS mechanic_zones;

-- Restart server to recreate tables via migrations
```

---

**Last Updated**: 2024-01-20
**Applies to**: DUSA Mechanic v1.2.0+
