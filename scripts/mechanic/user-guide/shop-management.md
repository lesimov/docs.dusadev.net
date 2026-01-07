# Shop Management

Complete guide to managing your mechanic shop - for owners and managers.

**Note**: This section is for **Rank 3+ (Manager)** and **Rank 4 (Owner)** only.

## Overview

As a shop manager or owner, you have access to:
- **Employee Management** - Hire, fire, and manage staff
- **Financial Management** - Shop account, transactions, withdrawals
- **Shop Settings** - Configure pricing, hours, permissions
- **Performance Metrics** - Statistics, reports, analytics

## Accessing Boss Menu

### Opening Management Panel

1. Open tablet → Mechanic app
2. Navigate to **"Management"** tab
3. Management dashboard opens

**Note**: If Management tab is not visible, you don't have sufficient rank.

### Management Dashboard

```
┌─────────────────────────────────────┐
│  Shop Management - Benny's          │
│                                     │
│  [Employees] [Finances] [Settings]  │
│  [Reports] [Analytics]              │
│                                     │
│  📊 Quick Stats                     │
│  • 8 Employees                      │
│  • $42,350 Shop Balance             │
│  • 156 Orders This Month            │
│  • $125,430 Revenue                 │
│                                     │
│  ⚠️ 2 Low Stock Items               │
│  ℹ️  3 Pending Employee Requests    │
└─────────────────────────────────────┘
```

## Employee Management

### Viewing Employees

**Employee list shows:**
- Employee name
- Rank/title
- Hire date
- Performance metrics
- Status (active/inactive)
- Last activity

**Employee details:**
```
┌──────────────────────────────┐
│  John Doe                    │
│  Rank 2 - Senior Mechanic    │
│                              │
│  Hired: Jan 15, 2024         │
│  Orders Completed: 45        │
│  Revenue Generated: $12,450  │
│  Customer Rating: 4.8/5.0    │
│  Last Active: 2 hours ago    │
│                              │
│  [Edit Rank] [Remove] [More] │
└──────────────────────────────┘
```

### Hiring Employees

**Prerequisites:**
- Player must be online
- Player must be nearby (configurable radius)
- Shop must have available slots (if limited)

**Hiring process:**

1. Management → Employees → **"Hire Employee"**
2. List of nearby players appears
3. Select player to hire
4. Assign initial rank:
   ```
   Rank 0: Trainee
   Rank 1: Mechanic
   Rank 2: Senior Mechanic
   Rank 3: Manager
   ```
5. Confirm hire
6. Player receives job offer notification
7. Player accepts/declines
8. If accepted, added to shop

**Hiring tips:**
- Start new employees at Rank 0 or 1
- Probation period recommended
- Verify they understand tablet
- Assign trainer/mentor
- Set expectations clearly

### Managing Ranks

**Change employee rank:**

1. Employee list → Select employee
2. Click **"Edit Rank"**
3. Select new rank (0-4)
4. Confirm change
5. Employee permissions update immediately

**Rank progression guidelines:**

```
Trainee (0) → Mechanic (1):
  - Completed training
  - Knows tablet system
  - Can work independently

Mechanic (1) → Senior (2):
  - 50+ orders completed
  - Good customer ratings
  - Team player

Senior (2) → Manager (3):
  - 100+ orders
  - Leadership qualities
  - Trusted with inventory

Manager (3) → Owner (4):
  - Business partner
  - Long-term commitment
  - Financial stake
```

**Rank permissions:**

| Permission | Rank 0 | Rank 1 | Rank 2 | Rank 3 | Rank 4 |
|------------|--------|--------|--------|--------|--------|
| View orders | ✅ | ✅ | ✅ | ✅ | ✅ |
| Create orders | ❌ | ✅ | ✅ | ✅ | ✅ |
| Tune vehicles | ❌ | ✅ | ✅ | ✅ | ✅ |
| Assign orders | ❌ | ❌ | ✅ | ✅ | ✅ |
| Order parts | ❌ | ❌ | ❌ | ✅ | ✅ |
| Hire/fire | ❌ | ❌ | ❌ | ✅ | ✅ |
| Withdraw funds | ❌ | ❌ | ❌ | ❌ | ✅ |
| Edit settings | ❌ | ❌ | ❌ | ❌ | ✅ |

**Note**: Permissions are configurable per server.

### Firing Employees

**Remove employee from shop:**

