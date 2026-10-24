# Changelog

All notable changes to Dusa Bridge, newest first. Download the latest version from [CFX Portal → Granted Assets](https://portal.cfx.re/assets/granted-assets).

***

### 0.9.8

_October 20, 2026_

* Fixed compatibility with ox\_lib 3.40.1 and newer, so resources using the bridge start cleanly without the “ox\_lib must be started before this resource” error or follow-on errors such as items not registering.
* Fixed module loading so files with the same name from different resources no longer load the wrong module.

***

### 0.9.7

_October 13, 2026_

* Fixed the shop failing to open on servers running ak47 inventory.
* Fixed shops, stashes and item checks not working with the ak47 inventory exports.
* Added ak47\_banking support for society (job) accounts.

***

### 0.9.6

_October 4, 2026_

* Added Qbox support for payments, so servers running Qbox can use the bridge without a separate adapter.
* Improved payment handling on ESX and QB servers for more consistent results.

***

### 0.9.5

_July 20, 2026_

* Fixed shops not opening on servers running tgiann-inventory; shops now open through tgiann-inventory's own shop export.

***

### 0.9.4

_July 13, 2026_

* Fixed compatibility with the origen\_inventory system, so supported inventory features now work reliably instead of failing through the wrong integration path.
* Improved inventory framework detection by giving origen\_inventory its own dedicated support for both ox and QBCore setups.

***

### 0.9.3

_June 14, 2026_

* Added a vehicle ownership check across supported frameworks so admin-spawned and other unowned vehicles are skipped when saving vehicle data, with a safe fallback if the database query fails.
* Added a live telemetry log store and browser-based debug dashboard to make diagnosing server issues easier.
