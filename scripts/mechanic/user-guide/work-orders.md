# Work Orders

Complete guide to creating, managing, and completing customer work orders.

**📹 Video Tutorial**: *A 5-minute video showing the complete work order workflow from creation to completion would be very helpful here.*

## Overview

Work orders are the core of the mechanic system. They track customer repairs from initial request through completion and payment.

**A work order includes:**
- Customer information
- Vehicle details
- Services to be performed
- Parts needed
- Labor and parts costs
- Status tracking
- Work history and notes

## Creating a Work Order

### Prerequisites

- Minimum rank 1 (Mechanic) required
- Access to mechanic tablet
- Customer vehicle information

### Step-by-Step Creation

#### Step 1: Gather Vehicle Information

Before creating the order, collect:
- **Vehicle plate number** (required)
- **Customer name** (required)
- **Vehicle model** (auto-detected if near vehicle)
- **Description of issue/service needed**

**Tip**: Have the customer nearby or note their details before starting.

#### Step 2: Open New Order Form

1. Open tablet → Mechanic app
2. Go to **Dashboard**
3. Click **"+ New Work Order"** button
4. Order creation form opens

#### Step 3: Enter Basic Information

Fill in the required fields:

**Vehicle Information:**
```
Plate Number: [ABC123]
Vehicle Model: [Auto-detected or manual entry]
```

**Customer Information:**
```
Customer Name: [John Doe]
Customer Phone: [Optional - if tracking enabled]
```

**Service Description:**
```
Description: [Oil change and brake inspection]
Notes: [Customer reports squeaking from front brakes]
```

**Tips:**
- Plate must be valid (vehicle must exist on server)
- Model auto-fills if you're near the vehicle
- Be specific in description for team communication

#### Step 4: Add Services

Click **"Add Service"** button to add work items:

**Service entry fields:**
- **Service name**: "Oil Change", "Brake Repair", "Tune-Up", etc.
- **Labor cost**: Your labor charge for this service
- **Estimated time**: How long it will take (optional)

**Example services:**
```
1. Oil Change - $150 - 15 min
2. Brake Pad Replacement - $300 - 30 min
3. Brake Fluid Flush - $100 - 15 min
```

**Add multiple services:**
- Click "Add Service" for each item
- Each service tracked separately
- Total auto-calculates

#### Step 5: Add Parts

Select parts needed from inventory:

1. Click **"Add Parts"** button
2. Search or browse parts catalog
3. Select item and quantity
4. Part added to order

**Parts list shows:**
- Part name and image
- Quantity needed
- Unit price
- Total cost
- Availability (in stock / out of stock)

**Out of stock?**
- Order shows warning
- Can create order anyway
- Status auto-updates to "Waiting Parts" when parts ordered

#### Step 6: Review & Set Pricing

Review order summary before creating:

**Cost breakdown:**
```
Labor Cost:    $550.00
Parts Cost:    $275.00
─────────────────────
Total Cost:    $825.00
```

**Pricing options:**
- **Auto-calculate** - System calculates based on config
- **Manual override** - Enter custom total
- **Discount** - Apply percentage or flat discount

**Pricing tips:**
- Check shop pricing guidelines
- Consider customer relationship
- Apply discounts for regulars
- Manager approval may be required for high values

#### Step 7: Assign Mechanic (Optional)

If you're a manager (rank 2+), you can assign the order:

- **Assign to me** - You'll do the work
- **Assign to other** - Select from employee list
- **Leave unassigned** - Anyone can claim it

**Assignment benefits:**
- Clarity on who's responsible
- Performance tracking
- Commission tracking (if enabled)

#### Step 8: Create Work Order

1. Review all information
2. Click **"Create Work Order"** button
3. Confirmation message appears
4. Order appears in order list
5. Customer notified (if notifications enabled)

**Success!** Your work order is now active.

## Managing Active Orders

### Viewing Orders

