---
icon: gun
---

# How to add custom weapon compatibility?

Actually, it's very simple to do this. Now I will show you step by step how you can do it.



{% stepper %}
{% step %}
### List your weapons

If you make incomplete additions to the weapons, this weapon type will not leave any evidence and will display a warning in your F8 console saying "Please add your weapon to weapons.lua". Therefore, it is important to comprehensively define your weapons.
{% endstep %}

{% step %}
### Follow the path:

Open the weapons.lua file with a code editor (such as Visual Studio Code or Notepad).
{% endstep %}

{% step %}
### Open the weapons.lua file with a

At this stage, we recommend using editors like Visual Studio Code or
{% endstep %}

{% step %}
### Scroll to the bottom of the file to find

The sample code you found should be like this

`-- [weapon_weaponname] = { name = 'weapon_weaponname', label = 'Weapon Display Name' },`
{% endstep %}

{% step %}
### Copy and paste the sample code as many times as your number of weapons.
{% endstep %}

{% step %}
### After duplicating, arrange these lines individually based on your weapon list.

For example, let's say the name of our custom weapon is weapon\_arpistol. In this case, we should update it as follows.

`[`weapon\_arpistol`] = { name = '`weapon\_arpistol`', label = 'AR Pistol' },`

The label value indicates how the name of the weapon should appear in the evidence.&#x20;

The name value and the initial value inside square brackets must be the same.
{% endstep %}

{% step %}
### Important

In the sample code, there are two "-" signs at the beginning of the line. You must remove these signs when adding your weapons. That is:

Incorrect Usage:

`-- [weapon_weaponname] = { name = 'weapon_weaponname', label = 'Weapon Display Name' },`

Correct Usage:

`[weapon_weaponname] = { name = 'weapon_weaponname', label = 'Weapon Display Name' },`
{% endstep %}
{% endstepper %}