1. Employee list → Select employee
2. Click **"Remove from Shop"** or **"Fire Employee"**
3. Confirm removal:
   ```
   Remove John Doe from shop?

   - Access revoked immediately
   - Active orders reassigned
   - Final commission paid

   Reason (optional): [___________]

   [Cancel] [Confirm]
   ```
4. Employee removed
5. Notification sent to employee

**What happens:**
- Job removed (player loses mechanic job)
- Tablet access revoked
- Active orders reassigned to others
- Commission paid out (if owed)
- Employee records archived

**Firing best practices:**
- Document performance issues
- Provide warnings first
- Be professional
- Pay final commissions
- Return any shop property

### Employee Performance

**Track employee metrics:**

**Individual stats:**
- Orders completed
- Average completion time
- Revenue generated
- Customer ratings
- Parts usage efficiency
- Attendance/activity

**Performance dashboard:**
```
┌─────────────────────────────────┐
│  Top Performers - This Month    │
│                                 │
│  1. John Doe     52 orders      │
│     Revenue: $15,240            │
│     Rating: 4.9/5               │
│                                 │
│  2. Jane Smith   48 orders      │
│     Revenue: $14,100            │
│     Rating: 4.8/5               │
│                                 │
│  3. Bob Wilson   45 orders      │
│     Revenue: $13,850            │
│     Rating: 4.7/5               │
└─────────────────────────────────┘
```

**Use metrics for:**
- Identifying top performers
- Determining raises/bonuses
- Finding training needs
- Fair work distribution
- Promotion decisions

## Financial Management

### Shop Balance

**View current balance:**

Management → Finances → **Balance Overview**

```
┌──────────────────────────────┐
│  Shop Account                │
│                              │
│  Current Balance:            │
│  $42,350.00                  │
│                              │
│  This Month:                 │
│  + Revenue:    $125,430.00   │
│  - Parts:      $ 48,250.00   │
│  - Wages:      $ 15,600.00   │
│  - Expenses:   $  8,230.00   │
│  ─────────────────────────   │
│  Net Profit:   $ 53,350.00   │
│                              │
│  [Transactions] [Withdraw]   │
└──────────────────────────────┘
```

**Balance components:**
- Work order revenue
- Parts sales
- Minus: parts purchased
- Minus: employee wages/commission
- Minus: operating expenses

### Withdrawing Funds

**Owner only** (Rank 4) can withdraw money:

1. Finances → **"Withdraw Funds"**
2. Enter amount:
   ```
   Current Balance: $42,350.00

   Withdraw Amount: [$5,000.00]

   Remaining: $37,350.00

   Withdraw to: [Personal Bank Account]

   [Cancel] [Withdraw]
   ```
3. Confirm withdrawal
4. Money transferred to personal account
5. Transaction recorded

**Withdrawal limits:**
- Can't withdraw more than balance
- May have daily/weekly limits
- Minimum balance requirements (configurable)

**Tax implications** (if applicable):
- Withdrawals may be taxed
- Record keeping for RP purposes
- Government reporting (some servers)

### Depositing Funds

**Add money to shop:**

1. Finances → **"Deposit Funds"**
2. Enter amount from personal account
3. Money transferred to shop
4. Transaction recorded

**Why deposit:**
- Cover operating costs
- Stock up on parts
- Invest in shop improvements
- Emergency fund

### Transaction History

**View all financial transactions:**

Finances → **"Transaction History"**

**Transactions include:**
- Date/time
- Type (revenue, expense, withdrawal, etc.)
- Amount
- Description
- Balance after transaction
- Associated employee (if applicable)

**Filter by:**
- Date range
- Transaction type
- Amount range
- Employee

**Export transactions:**
- Generate reports
- Export to CSV
- Print statements
- Tax documentation

### Revenue Sources

**Income breakdown:**

```
Work Orders:        $98,450  (78%)
Parts Sales:        $18,230  (15%)
Tuning Services:    $ 8,750  (7%)
─────────────────────────────
Total Revenue:     $125,430
```

**Track by:**
- Service type
- Employee
- Time period
- Customer

### Expense Tracking

**Operating expenses:**

```
Parts Purchases:    $48,250  (58%)
Employee Wages:     $15,600  (19%)
Shop Supplies:      $ 5,430  (7%)
Utilities:          $ 2,800  (3%)
Other:              $    500 (1%)
─────────────────────────────
Total Expenses:     $72,580
```

**Reduce costs by:**
- Bulk ordering
- Supplier negotiations
- Efficient scheduling
- Waste reduction
- Energy efficiency

