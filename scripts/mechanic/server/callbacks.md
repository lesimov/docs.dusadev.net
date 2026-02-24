# Callbacks

-----

## Server Callbacks

### Listing Work Orders

```lua
lib.callback.register('mechanic:getWorkOrders', function(source, data)
    -- Parameters:
    -- data.shopId (int) - Shop ID
    -- data.status (string) - 'pending', 'in_progress', 'completed'
    -- data.page (int) - Page Number (pagination)
    -- data.limit (int) - Limit returned order count

    -- Usage:
    local result = lib.callback.await('mechanic:getWorkOrders', false, {
        shopId = 1,
        status = 'pending',
        page = 1,
        limit = 20
    })
end)
```

-----

## Client Callbacks

### Creating New Work Order

```lua
local result = lib.callback.await('mechanic:createWorkOrder', false, {
    vehicleModel = GetDisplayNameFromVehicleModel(GetEntityModel(vehicle)),
    vehiclePlate = GetVehicleNumberPlateText(vehicle),
    description = "Full tuning package",
    shopId = "1" -- Desired shop id can be found at ds_mechanic_shops > id column
})

if result.success then
    print("Order created: " .. result.orderId)
end
```

-----

### Hire Employee

```lua
local result = lib.callback.await('mechanic:hireEmployee', false, {
    serverId = 42,           -- Target Player Server ID (Source)
    shopId = "1", -- Desired shop id can be found at ds_mechanic_shops > id column
    jobGrade = 0
})

if result.success then
    print("Hired employee successfully")
else
    print("Error: " .. result.error)
end
```

-----

### Withdraw Money

```lua
local result = lib.callback.await('mechanic:withdrawFromVault', false, {
    shopId = "1",
    amount = 50000
})

if result.success then
    print("Done! New balance: " .. result.newBalance)
else
    print("Error: " .. result.error)
end
```

> **Info:** Withdraw money and Hiring employee callbacks would require player to own defined shop. Otherwise they gonna throw error.

-----
