---
icon: folder-arrow-down
---

# Installation

### **First Steps**



{% stepper %}
{% step %}
Login to your [keymaster](https://keymaster.fivem.net/asset-grants/) account


{% endstep %}

{% step %}
Check **"Granted Assets"**


{% endstep %}

{% step %}
Find **Bridge, Vehicle Keys and Lockpick** from the list


{% endstep %}

{% step %}
Install them


{% endstep %}

{% step %}
Unzip all of them to your resources folder


{% endstep %}
{% endstepper %}

### **IMPORTANT - Replacing baseevents**

Replace your baseevents script with this one

{% embed url="https://github.com/lesimov/baseevents" %}

### Setting Start Order

Firstly, head into your **server.cfg** file

Place script with this start order **(ox\_lib, core firstly after that follow this order)**

```
start ox_lib
start qb-core
start dusa_bridge
start dusa_lockpick
start dusa_vehiclekeys
```



### Configuration

You can configure small details depends on your own will. Configuration not including anything that blocks script running
