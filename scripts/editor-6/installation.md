---
icon: folder-arrow-down
---

# Installation

## Step-by-step

{% stepper %}
{% step %}
### Download dusa\_dispatch and dusa\_bridge from your keymaster portal

You can find [keymaster portal](https://portal.cfx.re/assets/granted-assets) link from here
{% endstep %}

{% step %}
### Unzip both zips to your server resources folder


{% endstep %}

{% step %}
### Head into dusa\_dispatch


{% endstep %}

{% step %}
### Run SQL file

Open run.sql and run it to your database
{% endstep %}

{% step %}
### Add to your server.cfg

Add script start to your server.cfg - **Start order is important!**

```
start ox_lib
start qbx_core # Or es_extended or qb-core

start dusa_bridge
start dusa_dispatch
```
{% endstep %}
{% endstepper %}

## If you had an issue with downloading <a href="#integrations-compatibilities" id="integrations-compatibilities"></a>

Open ticket from our discord server\
https://discord.gg/dusa

{% embed url="https://discord.gg/dusa" %}
