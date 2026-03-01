# Events

***

## Client Events

### Opening Tuning Menu

**Parameters**

| mechanicId                                           | zoneId                                         |
| ---------------------------------------------------- | ---------------------------------------------- |
| Mechanic id from ds\_mechanic\_zones shop\_id column | Mechanic id from ds\_mechanic\_zones id column |

**Event**

```lua
TriggerEvent('mechanic:tuning:open', mechanicId, zoneId)
```

***

### Opening Redline App

**Parameters**

No parameters required.

**Event**

```lua
TriggerEvent('dusa_mechanic:openStandaloneRedline')
```

***

### Opening Tablet (Requires dusa\_tablet package)

**Parameters**

No parameters required.

**Event**

```lua
TriggerEvent('dusa_tablet:openFromItem')
```

[dusa\_tablet](https://dusadev.net/scripts/7223228)

***

### Opening Mechanic Admin Editor

**Parameters**

No parameters required.

**Event**

```lua
TriggerEvent('mechanic:admin:openUI')
```

> **Warning:** This event opens admin special menu. We already added extra security steps but we suggest you to add extra security steps for your code too before triggering this event.

***

### Opening Police Vehicle Scanner

Opens the floating police vehicle scanner UI on the target player's screen. Requires the player to have analysis permissions (`policeCanAnalyze` must be enabled in Redline config).

```lua
-- Open scanner for a specific player
TriggerEvent('dusa_mechanic:openPoliceScanner')
```
