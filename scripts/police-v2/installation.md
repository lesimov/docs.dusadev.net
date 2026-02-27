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

* Install package named **"Dusa Police V2"**
* Install other package named **"Police Job Props"**
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

1. Navigate into path: `[dusa]/dusa_police/INSTALL`
2. **If you using `ox_inventory`**
   1. Open `items/ox.txt`, copy content
   2. Navigate into `ox_inventory/data/items.lua` and paste to bottom
3. **If you using `other inventories`**
   1. Add the items that included at `items/qb.txt` to your framework or your core. It depends on which inventory or core is this.
{% endstep %}

{% step %}
### Add item images

1. Navigate into path: `[dusa]/dusa_police/INSTALL/images/`&#x20;
2. Copy images inside
3. Paste item images to your inventory `images` folder
{% endstep %}
{% endstepper %}

