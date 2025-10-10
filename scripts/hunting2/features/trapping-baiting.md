---
icon: box-taped
---

# Trapping & Baiting

Master passive hunting techniques with traps and bait to catch animals efficiently while you focus on other activities.

## Baiting System

Bait attracts animals to specific locations, making hunting easier and more strategic.

### How Bait Works

**Mechanics:**
1. Place bait in desired location
2. Bait creates attraction radius (50m default)
3. Animals within zone are drawn to bait
4. Bait lasts for configurable duration (15 minutes default)
5. One animal consumes bait on arrival

**Attraction Rules:**
- Only works in hunting zones
- Attracts animal types from that zone
- Multiple baits can be active
- Consumed by first animal to reach it
- Increases spawn chance nearby

### Types of Bait

#### Standard Bait

**Animal Bait (Basic)**
```yaml
Price: $50
Duration: 15 minutes
Attraction Radius: 50m
Attracted Animals: Common (Rabbit, Deer, Coyote)
Success Rate: 60%
```

**How to Use:**
1. Purchase from hunting shop
2. Open inventory
3. Use "Animal Bait" item
4. Place on ground
5. Move away and wait

**Tips:**
- Place in open areas
- Multiple bait = more animals
- Use near your hunting position
- Combine with traps for efficiency

#### Premium Bait

**Predator Bait**
```yaml
Price: $150
Duration: 20 minutes
Attraction Radius: 75m
Attracted Animals: Predators (Coyote, Mountain Lion, Bear)
Success Rate: 75%
```

**Special Bait**
```yaml
Price: $250
Duration: 30 minutes
Attraction Radius: 100m
Attracted Animals: All animals in zone
Success Rate: 80%
Bonus: Higher quality animals
```

**Legendary Bait**
```yaml
Price: $500 (Quest Reward Only)
Duration: 45 minutes
Attraction Radius: 150m
Attracted Animals: Legendary/Rare spawns
Success Rate: 90%
Bonus: Guaranteed high-star quality
```

### Bait Placement Strategy

**Optimal Placement:**

**Open Field Method**
```
You (Hidden) ← 50m → Bait (Open Area)
```
- Place bait in clearing
- Position yourself in cover
- Animals come to bait
- Easy shots

**Trap Combo Method**
```
Trap ← 5m → Bait ← 30m → You
```
- Bait near trap
- Animals trigger trap while approaching
- Guaranteed catch

**Multi-Bait Setup**
```
        Bait
       /    \
   Bait  You  Bait
       \    /
        Bait
```
- Surround position with bait
- Animals come from all directions
- Maximum efficiency
- Great for group hunting

### Bait Management

**Active Bait Tracking:**
- Check map for bait markers
- Notification when bait is consumed
- Countdown timer on bait items
- Limited active baits per player (5 default)

**Economy Tips:**
💰 Bait vs Direct Hunting
- Bait cost: $50
- Average hunt profit: $200
- Break-even: 1 successful hunt
- ROI: Use bait for rare animals

## Trapping System

Set up traps to catch animals passively while you hunt or do other activities.

### Trap Mechanics

**How Traps Work:**
1. Deploy trap in hunting zone
2. Trap becomes active after 30 seconds
3. Animals passing by have chance to trigger
4. Return later to check trap
5. Collect caught animal (if any)

**Trap Statistics:**
- Max traps per player: 5 (default)
- Check interval: 5 minutes minimum
- Trap duration: 1 hour before despawn
- Success chance: 30% (60% with bait)

### Setting Up Traps

**Step-by-Step:**

1. **Purchase Traps**
   - Buy from hunting shop ($250 each)
   - Carry in inventory
   - Weight: 500 per trap

2. **Choose Location**
   - Must be in hunting zone
   - Flat ground preferred
   - Near animal paths
   - Away from roads

3. **Deploy Trap**
   - Use trap from inventory
   - Position with ghost preview
   - Confirm placement
   - Deployment animation plays

4. **Activate Trap**
   - Automatically activates after 30s
   - Notification confirms activation
   - Marker added to map

