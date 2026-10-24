# Changelog

All notable changes to Dusa Hunting, newest first. Download the latest version from [CFX Portal → Granted Assets](https://portal.cfx.re/assets/granted-assets).

***

### 1.6.4

_October 2, 2026_

* Fixed animals wandering onto roads; they now steer back into the wild, away from traffic.
* Fixed a single kill sometimes counting twice toward hunt quests; each nearby dead animal now advances a quest only once.
* Fixed errors on servers that do not run ox\_inventory when the script looks up item names.

***

### 1.6.3

_August 9, 2026_

* Fixed butchering so each unit of a part creates its own world object, including quality bonuses, instead of only one per part type.
* Fixed pickup notifications to show readable item labels and fixed placed props despawning or floating.
* Added an option to disable animal tracking.
* Fixed the tournament menu remaining visible when tournaments are disabled.

***

### 1.6.2

_June 15, 2026_

* Fixed the quest tracker disappearing after a restart or reconnect, so the active quest now stays visible until it is completed.
* Fixed animal kills not counting toward hunt quest progress, so your own kills now advance the objective correctly.
* Fixed rental vehicles spawning with an empty fuel tank, so they now arrive fully fueled with supported fuel systems.
* Fixed the butcher zone hint appearing on every vehicle entry, so it now shows at most twice per vehicle.

***

### 1.6.0

_April 8, 2026_

* Added ATV (Blazer) rentals alongside existing rental vehicles, including per-vehicle carcass capacity limits and animal restrictions.
* Added the ability to carry animal carcasses on rented ATVs, with properly aligned positioning for each supported animal type.
* Improved the vehicle purchase menu with a redesigned interface and clear vehicle selection so players can browse and buy more easily.
* Fixed the co-op lobby menu sometimes staying on screen after closing it with ESC or Backspace.

***

### 1.5.2

_March 30, 2026_

* Fixed the in-game laptop not closing with ESC, so players can exit the map screen and regain control of their character immediately.
* Improved the laptop map to load instantly from local files, removing the external CDN dependency and fixing cases where the map failed to display.
* Improved predator animals so they actively hunt and attack players with tougher, more aggressive combat behavior instead of fleeing.
* Fixed cameras and laptop objects staying active after a resource restart, preventing stuck cameras and lost player controls.
* Fixed missing tournament interface text in English and Turkish.
