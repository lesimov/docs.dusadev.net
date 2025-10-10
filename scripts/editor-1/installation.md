---
icon: folder-arrow-down
---

# Installation

## Step-by-step

{% stepper %}
{% step %}
### Download dusa\_evidence and dusa\_bridge from your keymaster portal

You can find [keymaster portal](https://portal.cfx.re/assets/granted-assets) link from here
{% endstep %}

{% step %}
### Unzip both zips to your server resources folder


{% endstep %}

{% step %}
### Head into dusa\_evidence/installation folder


{% endstep %}

{% step %}
### Run SQL file

Open run.sql and run it to your database
{% endstep %}

{% step %}
## Add items to your inventory

1. **For ox\_inventory**

Open ox\_items and copy its content

Go to ox\_inventory/data/items.lua

Paste the items you copied bottom of items.lua

2. **For qb-inventory**

Open qb\_items and copy its content

Go to qb-core/shared/items.lua

Paste the items you copied bottom of items.lua
{% endstep %}

{% step %}
### Add item images to your inventory

Head into dusa\_evidence/installation/images folder

Copy all images

1. For ox\_inventory head into ox\_inventory/web/images and paste
2. For qb-inventory head into qb-inventory/html/images and paste
{% endstep %}

{% step %}
### Add to your server.cfg

Add script start to your server.cfg - **Start order is important!**

```
start ox_lib
start qbx_core # Or es_extended or qb-core

start dusa_bridge
start dusa_evidence
```
{% endstep %}
{% endstepper %}

## If you had an issue with downloading <a href="#integrations-compatibilities" id="integrations-compatibilities"></a>

Open ticket from our discord server\
https://discord.gg/dusa

{% embed url="https://discord.gg/dusa" %}
