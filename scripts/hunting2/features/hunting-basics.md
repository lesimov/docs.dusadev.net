---
icon: crosshairs
---

# Hunting Basics

Master the fundamentals of hunting in this comprehensive guide covering mechanics, techniques, and strategies.

## Core Hunting Mechanics

### Finding Animals

Animals spawn dynamically in designated hunting zones based on several factors:

- **Zone Configuration**: Each zone has specific animal types
- **Spawn Chances**: Rarity determines how often animals appear
- **Time of Day**: Some animals are more active at dawn/dusk
- **Player Proximity**: Animals spawn within configured distance
- **Zone Capacity**: Limited number of animals per zone

### Weapon Selection

Choosing the right weapon is crucial for hunt success:

#### Recommended Weapons by Animal Size

| Animal Size | Best Weapon | Quality Modifier |
|-------------|-------------|------------------|
| **Small** (Rabbit, Fox) | Bow, Pistol | Bow: 100%, Pistol: 90% |
| **Medium** (Deer, Coyote) | Rifle, Bow | Rifle: 100%, Bow: 90% |
| **Large** (Boar, Elk) | Rifle, Sniper | Both: 100% |
| **Dangerous** (Mountain Lion, Bear) | Rifle, Sniper | Rifle: 100% |

#### Weapon Characteristics

**Hunting Rifle**
- ✅ High damage
- ✅ Good accuracy
- ✅ Best overall choice
- ❌ Loud (may scare other animals)

**Bow**
- ✅ Silent hunting
- ✅ Good pelt quality
- ✅ Skill-based gameplay
- ❌ Requires practice
- ❌ Lower damage

**Sniper Rifle**
- ✅ Long range
- ✅ High accuracy
- ✅ Perfect for cautious animals
- ❌ Expensive ammo
- ❌ Slow fire rate

**Pistol**
- ⚠️ Only for small game
- ❌ Low damage
- ❌ Reduced pelt quality
- ❌ Not recommended for hunting

## Shot Placement & Quality System

The quality of your kill affects rewards significantly.

### Quality Ratings

**⭐⭐⭐ Perfect (3-Star)**
- Headshot with appropriate weapon
- Single clean kill shot
- Maximum rewards
- Best pelt quality

**⭐⭐ Good (2-Star)**
- Clean body shot
- Appropriate weapon used
- Standard rewards
- Good pelt quality

**⭐ Poor (1-Star)**
- Multiple shots required
- Wrong weapon used
- Reduced rewards
- Damaged pelt

### Quality Multipliers

```lua
-- Example calculation
Base Reward: $100
Perfect Quality: $100 × 2.0 = $200
Good Quality: $100 × 1.5 = $150
Poor Quality: $100 × 1.0 = $100
```

### Tips for Perfect Kills

1. **Use the Right Weapon**: Match weapon to animal size
2. **Aim for the Head**: Headshots guarantee perfect quality
3. **Wait for Clear Shot**: Don't rush
4. **Single Shot Kills**: Multiple shots reduce quality
5. **Don't Overkill**: Sniper on rabbit = poor quality

## Harvesting Animals

After successfully killing an animal:

### Harvesting Process

1. **Approach the Carcass**
   - Walk up to the dead animal
   - Interaction prompt appears

2. **Initiate Harvest**
   - Press interaction key (default: E)
   - Harvesting animation plays
   - Requires hunting knife in inventory

3. **Receive Rewards**
   - Pelt (quality-based)
   - Meat (quantity varies)
   - Special items (chance-based)
   - XP for your hunting level

### What You Can Harvest

**From Deer:**
- 1× Deer Pelt (quality-dependent)
- 2-4× Deer Meat
- 0-1× Deer Antler (30% chance)
- 50 XP

**From Rabbit:**
- 1× Rabbit Pelt
- 1-2× Rabbit Meat
- 15 XP

**From Boar:**
- 1× Boar Hide
- 3-5× Boar Meat
- 0-1× Boar Tusk (25% chance)
- 75 XP

**From Mountain Lion (Rare):**
- 1× Lion Pelt (premium)
- 1-2× Lion Tooth (trophy item)
- 200 XP
- $500 bonus

### Harvesting Requirements

⚠️ **You MUST have these items:**
- Hunting Knife (required)
- Inventory space for loot
- Hunting License (to avoid illegal status)

## Hunting Techniques

### Stalking

The art of approaching animals without spooking them.

**Stealth Movement:**
```
Walk (Default) - Normal movement, audible
Crouch (Ctrl) - Quiet, slower, less visible
Sprint (Shift) - Very loud, scares animals
```

