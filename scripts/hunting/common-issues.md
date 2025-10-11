---
icon: worm
---

# Common Issues

This guide addresses common issues and questions when setting up or using the Dusa Hunting System.

## Table of Contents

* [Installation Issues](common-issues.md#installation-issues)
* [Animal Spawning Issues](common-issues.md#animal-spawning-issues)
* [Item & Inventory Issues](common-issues.md#item--inventory-issues)
* [Shop & NPC Issues](common-issues.md#shop--npc-issues)
* [Vehicle Rental Issues](common-issues.md#vehicle-rental-issues)
* [Quest & Level System Issues](common-issues.md#quest--level-system-issues)
* [Performance Issues](common-issues.md#performance-issues)
* [Integration Issues](common-issues.md#integration-issues)
* [Frequently Asked Questions](common-issues.md#frequently-asked-questions)

***

## Installation Issues

### Script Won't Start

**Symptoms**: Script fails to start, console shows errors

**Common Causes**:

1. Missing dependencies
2. Incorrect resource order
3. Corrupted files
4. Wrong folder name

**Solutions**:

1.  **Check dependencies** are installed and started:

    ```cfg
    ensure ox_lib
    ensure dusa_bridge
    ensure dusa_hunting
    ```
2. **Verify folder name** is exactly `dusa_hunting`
3. **Check console** for specific error messages
4. **Ensure proper load order**:
   * ox\_lib must start before dusa\_hunting
   * dusa\_bridge must start before dusa\_hunting
5. **Verify file integrity** - re-download if necessary

***

### Database Errors

**Symptoms**: SQL errors on resource start

**Solutions**:

1. **Manual import**: Import the provided SQL file if auto-creation fails
2. **Check permissions**: Ensure database user has CREATE TABLE privileges
3. **Verify connection**: Check your framework's database connection

***

### Missing ox\_lib Error

**Symptoms**: Error message about missing ox\_lib

**Solution**:

1. Download ox\_lib from: https://github.com/overextended/ox\_lib/releases
2. Place in resources folder
3.  Add to server.cfg BEFORE dusa\_hunting:

    ```cfg
    ensure ox_lib
    ```

***

## Animal Spawning Issues

### Animals Not Spawning

**Symptoms**: No animals appear in hunting zones

**Common Causes**:

1. Player not in hunting zone
2. Zone configuration issue
3. Model not loaded
4. maxCount too low

**Solutions**:

1.  **Check zone radius**:

    ```lua
    Config.HuntingZones['Zone1'] = {
        coords = vec3(x, y, z),
        range = 250.0,  -- Increase if needed
    }
    ```
2.  **Enable debug mode** to see zone boundaries:

    ```lua
    debug = true
    ```
3. **Verify animal model** exists in game
4.  **Increase maxCount**:

    ```lua
    animal = {
        maxCount = 15,  -- Increase from 5
    }
    ```

    **Warning**: Don't set too high (causes performance issues)
5. **Check console** for model loading errors

***

### Animals Not Responding to Shots

**Symptoms**: Animals don't die when shot

**Common Causes**:

1. Using non-hunting weapon
2. OnlyHuntByHuntingWeapons enabled
3. God mode enabled

**Solutions**:

1.  **Check weapon configuration**:

    ```lua
    Config.OnlyHuntByHuntingWeapons = true
    Config.HuntingWeapons = {
        'WEAPON_DHR31',
        -- Add your weapon here
    }
    ```
2. **Disable god mode** on player
3. **Verify weapon ammo type** is correct

***

## Item & Inventory Issues

### Items Not Appearing in Inventory

**Symptoms**: Killed animal but no items received

**Common Causes**:

1. Inventory full
2. Items not added to inventory system
3. Item name mismatch

**Solutions**:

1. **Check inventory space** - ensure player has room
2.  **Verify items are registered** in inventory:

    ```lua
    -- QBCore: shared/items.lua
    -- ESX: database items table
    ['deer_beef'] = {
        label = 'Deer Beef',
        weight = 200,
        -- ...
    }
    ```
3. **Check item names match** exactly between:
   * Config files
   * Inventory items
   * Database
4. **Check console** for "item not found" errors

***

### Images Not Showing

**Symptoms**: Item images appear as placeholders

**Solutions**:

1. **Check image paths** exist:
   * Default: `ox_inventory/web/images/ (or your inventory)`
   * Format: `item_name.png` or `item_name.webp`
2.  **Set correct extension** in config:

    ```lua
    Shared.InventoryImageExtension = 'png'  -- or 'webp'
    ```
3. **Verify image files** are named exactly as item names
4. **Clear browser cache** if using web-based inventory

***

## Shop & NPC Issues

### Shop NPC Not Appearing

**Symptoms**: Shop ped doesn't spawn

**Solutions**:

1.  **Check coordinates**:

    ```lua
    Shared.Shop.Ped.coords = vec4(x, y, z, heading)
    ```
2.  **Verify model exists**:

    ```lua
    Shared.Shop.Ped.model = 'a_m_m_hillbilly_01'
    ```
3.  **Ensure shop is enabled**:

    ```lua
    Shared.EnableShopSystem = true
    ```
4. **Check distance** - you may be too far
5. **Restart resource** after config changes

***

### Can't Interact with Shop

**Symptoms**: Can't open shop menu

**Common Causes**:

1. Wrong interaction system
2. Job requirement
3. Distance too far

**Solutions**:

1.  **Check interaction system**:

    ```lua
    Config.UseTarget = false  -- Use dusa_bridge
    -- OR
    Config.UseTarget = true   -- Use target system
    ```
2.  **Disable job requirement**:

    ```lua
    Config.RequireJob = false
    ```
3.  **Increase interaction distance**:

    ```lua
    Shared.Shop.Ped.distance = 5.0  -- Increase from 3.5
    ```
4. **Verify target system** is installed (if using target)

***

### Shop Prices Wrong

**Symptoms**: Items selling for incorrect prices

**Solutions**:

1.  **Check quality multipliers**:

    ```lua
    Shared.Shop.QualityMultipliers = {
        [1] = 1.0,    -- 100%
        [2] = 1.5,    -- 150%
        [3] = 2.0,    -- 200%
    }
    ```
2.  **Verify base prices**:

    ```lua
    Shared.Shop.Sell = {
        {
            item = 'deer_beef',
            price = 45  -- Base price
        }
    }
    ```
3. **Remember**: Final price = base price × quality multiplier

***

## Vehicle Rental Issues

### Vehicle Not Spawning

**Symptoms**: Money deducted but no vehicle

**Solutions**:

1.  **Check spawn location** is clear:

    ```lua
    Shared.Rent.coords = vector3(x, y, z)
    ```
2.  **Verify vehicle model** exists:

    ```lua
    Shared.Rent.vehicle = 'sandking'
    ```
3. **Check console** for spawn errors
4. **Money is refunded** automatically if spawn fails

***

### Can't Return Vehicle

**Symptoms**: Unable to return rented vehicle

**Solutions**:

1. **Must be in vehicle** and in return zone
2. **Must be driver** (seat -1)
3. **Must be vehicle owner** (renter)
4.  **Check return zone location**:

    ```lua
    -- Vehicle return zone is at rental location
    Shared.Rent.coords = vector3(x, y, z)
    ```

***

### Vehicle Keys Not Working

**Symptoms**: Can't access vehicle after rental

**Solutions**:

1. **Check vehicle key system** is installed and supported, if not integrate yourself:
   * dusa\_vehiclekeys
   * wasabi\_carlock
   * qb-vehiclekeys
   * qs-vehiclekeys
   * vehicles\_keys
   * ak47\_vehiclekeys
   * Renewed-Vehiclekeys
2. **Verify integration** in `game/opensource/functions.lua`
3. **Check console** for key system errors

***

## Quest & Level System Issues

### Quest Progress Not Updating

**Symptoms**: Quests don't track progress

**Solutions**:

1. **Check quest type matches action**:
   * `type = 'hunt'` - Requires killing animals
   * `type = 'trap'` - Requires trapping animals
   * `type = 'cook'` - Requires cooking meat
2.  **Verify target\_animal matches**:

    ```lua
    target_animal = 'deer'  -- Must match Shared.Species type
    ```
3. **Check database** quest\_progress table
4.  **Use export to update manually**:

    ```lua
    exports['dusa_hunting']:UpdateQuestProgress(source, 'hunt', 'deer', 1)
    ```

***

### Not Gaining XP

**Symptoms**: No experience from hunting

**Solutions**:

1.  **Check XP is configured** for zone:

    ```lua
    animal = {
        xp = 10,  -- XP per kill
    }
    ```
2.  **Verify level system** is working:

    ```lua
    Config.MaximumLevel = 10
    ```
3. **Check database** hunting\_data table
4.  **Add XP manually** for testing:

    ```lua
    exports['dusa_hunting']:addExperience(source, 50)
    ```

***

### Level Not Increasing

**Symptoms**: XP increases but level stays the same

**Solutions**:

1. **Check XP requirements** - may need more XP
2.  **Verify max level** isn't reached:

    ```lua
    Config.MaximumLevel = 10
    ```
3.  **Check title configuration**:

    ```lua
    Config.Title = {
        beginner = 1,
        novice = 2,
        -- ...
    }
    ```

***

## Performance Issues

### Server Lag with Animals

**Symptoms**: Server performance drops in hunting zones

**Solutions**:

1.  **Reduce maxCount** per zone:

    ```lua
    animal = {
        maxCount = 8,  -- Reduce from 15
    }
    ```
2. **Reduce number of zones** simultaneously active
3.  **Increase CheckInterval**:

    ```lua
    Config.CheckInterval = 5  -- Check every 5 minutes instead of 1
    ```
4.  **Disable debug mode**:

    ```lua
    debug = false
    ```

***

### Client FPS Drops

**Symptoms**: FPS drops near hunting zones

**Solutions**:

1. **Reduce animal models** - use lower poly models
2. **Reduce maxCount** in zones
3.  **Optimize zone ranges**:

    ```lua
    range = 150.0  -- Reduce from 300.0
    ```

***

## Integration Issues

### Framework Not Detected

**Symptoms**: "Framework not found" errors

**Solutions**:

1. **Check dusa\_bridge** is installed and started
2. **Verify framework** is started before dusa\_hunting
3. **Check framework support**:
   * QBCore
   * ESX
   * QBox
4. **Update dusa\_bridge** to latest version

***

### Custom Inventory Not Working

**Symptoms**: Items don't work with custom inventory

**Solutions**:

1. **Check inventory is supported** by dusa\_bridge
2. **Verify metadata support** in inventory
3. **Contact support** for custom inventory integration

***

## Frequently Asked Questions

### Can I add custom animals?

Yes! See the [Configuration Guide - Adding Custom Animals](configuration/#adding-custom-animals) section.

### Does it work with ESX/QBCore/QBox?

Yes, via dusa\_bridge.

### Can I disable the tournament system?

Yes:

```lua
Shared.EnableTournamentSystem = false
```

### How do I change the shop location?

Edit in `config_shared.lua`:

```lua
Shared.Shop.Ped.coords = vec4(x, y, z, heading)
```

### Can players hunt without the hunting rifle?

Configure in `config_client.lua`:

```lua
Config.OnlyHuntByHuntingWeapons = false  -- Allow any weapon
```

### How do I add more hunting zones?

Add new entries in `config_client.lua`:

```lua
Config.HuntingZones['NewZone'] = {
    name = 'My Custom Zone',
    type = 'deer',
    coords = vec3(x, y, z),
    range = 250.0,
    -- ...
}
```

### Can I customize XP requirements?

XP requirements are calculated automatically based on level. To modify, edit the level system in server-side scripts.

### How do I reset a player's hunting data?

Delete or update the player's entry in the `dusa_hunting` database table.

### Does it support multiple languages?

Yes! Currently supports:

* English (`en`)
* Turkish (`tr`)

Add more in `locales/` folder.

### How do I disable the DUI laptop?

In `config_shared.lua`:

```lua
Shared.EnableDUILaptop = false
```

### How do I get support?

1. Check this documentation first
2. Review console errors
3. Contact script author
4. Join support [Discord](https://discord.gg/dusa)
5. Open a ticket with:
   * Error messages
   * Server version
   * Framework version
   * Steps to reproduce

***

## Debugging Tips

### Enable Debug Mode

In `config_shared.lua`:

```lua
Shared.Debug = true
```

This will show detailed logs in console.

### Check Console Logs

Always check both:

* **Server console** - for server-side errors
* **F8 console** - for client-side errors

### Test in Steps

1. Test shop first
2. Then test animal spawning
3. Then test killing/butchering
4. Finally test quests/tournaments

### Common Error Messages

#### "Player not found"

* Framework player object not loading
* Check framework is running
* Player may not be fully loaded

#### "Item not found"

* Item not registered in inventory
* Check item name matches exactly

#### "Model not found"

* Animal/ped model doesn't exist
* Check model name is correct
* Some models require DLC

#### "Callback timeout"

* Server not responding
* Check server performance
* Increase timeout if needed

***

## Still Having Issues?

If your issue isn't covered here:

1. **Re-read installation guide** carefully
2. **Check for updates** - newer version may fix it
3. **Review API reference** for correct usage
4. **Contact support** with:
   * Detailed description
   * Error messages
   * Server/framework versions
   * Configuration files
   * Steps to reproduce

***

## Reporting Bugs

When reporting bugs, include:

1. **Script version**: Check `fxmanifest.lua`
2. **Framework**: QBCore/ESX/QBox and version
3. **Error message**: Full error from console
4. **Steps to reproduce**: How to trigger the bug
5. **Expected behavior**: What should happen
6. **Actual behavior**: What actually happens
7. **Related configuration**: Relevant config sections

This helps developers fix issues faster!
