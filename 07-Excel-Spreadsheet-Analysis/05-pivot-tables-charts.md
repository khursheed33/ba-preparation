# Pivot Tables, Pivot Charts, and Charts

## Definition

A **Pivot Table** summarises rows into groups and measures (sum, count, average) without writing formulas for every city. A **Pivot Chart** is a chart tied to that pivot. A **chart** is a visual of comparison, trend, or (rarely) part-to-whole.

Pivots answer repeated business questions on a clean table. They do not replace a definition of GMV or return.

## Why it matters

Leadership asks "sales by city" and "return rate by category" every Monday. Building 40 `SUMIFS` is slow and error-prone. A pivot on a Table named `Orders` is the BA's default.

## Build a pivot from ShopEase orders

Sample columns (Excel Table `Orders`):

| Column | Example | Role |
|---|---|---|
| OrderDate | 2026-08-01 | Date (group by month) |
| City | Pune | Row / filter |
| Category | Electronics | Row / column |
| GMV | 2499 | Sum |
| Status | Delivered / Cancelled / Returned | Filter or calculated |
| Returned | 0 / 1 | Sum for return count |

Steps: Insert → PivotTable → from `Orders` → New sheet.

| Pivot area | Field |
|---|---|
| Filters | Status (optional) |
| Rows | City |
| Values | Sum of GMV, Count of OrderId |

Second pivot: Rows = Category; Values = Sum of GMV, Sum of Returned. Helper or calculated field for return rate:

```excel
=Returned/OrderCount
```

If `Returned` is 0/1: `Sum of Returned / Count of OrderId`. Show as `%`.

**Questions pivots answer**

| Question | Rows | Values | Filter |
|---|---|---|---|
| Sales by city | City | Sum GMV | Status = Delivered |
| Return rate by category | Category | Sum Returned / Count orders | Date this month |
| Daily GMV trend | OrderDate (day) | Sum GMV |  |
| Cancelled share | Status | Count OrderId |  |
| City × category GMV | City, Category | Sum GMV |  |

Group dates: right-click OrderDate → Group → Months / Days.

Calculated field (simple):

```text
Name: ReturnRate
Formula: =Returned/'OrderId'
```

Better: add a column on `Orders` first:

```excel
=IF([@Status]="Returned",1,0)
```

Then pivot. Calculated fields are harder to audit.

## Chart choice

| Question | Chart | Avoid |
|---|---|---|
| GMV over weeks | Line | Pie |
| GMV by city | Horizontal bar (long names) | 3D bar |
| Status mix (3–4 slices) | Pie only if PO insists | Pie with 12 categories |
| Return rate vs GMV by category | Bar for rate; do not mix scales silently | Dual axis without a caption |
| TAT distribution | Column of buckets | Smooth line on categories |

Pivot Chart: click the pivot → PivotChart. Slicers for City and Month make a mini dashboard.

Formatting: one colour, data labels for small series, title = the question ("Return rate by category, Aug 2026, ShopEase").

## Real-world examples

1. **QuickBite**: pivot late flag by city — same question as COUNTIFS, faster to slice.
2. **MediCare+**: count of no-shows by clinic and weekday — staffing hypothesis.

## Scenario / Use case

ShieldSure claims lead asks: "Where are claims stuck, and is TAT worse for motor?"

Clean table `Claims`: `ClaimId`, `Line` (Motor/Health), `Status` (Open, Query, Approved, Paid, Rejected), `OpenedOn`, `ClosedOn`, `TATDays`.

Pivot 1 — count of ClaimId, Rows = Status, Columns = Line. Shows Health has 40% in Query vs Motor 12%.

Pivot 2 — Average of TATDays, Rows = Line, Filter Status = Paid. Motor 9.2 days, Health 4.1.

Line chart: count of OpenedOn by week (new FNOL). Column chart: open claims by status.

The BA does not say "motor is slow because of fraud". She says "Paid motor TAT is 9.2 vs 4.1; Query pile is mostly Health." Next stories: document chase for Health Query; TAT deep-dive for Motor Paid.

## Weak vs strong

| Weak | Strong |
|---|---|
| Pivot on unclean city names | Clean, then pivot |
| Pie of 15 categories | Bar |
| Title "Chart 1" | Question + period + source |
| GMV includes cancelled | Filter Status |
| Screenshot, no refresh | Table source; Refresh All |
| Return rate = returns / GMV | Returns / orders (define it) |

## Notes

- Refresh the pivot after new rows; Tables help, but Refresh is still required.
- "Show values as % of row" is not the same as a true rate — check the denominator.
- Do not put two unrelated measures on one pie.
- Keep a `data` sheet and a `pivot` sheet; do not stack pivots on the raw extract.
- If the PO changes "GMV" definition, the pivot is wrong until the column is wrong.
- Slicers on two pivots: use Report Connections so month filters both.
- Export values via Paste Special → Values if you must freeze a board pack.