**Access order list:**
1. Tablet → Mechanic app → **Orders** tab
2. View all shop orders or filter

**Filter options:**
- **All Orders** - Every order in shop
- **My Orders** - Assigned to you
- **Pending** - Not started
- **In Progress** - Currently working
- **Waiting Parts** - Parts on order
- **Completed** - Finished
- **Cancelled** - Void orders

### Order Statuses

Work orders progress through statuses:

| Status | Icon | Meaning | Next Action |
|--------|------|---------|-------------|
| Pending | 🟡 | Awaiting start | Claim and start work |
| In Progress | 🟢 | Being worked on | Continue work, update notes |
| Waiting Parts | 🔴 | Parts not available | Wait for delivery |
| Completed | ✅ | Work finished | Bill customer, archive |
| Cancelled | ❌ | Order void | Archive only |

### Claiming an Order

If order is unassigned:

1. Open order details
2. Click **"Claim Order"** button
3. Order assigned to you
4. Status changes to "In Progress"
5. Start working

### Updating Order Status

As work progresses, update status:

1. Open order details
2. Click **"Update Status"** dropdown
3. Select new status:
   - Start Work (Pending → In Progress)
   - Need Parts (→ Waiting Parts)
   - Resume (Waiting Parts → In Progress)
   - Complete (In Progress → Completed)
   - Cancel (→ Cancelled)
4. Confirm status change

**Status rules:**
- Can only move forward (mostly)
- Some transitions require permissions
- Completed orders can't be reopened (usually)

### Adding Notes

Keep team informed with order notes:

1. Open order details
2. Scroll to **Notes** section
3. Click **"Add Note"** button
4. Type your note:
   ```
   "Front brake pads 60% worn, recommend replacement within 5k miles"
   "Customer approved additional work - documented in note"
   "Test drive completed - no issues found"
   ```
5. Click "Save"

**Notes best practices:**
- Document all findings
- Record customer approvals
- Note any deviations from plan
- Time-stamp important events

### Adding/Removing Parts

Modify parts during work:

**Add more parts:**
1. Order details → Parts section
2. Click "Add Parts"
3. Select items
4. Confirm - price updates

**Remove parts:**
1. Find part in list
2. Click "Remove" icon
3. Confirm removal
4. Inventory returned (if applicable)

**Note**: Some servers restrict part changes after customer approval.

### Assigning to Another Mechanic

If you're rank 2+ (Senior Mechanic):

1. Open order details
2. Click **"Assign To"** button
3. Select mechanic from list
4. Confirm assignment
5. Selected mechanic receives notification

**Why reassign?**
- Workload balancing
- Specialist needed
- Employee unavailable

## Completing a Work Order

### Pre-Completion Checklist

Before marking complete, verify:

- [ ] All services performed
- [ ] All parts used/installed
- [ ] Quality check completed
- [ ] Customer notified and approved
- [ ] Test drive done (if applicable)
- [ ] All notes documented
- [ ] Photos uploaded (if required)

### Completion Steps

1. Open work order details
2. Review final costs (should match estimate)
3. Click **"Complete Work Order"** button
4. Confirmation dialog appears:
   ```
   Complete this work order?

   Total: $825.00
   Customer will be charged

   [Cancel] [Complete]
   ```
5. Click **"Complete"**

### What Happens on Completion

**Automatic processes:**
1. ✅ Order status → Completed
2. 💰 Customer charged (if automatic billing)
3. 📦 Parts deducted from inventory
4. 💵 Payment distributed (shop account / commission)
5. 📊 Statistics updated
6. 🕐 Completion timestamp recorded

**Manual processes (if configured):**
- Customer must approve payment
- Admin must verify completion
- Quality control review

### Payment Processing

Depending on server configuration:

**Option 1: Automatic**
- Customer charged immediately
- Money goes to shop account
- Employee receives commission (if configured)

**Option 2: Customer Approval**
- Customer receives payment request
- Can approve or dispute
- Payment processes after approval