**Wind Direction:**
- Animals can detect scent
- Approach from downwind when possible
- Use bait to control animal position

**Line of Sight:**
- Stay in cover when possible
- Use vegetation and rocks
- Don't silhouette yourself on ridges

### Tracking

Finding animal trails and patterns.

**Animal Behavior:**
- Animals follow paths to water
- Feeding areas have more activity
- Some animals are territorial
- Herd animals stay together

**Environmental Clues:**
- Movement in bushes
- Sound cues (birds, rustling)
- Other players hunting (competition)

### Ambush Hunting

Set up and wait for animals to come to you.

1. **Find a Good Position**
   - High ground advantage
   - Cover available
   - Good sightlines
   - Near animal paths

2. **Use Bait**
   - Place bait in open area
   - Position yourself nearby
   - Stay downwind
   - Wait patiently

3. **Stay Still**
   - Movement attracts attention
   - Use first-person for better aim
   - Don't AFK (animals have timers)

## Legal vs Illegal Hunting

### Legal Hunting Requirements

✅ Valid hunting license in inventory
✅ Hunting within designated zones
✅ Non-protected species
✅ Following server rules

### Illegal Hunting Consequences

❌ **Hunting without license:**
- Wanted level
- Police dispatch
- Fine if caught
- Items may be confiscated

❌ **Hunting protected species:**
- Higher wanted level
- Larger fine
- Possible jail time
- Loss of hunting privileges

❌ **Poaching (outside zones):**
- Illegal status
- Police alerted
- Severe penalties

### Protected Species

These animals are typically illegal to hunt:
- Mountain Lions (sometimes)
- Eagles
- Black Bears (rare spawns)
- Any animal marked as "protected" in config

⚠️ **Always check your hunting license status before hunting!**

## Experience & Progression

### Gaining XP

Every hunting activity grants experience:

| Action | XP Gained |
|--------|-----------|
| Kill Rabbit | 15 XP |
| Kill Deer | 50 XP |
| Kill Boar | 75 XP |
| Kill Rare Animal | 200+ XP |
| Perfect Quality Bonus | +50% XP |
| Complete Quest | 250-1000 XP |
| Cook Meat | 5-10 XP |

### Level Benefits

**Level 1-5: Novice Hunter**
- Access to basic zones
- Common animals only
- Standard rewards

**Level 6-10: Experienced Hunter**
- Unlock medium zones
- Medium game animals
- Better shop prices (10% discount)

**Level 11-15: Expert Hunter**
- Unlock premium zones
- Rare animal spawns
- Exclusive quests available

**Level 16+: Master Hunter**
- All zones accessible
- Legendary animals
- Maximum rewards
- Tournament advantages

### Tracking Your Progress

Open the hunting menu (default: F7) to view:
- Current level and XP
- XP needed for next level
- Total animals hunted
- Best quality kills
- Zones unlocked
- Active quests

## Advanced Tips

### Maximizing Profits

1. **Focus on Quality**: One perfect kill > multiple poor kills
2. **Complete Quests**: Better rewards than selling alone
3. **Cook Meat**: Cooked sells for more than raw
4. **Save Rare Items**: Hold for quests or tournaments
5. **Efficient Routes**: Plan hunting paths through zones

### Time Management

- **Early Morning (6-8 AM)**: High animal activity
- **Midday (12-4 PM)**: Lower spawns
- **Evening (6-8 PM)**: Peak hunting time
- **Night (10 PM+)**: Nocturnal animals

### Inventory Optimization

- Bring vehicle for storage
- Don't overhunt in one trip
- Sell regularly to free space
- Prioritize high-value items
- Keep quest items separate

### Group Hunting

- Split up to cover more area
- Share bait costs
- Coordinate on rare spawns
- Split rewards fairly
- Use voice chat for callouts

## Common Mistakes

❌ **Using wrong weapon**: Reduces pelt quality
❌ **Sprinting everywhere**: Scares all animals
❌ **No knife**: Can't harvest kills
❌ **Over-encumbering**: Can't run from danger
❌ **Ignoring zones**: Some animals only spawn in specific zones
❌ **Selling everything**: Save items for quests
❌ **Hunting in storms**: Reduced visibility and spawns

## Next Topics

Now that you understand hunting basics:

- 🔥 Master [Camping & Cooking](camping-cooking.md)
- 🪤 Learn [Trapping & Baiting](trapping-baiting.md)
- 🎯 Explore the [Quest System](quest-system.md)
- 🏆 Compete in [Tournaments](tournaments.md)
- 📈 Understand [Progression](progression.md)