### Profit & Loss

**P&L statement:**

```
┌────────────────────────────────┐
│  Profit & Loss - January 2024  │
│                                │
│  Revenue:         $125,430.00  │
│  COGS:            $ 48,250.00  │
│  ──────────────────────────    │
│  Gross Profit:    $ 77,180.00  │
│  Margin:          61.5%        │
│                                │
│  Operating Exp:   $ 23,830.00  │
│  ──────────────────────────    │
│  Net Profit:      $ 53,350.00  │
│  Margin:          42.5%        │
│                                │
│  [Export] [Details] [Compare]  │
└────────────────────────────────┘
```

**Use P&L to:**
- Measure profitability
- Identify trends
- Plan budgets
- Make business decisions
- Set pricing

## Shop Settings

### General Settings

**Configure shop:**

Settings → **"General Settings"**

**Shop Information:**
```
Shop Name: [Benny's Motorworks]
Display Name: [Benny's Motorworks]
Description: [Premium vehicle customization]

Contact Phone: [555-0123]
Shop Email: [bennys@email.com]
```

**Business Hours** (if enabled):
```
Monday:     09:00 - 18:00
Tuesday:    09:00 - 18:00
Wednesday:  09:00 - 18:00
Thursday:   09:00 - 18:00
Friday:     09:00 - 20:00
Saturday:   10:00 - 18:00
Sunday:     Closed
```

**During closed hours:**
- No new work orders accepted
- Existing orders can be worked
- Customers notified of hours

### Pricing Configuration

**Set service pricing:**

Settings → **"Pricing & Services"**

**Labor rates:**
```
Basic Labor:       $100/hour
Diagnostic:        $125/hour
Specialized:       $150/hour
Emergency:         $200/hour
```

**Service packages:**
```
Oil Change:        $150
Brake Service:     $300
Tune-Up:           $450
Full Detail:       $200
```

**Tuning prices:**
```
Cosmetic Mods:     $500 base
Performance:       $2,000 base
Stance:            $1,500 base
Engine Swaps:      $25,000+
```

**Discounts:**
- Regular customers: 5-10%
- Fleet vehicles: 15%
- Referrals: $50 credit
- Seasonal promotions

### Service Menu

**Enable/disable services:**

Settings → **"Services Offered"**

```
✅ Oil Changes
✅ Brake Service
✅ Engine Repair
✅ Transmission Work
✅ Electrical Diagnostics
✅ Body Work
✅ Paint Jobs
✅ Vehicle Tuning
❌ Engine Swaps (temporarily disabled)
✅ Detailing
```

**Why disable services:**
- No qualified staff
- Parts unavailable
- Equipment broken
- Seasonal (winter tires, AC)
- Liability concerns

### Notification Settings

**Configure shop notifications:**

**Notify on:**
- New work order created
- Work order completed
- Parts delivered
- Low stock alert
- Employee hired/fired
- Large withdrawals
- Customer complaints
- Positive reviews

**Notification methods:**
- In-game tablet
- Discord webhook (if configured)
- Email (if configured)

### Permissions

**Fine-tune rank permissions:**

Settings → **"Permissions"**

**Customize which ranks can:**
- Create work orders
- Assign orders
- Complete orders
- Access tuning
- Order parts
- View finances
- Hire employees
- Withdraw funds
- Edit settings

**Example custom permission:**
```
Create Work Orders:
  Minimum Rank: [1 - Mechanic]

Order Parts:
  Minimum Rank: [2 - Senior Mechanic]
  Daily Limit: [$5,000]

Withdraw Funds:
  Minimum Rank: [4 - Owner]
  Max Per Day: [$10,000]
```

## Performance Metrics

### Shop Statistics

**Dashboard metrics:**

```
┌──────────────────────────────────┐
│  Shop Performance - Last 30 Days │
│                                  │
│  Total Orders:      156          │
│  Completed:         148  (95%)   │
│  Cancelled:           8  (5%)    │
│  Average Value:   $825           │
│                                  │
│  Total Revenue:   $125,430       │
│  Total Expenses:  $ 72,580       │
│  Net Profit:      $ 53,350       │
│                                  │
│  Customer Rating:  4.7 / 5.0     │
│  Completion Time:  2.5 hrs avg   │
│  Repeat Customers: 68%           │
└──────────────────────────────────┘
```

### Service Analytics

