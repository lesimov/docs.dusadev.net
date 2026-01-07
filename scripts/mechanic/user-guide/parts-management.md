# Parts Management

Guide to managing mechanic shop parts inventory and ordering system.

## Overview

The parts management system helps you:
- Track current inventory levels
- Order new parts from suppliers
- Monitor part usage
- Set minimum stock alerts
- Manage shop inventory efficiently

**Access required**: All mechanics can view inventory. Rank 3+ (Manager) required to order parts.

## Parts Catalog

### Part Categories

Parts are organized into categories:

**Engine Parts:**
- Engine oil
- Oil filters
- Air filters
- Spark plugs
- Belts and hoses
- Gaskets and seals

**Transmission Parts:**
- Transmission fluid
- Transmission filters
- Clutch kits
- Transmission mounts

**Brake Components:**
- Brake pads (front/rear)
- Brake rotors (front/rear)
- Brake fluid
- Brake lines
- Calipers

**Suspension Parts:**
- Shock absorbers
- Struts
- Springs
- Control arms
- Bushings

**Electrical Components:**
- Batteries
- Alternators
- Starters
- Wiring kits
- Fuses

**Body Panels:**
- Bumpers
- Fenders
- Hoods
- Doors
- Trunk lids

**Fluids & Consumables:**
- Engine oil (various weights)
- Coolant
- Brake fluid
- Power steering fluid
- Windshield washer fluid
- Shop rags
- Cleaning supplies

**Tools:**
- Diagnostic tools
- Repair kits
- Specialty tools

### Part Information

Each part has:
- **Name**: Part description
- **Item Code**: Internal inventory code
- **Category**: Part type
- **Unit Price**: Cost per unit
- **Current Stock**: Quantity on hand
- **Min Stock**: Minimum quantity before alert
- **Supplier**: Where it's ordered from (if multiple suppliers)

## Checking Stock Levels

### Via Tablet

1. Open tablet → Mechanic app
2. Navigate to **Parts** tab
3. Parts inventory displays

**Inventory view shows:**
```
┌─────────────────────────────────────┐
│  Parts Inventory                    │
│                                     │
│  [All] [Low Stock] [Categories ▼]  │
│                                     │
│  🔧 Engine Oil 5W-30                │
│  Stock: 24 units   Min: 10          │
│  Price: $15.00                      │
│  ───────────────────────────────    │
│  ⚠️ Brake Pads (Front)              │
│  Stock: 3 units    Min: 5   [ORDER]│
│  Price: $45.00                      │
│  ───────────────────────────────    │
│  ...                                │
└─────────────────────────────────────┘
```

### Filter Options

**Filter by status:**
- **All Parts**: Every item in catalog
- **In Stock**: Items with stock > 0
- **Low Stock**: Items below minimum
- **Out of Stock**: Items with 0 quantity

**Filter by category:**
- Select category from dropdown
- View only parts in that category
- Useful for focused inventory checks

**Search:**
- Type part name or code
- Results filter in real-time
- Finds partial matches

### Low Stock Alerts

Parts below minimum stock show:
- ⚠️ Warning icon
- Red highlight
- "Order Now" button (if manager+)

**Automatic notifications:**
- Daily summary of low stock items
- Immediate alert when critical (0 stock)
- Can configure alert thresholds per part

**Why low stock matters:**
- Can't complete work orders without parts
- Work orders auto-pause if parts unavailable
- Customer delays = unhappy customers

## Ordering Parts

### Prerequisites

- **Rank 3+ (Manager)** required
- **Shop funds** must be sufficient
- **Parts supplier** must be available

### Placing an Order

**Method 1: From Parts Inventory**

1. Parts tab → Find item needing restock
2. Click item or **"Order"** button
3. Order dialog opens:
   ```
   ┌──────────────────────────┐
   │  Order: Engine Oil 5W-30 │
   │                          │
   │  Current: 8 units        │
   │  Minimum: 10 units       │
   │                          │
   │  Quantity: [20] units    │
   │  Unit Price: $15.00      │
   │  Total: $300.00          │
   │                          │
   │  Delivery: 5-10 minutes  │
   │                          │
   │  [Cancel] [Place Order]  │
   └──────────────────────────┘
   ```
4. Enter quantity to order
5. Review total cost
6. Click **"Place Order"**
7. Order submitted

**Method 2: Bulk Ordering**

1. Parts tab → **"Bulk Order"** button (if enabled)
2. Select multiple items
3. Set quantities for each
4. Review total
5. Place order

**Method 3: Auto-Restock**

If configured:
- Parts auto-order when below minimum
- Orders quantity to reach maximum stock
- Runs daily or on-demand
- Manager approval may be required

### Order Confirmation

After placing order:

