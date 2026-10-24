# Changelog

All notable changes to Dusa Mechanic, newest first. Download the latest version from [CFX Portal → Granted Assets](https://portal.cfx.re/assets/granted-assets).

***

### 2.1.14

_October 24, 2026_

* Fixed saved stance and fitment not persisting reliably; camber, offset, width and suspension now restore after storing, respawning, leaving the area and collision resets.
* Added a server-side garage hook: your garage must call it after spawning a vehicle so saved stance is restored. See the [Garage Integration](garage-integration.md) guide.
* Improved stance purchases: a failed save no longer completes the order, partially saved values are kept and failed direct purchases are refunded.
* Fixed the tablet and MechanicOS appearing too small on 1440p, 4K and ultrawide displays; the interface now fills the screen at a consistent size, while 1080p rendering stays unchanged.
* Fixed assembly orders getting stuck as in progress after a disconnect; completed steps are preserved and the same character can resume the order after rejoining, with a Resume Assembly button and reminder.
* Added a configurable 30-minute timeout that reopens an unfinished assembly order and unlocks the vehicle, while preventing another mechanic from starting an order that is already active.

***

### 2.1.13

_October 23, 2026_

* Fixed Redline vehicle analysis rejecting authorized shop employees, owners and custom mechanic jobs who could already open the tablet, so analysis now uses their existing shop access.
* Improved vehicle history and illegal-mod removal to recognize the same active shop membership access already used by the tablet.

***

### 2.1.12

_October 20, 2026_

* Added Brazilian Portuguese support across the tablet, MechanicOS, tutorials and configuration panel, including notifications and tuning labels.
* Improved language loading so untranslated entries fall back to English instead of showing raw translation keys, and unsupported languages default to English.
* Improved Turkish translation coverage and made previously untranslated interface text translatable.
* Improved default tuning, assembly and craft labels with translations while keeping existing custom server-owner text unchanged.

***

### 2.1.11

_October 19, 2026_

* Fixed an error when saving suspension in the tuning menu while the stance module is disabled.
* Fixed purchased wheel fitment (camber and offset) resetting after driving or a collision.
* Fixed society banking so shop income, vault balance and withdrawals use the shop's job society account when no society name has been set for the shop.
* Fixed banking integrations reporting a successful deposit or withdrawal when the bank refused it; the balance now stays unchanged and the failure is reported.
* Fixed repair-kit use so a kit is only consumed when the repair actually succeeds, and rapid repeated use can no longer trigger overlapping repairs or consume extra kits.
* Fixed shop owners without a linked employee record not seeing mechanic-only tablet apps; ownership alone now grants the same tablet access as shop staff.
* Fixed repeated ECU flashes and trouble-code clearing stacking performance boosts; each operation now applies the tune once at its intended strength.
* Fixed restoring stock tuning after repeated flashes leaving inflated acceleration or top speed; the vehicle's original handling is now restored.
* Fixed ECU tunes carrying over between vehicles; each vehicle now keeps its own baseline and settings.
* Fixed onboard diagnostics sometimes reading a previously used vehicle after switching cars; checks now follow the current vehicle.
* Fixed the repair NPC ignoring on-duty shop staff and being blocked by off-duty mechanics; availability now follows actual shop membership and duty status.
* Added full localization for the AutoServe dashboard and shop profile, including labels, status badges, alerts and feedback, so they follow the selected language.
* Improved custom language files: they can now translate the new dashboard and profile texts, and readable English is shown until a translation is added.
* Fixed car lifts dropping a raised vehicle when something collided with the lift; the lift now stays anchored in place while it carries a car.
* Fixed the Duty Zone prompt so it switches between clocking on and clocking off after pressing E, and the tablet duty badge now matches the duty status the server enforces.
* Fixed car lifts sinking into the ground when a vehicle is driven onto them; lifts now stay locked in place for every player.
* Fixed saved tuning, ECU tunes and drivetrain changes not applying to vehicles taken out of a garage until the driver got out and back in.
* Fixed saved ECU tunes being applied a second time when re-entering a vehicle, which could leave the vehicle with stacked or outdated performance changes.

***

### 2.1.10

_October 13, 2026_

* Fixed review submissions failing with a database error, so order ratings are now saved correctly.
* Fixed shop income not reaching the society account when society banking is enabled; assembly, tuning and standalone order payouts now credit the correct account.
* Added a configuration option to allow or block overlapping ramp and tuning zones so staff can place them where needed.
* Added a hook for tow truck keys so they can be issued through your own key resource; brief configuration or integration is required.
