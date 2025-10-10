---
icon: question
---

# How to send custom dispatch?

Normally, every custom dispatch call integrated into ps-dispatch will work smoothly for us as well. Still, I will only show the method for Dusa Dispatch.



### Create Custom Notifications for dusa\_dispatch

If you have to trigger event from client-side, use exports instead.



```lua
local function TestAlert()
    local coords = GetEntityCoords(cache.ped)
    
    local dispatchData = {
        id = 0,
        event = 'NEW ALERT',
        title = 'New Robbery Alert',
        description = 'A store robbery is in progress!',
        code = '10-15',
        codeName = 'storerobbery',
        coords = coords,
        icon = 'theft', -- theft, suspect, conflict, traffic
        time = '05:33 PM',
        priority = 1, -- 0, 1, 2
        img = "",
        street = 'Paleto Bay',
        gender = gender, -- 'm' or 'f'
        recipientJobs = { 'leo' },
    }

    exports.dusa_dispatch:CustomDispatch(dispatchData)
end
RegisterCommand('TestAlert', TestAlert)
```



If you have to trigger event from server-side, use events instead.

<pre class="language-lua"><code class="lang-lua">local function TestAlert(source)
    local src = source
    local ped = GetPlayerPed(src)
    local coords = GetEntityCoords(ped)
    
    local dispatchData = {
        id = 0,
        event = 'NEW ALERT',
        title = 'New Robbery Alert',
        description = 'A store robbery is in progress!',
        code = '10-15',
        codeName = 'storerobbery',
        coords = coords,
        icon = 'theft', -- theft, suspect, conflict, traffic
        time = '05:33 PM',
        priority = 1, -- 0, 1, 2
        img = "",
        street = 'Paleto Bay',
        gender = 'm', -- 'm' or 'f'
        recipientJobs = { 'leo' },
    }

<strong>    TriggerClientEvent('dusa_dispatch:sendCustomDispatch', src, dispatchData)
</strong>end
RegisterCommand('TestAlert', function(source)
    TestAlert(source)
end)
</code></pre>