```
✅ Order Placed Successfully!

Items: 5
Total Cost: $1,250.00
Delivery: 5-10 minutes

Order #: 12345
```

**What happens next:**
1. Money deducted from shop account
2. Order enters "Processing" status
3. Delivery countdown starts
4. Parts arrive after delivery time
5. Inventory auto-updates
6. Notification sent

### Delivery Times

Typical delivery times (configurable):

```
Standard Parts:    5-10 minutes
Special Order:     15-30 minutes
Performance Parts: 30-60 minutes
Import Parts:      1-2 hours (real-time)
```

**Delivery notifications:**
- On-screen notification
- Tablet notification
- Can check order status in Parts → Orders

### Order History

View past orders:

1. Parts tab → **"Order History"**
2. List of all orders with:
   - Order date/time
   - Items ordered
   - Total cost
   - Delivery status
   - Who placed order

**Useful for:**
- Tracking spending
- Verifying deliveries
- Auditing inventory
- Finding order patterns

## Using Parts in Work Orders

### Automatic Deduction

When you add parts to a work order:

1. Part selected from inventory
2. Quantity specified
3. System checks availability
4. Part reserved for order
5. When order completed:
   - Parts deducted from stock
   - Cost added to order total
   - Inventory updated

**Stock checking:**
- Real-time availability check
- Can't add more than in stock
- Out of stock parts show warning

### Out of Stock Parts

If part needed but not available:

**Option 1: Order Part**
1. Work order shows "Part needed"
2. Click "Order Part" button
3. Part ordered immediately
4. Work order status → "Waiting Parts"
5. Auto-resumes when part arrives

**Option 2: Substitute Part**
1. Select alternative part (if available)
2. May need customer approval
3. Price adjusts accordingly

**Option 3: Pause Work**
1. Work order paused
2. Customer notified
3. Resume when part available

### Part Substitution

If exact part unavailable:

**Substitution rules:**
- Must be compatible
- Customer approval required for upgrades
- Price difference documented
- Noted in work order

**Example:**
```
Requested: Generic brake pads ($45)
Stock: Out of stock

Available substitute: Premium ceramic pads ($75)
Price difference: +$30

Customer approval: ✅ Yes / ❌ No
```

## Stock Management (Manager/Owner)

### Setting Stock Levels

Configure min/max stock for each part:

1. Parts tab → Click part
2. Part details page
3. Click **"Edit Stock Levels"**
4. Set values:
   ```
   Minimum Stock: [10]
   Maximum Stock: [50]
   Reorder Point: [15]
   Reorder Quantity: [30]
   ```
5. Save changes

**Stock level strategy:**

**Fast-moving items** (oil, filters):
- Higher minimum (20-30 units)
- Order frequently
- Never run out

**Slow-moving items** (specialty parts):
- Lower minimum (2-5 units)
- Order on-demand
- Don't over-stock

**Seasonal items**:
- Adjust seasonally
- Winter: antifreeze, batteries
- Summer: coolant, AC parts

### Bulk Ordering

Order multiple items at once:

1. Parts → **"Bulk Order"** tab
2. **"Add to Order"** for each item needed
3. Review cart:
   ```
   ┌──────────────────────────────┐
   │  Bulk Order Cart             │
   │                              │
   │  Engine Oil 5W-30    x20     │
   │  Brake Pads (Front)  x10     │
   │  Oil Filters         x15     │
   │                              │
   │  Subtotal:       $1,125.00   │
   │  Discount (5%):    -$56.25   │
   │  Total:          $1,068.75   │
   │                              │
   │  [Clear] [Place Order]       │
   └──────────────────────────────┘
   ```
4. Apply discounts if available
5. Place bulk order

**Bulk order benefits:**
- Volume discounts
- Single delivery
- Efficient restocking
- Reduced delivery fees (if applicable)

### Supplier Management

If multiple suppliers available:

**Supplier comparison:**
```
Part: Brake Pads (Front)

Supplier A:   $45.00   Delivery: 5 min
Supplier B:   $42.00   Delivery: 15 min
Supplier C:   $40.00   Delivery: 30 min
```

**Choose based on:**
- Price
- Delivery time
- Part quality
- Supplier reputation
- Bulk discounts

**Set preferred suppliers:**
1. Parts → Settings
2. Configure supplier preferences
3. Auto-orders use preferred supplier

### Inventory Audits

Perform regular inventory checks:

**Monthly audit checklist:**
- [ ] Physical count matches system
- [ ] Identify discrepancies
- [ ] Adjust inventory if needed
- [ ] Review usage patterns
- [ ] Identify obsolete stock
- [ ] Order popular items
- [ ] Clear old/unused parts

