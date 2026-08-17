# Power BI / Tableau: Visuals, Filters, and Dashboard Design

## Definition

In BI tools, a **report** is a designed set of pages of visuals. A **dashboard** (especially executive) is a one-screen (or few-screen) decision surface. A **visualization** is a chart, KPI card, map, or table that encodes data.

**Filters** restrict the data (date range, city). **Slicers** are on-canvas filter controls the user clicks.

**KPIs** on a canvas are cards or gauges tied to a target (on-time %, GMV vs plan).

**Drill-down** stays in the same visual hierarchy (Year → Month → Day). **Drill-through** jumps to another page with a filtered context (this order, this clinic).

**Dashboard design** is choosing one question, one audience, and a layout that leads to action — not filling every pixel.

## Why it matters

Wrong chart + no filter discipline = pretty confusion. ShopEase daily ops cannot use a 16-chart “strategy” page. NovaBank risk cannot use a pie of 40 products. MediCare+ doctors ignore a dashboard that needs three clicks to see today’s no-shows.

The BA specifies *what must be visible to decide*, then partners with a BI developer on *how*.

## Chart chooser

| You need to show | Prefer | Avoid |
|---|---|---|
| One number vs target | KPI card | 3D pie |
| Part of whole (≤5–6 parts) | Bar (sorted) or simple pie | Pie with 20 slices |
| Rank / comparison | Horizontal bar | Spaghetti 12-line chart |
| Trend over time | Line | Pie per month |
| Two metrics vs time | Dual axis only if scales are honest | Dual axis that hides units |
| Distribution / tail | Histogram or percentile table | Mean-only card |
| Relationship of two measures | Scatter | Line connecting unordered categories |
| Exact values / audit | Table / matrix | Chart only |
| Geography | Map *if* location is the question | Map as decoration |

Tables are valid. Ops often needs a table of late orders more than a donut.

## Filters, slicers, drill-down, drill-through

| Control | What it does | Example |
|---|---|---|
| Page / report filter | Applies to the page or whole report | ShopEase: last 7 days, exclude test orders |
| Slicer | User-driven | City, warehouse, channel |
| Drill-down | Hierarchy inside one visual | GMV: year → quarter → month |
| Drill-through | New page, same entity filtered | From “late % by city” to order list for Pune |
| Tooltip / drill | Extra detail on hover | On-time % tooltip shows n and p90 |

**ShopEase drill-down:** Category GMV → SKU GMV.

**ShopEase drill-through:** Click warehouse “BHI-01” late % → page of orders with promised vs actual dispatch.

**MediCare+ drill-down:** Specialty no-show % → doctor.

**MediCare+ drill-through:** Doctor row → today’s appointment list with status.

**NovaBank:** Drill-down product family → scheme; drill-through to loan application IDs in “pending documents.”

## Dashboard design rules

1. **One page, one question** (or one tightly related set). Daily ops ≠ board strategy.
2. **Action at the top:** KPI cards with target, RAG (red/amber/green), and “what to do if red.”
3. **Then the why:** 1–2 charts that split the KPI (city, warehouse, hour).
4. **Then the list:** table of exceptions to work today.
5. **Filters that match the job:** date default = today or last 24h for ops; month for finance.
6. **No decoration:** drop maps, gauges, and 3-D if they do not change a decision.
7. **Consistent definitions** in a visible footnote: “On-time = dispatched by promised_at.”

### Weak vs strong

| Weak | Strong |
|---|---|
| 20 visuals, no owner, no target | 4 KPIs, 2 splits, 1 work queue table |
| Pie of every category | Sorted bar, top 10 + Other |
| Drill-down used when people need a case list | Drill-through to the work list |
| Slicers for 15 dimensions | 3 slicers the audience actually uses |
| Same page for CEO and warehouse | Separate ops vs exec views |

## Sample dashboard wire (words): ShopEase daily ops

**Audience:** warehouse + CX shift lead. **Question:** “Are we going to miss today’s promise, and which orders should we work now?”

| Zone | Content |
|---|---|
| Top row (action) | KPI: Orders today vs plan; On-time dispatch % vs 95%; Delayed now (count); Return requests opened today |
| Slicers | Date (default today), warehouse, channel (app / web / store) |
| Middle | Line: dispatch volume by hour vs last 7-day same weekday. Bar: delayed count by reason (pick delay, pack, courier handover) |
| Bottom | Table: order_id, SKU, promised_at, minutes late, reason, owner — drill-through from Delayed KPI |
| Footer | Refresh time, definition of on-time, exclude cancelled |

Not on this page: annual GMV, brand awareness, 12-month cohort — that is a different report.

## Real-world examples

**QuickBite.** Ops dashboard: on-time %, food-ready delay, unassigned > 3 min. Not a 3-D rider map as the only visual.

**ShieldSure.** Claims: open aging buckets (0–7, 8–15, 16–30, 30+), not a rainbow pie of 30 statuses.

**Telecom.** Outage dashboard: sites down, customers affected, ETA — table + KPI, not a slow scatter of every tower.

## Scenario / Use case: choosing drill-down vs drill-through

ShopEase category head sees electronics on-time at 88% (red). **Drill-down** on the bar: phones 92%, large appliances 71%. That answers “which category.” They still cannot assign work. **Drill-through** from large appliances to the order table filtered to delayed TVs in warehouse BHI-01. Now a human calls the 3PL. The BA specified both: hierarchy for diagnosis, drill-through for action.

## Notes

- Chart type follows the question: trend, rank, part-of-whole, distribution, or list.
- Filters and slicers must match the job-to-be-done.
- Drill-down = hierarchy in place; drill-through = another page with context.
- One page, one question; action KPIs at the top.
- Tables are first-class for operational work queues.
- Reports document; dashboards decide.
- Default date range is a requirement, not a preference.
- If a visual cannot change today’s action, cut it.
