---
icon: wrench
---

# Configuration & Exports (ESX)

### <img src="https://dusadev.gitbook.io/~gitbook/image?url=https%3A%2F%2F870197722-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMeOc2gAfx3fqBg4QY2uJ%252Fuploads%252F4aiKhHzAPeGiB2A4DFMs%252Fc44b4e80c2f4dfff7d698eae69c85a98-removebg-preview.png%3Falt%3Dmedia%26token%3D84674aef-d34f-4541-aaec-cd415b9dd5a3&#x26;width=53&#x26;dpr=4&#x26;quality=100&#x26;sign=e19d0c11&#x26;sv=1" alt="" data-size="line">Configuration <a href="#configuration" id="configuration"></a>

**Set Framework**

```lua
DUSA.Framework = "esx" -- esx / oldesx
DUSA.CustomFramework = true
function CustomFrameworkExport() -- Add the export here, as in the following example.
    ESX = exports["es_extended"]:getSharedObject()
end

DUSA.PlayerLoadedExport = 'esx:playerLoaded'
DUSA.PlayerJoinedExport = 'esx:onPlayerJoined'
```

**Custom Spawnselector ( IF YOU WANT TO USE ANOTHER SPAWN SELECTOR SCRIPT )**

Set DUSA.CustomSpawnSelector = true

Place your spawn selector open event inside function

```lua
DUSA.CustomSpawnSelector = false    -- true value will disable dusa_spawnselector, will run export below
function CustomSpawnSelector()
    -- Add your custom spawn selector trigger here (client side only)
end
```

**Translation**

You can edit these lines for all translations ( UI included )

```lua
DUSA.Language = {
    Server_Name = 'Dusa Roleplay',
    Select_Character = 'Select Character',
    Create_Character = 'Create New Character',
    Buy_Slot = 'Buy New Character Slot',
    Delete_Button = 'Delete',
    Player_Button = 'Player',
    Bank_Account = 'Bank Account',
    Cash_Money = 'Cash Money',
    Dateof_Birth = 'Date of Birth',
    Phone_Number = 'Phone Number',
    Gender_Translation = 'Gender',
    Slot_Code = 'Slot Code',
    Buy_Code = 'Buy Code',
    Cancel_Text = 'Cancel',
    Accept_Text = 'Accept',
    Create_Text = 'Create',
    Footer_Text = 'Dusa Roleplay',
    Footer_Text2 = '© DUSA 2023',
}
```

**Trigger Anything When Player Loaded**

Configure which items will be given when player loaded

Trigger anything when player is loaded after character spawn

```lua
-- Give Items When Player Loaded
DUSA.StarterItems = {
    {item = "id_card", amount = 1},
    {item = "water_bottle", amount = 3},
    {item = "tosti", amount = 3},
    {item = "cash", amount = 5000},
    {item = "blue_phone", amount = 1}
}

-- Handle Player Load
DUSA.PlayerLoaded = function(identifier)
    -- Trigger an event when player is loaded (Client Side)
end
```

### <img src="https://dusadev.gitbook.io/~gitbook/image?url=https%3A%2F%2F870197722-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMeOc2gAfx3fqBg4QY2uJ%252Fuploads%252FyAI89ka8nrOrFklc5cDj%252Findir.png%3Falt%3Dmedia%26token%3D7cc214e1-67ae-4215-bd82-f436b9eadfd2&#x26;width=40&#x26;dpr=4&#x26;quality=100&#x26;sign=1127353e&#x26;sv=1" alt="" data-size="line"> Tebex Integration <a href="#tebex-integration" id="tebex-integration"></a>

1 - Find your tebex secret key (From tebex page)

2 - Add this to server.cfg -> set sv\_tebexSecret "secretkey"

3 - Create a package for sell slot

4 - Check below and find "Add Command"

5 - Paste this command -> dusa\_activateslot {"transid": "{transaction}"}

6 - Click setting icon at the right and change Require Player To Be Online > Execute the command even if the player is offline

[\
](https://dusadev.gitbook.io/dusa-docs/esx/multicharacter-+-spawnselector)
