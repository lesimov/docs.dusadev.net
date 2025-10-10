---
icon: function
---

# Exports

## Export List

<table><thead><tr><th width="191">export</th><th>parameters</th><th width="99">return</th><th>description</th></tr></thead><tbody><tr><td>ShowHud</td><td>none</td><td>none</td><td>Set hud visible</td></tr><tr><td>HideHud</td><td>none</td><td>none</td><td>Set hud invisible</td></tr><tr><td>ToggleCruise</td><td>none</td><td>none</td><td>Toggle speed cruise</td></tr><tr><td>ToggleSeatbelt</td><td>none</td><td>none</td><td>Toggle seatbelt</td></tr><tr><td>OpenSettingsMenu</td><td>none</td><td>none</td><td>Open hud customization menu</td></tr></tbody></table>



## How to use exports?

Exports are used for different purposes in different places. For example, if I want to set hud as visible, I need to use a code like this

```lua
-- Open HUDCommand
RegisterCommand('showhud', function()
    exports['dusa_hud']:ShowHud()
end)
```
