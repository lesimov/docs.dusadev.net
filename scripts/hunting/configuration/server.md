---
icon: circle-small
---

# Server Configuration

File: `configurations/config_server.lua`

This file contains server-side configuration including level system, animal rewards, cooking configuration, and quality-based bonuses.

***

## Level System

```lua
Config.MaximumLevel = 10

Config.Title = {
    beginner = 1,
    novice = 2,
    apprentice = 4,
    adept = 6,
    expert = 8,
    master = 10,
}
```

**Configuration**:

* `MaximumLevel` - Maximum hunting level players can reach
* `Title` - Title names and their level requirements
  * Titles are localized in `locales/` files

**Title Progression**:

* Level 1: Beginner
* Level 2-3: Novice
* Level 4-5: Apprentice
* Level 6-7: Adept
* Level 8-9: Expert
* Level 10: Master

***

## Quality-Based Rewards

```lua
Config.IncreaseAmountByQuality = true  -- Enable quality-based bonus amounts
```

When enabled, higher quality kills grant bonus items:

* **Quality 1**: +0 bonus items (base amount)
* **Quality 2**: +1 bonus item
* **Quality 3**: +2 bonus items

**Example**:

* Deer beef base amount: 3
* Quality 1 kill: 3 beef
* Quality 2 kill: 4 beef
* Quality 3 kill: 5 beef

***

## Animal Rewards

Configure what items players receive when butchering animals:

```lua
Config.AnimalRewards = {
    ['deer'] = {
        meat = {
            item = 'deer_meat',
            parts = {
                beef = {
                    amount = 3,  -- Base amount
                    model = 'propk_deer_beef_raw',
                    item = 'deer_beef',
                    cook = {
                        method = {'grill', 'stick'},  -- Cooking methods
                        cookingTime = 10,  -- Seconds
                        cookedModel = 'propk_deer_beef_cooked',
                        cookedItem = 'deer_beef_cooked'
                    }
                },
                rib = {
                    amount = 1,
                    model = 'propk_deer_rib_raw',
                    item = 'deer_rib',
                    cook = {
                        method = {'grill'},
                        cookingTime = 10,
                        cookedModel = 'propk_deer_rib_cooked',
                        cookedItem = 'deer_rib_cooked'
                    }
                },
                leg = {
                    amount = 4,
                    model = 'propk_deerleg_raw',
                    item = 'deer_leg',
                    cook = {
                        method = {'grill'},
                        cookingTime = 10,
                        cookedModel = 'propk_deerleg_cooked',
                        cookedItem = 'deer_leg_cooked'
                    }
                },
            },
        },
        hide = {
            amount = 1
        },
    },
}
```

### Reward Structure

Each animal can have:

**Meat Parts**:

* `amount` - Base number of items
* `model` - Prop model for the raw meat
* `item` - Item name (must match inventory item)
* `cook` - Cooking configuration (optional)
  * `method` - Array of cooking methods: `'grill'`, `'stick'`
  * `cookingTime` - Time in seconds to cook
  * `cookedModel` - Prop model for cooked meat
  * `cookedItem` - Cooked item name

**Hide**:

* `amount` - Number of hides to give

***

## Cooking Methods

Two cooking methods are available:

1. **Grill** (`'grill'`)
   * Requires `primitive_grill` or `advanced_grill`
   * Can cook multiple items at once
   * Best for ribs and larger cuts
2. **Stick** (`'stick'`)
   * Requires `campfire`
   * Cooks one item at a time
   * Best for small cuts and quick cooking

**Example Configuration**:

```lua
cook = {
    method = {'grill', 'stick'},  -- Can use both methods
    cookingTime = 10,
    cookedModel = 'propk_deer_beef_cooked',
    cookedItem = 'deer_beef_cooked'
}
```

***

## Complete Animal Examples

### Deer (Large Animal)

```lua
['deer'] = {
    meat = {
        item = 'deer_meat',
        parts = {
            beef = { amount = 3, model = 'propk_deer_beef_raw', item = 'deer_beef', cook = {...} },
            rib = { amount = 1, model = 'propk_deer_rib_raw', item = 'deer_rib', cook = {...} },
            leg = { amount = 4, model = 'propk_deerleg_raw', item = 'deer_leg', cook = {...} },
        },
    },
    hide = { amount = 1 },
}
```

### Rabbit (Small Animal)

```lua
['rabbit'] = {
    meat = {
        item = 'rabbit_meat',
        parts = {
            body = { amount = 1, model = 'propk_rabbit_raw', item = 'rabbit_body', cook = {...} },
            leg = { amount = 4, model = 'propk_rabbit_leg_raw', item = 'rabbit_leg', cook = {...} },
            beef = { amount = 1, item = 'rabbit_beef', cook = {...} },
        },
    },
    hide = { amount = 1 },
}
```

### Bear (Dangerous Animal)

