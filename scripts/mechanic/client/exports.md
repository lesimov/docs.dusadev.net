# Exports

***

## Client Exports

### Show / Hide Text UI

**Showing Text UI**

```lua
exports.dusa_bridge:ShowTextUI(locale('zones.tuning.prompt'), {
    position = 'right-center',
    key = 'E',
})
```

**Hiding Text UI**

```lua
exports.dusa_bridge:HideTextUI()
```

***

### isNitroActive

```lua
local ret = exports.dusa_mechanic:isNitroActive() -- ret: true | false
```

***

### Open / Close Police Scanner

#### Opening Police Scanner

Opens the floating vehicle scanner UI. Checks permissions internally before opening.

```lua
exports['dusa_mechanic']:OpenPoliceScanner()
```

#### Closing Police Scanner

Closes the police scanner UI if it's currently open.

```lua
exports['dusa_mechanic']:ClosePoliceScanner()
```

#### Check Scanner State

Returns whether the police vehicle scanner is currently open.

```lua
local isOpen = exports['dusa_mechanic']:IsPoliceVehicleScannerOpen()
print(isOpen) -- true or false
```
