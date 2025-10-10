---
icon: wrench
---

# Configuration & Exports (ESX/QBCore)

### <img src="https://dusadev.gitbook.io/~gitbook/image?url=https%3A%2F%2F870197722-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMeOc2gAfx3fqBg4QY2uJ%252Fuploads%252F4aiKhHzAPeGiB2A4DFMs%252Fc44b4e80c2f4dfff7d698eae69c85a98-removebg-preview.png%3Falt%3Dmedia%26token%3D84674aef-d34f-4541-aaec-cd415b9dd5a3&#x26;width=53&#x26;dpr=4&#x26;quality=100&#x26;sign=e19d0c11&#x26;sv=1" alt="" data-size="line"> Integrations - Compatibilities <a href="#integrations-compatibilities" id="integrations-compatibilities"></a>

To ensure that our script operates harmoniously with other scripts, you will need to adjust the following settings.

#### Dispatch <a href="#dispatch" id="dispatch"></a>

To ensure the dispatch tab functions correctly, you need to make a small change to your dispatch script within your code.

**1-) ps-dispatch**

If you are a ps-dispatch user, you need to make a small change to your dispatch system:

1. Find ps-dispatch on your resources folder
2. Go to path ps-dispatch/client/main.lua
3.  Find event named:

    ```lua
    ps-dispatch:client:notify
    ```
4.  Replace the whole code with code block at the below, or just add this code to right place:

    ```lua
    exports['dusa_mdt']:SendDispatch(data, source)
    ```

```lua
RegisterNetEvent('ps-dispatch:client:notify', function(data, source)
    if data.alertTime == nil then data.alertTime = Config.AlertTime end
    local timer = data.alertTime * 1000
    
    if alertsDisabled then return end
    if not isJobValid(data.jobs) then return end
    if not IsOnDuty() then return end

    timerCheck = true

    SendNUIMessage({
        action = 'newCall',
        data = {
            data = data,
            timer = timer,
        }
    })

    addBlip(data, Config.Blips[data.codeName] or data)

    RespondToDispatch:disable(false)
    OpenDispatchMenu:disable(true)

    local startTime = GetGameTimer()
    while timerCheck do
        Wait(1000)

        local currentTime = GetGameTimer()
        local elapsed = currentTime - startTime

        if elapsed >= timer then
            break
        end
    end

    exports['dusa_mdt']:SendDispatch(data, source)
    timerCheck = false
    OpenDispatchMenu:disable(false)
    RespondToDispatch:disable(true)
end)
```

It should look like this at the end.

After completing these steps, our system will operate seamlessly with ps-dispatch

**2-) rcore\_dispatch**

If you are a rcore\_dispatch user, you need to make a small change to your dispatch system:

integrations will be added here

#### Billing <a href="#billing" id="billing"></a>

**...**

#### Jail <a href="#jail" id="jail"></a>

...

#### Community Service <a href="#community-service" id="community-service"></a>

...

### API <a href="#api" id="api"></a>

The details for operations in this category have not been provided extensively, as anyone with basic knowledge can perform the necessary actions. Therefore, it is recommended to reserve this part more for your developers. Developers can refer to the provided snippets and integrate them into your scripts for extended functionality.

#### client <a href="#client" id="client"></a>

**Insert Dispatches to MDT**

To insert your dispatches for MDT to manage them, use this function at your dispatch script

But before that, make sure you integrated your dispatch to `modules/dispatch/scripts/custom.lua`

If there is a file named your dispatch script, that means your dispatch is already integrated by us.

**Export**

```
exports['dusa_mdt']:SendDispatch(data)
```

**Parameters**

| Name   | Data Type | Description                                    |
| ------ | --------- | ---------------------------------------------- |
| `data` | table     | Table of data related to the reported incident |

***

### Common Errors <a href="#common-errors" id="common-errors"></a>

#### Common Error Codes and Solutions <a href="#common-error-codes-and-solutions" id="common-error-codes-and-solutions"></a>

If you're encountering issues with the MDT system, it may be a simple fix. Review the error codes below to identify and resolve your specific issue:

```
// server.cfg
ensure es_extended / qb-core ( depends on your framework )
ensure ox_lib
ensure dusa_mdt
```

* **Error 101 : Throws many errors when script started at first start of server**
  *   **Error report screenshots may look like ;**

      * **Solution**: Check your server.cfg start order. The order should be like this

      ```lua
      // server.cfg
      ensure es_extended / qb-core ( depends on your framework )
      ensure ox_lib
      ensure dusa_mdt
      ```

      <figure><img src="https://dusadev.gitbook.io/~gitbook/image?url=https%3A%2F%2F870197722-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMeOc2gAfx3fqBg4QY2uJ%252Fuploads%252FsRMagOTJLlnAVR7GI3sc%252Fimage.png%3Falt%3Dmedia%26token%3D6bd866f4-6d00-4885-9dd2-2bd7b799e0dd&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=41de8e08&#x26;sv=1" alt=""><figcaption><p>at server cmd</p></figcaption></figure>

      <figure><img src="https://dusadev.gitbook.io/~gitbook/image?url=https%3A%2F%2F870197722-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMeOc2gAfx3fqBg4QY2uJ%252Fuploads%252F33hsZuxIQh1vMkL398vC%252Fimage.png%3Falt%3Dmedia%26token%3D6747cfd1-dc8b-4c7b-86b5-90779551d8f7&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6d469e73&#x26;sv=1" alt=""><figcaption><p>at f8 console</p></figcaption></figure>
* **Error 202**: New dispatchs are not listed in my mdt
  * **Solution**: Follow integration step depends on your dispatch system.
* **Error 303**: .
  * **Solution**:
*   **Error 404**: .

    * **Solution**:

    Remember to always check the latest documentation for any updates or changes to error codes and solutions.[\
    ](https://dusadev.gitbook.io/dusa-docs/qbcore/police-mdt)

[\
](https://dusadev.gitbook.io/dusa-docs/esx/multicharacter-+-spawnselector)