```lua
['bear'] = {
    meat = {
        item = 'bear_meat',
        parts = {
            beef = { amount = 7, model = 'propk_bear_beef_raw', item = 'bear_beef', cook = {...} },
            rib = { amount = 1, model = 'propk_bear_rib_raw', item = 'bear_rib', cook = {...} },
            leg = { amount = 4, model = 'propk_bear_arm_raw', item = 'bear_leg', cook = {...} },
        },
    },
    hide = { amount = 1 },
}
```

***

## Quality System

The quality system is based on shot location:

### Quality Levels

* **Quality 3 (Perfect)**:
  * Headshot (bones 99 or 98)
  * Trapped animals
  * Grants best rewards and highest sell price
* **Quality 2 (Good)**:
  * Leg shot (bones 1-20)
  * Decent rewards and sell price
* **Quality 1 (Normal)**:
  * Body shot (all other bones)
  * Base rewards and sell price

### Level Bonuses

Players receive quality bonuses based on their hunting level:

* Every 3 levels grants +1 quality (up to max quality 3)

**Example**:

* Level 1 player body shot = Quality 1
* Level 3 player body shot = Quality 2
* Level 6 player body shot = Quality 3
* Level 9 player leg shot = Quality 3 (2 + 1 from level)

**Note**: Quality is calculated in `game/client/main.lua` in the `CheckHitAnimalQuality` function.

***

## Sell Price Calculation

Final sell price = Base price × Quality multiplier

**Example** (Deer Beef):

* Base price: $45 (from `Shared.Shop.Sell`)
* Quality 1: $45 × 1.0 = $45
* Quality 2: $45 × 1.5 = $67.5
* Quality 3: $45 × 2.0 = $90

Quality multipliers are configured in [Shared Configuration](shared.md#quality-multipliers).

***

## XP Calculation

XP is awarded from multiple sources:

### Hunting XP

* Base XP from zone configuration (`animal.xp`)
* No quality modifiers for hunting XP

### Selling XP

Quality-based XP when selling items:

**Quality 3 Items**:

* 20% chance to gain 3-4 XP per 10 items sold
* 30% chance for 1-2 XP if selling 5-9 items

**Quality 2 Items**:

* 15% chance to gain 1-2 XP per 10 items sold
* 20% chance for 1 XP if selling 5-9 items

**Quality 1 Items**:

* No XP from selling

### Quest XP

* Defined per quest in `Shared.Quests`
* Awarded when quest is completed

***

## Customizing Rewards

To add a new animal reward:

1. **Add to AnimalRewards**:

```lua
Config.AnimalRewards['wolf'] = {
    meat = {
        item = 'wolf_meat',
        parts = {
            beef = {
                amount = 4,
                model = 'propk_wolf_beef_raw',
                item = 'wolf_beef',
                cook = {
                    method = {'grill', 'stick'},
                    cookingTime = 12,
                    cookedModel = 'propk_wolf_beef_cooked',
                    cookedItem = 'wolf_beef_cooked'
                }
            },
            rib = {
                amount = 2,
                model = 'propk_wolf_rib_raw',
                item = 'wolf_rib',
                cook = {
                    method = {'grill'},
                    cookingTime = 12,
                    cookedModel = 'propk_wolf_rib_cooked',
                    cookedItem = 'wolf_rib_cooked'
                }
            },
        },
    },
    hide = {
        amount = 2  -- Wolves give 2 hides
    },
}
```

2. **Add sell prices** in [Shared Configuration](shared.md#sellable-items)
3. **Add items to inventory** (see [Installation Guide](../installation.md))

***

## Best Practices

### Balancing Economy

1. **Consider rarity**:
   * Common animals (deer, rabbit) = lower prices
   * Rare animals (lion, bear) = higher prices
2. **Consider difficulty**:
   * Passive animals = lower rewards
   * Aggressive animals = higher rewards
3. **Quality system**:
   * Encourage skillful hunting (headshots)
   * Reward experienced players (level bonuses)

### Meat Amounts

Balance meat amounts based on:

* Animal size (bear > deer > rabbit)
* Realism (4 legs, multiple cuts of beef, etc.)
* Server economy

### Cooking Times

* Small items (rabbit leg): 5-10 seconds
* Medium items (deer beef): 10-15 seconds
* Large items (bear rib): 15-20 seconds

***

## Advanced Configuration

### Fallback Models

If an animal part doesn't have a model, the system uses fallback models:

```lua
local fallbackModels = {
    leg = 'propk_redpanda_arm_raw',
    beef = 'propk_deer_beef_raw',
    rib = 'propk_deer_rib_raw',
    body = 'propk_pork_beef_big_raw',
}
```

You can omit `model` from configuration if you want to use fallback.

### Disabling Cooking

To make an item non-cookable, simply omit the `cook` configuration:

```lua
hide = {
    amount = 1,
    item = 'wolf_pelt',
    -- No cook configuration = cannot be cooked
}
```

***

## Next Steps

* Configure [Client Settings](client.md) for hunting zones
* Review [Shared Configuration](shared.md) for shop and quests
* Check [API Reference](../api-reference.md) for custom integrations
