# BI Fundamentals and Data Prep

## Definition

**Business Intelligence (BI)** is the practice of turning operational data into trusted views that help people decide. Power BI and Tableau are tools. BI is the discipline: sources, definitions, models, and questions.

A **data source** is where facts live (core banking, OMS, EMR, Excel, API, data warehouse).

**Data import** is bringing that data into the BI tool or warehouse.

**Data transformation** is cleaning, joining, and reshaping (types, keys, calendars, status maps).

**Data modeling** is designing tables so questions are easy and numbers do not double-count.

**Relationships** connect tables on keys (order to customer).

**Dimensions** are the “who / what / when / where” (customer, product, date, branch).

**Measures** are the aggregations (sum of GMV, count of claims, average TAT).

## Why it matters — BI is decision support, not pretty dashboards

A colourful board that cannot answer “should we stop COD in Zone 7?” is decoration. BI exists so a ShopEase ops lead, a NovaBank credit manager, or a ShieldSure claims head can see the same definition, slice it, and act.

If the model is wrong, the dashboard is a confident liar. ShieldSure can show “claims down” because a bad relationship duplicated or dropped rows. Executives will still present it.

## Data sources, import, transformation

| Source type | Example | BA concern |
|---|---|---|
| Operational DB | ShopEase orders, MediCare+ appointments | Grain, keys, delayed jobs |
| Files | Monthly target Excel | Version, who edits |
| APIs / events | QuickBite rider pings | Duplicates, late events |
| Warehouse / lake | Enterprise GMV | Refresh SLA, certified vs sandbox |
| Unstructured sidecar | Call notes | Not in the star until coded |

**Import:** scheduled refresh, incremental vs full, credentials, row limits.

**Transform (Power Query / Tableau Prep — BA level):** rename fields, split status codes, map “DELIVRD” and “Delivered” to one value, create `order_date`, filter test orders, handle nulls.

Write transformation rules as **business rules**, not only as UI clicks.

### Weak vs strong

| Weak | Strong |
|---|---|
| Connect Excel and chart. | Source system of record, grain, refresh time, owner of definition. |
| Relationship: customer name to customer name. | Relationship: `customer_id` many-to-one to `dim_customer`. |
| “Sales” measure = count of rows. | Sales = SUM(fact_orders[net_amount]) where status in paid set. |
| One flat dump of everything. | Star: facts + dimensions; no claim ID repeated per coverage row without a rule. |

## Data modeling — star schema lite

A **star schema** puts a **fact** table (events/transactions) in the center, surrounded by **dimension** tables.

ShopEase / ShieldSure-style sales or claims:

```
dim_date          dim_customer
     \                /
      \              /
       fact_orders  (or fact_claims)
      /              \
     /                \
dim_product        dim_channel  (optional)
```

| Table | Grain | Typical columns |
|---|---|---|
| fact_orders | One row = one order line or one order (pick one and stick) | order_id, date_key, customer_key, product_key, qty, gmv, discount, status |
| dim_date | One row = one day | date, week, month, FY, holiday flag |
| dim_customer | One row = one customer | customer_key, segment, city, acquire_channel |
| dim_product | One row = one SKU or product | category, brand, perishable flag |

**Measures** live as calculations on facts: `Total GMV = SUM(gmv)`, `Order count = DISTINCTCOUNT(order_id)`.

**Dimensions** are how you slice: by month, city, category.

**Relationship cardinality:** many orders to one customer (many-to-one). If you accidentally relate so one claim matches many policy versions *and* you sum claim_amount from the many side, you **duplicate claims**.

## Real-world examples

**NovaBank.** Fact: disbursals. Dimensions: product, branch, RM, date. A many-to-many between loan and collateral without a bridge table inflates “loans covered.”

**MediCare+.** Fact: appointments. Dimensions: doctor, clinic, specialty, date. If patient has multiple insurance rows joined into the fact, visit counts explode.

**Manufacturing / logistics.** Fact: shipments. Dimensions: warehouse, carrier, SKU, date. BOM (bill of materials) is a hierarchy — do not treat it as a simple one-to-one product dimension without a plan.

**Retail stores vs online.** Same `dim_product`, different `dim_channel`. One fact with `channel_key` beats two disconnected workbooks.

## Scenario / Use case: ShieldSure claims dashboard duplicates claims

**Context.** Claims head shows the board: “Open claims are 18,400, down 12%.” Ops floor says the queue is worse. The BA traces the Power BI model.

**What broke.** `fact_claims` (one row per claim) was related to `dim_coverage` (one claim can have many coverage lines: hospital, OT, pharmacy). The relationship was both-directions with no bridge. Visual “claim count” used COUNT of rows after the join — each claim with 3 coverages counted as 3.

**Stakeholders.** Claims ops, finance (reserves), BI developer, policy admin, BA.

**What the BA does.**

1. Freeze the grain: “Open claim count” = distinct `claim_id` where status in Open set as of report date.
2. Split models: `fact_claims` for claim-level KPIs; `fact_claim_lines` for amount by coverage.
3. Relationship: claim lines many-to-one to claims; claims many-to-one to `dim_customer` and `dim_date`.
4. Measures: `Claim count = DISTINCTCOUNT(claim_id)`; `Paid amount = SUM(line_amount)` only on the line fact.
5. Add a reconciliation tile: BI count vs core claims system (daily).

**If ignored.** Reserves look light, staffing looks surplus, and a “successful” dashboard trains leadership on the wrong number.

## BA checklist for a BI story

1. What question will this answer this week?
2. What is one row in the fact?
3. What is the relationship key and direction?
4. Which measure uses SUM vs DISTINCTCOUNT?
5. When did data last refresh, and what is excluded (test, cancelled, void)?

## Notes

- BI is a decision-support system; charts are the last mile.
- Grain first, visuals second.
- Star schema: facts in the middle, dimensions around, measures on facts.
- Many-to-many and bidirectional filters are common duplication traps.
- Dimensions describe; measures calculate.
- Import without a dictionary produces debate, not insight.
- Transformation rules are requirements (status maps, test-order filters).
- Always reconcile a dashboard KPI to the source system of record.
