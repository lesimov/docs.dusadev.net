# Events

-----

## Client Events

### Opening Tuning Menu

**Parameters**

| mechanicId                                        | zoneId                                       |
| ------------------------------------------------- | -------------------------------------------- |
| Mechanic id from ds_mechanic_zones shop_id column | Mechanic id from ds_mechanic_zones id column |

**Event**

```lua
TriggerEvent('mechanic:tuning:open', mechanicId, zoneId)
```

-----

### Opening Redline App

**Parameters**

No parameters required.

**Event**

```lua
TriggerEvent('dusa_mechanic:openStandaloneRedline')
```

-----

### Opening Tablet (Requires dusa_tablet package)

**Parameters**

No parameters required.

**Event**

```lua
TriggerEvent('dusa_tablet:openFromItem')
```

[dusa_tablet](https://dusadev.net/scripts/7223228)

-----

### Opening Mechanic Admin Editor

**Parameters**

No parameters required.

**Event**

```lua
TriggerEvent('mechanic:admin:openUI')
```

> **Warning:** This event opens admin special menu. We already added extra security steps but we suggest you to add extra security steps for your code too before triggering this event.

-----
