# Tablet Basics

Learn how to use the mechanic tablet interface effectively.

**📹 Video Tutorial**: *A 3-minute video tutorial covering tablet navigation and common actions would be very helpful here.*

## Opening the Tablet

The mechanic tablet is your primary tool for managing all mechanic operations.

**To open the tablet:**
1. Open your inventory (default: Tab or I key)
2. Find the `mechanic_tablet` item
3. Click "Use" or right-click to use the item
4. The tablet interface will open full-screen

**Alternative methods** (if configured by server):
- Command: `/tablet` (if enabled)
- Keybind: Custom key (if configured)

**Closing the tablet:**
- Press **ESC** key
- Click the home button and select "Close"

## Tablet Interface Overview

The tablet has an iPad-style interface with multiple apps.

### Home Screen

When you first open the tablet, you'll see the **app list**:

```
┌─────────────────────────────────┐
│         DUSA Tablet             │
│                                 │
│   [📱] [🔧] [📊] [⚙️]          │
│   Phone  Mechanic  Stats  Settings │
│                                 │
│   [➕] [📧] [📋] [💰]          │
│   More apps...                  │
│                                 │
│                                 │
│         [🏠 Home]              │
└─────────────────────────────────┘
```

**Navigation elements:**
- **App Icons** - Tap to open an app
- **Home Button** - Return to app list (bottom center)
- **Status Bar** - Shows time, battery, signal (top)

### Mechanic App

The mechanic app is your main workspace. Click the **Mechanic (🔧)** app icon to open it.

**Mechanic app sections:**
```
┌─────────────────────────────────┐
│    ← Mechanic - Benny's        │
│                                 │
│  [Dashboard] [Orders] [Tuning]  │
│  [Parts] [Management]           │
│                                 │
│  • 5 Active Orders              │
│  • $12,450 Today                │
│  • 3 Pending                    │
│                                 │
│  [+ New Work Order]             │
│                                 │
└─────────────────────────────────┘
```

**Sections explained:**
- **Dashboard** - Overview of shop status, quick actions
- **Orders** - View and manage all work orders
- **Tuning** - Access vehicle tuning interface
- **Parts** - Inventory management
- **Management** - Boss menu (rank 3+ only)

## Dashboard

The dashboard is your control center.

### Dashboard Widgets

**Active Orders**
- Shows count of ongoing work orders
- Click to view order list
- Color-coded by status:
  - 🟢 Green = In Progress
  - 🟡 Yellow = Pending
  - 🔴 Red = Waiting Parts

**Today's Revenue**
- Shows money earned today
- Updates in real-time
- Click for detailed breakdown

**Quick Actions**
- **New Work Order** - Create customer job
- **Quick Tune** - Fast access to tuning
- **Parts Check** - View low-stock items

### Dashboard Features

**Shop Selector** (if you work at multiple shops)
1. Tap shop name at top of screen
2. Menu appears with all your shops
3. Select different shop
4. Dashboard updates to show that shop's data

**Notifications**
- New work orders assigned to you
- Parts delivered
- Shop messages
- Payment received

## Navigation Patterns

### Basic Navigation

**Opening a section:**
- Tap the section name in tab bar
- Example: Tap "Orders" to view work orders

**Going back:**
- Tap "←" (back arrow) in top-left
- Or press ESC to close tablet completely

**Scrolling:**
- Use mouse wheel to scroll long lists
- Or click and drag on scrollbar

### Common Gestures

**Tap** - Select item or open
**Double-tap** - Quick action (if enabled)
**Hold** - Show context menu (on some items)
**Swipe** - Navigate between tabs (touch screens)

## Work Orders Tab

Access all work orders for your shop.

**View options:**
- **All Orders** - Show everything
- **My Orders** - Orders assigned to you
- **Pending** - Awaiting start
- **In Progress** - Currently working
- **Completed** - Finished jobs

**Order list displays:**
- Vehicle plate and model
- Customer name
- Status indicator
- Total cost
- Created date

**Actions:**
- **Click order** - View details
- **Status button** - Update progress
- **Assign button** - Assign to mechanic (if manager+)

## Tuning Tab

Access vehicle modification interface.

**Requirements to use tuning:**
1. ✅ You must be in a vehicle
2. ✅ You must be the driver
3. ✅ Vehicle must be in tuning zone
4. ✅ You must have mechanic job

**When conditions are met:**
- Tuning tab becomes active (not grayed out)
- Click "Tuning" to open tuning interface
- Vehicle modification menu appears

