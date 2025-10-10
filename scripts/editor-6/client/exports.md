---
icon: function
---

# Exports

## Export List

<table><thead><tr><th width="191">export</th><th>parameters</th><th width="99">return</th><th>description</th></tr></thead><tbody><tr><td>openDispatch</td><td>none</td><td>none</td><td>Open dispatch menu</td></tr><tr><td>closeDispatch</td><td>none</td><td>none</td><td>Close dispatch menu</td></tr><tr><td>openAlert</td><td>none</td><td>none</td><td>Open alert widget</td></tr><tr><td>closeAlert</td><td>none</td><td>none</td><td>Close alert widget</td></tr><tr><td>openBodycam</td><td>none</td><td>none</td><td>Open bodycam UI</td></tr><tr><td>closeBodycam</td><td>none</td><td>none</td><td>Close bodycam UI</td></tr><tr><td>toggleBodycam</td><td>none</td><td>none</td><td>Toggle bodycam UI</td></tr><tr><td>CustomDispatch</td><td><code>alertData</code></td><td>none</td><td>Export to create custom dispatches, requires <code>alertData</code>. Head into <a href="../how-to-send-custom-dispatch.md">tutorial </a>to create custom dispatches</td></tr></tbody></table>



## How to use exports?

Exports are used for different purposes in different places. For example, if I want to turn on the alert menu and do it with a command, I need to use the following code:

```lua
-- Open GPS Command
RegisterCommand('openalert', function()
    exports['dusa_dispatch']:openAlert()
end)
```



