---
icon: fire
---

# Camping & Cooking

Learn how to set up camp, cook your catch, and survive in the wilderness with this comprehensive camping and cooking guide.

## Camping System Overview

The camping system allows you to establish temporary bases in the wilderness for extended hunting trips.

### Camping Equipment

| Item | Purpose | Weight | Duration |
|------|---------|--------|----------|
| **Tent** | Shelter and rest point | 2000 | Until picked up |
| **Campfire Kit** | Cooking and warmth | 1000 | 10 minutes (burns out) |
| **Sleeping Bag** | Save spawn point | 500 | Until picked up |
| **Storage Box** | Store items at camp | 1500 | Until picked up |

### Where to Buy

Purchase camping equipment from any hunting shop:
- Tent: $1,500
- Campfire Kit: $500
- Sleeping Bag: $750
- Storage Box: $2,000

## Setting Up Camp

### Choosing a Camp Location

**Good Camp Locations:**
✅ Flat terrain
✅ Near hunting zones
✅ Away from roads
✅ Good visibility
✅ Near water (immersion)

**Avoid:**
❌ Steep slopes
❌ Inside buildings
❌ On roads
❌ Near police stations
❌ Too close to other camps

### Deploying Your Tent

1. **Open Your Inventory**
   - Find your tent item
   - Use the tent item

2. **Position the Tent**
   - Ghost placement preview appears
   - Move to adjust position
   - Rotate with mouse wheel
   - Green = valid placement
   - Red = invalid placement

3. **Confirm Placement**
   - Press E to place
   - Animation plays
   - Tent is deployed

4. **Interact with Tent**
   - Approach tent
   - Press E to open menu
   - Options:
     - Enter tent (camera transition)
     - Rest (restore health/armor)
     - Pack up tent (remove and get item back)

### Setting Up a Campfire

**Quick Setup:**

1. **Use Campfire Kit**
   - Select from inventory
   - Position on flat ground
   - Confirm placement

2. **Light the Fire**
   - Automatic lighting animation
   - Fire starts burning
   - Timer begins (10 min default)

3. **Cooking Interface**
   - Approach lit campfire
   - Interaction prompt appears
   - Press E to open cooking menu

**Campfire Duration:**
- Burns for 10 minutes (configurable)
- Can add wood to extend (+5 min per wood)
- Goes out automatically when timer ends
- Can be extinguished manually

## Cooking System

Transform raw meat into delicious consumables that restore hunger and can be sold for profit.

### Basic Cooking

**Step-by-Step:**

1. **Approach Active Campfire**
   - Must be lit and burning
   - Stand close enough for prompt

2. **Open Cooking Menu**
   - Press E to interact
   - Recipe list displays
   - Shows available ingredients

3. **Select Recipe**
   - Click on recipe
   - View requirements
   - Check if you have ingredients

4. **Start Cooking**
   - Confirm recipe selection
   - Cooking animation plays
   - Progress bar shows time remaining

5. **Collect Cooked Food**
   - Automatically added to inventory
   - Notification shows result
   - Small XP reward

### Cooking Recipes

#### Basic Recipes

**Cooked Meat**
```yaml
Input: 1× Deer Meat (raw)
Output: 1× Cooked Meat
Time: 10 seconds
Effect: +20% hunger
Sell Price: $40
XP: 5
```

**Grilled Rabbit**
```yaml
Input: 2× Rabbit Meat (raw)
Output: 1× Grilled Rabbit
Time: 8 seconds
Effect: +15% hunger, +5% health
Sell Price: $35
XP: 5
```

**Boar Steak**
```yaml
Input: 1× Boar Meat (raw)
Output: 1× Boar Steak
Time: 15 seconds
Effect: +30% hunger, +10% health
Sell Price: $60
XP: 10
```

#### Advanced Recipes

**Hunter's Stew**
```yaml
Input:
  - 1× Deer Meat
  - 1× Rabbit Meat
  - 1× Vegetable
Output: 1× Hunter's Stew
Time: 20 seconds
Effect: +50% hunger, +20% health, +10% armor
Sell Price: $100
XP: 15
```

**Smoked Meat**
```yaml
Input: 2× Any Raw Meat
Output: 3× Smoked Meat
Time: 25 seconds
Effect: +25% hunger (lasts longer)
Sell Price: $50 each
XP: 20
Note: Requires salt item
```

**Camp Breakfast**
```yaml
Input:
  - 2× Cooked Meat
  - 1× Egg
  - 1× Bread
Output: 1× Camp Breakfast
Time: 18 seconds
Effect: +60% hunger, Full health restore
Sell Price: $120
XP: 25
Note: Best meal option
```

### Cooking Tips

📝 **Efficiency:**
- Cook in batches during downtime
- Cooked meat sells for more than raw
- Some recipes yield multiple portions
- Save advanced recipes for personal use

📝 **XP Optimization:**
- Cooking grants small XP rewards
- Advanced recipes give more XP
- Level up cooking for bonus effects
- Combine with hunting XP for faster progression

📝 **Economic Strategy:**
- Raw meat → Sell immediately for quick cash
- Cooked meat → Better price, takes time
- Advanced recipes → Best for personal use
- Save rare ingredients for valuable recipes

## Advanced Camping Features

### Camp Storage

Deploy storage boxes at your camp to safely store items.

