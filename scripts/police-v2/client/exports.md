# Exports

***

#### Handcuff Status

```lua
local isCuffed = exports.dusa_police:IsHandcuffed()
-- @return boolean - true: handcuffed, false: free

local isSoftCuffed = exports.dusa_police:IsSoftCuffed()
-- @return boolean - true: soft cuffed, false: not soft cuffed
```

**Use Case**: Inventory, garage, or other scripts can block handcuffed players from certain actions



#### **Prison Status**

```lua
local isPrisoner = exports.dusa_police:IsPrisoner()
-- @return boolean - true: in prison, false: not in prison

local remainingTime = exports.dusa_police:GetRemainingPrisonTime()
-- @return number - remaining time in minutes (0 = free)
```

**Use Case**: HUD scripts can display prison timer, your system can restrict prisoner actions



#### Vision Status

```lua
local hasVisor = exports.dusa_police:IsVisorEquipped()
-- @return boolean - true: visor equipped, false: not equipped

local visionMode = exports.dusa_police:GetVisionMode()
-- @return string - 'none' | 'night' | 'thermal'
```

**Use Case**: HUD effects, custom camera effects, compatibility with other vision systems



#### **Player Search**

```lua
exports.dusa_police:SearchPlayer()
-- @return void - no return value, directly opens inventory
```

**Use Case**: Force player to search nearby



***