**Popular services:**
```
1. Oil Changes           42 orders
2. Brake Service         28 orders
3. Vehicle Tuning        24 orders
4. Engine Diagnostics    18 orders
5. Paint Jobs            12 orders
```

**Revenue by service:**
```
Vehicle Tuning:      $45,250  (36%)
Brake Service:       $28,400  (23%)
Engine Work:         $22,150  (18%)
Paint Jobs:          $15,480  (12%)
Other:               $14,150  (11%)
```

**Use to:**
- Focus marketing
- Stock right parts
- Train staff
- Set pricing
- Plan capacity

### Customer Analytics

**Customer insights:**

**Demographics:**
- New customers: 48
- Returning: 108
- VIP customers: 12

**Satisfaction:**
- 5 stars: 78 orders (51%)
- 4 stars: 62 orders (40%)
- 3 stars: 10 orders (6%)
- 2 stars:  4 orders (3%)
- 1 star:   2 orders (1%)

**Top customers:**
```
1. Michael R.   $4,250  12 orders
2. Sarah K.     $3,840   8 orders
3. David M.     $3,520   7 orders
```

**Customer retention:**
- 30-day: 68%
- 90-day: 54%
- 1-year: 38%

### Competitive Analysis

**Benchmark against:**
- Industry averages
- Other shops in city
- Previous months
- Goals/targets

```
Your Shop:          4.7/5.0 rating
City Average:       4.2/5.0
Top Shop:           4.9/5.0

Your Completion:    2.5 hours avg
City Average:       3.2 hours avg
Fastest Shop:       2.0 hours avg
```

## Reports

### Generating Reports

**Available reports:**

1. **Monthly Summary**
   - Revenue and expenses
   - Orders completed
   - Employee performance
   - Customer satisfaction

2. **Financial Report**
   - Detailed P&L
   - Cash flow
   - Balance sheet
   - Tax summary

3. **Employee Report**
   - Individual performance
   - Attendance
   - Commissions earned
   - Training completed

4. **Inventory Report**
   - Stock levels
   - Parts usage
   - Ordering patterns
   - Waste/loss

5. **Customer Report**
   - New vs returning
   - Satisfaction scores
   - Service preferences
   - Retention rates

**Generate report:**
1. Reports → Select report type
2. Choose date range
3. Select filters/options
4. Click "Generate"
5. Report displays
6. Export if needed (PDF, CSV, Print)

### Scheduled Reports

**Auto-generate reports:**

Settings → Reports → **"Scheduled Reports"**

**Configuration:**
```
Monthly Summary:
  Schedule: Last day of month at 11:59 PM
  Recipients: Shop owners
  Format: PDF + CSV
  Delivery: Email + Tablet notification

Weekly Employee Report:
  Schedule: Every Sunday at 8:00 PM
  Recipients: Managers
  Format: PDF
  Delivery: Tablet notification
```

**Benefits:**
- Automatic tracking
- Consistent review
- No forgetting
- Easy comparison

## Best Practices

### As a Manager

**Daily tasks:**
- [ ] Check stock levels
- [ ] Review new orders
- [ ] Monitor employee activity
- [ ] Order needed parts
- [ ] Respond to issues

**Weekly tasks:**
- [ ] Review financials
- [ ] Employee performance check
- [ ] Inventory audit
- [ ] Customer feedback review
- [ ] Plan next week

**Monthly tasks:**
- [ ] Full financial review
- [ ] Employee evaluations
- [ ] Strategic planning
- [ ] Pricing review
- [ ] Marketing planning

### As an Owner

**Leadership:**
- Set clear expectations
- Lead by example
- Reward good performance
- Address issues quickly
- Maintain team morale

**Financial:**
- Monitor profitability
- Control costs
- Invest wisely
- Plan for growth
- Build cash reserves

**Strategic:**
- Long-term planning
- Competition awareness
- Market trends
- Service expansion
- Quality focus

## Troubleshooting

### Can't access management

**Solutions:**
- Verify you have rank 3+
- Check you're assigned to shop
- Restart tablet
- Contact owner

### Can't hire players

**Solutions:**
- Ensure player is nearby
- Verify they don't have mechanic job
- Check shop has available slots
- Try different player
- Restart both resources

### Financial numbers wrong

**Solutions:**
- Review transaction history
- Check for duplicate entries
- Verify work order completion
- Audit inventory deductions
- Contact admin if persists

---

**Congratulations!** You now have the knowledge to effectively manage a mechanic shop. For more advanced topics, see the [Developer Documentation](../developer/) and [Guides](../guides/).
