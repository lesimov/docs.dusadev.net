# Events

Player Interactions


### SearchPlayer

```lua
TriggerEvent('police:client:SearchPlayer')
```

Opens the search player menu to search the nearest player's inventory.

**Parameters:** None

**Usage:** Trigger this event to make a player search the closest nearby player. The player must be within the configured distance and authorized (LEO or allowed by config).

***

### EscortPlayer

```lua
TriggerEvent('police:client:EscortPlayer')
```

Toggles escorting the nearest player.

**Parameters:** None

**Usage:** Starts or stops escorting the closest player. The target must be handcuffed or in an appropriate state to be escorted. LEO authorization may be required based on config.

***

### CuffPlayer

```lua
TriggerEvent('police:client:CuffPlayer')
```

Applies hard handcuffs (behind back) to the nearest player.

**Parameters:** None

**Usage:** Handcuffs the nearest player with standard handcuffs. Plays full handcuffing animation and restricts player movement. Requires handcuffs in inventory unless forced by config.

***

### CuffPlayerSoft

```lua
TriggerEvent('police:client:CuffPlayerSoft')
```

Applies soft handcuffs (can walk) to the nearest player.

**Parameters:** None

**Usage:** Applies soft handcuffs allowing the target to walk. Useful for cooperative arrests or escorts. Requires handcuffs in inventory unless forced by config.

***

### UnCuffPlayer

```lua
TriggerEvent('police:client:UnCuffPlayer')
```

Removes handcuffs from the nearest player.

**Parameters:** None

**Usage:** Uncuffs the nearest handcuffed player. Plays uncuffing animation and restores normal player controls. Requires keys in inventory unless forced by config.

***

### Prison System

#### OpenJailMenu

```lua
TriggerEvent('police:client:openJail', {targetId = serverId})
```

Opens the jail/prison menu to send a player to prison.

**Parameters:**

| Name       | Type          | Description                          |
| ---------- | ------------- | ------------------------------------ |
| `targetId` | `number\|nil` | Target player's server ID (optional) |

**Usage:** Opens the jail menu UI. If targetId is provided, pre-fills the menu with that player's data. Otherwise, allows selecting from nearby players.

