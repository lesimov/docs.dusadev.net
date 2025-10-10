---
icon: wrench
---

# Configuration & Exports (QB)

### <img src="https://lesimov.gitbook.io/~gitbook/image?url=https%3A%2F%2F870197722-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMeOc2gAfx3fqBg4QY2uJ%252Fuploads%252F4aiKhHzAPeGiB2A4DFMs%252Fc44b4e80c2f4dfff7d698eae69c85a98-removebg-preview.png%3Falt%3Dmedia%26token%3D84674aef-d34f-4541-aaec-cd415b9dd5a3&#x26;width=53&#x26;dpr=4&#x26;quality=100&#x26;sign=e19d0c11&#x26;sv=1" alt="" data-size="line">Configuration <a href="#configuration" id="configuration"></a>

**General Options**

```lua
------------------------GENERAL OPTIONS------------------------
---------------------------------------------------------------
Config.Commands = {
  OpenBilling = "billing",
  OpenAdminMenu = "billingadmin",
  PosDevice = "pos"
}

Config.WAT = 10 -- Tax will be added to invoice amount
Config.PosToJobVault = true -- Add pos moneys to player's job vault / if you set this false, money will be added to pos holder bank account
```

**Job Bills ( Config File )**

```lua
--------------------------JOB BILLS----------------------------
---------------------------------------------------------------
--[[	
	name = "Job Name" -- must be equal to your job set code
        image = "url" -- will be shown at the right top corner when invoice request sent
]]

Config.JobBills = {
  [1] = {
    name = "ambulance",
    image = "https://media.discordapp.net/attachments/1143528082913906688/1193632716617416846/Rectangle_13.png?ex=65ad6c18&is=659af718&hm=6687185cd08e20decfa93d55ceb53e732cb49a2f61bfd435ec2639617dd523f2&=&format=webp&quality=lossless"
  },
  [2] = {
    name = "police",
    image = "https://media.discordapp.net/attachments/1143528082913906688/1193632388287307958/image_1.png?ex=65ad6bc9&is=659af6c9&hm=308bf239d0530395c87f1d6a7578d6928ca30b1aaea3f021a97be2cc72174bd5&=&format=webp&quality=lossless"
  },
  [3] = {
    name = "mechanic",
    image = "https://media.discordapp.net/attachments/1143528082913906688/1193632716160249966/image_2.png?ex=65ad6c18&is=659af718&hm=6c0aa31ea7f6a2663e7b01a765a7fa7860964403e31f81e12dcf049437b6aa5f&=&format=webp&quality=lossless"
  },
  [4] = {
    name = "uwucafe",
    image = "https://media.discordapp.net/attachments/1143528082913906688/1195509620828028979/image.png?ex=65b44019&is=65a1cb19&hm=2b2f51506fb5ae7fa6b4a460d7dfa6336286e19d13fabf9017d0f1615ae324a3&=&format=webp&quality=lossless"
  },
}
```

### <img src="https://lesimov.gitbook.io/~gitbook/image?url=https%3A%2F%2F870197722-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMeOc2gAfx3fqBg4QY2uJ%252Fuploads%252F4aiKhHzAPeGiB2A4DFMs%252Fc44b4e80c2f4dfff7d698eae69c85a98-removebg-preview.png%3Falt%3Dmedia%26token%3D84674aef-d34f-4541-aaec-cd415b9dd5a3&#x26;width=53&#x26;dpr=4&#x26;quality=100&#x26;sign=e19d0c11&#x26;sv=1" alt="" data-size="line"> Integrations <a href="#integrations" id="integrations"></a>

#### Check if player has an unpaid bill <a href="#check-if-player-has-an-unpaid-bill" id="check-if-player-has-an-unpaid-bill"></a>

```lua
-- Client Side
local hasBill = exports['dusa_billing']:hasBills()
print(hasBill)
-- output: true or false
```

#### **Create Custom Invoice** <a href="#create-custom-invoice" id="create-custom-invoice"></a>

```lua
-- Client Side
TriggerServerEvent('dusa_billing:sv:createCustomInvoice', targetSource, title, description, amount, type)
```

**Variables**

**targetSource:** `GetPlayerServerId(playerId)`

**title:** `Gun fight`

**description:** `Player killed a person with a gun`

**amount:** `250`

**type:** `personel` or `company`

#### **Open Billing Menu** <a href="#open-billing-menu" id="open-billing-menu"></a>

```lua
--  Client Side
exports['dusa_billing']:openBilling()

-- Server Side
TriggerClientEvent('dusa_billing:cl:openBilling', source)
```

#### **Open Admin Menu** <a href="#open-admin-menu" id="open-admin-menu"></a>

```lua
--  Client Side
exports['dusa_billing']:openAdmin()

-- Server Side
TriggerClientEvent('dusa_billing:cl:openAdmin', source)
```

#### Open POS Device <a href="#open-pos-device" id="open-pos-device"></a>

```lua
-- Client Side
TriggerEvent('dusa_billing:openPos')

-- Server Side
TriggerClientEvent('dusa_billing:openPos', source)
```
