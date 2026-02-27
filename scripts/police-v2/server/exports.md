# Exports

## 1. Prison Management

### GetPrisoner

```lua
local prisoner = exports.dusa_police:GetPrisoner(citizenid)
```

**Parameters:**

| Name        | Type     | Description                                 |
| ----------- | -------- | ------------------------------------------- |
| `citizenid` | `string` | Player's citizen ID (or identifier for ESX) |

**Returns:** `table` or `nil`

| Field                | Type          | Description                    |
| -------------------- | ------------- | ------------------------------ |
| `id`                 | `number`      | Database record ID             |
| `citizenid`          | `string`      | Player's citizen ID            |
| `name`               | `string`      | Player's full name             |
| `reason`             | `string`      | Reason for imprisonment        |
| `totalTime`          | `number`      | Total sentence in minutes      |
| `remainingTime`      | `number`      | Remaining time in minutes      |
| `dateJailed`         | `string`      | ISO date when jailed           |
| `jailedBy`           | `string`      | Officer who jailed them        |
| `confiscatedStashId` | `string\|nil` | Stash ID for confiscated items |
| `mugshotUrl`         | `string\|nil` | URL to mugshot image           |

### **GetAllActivePrisoners**

```lua
local prisoners = exports.dusa_police:GetAllActivePrisoners()
```

**Returns:** `table[]` - Array of prisoner objects (same structure as GetPrisoner)



### **JailPlayer**

```lua
local success, error = exports.dusa_police:JailPlayer(targetServerId, data, officerSource)
```

**Parameters:**

| Name             | Type     | Description               |
| ---------------- | -------- | ------------------------- |
| `targetServerId` | `number` | Target player's server ID |
| `data`           | `table`  | Jail data (see below)     |
| `officerSource`  | `number` | Officer's server ID       |

**Data Table:**

| Field      | Type     | Description                      |
| ---------- | -------- | -------------------------------- |
| `reason`   | `string` | Reason for jailing               |
| `duration` | `number` | Jail duration                    |
| `timeUnit` | `string` | `"minute"`, `"hour"`, or `"day"` |

**Returns:**

| Index | Type          | Description             |
| ----- | ------------- | ----------------------- |
| 1     | `boolean`     | Success status          |
| 2     | `string\|nil` | Error message if failed |

#### **ReleasePrisoner**

```lua
local success = exports.dusa_police:ReleasePrisoner(citizenid, releasedBy)
```

**Parameters:**

| Name         | Type          | Description           |
| ------------ | ------------- | --------------------- |
| `citizenid`  | `string`      | Prisoner's citizen ID |
| `releasedBy` | `string\|nil` | Who released them     |

**Returns:** `boolean` - `true` if released successfully

***

## 2. Object Placement System

### **PlaceObject**

```lua
local objectId = exports.dusa_police:PlaceObject(model, coords, rotation, heading, freeze, placerSource)
```

**Parameters:**

| Name           | Type          | Description                 |
| -------------- | ------------- | --------------------------- |
| `model`        | `string`      | Object model hash           |
| `coords`       | `vector3`     | World coordinates           |
| `rotation`     | `vector3`     | Object rotation             |
| `heading`      | `number`      | Object heading              |
| `freeze`       | `boolean`     | Freeze object in place      |
| `placerSource` | `number\|nil` | Player source who placed it |

**Returns:** `string` - Unique object ID



### **RemoveObject**

```lua
local success = exports.dusa_police:RemoveObject(objectId)
```

**Parameters:**

| Name       | Type     | Description         |
| ---------- | -------- | ------------------- |
| `objectId` | `string` | Object ID to remove |

**Returns:** `boolean` - `true` if removed successfully



### **GetPlacedObjects**

```lua
local objects = exports.dusa_police:GetPlacedObjects()
```

**Returns:** `table` - Dictionary `{ [objectId] = objectData }`

**Object Data Structure:**

| Field       | Type          | Description    |
| ----------- | ------------- | -------------- |
| `id`        | `string`      | Object ID      |
| `model`     | `string`      | Model hash     |
| `coords`    | `vector3`     | Position       |
| `rotation`  | `vector3`     | Rotation       |
| `heading`   | `number`      | Heading        |
| `freeze`    | `boolean`     | Frozen state   |
| `placer`    | `number\|nil` | Who placed it  |
| `timestamp` | `number`      | Unix timestamp |

***

## 3. Duty Management

### **GetOnDutyOfficers**

```lua
local officers = exports.dusa_police:GetOnDutyOfficers()
```

**Returns:** `table[]` - Array of officer data

**Officer Data Structure:**

| Field             | Type     | Description        |
| ----------------- | -------- | ------------------ |
| `source`          | `number` | Player server ID   |
| `name`            | `string` | Officer name       |
| `identifier`      | `string` | Citizen ID         |
| `job`             | `string` | Job name           |
| `clockInTime`     | `string` | Clock-in timestamp |
| `durationMinutes` | `number` | Minutes on duty    |

### **GetDutyHistory**

```lua
local history = exports.dusa_police:GetDutyHistory(identifier)
```

**Parameters:**

| Name         | Type          | Description                    |
| ------------ | ------------- | ------------------------------ |
| `identifier` | `string\|nil` | Optional: filter by citizen ID |

**Returns:** `table[]` - Array of completed duty sessions



### **IsPlayerOnDuty**

```lua
local isOnDuty = exports.dusa_police:IsPlayerOnDuty(source)
```

**Parameters:**

| Name     | Type     | Description      |
| -------- | -------- | ---------------- |
| `source` | `number` | Player server ID |

**Returns:** `boolean` - `true` if on duty



### **GetPlayerDutySession**

```lua
local session = exports.dusa_police:GetPlayerDutySession(source)
```

**Parameters:**

| Name     | Type     | Description      |
| -------- | -------- | ---------------- |
| `source` | `number` | Player server ID |

**Returns:** `table` or `nil` - Session data or nil if not on duty

***

## 4. Mugshot System

### **GetMugshots**

```lua
local mugshots = exports.dusa_police:GetMugshots(citizenId)
```

**Parameters:**

| Name        | Type          | Description                    |
| ----------- | ------------- | ------------------------------ |
| `citizenId` | `string\|nil` | Optional: filter by citizen ID |

**Returns:** `table[]` - Array of mugshot records

* If `citizenId` provided: returns all mugshots for that citizen
* If `nil`: returns last 100 mugshots