**Audit process:**
1. Parts → **"Inventory Audit"**
2. System generates count sheet
3. Physically count parts
4. Enter actual counts
5. System shows discrepancies
6. Adjust inventory
7. Report generated

**Discrepancy reasons:**
- Theft/loss
- Miscounted
- Unreported usage
- Data entry error
- Damaged/returned parts

### Price Management

Adjust part prices (owner only):

**Pricing strategies:**
- **Cost + Markup**: Supplier cost × 1.3 (30% markup)
- **Market Rate**: Match competitor pricing
- **Premium**: Higher price, better service
- **Loss Leader**: Low price to attract customers

**Setting prices:**
1. Parts → Part details
2. **"Edit Pricing"**
3. Set:
   - Purchase cost (from supplier)
   - Markup percentage
   - Retail price
4. Save

**Bulk price changes:**
- Category-wide adjustments
- Percentage increases
- Seasonal promotions

## Best Practices

### For All Mechanics

✅ **Do:**
- Check stock before creating work orders
- Report low stock to managers
- Use correct parts for jobs
- Document part usage
- Return unused parts to stock

❌ **Don't:**
- Use parts without documenting
- Hoard parts at workstation
- Waste consumables
- Ignore low stock warnings
- Substitute without approval

### For Managers

✅ **Do:**
- Monitor stock levels daily
- Order before running out
- Track usage patterns
- Set appropriate minimums
- Audit inventory monthly
- Compare supplier pricing
- Plan for seasonal demands

❌ **Don't:**
- Over-order slow movers
- Ignore stock alerts
- Skip audits
- Pay inflated prices
- Let stock expire/degrade

### Inventory Efficiency

**Organize stock:**
- Label storage areas
- Group by category
- FIFO (First In, First Out)
- Keep work areas stocked
- Secure valuable parts

**Track metrics:**
- Parts turnover rate
- Stock-out frequency
- Order costs
- Supplier performance
- Waste/loss rates

**Optimize ordering:**
- Weekly routine orders
- Monthly bulk orders
- Just-in-time for specialty items
- Buffer stock for emergencies

## Advanced Features

### Auto-Restock System

If enabled, automatically orders parts:

**Configuration:**
1. Parts → Settings → **"Auto-Restock"**
2. Enable auto-restock
3. Set rules:
   ```
   Trigger: When stock < minimum
   Order Quantity: Restore to maximum
   Frequency: Check daily at 6 AM
   Approval: Manager approval required ✓
   Budget Limit: $5,000 per day
   ```
4. Save settings

**Auto-restock runs:**
- Checks all parts
- Identifies items below minimum
- Calculates order quantities
- Submits orders (or pending approval)
- Sends summary notification

### Parts Analytics

View usage analytics (manager+):

**Dashboard shows:**
- Top 10 used parts this month
- Spending by category
- Order frequency
- Stock value
- Waste/loss tracking

**Reports available:**
- Monthly usage report
- Cost analysis
- Supplier performance
- Inventory valuation
- Turnover rates

**Use analytics to:**
- Optimize stock levels
- Identify cost savings
- Plan budgets
- Negotiate with suppliers
- Forecast demand

### Supplier Contracts

Negotiate contracts with suppliers (owner):

**Contract types:**
- **Volume Discount**: 10% off orders over $1,000
- **Exclusive Supplier**: Best prices, must order only from them
- **Credit Terms**: Pay Net-30 instead of upfront
- **Rush Delivery**: Priority delivery for extra fee

**Managing contracts:**
1. Parts → Suppliers → Contract Management
2. View active contracts
3. Negotiate new terms
4. Renew or cancel

## Troubleshooting

### Can't order parts

**Solutions:**
- Check you have rank 3+ (Manager)
- Verify shop has sufficient funds
- Ensure supplier is available (business hours?)
- Check for pending orders (max limit?)
- Contact owner for budget increase

### Parts not delivered

**Solutions:**
- Check order status (may still be processing)
- Verify delivery time hasn't elapsed
- Check for server issues
- Review order history to confirm it placed
- Contact admin if order lost

### Inventory count wrong

**Solutions:**
- Perform manual audit
- Check for unreported usage
- Review recent work orders
- Look for duplicate entries
- Adjust inventory manually

### Can't use part in work order

**Solutions:**
- Verify part is in stock
- Check part is not reserved
- Ensure part is compatible with service
- Refresh inventory list
- Check work order permissions

## Next Steps

Now that you understand parts management:

- Learn **[Shop Management](shop-management.md)** for complete boss features
- Review **[Work Orders](work-orders.md)** to understand part usage
- Check **[Item Catalog](../reference/item-catalog.md)** for complete part list

---

**Need help?** See [Troubleshooting](../troubleshooting.md) or contact your shop manager.
