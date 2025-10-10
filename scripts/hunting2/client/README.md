---
icon: desktop
---

# Client API

Client-side exports and events for integrating the hunting system with other resources.

## Overview

The hunting script provides client-side exports and events that allow you to:
- Trigger hunting actions programmatically
- Listen to hunting events
- Get hunting data for UI/HUD integration
- Control hunting features from other scripts

## Available Documentation

### [Exports](exports.md)

Client-side functions you can call from other resources:
- Get player hunting data
- Open hunting menus
- Manage hunting state
- Control hunting features

### [Events](events.md)

Client-side events you can listen to or trigger:
- Hunting action events
- State change notifications
- UI update triggers
- Custom event handlers

## Quick Example

```lua
-- Get player's hunting level from another resource
local huntingLevel = exports['dusa_hunting']:GetHuntingLevel()

-- Listen to animal kill event
RegisterNetEvent('dusa_hunting:client:animalKilled', function(animalType, quality)
    print('Killed a ' .. animalType .. ' with ' .. quality .. ' star quality')
end)
```

## Integration Guide

See [Integration Examples](../integration/examples.md) for complete integration scenarios with other scripts.
