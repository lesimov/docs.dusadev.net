---
icon: function
---

# Exports

### GiveKeys

```lua
exports.dusa_vehiclekeys:GiveKeys(id, plate)
```

* id: `number` | Player ID
* plate: `string` | Vehicle Plate



### RemoveKeys

```lua
exports.dusa_vehiclekeys:RemoveKeys(id, plate)
```

* id: `number` | Player ID
* plate: `string` | Vehicle Plate



### HasKeys

<pre class="language-lua"><code class="lang-lua"><strong>local haskeys = exports.dusa_vehiclekeys:HasKeys(id, plate)
</strong><strong>print(haskeys) -- true or false
</strong></code></pre>

* id: `number` | Player ID
* plate: `string` | Vehicle Plate

