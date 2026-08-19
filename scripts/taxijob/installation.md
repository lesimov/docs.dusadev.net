---
icon: down
---

# Installation

***

## Steps

{% stepper %}
{% step %}
### Install packages

* Install package named **"Taxi Job: Manage Stations, Quests"**
* Install bridge package named **"Dusa Bridge"**
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
ensure dusa_bridge
ensure dusa_taxijob
```
{% endstep %}

{% step %}
### Add jobs

1. Navigate into dusa\_taxijob/\_INSTALL/qb-jobs.lua or esx-jobs.lua (qb-jobs.lua for QBCore and QBOX, esx-jobs.lua for ESX)
2. Copy content **without** return blocks
3. Paste it to your framework jobs section
4. Restart your server
{% endstep %}
{% endstepper %}

***

## Phone App

To use phone app, download package named **"Taxi Job Phone App"** from your Portal account. Drag & drop to your resources folder



Start order

```
start your_phone_resource # e.g lb-phone, qs-smartphone

start dusa_taxijob
start dusa_taxiapp
```

{% hint style="warning" %}
The key point is that the app must be launched after the phone's resources and Taxi Job have been initialized. Otherwise, you may experience startup issues.
{% endhint %}