**If tuning is disabled:**
- Check you're in tuning zone (usually the shop area)
- Ensure you're in driver seat, not passenger
- Verify you have mechanic job active

See [Vehicle Tuning](vehicle-tuning.md) for complete tuning guide.

## Parts Tab

View and manage parts inventory.

**Parts inventory shows:**
- Item name and image
- Current stock quantity
- Low stock warning (if below minimum)
- Unit price

**Actions available:**
- **View Details** - See item information
- **Order Parts** - Place order (if manager+)
- **Usage History** - See recent consumption

**Low stock alerts:**
- Items below minimum show 🔴 red warning
- Click item to order more
- Set alerts in Management section

## Management Tab

**Note**: Only visible to rank 3 (Manager) and rank 4 (Owner).

**Management sections:**
- **Employees** - Hire, fire, manage staff
- **Finances** - Shop balance, transactions, withdraw funds
- **Settings** - Shop configuration, pricing, permissions
- **Reports** - Performance metrics, statistics

See [Shop Management](shop-management.md) for detailed boss features.

## Switching Shops

If you work at multiple mechanic shops:

1. Open Mechanic app
2. Tap **shop name** at top of screen (e.g., "Benny's Motorworks")
3. Shop selector menu appears
4. Select different shop from list
5. Dashboard and all data updates to new shop

**Each shop has separate:**
- Work orders
- Inventory
- Employees
- Financial accounts

## Search & Filters

### Searching Orders

1. Open Orders tab
2. Use search box at top
3. Search by:
   - Vehicle plate
   - Customer name
   - Order number

### Filtering

Apply filters to narrow results:
- **Status** - Pending, In Progress, Completed, etc.
- **Date Range** - Today, This Week, This Month, Custom
- **Assigned To** - All, Me, Specific mechanic
- **Sort By** - Date, Price, Status, Vehicle

## Notifications

The tablet shows notifications for:
- ✉️ New work order created
- 👤 Order assigned to you
- 📦 Parts delivered
- 💰 Payment received
- ⚠️ Low stock alert
- 📢 Shop announcements

**Managing notifications:**
1. Click notification icon (if visible)
2. View recent notifications
3. Click to open related item
4. Mark as read or dismiss

## Tips & Tricks

### Efficiency Tips

**Keyboard Shortcuts** (if enabled):
- **ESC** - Close tablet
- **↑↓** - Navigate lists
- **Enter** - Select/Confirm
- **Backspace** - Go back

**Quick Actions:**
- Double-click order to open details
- Right-click for context menu (some items)
- Use search instead of scrolling

### Best Practices

**Keep tablet organized:**
- Complete old work orders
- Archive finished jobs
- Update order status promptly

**Stay informed:**
- Check notifications regularly
- Review dashboard daily
- Monitor parts inventory

**Communication:**
- Add notes to work orders
- Update status for team visibility
- Use shop announcements

### Common Shortcuts

| Action | How To |
|--------|--------|
| New work order | Dashboard → + button |
| Check all orders | Orders tab → All filter |
| My active jobs | Orders tab → My Orders |
| Quick tune | Dashboard → Quick Tune button |
| Low stock items | Parts tab → filter by low stock |
| Shop stats | Dashboard widgets |

## Troubleshooting

### Tablet won't open

**Solutions:**
1. Check you have mechanic_tablet item
2. Try using item again
3. Check F8 console for errors
4. Verify dusa_tablet resource is running
5. Relog to server

### Mechanic app missing

**Solutions:**
1. Verify you have mechanic job
2. Check dusa_mechanicv2 is running
3. Restart resources: `restart dusa_tablet` then `restart dusa_mechanicv2`
4. Contact server admin

### Blank/broken interface

**Solutions:**
1. Clear FiveM cache
2. Check F8 console for JavaScript errors
3. Try different graphics settings
4. Report to server admin with console errors

### Data not updating

**Solutions:**
1. Close and reopen tablet
2. Switch shops and switch back
3. Check internet connection
4. Verify server is responsive

## Next Steps

Now that you understand the tablet interface:

1. Learn to **[create work orders](work-orders.md)**
2. Master **[vehicle tuning](vehicle-tuning.md)**
3. Understand **[parts management](parts-management.md)**
4. Explore **[shop management](shop-management.md)** (if boss)

---

**Need help?** Check the [Troubleshooting Guide](../troubleshooting.md) for common issues and solutions.