**Option 3: Manager Approval**
- Manager reviews completed work
- Approves payment
- Then customer charged

**Commission split example:**
```
Total: $825.00
Shop Account: $577.50 (70%)
Employee Commission: $247.50 (30%)
```

## Work Order History

### Viewing Completed Orders

1. Orders tab → **Completed** filter
2. View all finished jobs
3. Click order to see details

**History includes:**
- All original order information
- Final costs
- Completion timestamp
- Who completed it
- All notes and updates

### Searching History

Search past orders by:
- **Vehicle plate**
- **Customer name**
- **Date range**
- **Mechanic who completed**
- **Services performed**

**Use cases:**
- Check vehicle service history
- Verify warranty work
- Review mechanic performance
- Customer dispute resolution

## Advanced Features

### Order Templates

Save common services as templates (if enabled):

**Create template:**
1. Set up order with common services/parts
2. Click "Save as Template"
3. Name template (e.g., "Basic Oil Change Package")
4. Template saved

**Use template:**
1. New order → "Load Template"
2. Select saved template
3. Services and parts auto-populate
4. Adjust as needed

**Popular templates:**
- Basic oil change
- Full brake service
- Standard tune-up
- Pre-purchase inspection

### Recurring Orders

Schedule regular maintenance (if enabled):

1. Create work order
2. Enable "Recurring" option
3. Set interval (every 2 weeks, monthly, etc.)
4. Order auto-creates at interval

**Good for:**
- Fleet vehicles
- Regular customers
- Preventive maintenance contracts

### Work Order Attachments

Attach photos or documents (if enabled):

1. Open order details
2. Click "Attach File"
3. Take photo or select file
4. File uploaded to order
5. Visible to all with access

**Attachment types:**
- Before/after photos
- Diagnostic reports
- Customer approval signatures
- Receipts

## Best Practices

### Creating Orders

✅ **Do:**
- Be specific in descriptions
- Verify vehicle plate before creating
- Itemize all services separately
- Add notes as you work
- Update status promptly

❌ **Don't:**
- Create vague orders ("fix car")
- Skip required fields
- Forget to add parts
- Leave status stale
- Complete without verification

### Managing Orders

✅ **Do:**
- Check orders regularly
- Claim orders you can complete
- Communicate with team via notes
- Document everything
- Test after repairs

❌ **Don't:**
- Claim more than you can handle
- Change prices without approval
- Skip quality checks
- Rush completions
- Forget customer updates

### Customer Service

✅ **Do:**
- Keep customers informed
- Provide accurate estimates
- Explain all charges
- Offer recommendations
- Follow up after service

❌ **Don't:**
- Add work without approval
- Surprise customers with costs
- Skip explanations
- Ignore complaints
- Forget courtesy checks

## Common Issues

### Can't create work order

**Problem**: "Permission denied" error

**Solutions:**
- Check your job rank (need rank 1+)
- Verify you're assigned to shop
- Check shop is active
- Contact manager

### Order not showing for others

**Problem**: Created order but team can't see it

**Solutions:**
- Verify order saved (check order list)
- Ask them to refresh tablet
- Check they're viewing same shop
- Verify network connection

### Can't complete order

**Problem**: Complete button grayed out

**Solutions:**
- Check order status (must be "In Progress")
- Verify you have permissions
- Ensure all required fields filled
- Check parts availability

### Customer not charged

**Problem**: Completed order but no payment

**Solutions:**
- Check server billing configuration
- Verify customer has funds
- Check payment mode settings
- Contact server admin

## Next Steps

Now that you understand work orders:

- Learn **[Vehicle Tuning](vehicle-tuning.md)** to perform modifications
- Understand **[Parts Management](parts-management.md)** for inventory
- Explore **[Shop Management](shop-management.md)** if you're a boss

---

**Need help?** Check [Troubleshooting](../troubleshooting.md) or ask your shop manager.