5. **Check Trap Later**
   - Return after minimum time (5 min)
   - Interact with trap
   - Collect animal if caught
   - Trap is consumed

### Trap Types

#### Basic Animal Trap

**Standard Trap**
```yaml
Cost: $250
Catch Rate: 30% base (60% with bait)
Suitable For: Small to medium animals
Catch: Rabbit, Fox, Raccoon, Coyote
Durability: Single use
```

**How to Use:**
- Best for small game
- Pair with bait
- Check every 5-10 minutes
- Place multiple traps

#### Large Game Trap

**Bear Trap**
```yaml
Cost: $500
Catch Rate: 40% base (70% with bait)
Suitable For: Large animals
Catch: Boar, Deer, Bear (if enabled)
Durability: Single use
Damage: Reduces quality by 1 star
```

**Warning:**
⚠️ Caught animals are wounded
⚠️ Quality reduced (use for quests, not pelts)
⚠️ Must finish animal with weapon
⚠️ More expensive than standard traps

#### Cage Trap

**Live Cage Trap**
```yaml
Cost: $400
Catch Rate: 50% base (80% with bait)
Suitable For: Small animals alive
Catch: Rabbit, Raccoon, Fox (alive)
Durability: Reusable (3 uses)
Quality: No quality reduction
```

**Benefits:**
✅ Catch animals alive
✅ Full quality preservation
✅ Reusable trap
✅ Better for quest completion
✅ Can sell live animals for more

**Downsides:**
❌ Only small animals
❌ Higher initial cost
❌ Must have cage space in vehicle

### Trapping Strategy

#### Passive Income Setup

**Morning Routine:**
1. Deploy 5 traps in different zones
2. Add bait to each trap
3. Mark locations on GPS
4. Continue hunting normally
5. Check traps every 10 minutes

**Expected Returns:**
- Trap + Bait Cost: $300 × 5 = $1,500
- Expected Catches: 3-4 (60% success rate)
- Average Value per Catch: $150
- Total Return: $450-600
- Profit: ~$0-100 + hunting XP

**Time Efficiency:**
- Active hunting: ~$200/hour
- Trap checking: +$50/hour passive
- Combined: $250/hour
- Best for extended sessions

#### Quest Focused Trapping

When completing quests requiring specific animals:

**Quest**: Hunt 10 Rabbits

**Efficient Method:**
1. Place 5 traps in rabbit zone
2. Add bait to all traps
3. Actively hunt while waiting
4. Check traps every 5 minutes
5. Quest completes faster

**Time Saved:**
- Active only: 30-45 minutes
- With traps: 15-25 minutes
- 40% time reduction

#### Zone Coverage

**Multi-Zone Strategy:**

```
Zone A (Rabbits)
  └─ 2 Traps

Zone B (Deer)
  └─ 2 Traps

Zone C (Boar)
  └─ 1 Trap

Your Position: Zone B (Active Hunting)
```

**Benefits:**
- Diverse animal catches
- Quest flexibility
- Rare spawn opportunities
- Maximizes trap value

### Trap Management

#### Tracking Your Traps

**Map Markers:**
- Trap icon on map
- Timer shows time since placed
- Color coding:
  - 🟢 Green: Ready to check (5+ min)
  - 🟡 Yellow: Too soon (< 5 min)
  - 🔴 Red: About to despawn (< 10 min left)

**Trap Log:**
- Open hunting menu (F7)
- View "Active Traps" tab
- Shows all trap locations
- Time since deployment
- Bait status

#### Collecting Catches

When a trap catches an animal:

1. **Notification Received**
   - "Your trap caught something!"
   - Map marker updates
   - GPS waypoint auto-sets (optional)

2. **Travel to Trap**
   - Follow map marker
   - Trap will be visible with animal

3. **Collect Animal**
   - Interact with trap
   - Choose action:
     - Harvest animal (instant loot)
     - Release animal (get trap back)
     - Take alive (if cage trap)

4. **Trap Disposal**
   - Standard traps consumed
   - Cage traps reusable
   - Can pick up empty traps early

### Bait + Trap Combinations

Maximize efficiency by combining bait and traps.

#### The Perfect Setup

