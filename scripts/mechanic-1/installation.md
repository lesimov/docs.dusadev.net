---
icon: down
---

# Installation

***

## Video Guide

{% embed url="https://youtu.be/oW-IZOjBRcA" %}

***

{% hint style="danger" %}
**DO NOT INSTALL DEPRECATED** _<mark style="color:$danger;">Dusa Mechanic V2 | Tuning, Tablet App, Illegal Tuning</mark>._ **We switched to&#x20;**_<mark style="color:$success;">**Dusa Mechanic v2 - 2.0 Update**</mark>**.**_**&#x20;Download it instead**
{% endhint %}

## Steps

{% stepper %}
{% step %}
### Install packages

* Install package named **"Dusa Mechanic v2 - 2.0 Update"**
* Install other package named **"Dusa Mechanic Assets"**
* Install last package named **"Dusa Bridge"**
{% endstep %}

{% step %}
### Unzip downloaded files

1. Create a new folder named `[dusa]`
2. Unzip all content inside `[dusa]` folder
{% endstep %}

{% step %}
### Add to server start

1. Open your `server.cfg`
2. Add the following line:

```
ensure [dusa]
```
{% endstep %}

{% step %}
### Add items

1. Navigate into path: `[dusa]/dusa_mechanic/INSTALL`
2. **If you using `ox_inventory`**
   1. Open `all_items_ox.txt`, copy content
   2. Navigate into `ox_inventory/data/items.lua` and paste to bottom
3. **If you using `other inventories`**
   1. Add the items that included at `all_items_qb.txt` to your framework or your core. It depends on which inventory or core is this.
{% endstep %}

{% step %}
### Add item images

1. Navigate into path: `[dusa]/dusa_mechanic/INSTALL/images/`&#x20;
2. Open the folder depends on your choice, `webp` or `png`. Commonly used extension is `png` for item images.
3. Copy images inside
4. Paste item images to your inventory `images` folder
{% endstep %}

{% step %}
### IF YOU USING BUNDLED VERSION

1. Navigate into path: `[dusa]/dusa_tablet/INSTALL/images/`&#x20;
2. Copy `tablet.png` or `tablet.webp` (extension depends on your using)
3. Paste to your inventory images folder
4. Open `ox_inventory.txt` or `qb-core.txt` (depends on your server), copy everything inside
5. Paste to your `ox_inventory items.lua`. If you don't using ox, apply same step depends on your inventory or core
{% endstep %}
{% endstepper %}

***

## Configuration

You can our synced config editor from [http://127.0.0.1:30120/dusa\_mechanic/config-panel](http://127.0.0.1:30120/dusa_mechanic/config-panel)

{% hint style="warning" %}
**Make sure you open this URL on the machine where you started the server. If it's running on your VPS, you can access it through your VPS.**
{% endhint %}

<figure><img src="../../.gitbook/assets/ChromeDemo (1).gif" alt=""><figcaption></figcaption></figure>

***

## If you got SQL errors at startup

Normally, SQL works properly by default and does not cause any errors. However, SQL services used for some servers may differ and may cause errors when running automatically.

**To resolve this issue:**

Go to the `dusa_mechanic` folder and run the `dusa_mechanic_full_install.sql` file in your database.

**If you are also using the tablet:**

Go to the `dusa_tablet` folder and run the `dusa_tablet_full_instal.sql` file in your database.

{% hint style="warning" %}
Ensure you are performing the operation on the correct database. Performing this operation on a database not connected to your server will prevent it from being detected.
{% endhint %}