**Storage Features:**
- 50-slot capacity (configurable)
- Shared with gang/org (optional)
- Persists until picked up
- Weight limit: 200kg

**Usage:**
1. Place storage box near tent
2. Interact to open storage UI
3. Transfer items like inventory
4. Secure from other players (if enabled)

**Security Settings:**
- Personal: Only you access
- Gang: Gang members access
- Public: Anyone can access (risky!)

### Sleeping & Rest

Use your tent or sleeping bag to rest.

**Rest Benefits:**
- Restore health to 100%
- Restore armor to 100%
- Save respawn point (optional)
- Pass time (skip to morning/evening)

**Rest Options:**

**Quick Rest** (1 minute)
- Heal health/armor
- No time skip
- Can be interrupted

**Full Rest** (5 minutes)
- Full restoration
- Time skip available
- Sets spawn point
- Cannot be interrupted

### Camp Defense

Protect your camp from other players (if PVP enabled).

**Defense Mechanics:**
- Camp zones can be marked PVP-free (config)
- Lock storage to prevent theft
- Proximity alerts when players approach
- Can add camp guards (NPC, config option)

## Camp Management

### Packing Up Camp

When leaving your hunting area:

1. **Pack Storage First**
   - Remove all items
   - Pack up storage box
   - Receive item back

2. **Extinguish Fire**
   - Manually put out campfire
   - Or wait for it to burn out
   - Can't pack up while lit (safety)

3. **Pack Tent Last**
   - Interact with tent
   - Select "Pack Up"
   - Animation plays
   - Tent returned to inventory

⚠️ **Important**: Items left in storage when packing will be lost!

### Multiple Camps

**Server Limits:**
- Maximum 1 active camp per player (default)
- Placing new camp removes old one
- Gang camps may have different limits
- Admin/VIP may have increased limits

**Camp Sharing:**
- Invite friends to camp
- Share cooking access
- Collaborative storage (optional)
- Split camping costs

## Cooking Skill System

As you cook more, you improve your cooking skill.

### Cooking Levels

**Level 1-5: Novice Cook**
- Basic recipes available
- Standard cooking times
- Normal food effects

**Level 6-10: Camp Chef**
- Unlock advanced recipes
- -10% cooking time
- +10% food effect duration

**Level 11-15: Master Chef**
- Unlock all recipes
- -25% cooking time
- +25% food effects
- Chance of bonus food

**Level 16+: Legendary Cook**
- Exclusive recipes
- -50% cooking time
- Double food effects
- Always get bonus portions

### Skill Benefits

| Skill Level | Cooking Time | Effect Boost | Bonus Chance |
|-------------|--------------|--------------|--------------|
| 1-5 | Normal | 0% | 0% |
| 6-10 | -10% | +10% | 5% |
| 11-15 | -25% | +25% | 10% |
| 16-20 | -50% | +50% | 25% |

## Practical Camping Scenarios

### Extended Hunting Trip

**Setup:**
1. Travel to remote hunting zone
2. Deploy tent and campfire
3. Place storage box
4. Begin hunting

**During Hunt:**
- Return to camp to store pelts
- Cook meat as inventory fills
- Rest when health is low
- Use camp as base of operations

**End of Trip:**
- Pack up all equipment
- Return to town with full inventory
- Sell cooked goods for profit

### Group Hunting Camp

**Setup:**
1. Leader places camp
2. Share access with group
3. Everyone contributes supplies
4. Coordinate hunting routes

**Benefits:**
- Shared storage reduces trips
- Group cooking sessions
- Social gathering point
- Split costs and rewards

### Survival Challenge

Test your wilderness survival skills:

**Rules:**
- Set up camp in remote area
- Survive only on hunting/cooking
- No fast travel
- No shop visits for X days
- Track supplies carefully

## Troubleshooting Camping

### Common Issues

**Can't Place Tent**
- Check terrain (must be flat)
- Move away from objects
- Not on roads or inside buildings
- Not too close to other camps

**Campfire Won't Light**
- Need campfire kit in inventory
- Must be on flat ground
- Can't place indoors
- Check for rain (if weather affects fires)

**Cooking Menu Won't Open**
- Fire must be lit and active
- Stand closer to fire
- Check if fire timer expired
- Make sure you have ingredients

**Lost Camp Items**
- Camps despawn on server restart (config)
- Items in storage may be lost
- Always pack up before logging out
- Check server rules on camp persistence

## Camping Tips & Tricks

💡 **Location Scouting**
- Scout camp spots during daytime
- Mark locations on map
- Remember good spots for future trips
- Share spots with hunting group

💡 **Resource Management**
- Bring extra campfire kits
- Stock up on salt for advanced recipes
- Keep backup knife in camp storage
- Always have emergency food

💡 **Time Optimization**
- Cook while friends hunt
- Set up camp near multiple zones
- Use rest feature to skip unproductive times
- Plan cooking batches during quiet periods

💡 **Safety First**
- Never leave valuables in camp on PVP servers
- Pack up before AFKing
- Watch for griefers near your camp
- Use gang camps for better security

## Next Steps

- 🪤 Learn [Trapping & Baiting](trapping-baiting.md) techniques
- 🎯 Complete [Quests](quest-system.md) for rewards
- 🏆 Compete in [Tournaments](tournaments.md)
- 📖 Master [Hunting Basics](hunting-basics.md)
