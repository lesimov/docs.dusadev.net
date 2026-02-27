# Callbacks

***

#### IsPlayerCuffed

```lua
local isCuffed = lib.callback.await('police:server:isPlayerCuffed', false, targetServerId)
```

**Parameters:**

| Name             | Type     | Description               |
| ---------------- | -------- | ------------------------- |
| `targetServerId` | `number` | Target player's server ID |

**Returns:** `boolean` - `true` if player is handcuffed

***

#### IsPlayerZiptieCuffed

```lua
local isZiptieCuffed = lib.callback.await('police:server:isPlayerZiptieCuffed', false, targetServerId)
```

**Parameters:**

| Name             | Type     | Description               |
| ---------------- | -------- | ------------------------- |
| `targetServerId` | `number` | Target player's server ID |

**Returns:** `boolean` - `true` if player is zip-tied

***

#### CuffPlayer

```lua
local success = lib.callback.await('police:server:CuffPlayer', false, targetServerId, isSoftcuff, isZiptie, isFront, forced)
```

**Parameters:**

| Name             | Type      | Description          |
| ---------------- | --------- | -------------------- |
| `targetServerId` | `number`  | Target player ID     |
| `isSoftcuff`     | `boolean` | Soft cuff (can walk) |
| `isZiptie`       | `boolean` | Use zip tie          |
| `isFront`        | `boolean` | Cuff in front        |
| `forced`         | `boolean` | Skip item check      |

**Returns:** `boolean` - `true` if successful

***

#### IsPlayerLegTied

```lua
local isLegTied = lib.callback.await('police:server:isPlayerLegTied', false, targetServerId)
```

**Parameters:**

| Name             | Type     | Description               |
| ---------------- | -------- | ------------------------- |
| `targetServerId` | `number` | Target player's server ID |

**Returns:** `boolean` - `true` if player's legs are tied

***

#### TiePlayerLegs

```lua
local success = lib.callback.await('police:server:TiePlayerLegs', false, targetServerId)
```

**Parameters:**

| Name             | Type     | Description      |
| ---------------- | -------- | ---------------- |
| `targetServerId` | `number` | Target player ID |

**Returns:** `boolean` - `true` if successful

***

#### UntiePlayerLegs

```lua
local success = lib.callback.await('police:server:UntiePlayerLegs', false, targetServerId)
```

**Parameters:**

| Name             | Type     | Description      |
| ---------------- | -------- | ---------------- |
| `targetServerId` | `number` | Target player ID |

**Returns:** `boolean` - `true` if successful

***

#### PutHeadBag

```lua
local success = lib.callback.await('police:server:PutHeadBag', false, targetServerId)
```

**Parameters:**

| Name             | Type     | Description      |
| ---------------- | -------- | ---------------- |
| `targetServerId` | `number` | Target player ID |

**Returns:** `boolean` - `true` if head bag applied

***

#### RemoveHeadBag

```lua
local success = lib.callback.await('police:server:RemoveHeadBag', false, targetServerId)
```

**Parameters:**

| Name             | Type     | Description      |
| ---------------- | -------- | ---------------- |
| `targetServerId` | `number` | Target player ID |

**Returns:** `boolean` - `true` if head bag removed

***

### Billing System

#### GetPlayerBills

```lua
local bills, error = lib.callback.await('police:server:getPlayerBills', false, targetPlayerId)
```

**Parameters:**

| Name             | Type     | Description             |
| ---------------- | -------- | ----------------------- |
| `targetPlayerId` | `number` | Target player server ID |

**Returns:**

| Index | Type           | Description          |
| ----- | -------------- | -------------------- |
| 1     | `table[]\|nil` | Bills array or nil   |
| 2     | `string\|nil`  | Error code if failed |

