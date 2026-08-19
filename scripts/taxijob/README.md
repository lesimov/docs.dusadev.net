---
icon: taxi
---

# Taxi Job

Good to have Taxi Job, stable and covers everything you need from a Taxi.

***

## Purchase

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th></tr></thead><tbody><tr><td><h3>Taxi  Job </h3></td><td><a href="https://dusadev.net/scripts/7594828">Purchase Here</a></td><td>Taxi job package</td><td><a href="../../.gitbook/assets/taxithumbnail.png">taxithumbnail.png</a></td></tr></tbody></table>

***

## Showcase

Explore `dusa_taxijob`



**Trailer**

{% embed url="https://youtu.be/yH_wq9TMpiY" %}

***

## Setup

Follow our guide to install mechanic properly.

{% content-ref url="../mechanic/installation.md" %}
[installation.md](../mechanic/installation.md)
{% endcontent-ref %}

***

## Config

```lua
TaxiConfig = {
    debug = false,
    locale = 'en',
    interaction = 'textui',
    currency = 'USD',

    blips = {
        enabled = true,
        sprite = 198,
        color = 5,
        scale = 0.8,
        display = 4,
        shortRange = true,
    },

    permissions = {
        managerUsesBossFlag = true,
    },

    recruitment = {
        radius = 5.0,
        inviteTimeoutSeconds = 30,
    },

    employment = {
        defaultJob = 'unemployed',
    },

    economy = {
        societyShare = 0.80,
        driverShare = 0.20,
        driverAccount = 'bank',
        tipAccount = 'cash',
        impoundFee = 2500,
    },

    progression = {
        levels = {
            [1] = { requiredTrips = 0, employeeCapacity = 3, vehicleCapacity = 5 },
            [2] = { requiredTrips = 25, employeeCapacity = 5, vehicleCapacity = 5 },
            [3] = { requiredTrips = 75, employeeCapacity = 10, vehicleCapacity = 10 },
        },
    },

    meter = {
        startKey = 'B',
        openingFare = 30.0,
        ratePerUnit = 18.0,
        maxFare = 1500.0,
        unit = 'km',
        priceIntervalMs = 4000,
        distanceIntervalMs = 400,
        maxSpeedMetersPerSecond = 70.0,
        manualIdleTimeoutSeconds = 120,
        manualCompletedTimeoutSeconds = 120,
        manualPassengerGraceSeconds = 10,
    },

    missions = {
        automaticAssignment = true,
        dispatchMinSeconds = 180,
        dispatchMaxSeconds = 300,
        offerTimeoutMinSeconds = 600,
        offerTimeoutMaxSeconds = 900,
        pickupTimeoutSeconds = 300,
        meterStartTimeoutSeconds = 35,
        tripTimeoutSeconds = 900,
        completionRadius = 18.0,
        pickupRadius = 28.0,
        pickupHighlightRadius = 55.0,
        destinationHighlightRadius = 120.0,
        destinationMarkerRadius = 10.0,
        passengerDepartureCleanupMs = 15000,
        passengerSpawnGraceMs = 2000,
        tip = {
            baseChance = 0.25,
            fastPickupBonus = 0.45,
            minAmount = 25,
            maxAmount = 90,
        },
        passengerModels = {
            'a_f_y_business_01',
            'a_m_y_business_02',
            'a_f_y_tourist_01',
            'a_m_y_beach_01',
            'a_f_m_bevhills_01',
        },
        points = {
            { label = 'Legion Square', address = 'Vespucci Blvd', coords = vector4(215.76, -810.12, 30.73, 159.0) },
            { label = 'Pillbox Hospital', address = 'Elgin Ave', coords = vector4(307.35, -595.31, 43.28, 70.0) },
            { label = 'Vespucci Beach', address = 'Magellan Ave', coords = vector4(-1222.63, -1495.72, 4.35, 303.0) },
            { label = 'Del Perro Pier', address = 'Red Desert Ave', coords = vector4(-1604.18, -1007.84, 13.02, 317.0) },
            { label = 'Rockford Plaza', address = 'Las Lagunas Blvd', coords = vector4(-716.22, -155.68, 37.42, 29.0) },
            { label = 'Mirror Park', address = 'Nikola Ave', coords = vector4(1181.76, -430.37, 67.02, 76.0) },
            { label = 'LSIA Terminal', address = 'New Empire Way', coords = vector4(-1037.71, -2737.86, 20.17, 329.0) },
            { label = 'Casino', address = 'Vinewood Park Dr', coords = vector4(925.11, 46.92, 81.11, 56.0) },
            { label = 'Alta Station', address = 'Occupation Ave', coords = vector4(-250.84, -886.77, 30.63, 161.0) },
            { label = 'Little Seoul', address = 'Ginger St', coords = vector4(-704.76, -823.64, 23.72, 94.0) },
        },
    },

    vehicle = {
        fuelSystem = 'ox_fuel',
        keySystem = 'qbx_vehiclekeys',
        spawnFuel = 100.0,
        shop = {
            { id = 'taxi-standard', model = 'taxi', price = 90000 },
            -- { id = 'taxi-classic', model = 'dynasty', price = 140000 },
        },
        blockedClasses = {
            [8] = true,
            [10] = true,
            [11] = true,
            [14] = true,
            [15] = true,
            [16] = true,
            [18] = true,
            [19] = true,
            [20] = true,
            [21] = true,
        },
    },

    stations = {
        {
            id = 'downtown',
            label = 'Downtown Cab Co.',
            job = 'taxi_downtown',
            bossGrade = 4,
            app = {
                location = 'Mission Row',
            },
            price = 1250000,
            starterVehicles = { 'taxi', 'taxi' },
            blip = {
                name = 'Downtown Taxi Station',
                coords = vector3(899.24, -170.78, 74.14),
            },
            purchase = { coords = vector3(895.68, -179.28, 74.70), size = vector3(2.0, 2.0, 2.5), rotation = 58.0 },
            management = { coords = vector3(907.19, -161.11, 74.12), size = vector3(1.8, 1.8, 2.5), rotation = 58.0 },
            employee = { coords = vector3(899.24, -170.78, 74.14), size = vector3(1.8, 1.8, 2.5), rotation = 58.0 },
            garage = {
                spawn = vector4(915.61, -164.74, 74.37, 98.0),
                returnZone = { coords = vector3(908.77, -177.58, 74.20), size = vector3(4.5, 6.0, 3.0), rotation = 58.0 },
            },
        },
        {
            id = 'vespucci',
            label = 'Vespucci Taxi',
            job = 'taxi_vespucci',
            bossGrade = 4,
            app = {
                location = 'Vespucci Beach',
            },
            price = 1050000,
            starterVehicles = { 'taxi', 'taxi' },
            blip = {
                name = 'Vespucci Taxi Station',
                coords = vector3(-1158.88, -1543.56, 4.38),
            },
            purchase = { coords = vector3(-1153.67, -1518.17, 10.63), size = vector3(2.0, 2.0, 2.5), rotation = 35.0 },
            management = { coords = vector3(-1162.01, -1551.73, 4.38), size = vector3(1.8, 1.8, 2.5), rotation = 35.0 },
            employee = { coords = vector3(-1158.88, -1543.56, 4.38), size = vector3(1.8, 1.8, 2.5), rotation = 35.0 },
            garage = {
                spawn = vector4(-1181.22, -1493.48, 4.38, 124.0),
                returnZone = { coords = vector3(-1174.18, -1502.52, 4.39), size = vector3(5.0, 7.0, 3.0), rotation = 35.0 },
            },
        },
    },
}

```

***

## Support

Join our [Discord](https://discord.gg/dusa) server and open a ticket from the related channel.
