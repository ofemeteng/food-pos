# Fastfood/Bakery Data-Intensive Management Framework (Nigeria)

## 1) Strategic Objective
Build a bespoke operating system that connects **front-of-house sales**, **kitchen/bakery production**, **inventory**, **cash/expense control**, and **profitability analytics** in one place so management can make fast, evidence-based decisions daily.

---

## 2) Core Business Targets (from your projection)

### Revenue assumptions
- Daily customers: **120**
- Average spend/customer: **₦2,000**
- Daily revenue: **₦240,000**
- Monthly revenue (28 days): **₦6,720,000**

### Monthly fixed OPEX
- Total fixed OPEX: **₦1,840,000**

### Operating targets
- Survival floor: **₦4,800,000/month** (₦174,000/day)
- Conservative target: **₦7,000,000/month** (₦250,000/day)
- Target COGS: **≤ 50% of revenue**

### Profit checkpoint at ₦7,000,000/month
- Gross profit (50%): **₦3,500,000**
- Less fixed OPEX: **₦1,840,000**
- Less lender payment (10%): **₦700,000**
- Operating surplus: **~₦960,000**

---

## 3) Product Modules (What to build)

## A. POS & Sales Intelligence (Frontend)
**Purpose:** Capture every sale and payment event cleanly.

Key features:
- Product catalog with variants (size/flavor/add-ons)
- Combo/bundle support
- Dine-in / takeout / delivery modes
- Payment channels: cash, transfer, POS card, wallet
- Discount/promo engine with manager approval controls
- Refund/void tracking with mandatory reason codes
- Shift opening/closing and cash reconciliation

Core analytics:
- Revenue by hour/day/week/month
- Product mix and contribution margin by item
- Channel performance (walk-in vs delivery)
- Discount leakage and refund rate

## B. Kitchen & Bakery Production Operations
**Purpose:** Convert demand into controlled production with minimal waste.

Key features:
- Daily production plan from sales forecast + par levels
- Recipe/BOM management (raw material quantities per SKU)
- Batch cooking/baking logs (start, end, yield)
- Wastage capture (burnt, expired, overproduction, spoilage)
- Rework/returns tracking
- Prep-to-service cycle times

Core analytics:
- Planned vs actual production yield
- Waste % by product and by reason
- Stock-out incidents linked to lost sales
- Throughput and station bottlenecks

## C. Inventory & Procurement Control
**Purpose:** Keep stock availability high while avoiding capital lock-up and shrinkage.

Key features:
- Central item master (raw materials, packaging, finished goods)
- Unit conversions (bag, kg, g, liter, ml, pcs)
- Goods received note (GRN) workflow
- Supplier records (price history, lead times, quality score)
- Reorder point + safety stock alerts
- Stock count cycles and variance approvals
- Transfer management (if multiple outlets)

Core analytics:
- Inventory days on hand
- Purchase price variance (PPV)
- Stock variance (book vs physical)
- Dead stock and near-expiry exposure

## D. Expense, Cashbook & Cost Accounting
**Purpose:** Track all outflows and align to P&L.

Key features:
- OPEX categories (staff, energy, rent, marketing, maintenance, misc.)
- Daily petty cash logging with receipts/photo upload
- Fixed vs variable cost classification
- Utility sub-meters tracking (diesel, gas, electricity)
- Approval matrix for spend thresholds
- Bank/cash reconciliation dashboard

Core analytics:
- OPEX as % of revenue
- Energy cost per ₦1,000 revenue
- Unexpected spend trend alerts
- Branch/department cost heatmap

## E. Profitability, KPI & Management Cockpit
**Purpose:** One command center for owners/managers.

Key features:
- Daily flash report (sales, COGS estimate, OPEX, cash, variance)
- Monthly P&L auto-generation
- Target-setting engine (daily/monthly/quarterly/yearly)
- Forecasting (best/base/worst-case)
- Scenario modeling (price increase, footfall drop, ingredient inflation)
- KPI scorecards by role (owner, branch manager, production lead)

Core analytics:
- Gross margin %, net margin %, contribution margin
- Break-even sales (monthly and daily)
- Budget vs actual variance
- Runway/coverage if revenue dips below floor

---

## 4) Data Model (Minimum entities)
- `stores`
- `users` and `roles`
- `products`, `product_variants`, `recipes_bom`
- `sales_orders`, `sales_order_items`, `payments`
- `daily_shift_closures`, `cash_reconciliation_checks`, `owner_signoffs`
- `production_batches`, `production_outputs`, `waste_logs`
- `inventory_items`, `inventory_movements`, `stock_counts`
- `suppliers`, `purchase_orders`, `grn_receipts`
- `expense_entries`, `cashbook_entries`
- `weekly_business_reviews`, `weekly_issues`, `weekly_actions`
- `monthly_pnl_snapshots`, `monthly_survival_status`, `loan_schedules`
- `targets`, `kpi_definitions`, `kpi_snapshots`
- `ledger_entries` (for P&L and audit trail)

Design principle:
- Treat every meaningful business event as a timestamped transaction.
- Ensure immutable transaction logs with reversal entries instead of destructive edits.

---

## 5) KPI Framework (Daily/Monthly/Quarterly/Yearly)

### Revenue & Demand KPIs
- Daily revenue
- Average order value (AOV)
- Customer count
- Sales per labor hour
- Category mix (% food, % bakery, % beverages)

### Cost KPIs
- COGS % (target <= 50%)
- OPEX % of revenue
- Energy % of revenue
- Waste % of production value
- Shrinkage % of inventory value

