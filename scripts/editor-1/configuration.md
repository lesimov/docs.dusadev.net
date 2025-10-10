---
icon: folder-arrow-down
---

# Configuration



## Config v0.9.6

```lua
Config = {
    Debug = false,
    ----------------------------------------------
    --[[
        Use Target or press E system on reaching evidence location 

        Default: false
    ]]
    Target = true,
    TargetOptions = {
        debug = false,
        size = { 0.5, 0.5, 0.5 },
        distance = 3.5,
        icon = 'fa-regular fa-hand',
    },
    ----------------------------------------------
    PoliceJobs = {'police', 'sheriff', 'sasp'},
    RequireDuty = true,
    PoliceDropEvidence = true,
    CanClearEvidence = true,

    --[[
        Enable or Disable type of evidences

        Default: true

        true: Enabled
        false: Disabled
    ]]
    
    IsEnabled = {
        blood = true,
        fingerprint = true,
        gsr = true
    },

    --[[
        Reach Evidence Menu
    ]]
    UseItem = true,
    EvidenceItem = 'evidence_tablet',

    UseCommand = true,
    Command = 'evidence',

    UseLocations = true,
    Locations = {
        ['LSPD'] = {
            coords = vector3(437.275, -995.332, 30.623),
        }
    },

    --[[
        Evidence present in an area is checked every 30 minutes, and any evidence that has been present for longer than the specified time is removed from the ground.
        IMPORTANT: This is a *critical* option for optimization. Increasing the values too much can put strain on the server and lead to timeouts. Therefore, be careful not to set the values too high.

        Default: 30 (minutes) That means if the evidence is on the ground for more than 30 minutes, it will be removed automatically.
    ]]
    DespawnTimeouts = {
        blood = 30,
        bullet = 30,
        casing = 30,
    },

    Thresholds = { -- Max evidence count on ground, if it exceeds, it will remove the oldest one. This is for serverside optimization
        blood = 50,
        bullet = 150,
        casing = 200,
    },

    RemoveItemAfterUse = false, -- Remove used items after use

    -- Enable / Disable timeout for each evidence drop between 2 drops
    TimerName = { 
        Shooting = true,
        Blood = true,
    },

    -- Determine the time between each evidence drop
    EvidenceDelay = {  -- in ms
        Shooting = 5000, -- 5 seconds is optimal for shooting, if you decrease this value might cause crashes when 100-200 players shooting at the same time
        Blood = 2000
    },
    
    Items = {
        evidence_bag = 'empty_evidence_bag',
        filled_bag = 'filled_evidence_bag',
    },

    WhitelistedWeapons = { -- Prevent these weapons to drop bullet casing
        `weapon_unarmed`,
        `weapon_snowball`,
        `weapon_stungun`,
        `weapon_petrolcan`,
        `weapon_hazardcan`,
        `weapon_fireextinguisher`
    },

    DropEvidenceObject = {
        ['casing'] = true,
        ['blood'] = true,
    }, -- Drop evidence object on the ground

    CasingObjects = {
        ['GROUP_PISTOL'] = `w_pi_singleshoth4_shell`,
        ['GROUP_RIFLE'] = `w_pi_singleshot_shell`,
        ['GROUP_SHOTGUN'] = `w_sg_pumpshotgunh4_mag1`,
        ['GROUP_SMG'] = `w_pi_singleshoth4_shell`,
        ['GROUP_SNIPER'] = `w_pi_singleshot_shell`,
        ['GROUP_STUNGUN'] = `w_ar_specialcarbinemk2_mag_fmj`,
        ['GROUP_MG'] = `w_pi_singleshoth4_shell`,
    },

    BloodObject = `p_bloodsplat_s`, -- Blood object

    --[[
        Enable or disable the feature that causes blood to appear only when the player takes damage from another player.

        Setting this to false will allow blood evidence to be created regardless of the cause of damage.
        Setting this to true will cause blood evidence to be created only when the player is attacked by another player.

        Default: true
    ]]
    BloodCanDropOnlyByAttacker = false, 

    WhitelistedGloves = {
        16,
        17,
        18
    },
    FingerprintItem = 'magnifying_glass',
    FingerprintProgress = 5, -- in second

    EnableLineAnalyze = true,
    LineAnalyzeItem = 'thermal_camera',
    AnalyzeRange = 20.0,

    EnableGSR = false,
    GSRItem = 'cleaningkit', -- default shared ox & qb item
}
```

