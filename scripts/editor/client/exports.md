---
icon: function
---

# Exports

## Export List

<table><thead><tr><th width="191">export</th><th>parameters</th><th width="99">return</th><th>description</th></tr></thead><tbody><tr><td>OpenBoss</td><td>none</td><td>none</td><td>Open Boss Menu</td></tr><tr><td>OpenJail</td><td>none</td><td>none</td><td>Open Jail Input Menu</td></tr><tr><td>OpenFine</td><td>none</td><td>none</td><td>Open Billing Input Menu</td></tr><tr><td>OpenService</td><td>none</td><td>none</td><td>Open Public Service Input Menu</td></tr><tr><td>IsHandcuffed</td><td>none</td><td><code>bool</code></td><td>Returns if player is cuffed or not</td></tr><tr><td>SearchPlayer</td><td>none</td><td>none</td><td>Open closest player inventory</td></tr><tr><td>SeizeCash</td><td>none</td><td>none</td><td>Seize closest player cash</td></tr><tr><td>RobPlayer</td><td>none</td><td>none</td><td>Rob closest player</td></tr><tr><td>OpenJobMenu</td><td>none</td><td>none</td><td>Open F6 Police Job Menu</td></tr><tr><td>AttachWheelLock</td><td>none</td><td>none</td><td>Attach wheel lock to vehicle wheel</td></tr><tr><td>RemoveWheelLock</td><td>none</td><td>none</td><td>Detach wheel lock from wheel</td></tr><tr><td>ShowBadge</td><td>none</td><td>none</td><td>Show officer's badge</td></tr><tr><td>EditBadge</td><td>none</td><td>none</td><td>Open badge edit input</td></tr><tr><td>SetCallsign</td><td>callsign: <code>string</code></td><td>none</td><td>Set callsign to defined value</td></tr><tr><td>OpenRadio</td><td>none</td><td>none</td><td>Open radio</td></tr><tr><td>OpenGps</td><td>none</td><td>none</td><td>Open gps device</td></tr><tr><td>PlaceGps</td><td>none</td><td>none</td><td>Place gps to nearby vehicle</td></tr><tr><td>RemoveGps</td><td>none</td><td>none</td><td>Remove attached gps from nearby vehicle</td></tr><tr><td>PanicButton</td><td>coords: <code>vec3</code>, name: <code>string</code></td><td>none</td><td>Create panic button notification</td></tr></tbody></table>



## How to use exports?

Exports are used for different purposes in different places. For example, if I want to turn on the GPS and do it with a command (normally, this is already available in the police job, but I'm explaining it just as a code example), I need to use the following code:

```lua
-- Open GPS Command
RegisterCommand('opengps', function()
    exports['dusa_police']:OpenGps()
end)
```



If the export requires various parameters, we need to provide the correct data. I am writing an<br>

1. SetCallsign export:

```lua
RegisterCommand('setcallsign', function(_, args)
    local callsign = args[1] -- args[1] equals to player's first input after command. Like /setcallsign AAA-111
    exports['dusa_police']:SetCallsign(callsign)
end)
```

2. PanicButton export:

```lua
RegisterCommand('panic', function()
    local playerPed = PlayerPedId()
    local playerCoords = GetEntityCoords(playerPed)
    local playerName = GetPlayerName()
    exports['dusa_police']:PanicButton(playerCoords, playerName)
end)
```



If an export returns data and you want to obtain this data, you can refer to the following examples

```lua
RegisterCommand('amicuffed', function() -- returns if player is cuffed
    local isCuffed = exports['dusa_police']:IsHandcuffed()
    print(isCuffed) -- prints true or false
end)
```