**Placement:**
```
  [You]
    |
   50m
    |
  (Bait)
    |
   2m
    |
  [Trap]
```

**Why This Works:**
1. Bait attracts animals
2. Animals walk toward bait
3. Trigger trap on approach
4. You're nearby for backup hunting
5. Maximum catch rate

#### Advanced Patterns

**The Gauntlet**
```
Trap → Bait → Trap → Bait → Trap
         (Your Position)
```
- Multiple catch opportunities
- Animals walk through trap line
- High success rate
- Good for small game

**The Ambush Circle**
```
      Trap
     /    \
  Bait    Trap
    |      |
  Trap-[You]-Bait
    |      |
  Bait    Trap
     \    /
      Trap
```
- 6 traps, 3 baits
- Surround yourself
- Passive + active hunting
- Group hunting friendly

### Trapping Tips & Tricks

💡 **Placement Wisdom**
- Near water sources (animals drink)
- Along animal paths (look for tracks)
- Edge of forest clearings
- Between rocks (natural funnels)

💡 **Time Optimization**
- Place traps before hunting
- Check during loot runs
- Set before logging off (if persistent)
- Morning placement = evening collection

💡 **Economic Efficiency**
- Use standard traps for common animals
- Save cage traps for quest animals
- Bait only when needed
- Calculate ROI per trap type

💡 **Quest Synergy**
- Check daily quests first
- Place traps for quest animals
- Passive quest completion
- Double dip: hunt + trap XP

### Bait & Trap Economy

#### Cost-Benefit Analysis

**Scenario 1: Pure Hunting**
- Time: 1 hour
- Cost: $0 (ammo minimal)
- Kills: 15 animals
- Profit: $3,000
- Hourly Rate: $3,000/hr

**Scenario 2: Hunting + Traps**
- Time: 1 hour
- Trap Cost: $1,500 (5 traps + bait)
- Active Kills: 12 animals
- Trapped: 3 animals
- Total: 15 animals
- Profit: $3,300 - $1,500 = $1,800
- Hourly Rate: $1,800/hr

**BUT:**
- Trapped animals = passive
- More time for other activities
- Quest completion bonus
- Less active effort required

**Scenario 3: Trap Farming**
- Initial Setup: 15 minutes (place 5 traps)
- AFK/Other Activities: 45 minutes
- Check Traps: 10 minutes
- Total Active Time: 25 minutes
- Profit: $600-900
- Effective Rate: $1,440-2,160/hr
- Best for multitasking

### Troubleshooting

**Trap Won't Place**
- Not in hunting zone
- Too close to objects
- Terrain too steep
- Already at trap limit

**Trap Not Catching**
- Check bait is active
- Wrong trap for animal size
- Too close to roads
- Low zone spawn rate
- Need more patience (RNG)

**Can't Find Trap**
- Check map for markers
- Use GPS waypoint feature
- May have despawned (1hr limit)
- Server restart removed it

**Bait Not Attracting**
- Animals already nearby (move away)
- Wrong time of day
- Zone at spawn limit
- Need to wait longer

## Advanced Techniques

### The Trap Line

Professional trappers use trap lines:

**Setup:**
1. Place traps along a route
2. Space 100m apart
3. Add bait to each
4. Walk the line every 10 minutes
5. Active hunt between checks

**Efficiency:**
- Passive + active income
- Consistent catches
- Good for grinding levels
- Requires map knowledge

### Rare Animal Trapping

Use premium bait + cage traps for rare animals:

**Strategy:**
1. Research rare spawn zones
2. Deploy cage traps with legendary bait
3. Check every 5 minutes (rare spawns don't last)
4. Capture for quests or selling
5. Premium rewards

**Cost:**
- Cage Trap: $400
- Legendary Bait: $500 (quest reward)
- Total: $900
- Rare Animal Value: $2,000+
- Profit: $1,100+

## Next Steps

- 🎯 Use traps for [Quest System](quest-system.md) completion
- 🏆 Trap rare animals for [Tournaments](tournaments.md)
- 🔥 Combine with [Camping](camping-cooking.md) for efficiency
- 📈 Level up through [Progression](progression.md) system
