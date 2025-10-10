---
description: >-
  Handlers allow you to add code when an event occurs (such as receiving a new
  report or creating a new GPS channel).
icon: circle-chevron-right
---

# Handlers

## Location of handlers file

`dusa_dispatch/edit/handlers.lua`

## Event List

<table><thead><tr><th width="286">export</th><th width="165">parameters</th><th>description</th></tr></thead><tbody><tr><td>dusa_dispatch:client:SendDispatch</td><td><code>data</code></td><td>It runs when a new alert arrives and sends the alert's data within the data</td></tr><tr><td>dusa_dispatch:MenuOpened</td><td>none</td><td>Runs when dispatch management menu is opened | <strong>Use this to hide your hud</strong></td></tr><tr><td>dusa_dispatch:MenuClosed</td><td>none</td><td>Runs when dispatch management menu is closed | <strong>Use this to show your hud</strong> </td></tr><tr><td>dusa_dispatch:CameraCreated</td><td><code>cameraId, cameraName</code></td><td>Runs when new camera is created</td></tr><tr><td>dusa_dispatch:UnitCreated</td><td><code>data</code></td><td>It runs when a new unit is created and sends information about the unit</td></tr><tr><td>dusa_dispatch:GpsCreated</td><td><code>gps</code></td><td>Runs when a new GPS channel created</td></tr><tr><td>dusa_dispatch:RadioCreated</td><td><code>frequency</code></td><td>Runs when a new Radio channel created</td></tr></tbody></table>