### Profitability KPIs
- Gross profit
- Contribution margin
- EBITDA proxy (if no depreciation tracking initially)
- Net operating surplus
- Break-even attainment %

### Control KPIs
- Refund/void %
- Discount % and unauthorized discount count
- Stock count variance %
- Late supplier delivery rate
- Production adherence % (planned vs actual)

### Daily/Weekly/Monthly health status KPIs
- **Daily Cash Status** (OK / Warning / Critical)
- **Weekly Cost Status** (within threshold vs above threshold)
- **Monthly Survival Status** (below floor / survival floor / target)
- Cash check variance and unresolved count
- Owner sign-off compliance rate

---

## 6) Decision Rules (Action thresholds)
- If daily revenue < ₦174,000 for 3 consecutive days -> trigger emergency review.
- If COGS > 52% in any rolling 7-day window -> review recipe yield + supplier price + pilferage.
- If waste > 4% of production value weekly -> reduce batch sizes and tighten forecast.
- If energy cost > 8% of revenue monthly -> audit generator runtime and oven scheduling.
- If stock variance > 2% in any category -> immediate count investigation and access control review.
- If owner sign-off misses 2 days in one week -> require branch manager escalation.

---

## 7) Reporting Cadence
- **Real-time dashboard:** Sales, cash position, stock alerts.
- **Daily close report:** Revenue, COGS estimate, key incidents, cash reconciliation.
- **Weekly ops review:** Product performance, waste analysis, procurement efficiency.
- **Monthly finance review:** Full P&L, variance to budget, rolling 3-month forecast.
- **Quarterly strategy review:** Pricing, menu engineering, capacity expansion, branch economics.

---

## 8) Spreadsheet-to-Software Transition (your current process)

To make your existing manual tracking immediately useful in the software rollout, capture the same structures below as digital forms and snapshots:

### Daily Sales & Cash Sheet
Fields to preserve:
- Date
- Opening cash
- Cash sales
- Transfer sales
- POS sales
- Total sales
- Expenses
- Closing cash
- Cash check (difference)
- Status
- Owner sign-off (Yes/No)

### Weekly Review Sheet
Fields to preserve:
- Week
- Total sales / avg daily sales / best day / worst day
- Ingredients, staff, power, marketing cost
- Ingredient %, staff %, power %
- Weekly status
- Opening cash / closing cash
- Revenue share due / paid
- Issues identified
- Actions taken

### Monthly Survival Sheet
Fields to preserve:
- Month
- Total revenue
- COGS
- Gross profit
- Operating expenses
- Net operating cash
- Rent / staff / power
- Fixed coverage status
- Cash balance
- Loan outstanding
- Runway (months)
- Key decisions

Recommendation:
- Keep these layouts as ingestion templates for the first 30-60 days.
- Run dual mode (manual + system) until variance is <2%.

---

## 9) Implementation Roadmap (Practical)

### Phase 1 (Weeks 1-4): Foundation
- POS transaction capture
- Product catalog and pricing
- Basic inventory in/out
- Daily flash dashboard
- Role-based access control
- Digital daily cash closure form (mirrors current sheet)

### Phase 2 (Weeks 5-8): Cost & Inventory Discipline
- Recipe/BOM and COGS calculator
- Purchase + GRN workflow
- Stock count + variance audit
- Expense capture and approvals
- Weekly cost-status report auto-generation

### Phase 3 (Weeks 9-12): Production Intelligence
- Batch planning and yield tracking
- Waste reason analytics
- Forecast-assisted production targets

### Phase 4 (Weeks 13-16): Profit Engine
- Full P&L automation
- KPI targets and alerts
- Scenario simulator
- Monthly survival dashboard with runway tracking
- Management scorecard

---

## 10) Suggested Technology Architecture
- **Frontend:** Web app (manager dashboard) + tablet POS UI.
- **Backend:** API service + background jobs for KPI snapshots.
- **Database:** PostgreSQL with strict audit fields (`created_at`, `created_by`, etc.).
- **Analytics layer:** Materialized views + scheduled ETL to KPI tables.
- **Offline resilience:** Local queue for POS transactions with auto-sync.
- **Security:** Role-based permissions, shift-level accountability, immutable logs.

---

## 11) Nigerian Operating Realities to Encode
- Multiple payment rails and unstable connectivity.
- Power cost volatility (diesel, gas, PHED).
- Inflation and supplier price swings requiring frequent menu/recipe repricing.
- Strong anti-leakage controls around cash and stock movement.
- Mobile-first workflows for supervisors.

---

## 12) Initial Build Checklist (MVP)
- [ ] Setup branches, environments, and deployment pipeline.
- [ ] Define data dictionary for all master/transaction tables.
- [ ] Build POS order + payment + receipt flow.
- [ ] Build inventory movement ledger.
- [ ] Add daily close workflow with manager sign-off.
- [ ] Launch KPI dashboard v1 (revenue, COGS%, OPEX%, cash).
- [ ] Add weekly and monthly status pages matching your existing business sheets.
- [ ] Pilot for 2 weeks and compare software metrics to manual books.

---

## 13) Success Criteria (First 90 days)
- 95%+ sales captured digitally with shift reconciliation.
- COGS stabilized at or below 50% (or a clear reduction trend).
- Waste reduced by at least 20% from baseline.
- Fixed OPEX visibility with <=5% unexplained variance.
- Weekly management meetings run directly from system reports.
- Daily owner sign-off completion >=95%.

