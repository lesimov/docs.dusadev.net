---
icon: function
---

# Exports



### GiveKeys

```lua
exports.dusa_vehiclekeys:GiveKeys(plate)
```

* plate?: `string` or `nil` | Returns closest vehicle plate if plate is nil



### RemoveKeys

```lua
exports.dusa_vehiclekeys:RemoveKeys(plate)
```

* plate: `string`



### GiveKeysAuto

```lua
exports.dusa_vehiclekeys:GiveKeysAuto()
```



### RemoveKeysAuto

```lua
exports.dusa_vehiclekeys:RemoveKeysAuto()
```



### HasKey

<pre class="language-lua"><code class="lang-lua"><strong>local haskey = exports.dusa_vehiclekeys:HasKey(plate)
</strong><strong>print(haskey) -- true or false
</strong></code></pre>

* plate: `string`&#x20;
