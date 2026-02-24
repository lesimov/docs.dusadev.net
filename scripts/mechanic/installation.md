---
icon: down
---

# Installation

***

## Video Guide

We'll share detailed installation video ASAP

***

## Steps

{% stepper %}
{% step %}
### Install packages

* Install package named **"Dusa Mechanic V2 | Tuning, Tablet App, Illegal Tuning, Job"**
* Install other package named **"Dusa Tablet | Hub for Dusa resources"**
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

1. Navigate into path: `[dusa]/dusa_tablet/INSTALL`
2. **If you using `ox_inventory`**
   1. Open `ox_inventory_items.txt`, copy content
   2. Navigate into `ox_inventory/data/items.lua` and paste to bottom
   3. Open `illegal_network_items_ox_inventory.txt`, copy content
   4. Open `ox_inventory/data/items.lua` and paste them too
3. **If you using `other inventories`**
   1. Add the items that included at `qb_core_items.txt` and `illegal_network_items_qb_core.txt` to your framework or your core. It depends on which inventory or core is this.
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

## If you got SQL errors at startup

Normally, SQL works properly by default and does not cause any errors. However, SQL services used for some servers may differ and may cause errors when running automatically.

**To resolve this issue:**

Go to the `dusa_mechanic` folder and run the `dusa_mechanic_full_install.sql` file in your database.

**If you are also using the tablet:**

Go to the `dusa_tablet` folder and run the `dusa_tablet_full_instal.sql` file in your database.

{% hint style="warning" %}
Ensure you are performing the operation on the correct database. Performing this operation on a database not connected to your server will prevent it from being detected.
{% endhint %}
