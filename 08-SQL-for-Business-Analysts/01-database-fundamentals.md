# Database Fundamentals for Business Analysts

## Definition

A **database** is an organised store of data. A **relational database** stores data in **tables** (relations). A **row** is one instance (one order). A **column** is one attribute (order_date). A **primary key (PK)** uniquely identifies a row. A **foreign key (FK)** points to a PK in another table. A **relationship** is how tables connect (customer has many orders). **Normalisation** is designing tables so each fact lives in one place, reducing update errors.

A BA does not administer the database. A BA must read a schema well enough to write queries, spot duplicate customers, and see why a report double-counts GMV.

## Why it matters

Requirements like "show last payment on the order" are impossible if you do not know that payments are a child table. Duplicate PKs or missing FKs are production incidents, not "data team problems" you ignore in UAT.

## Tables, rows, columns

ShopEase (simplified):

| Table | One row means | Example columns |
|---|---|---|
| customers | One customer account | customer_id (PK), email, phone, created_at |
| orders | One checkout | order_id (PK), customer_id (FK), status, gmv, placed_at |
| order_items | One line on an order | item_id (PK), order_id (FK), sku, qty, line_gmv |
| payments | One payment attempt | payment_id (PK), order_id (FK), amount, status, method |
| returns | One return request | return_id (PK), order_id (FK), item_id (FK), reason, status |

How to draw this as a proper diagram (entities, crow’s foot, conceptual vs physical): [Entity relationship diagrams](../04-User-Stories-Use-Cases-Process-Modeling/13-entity-relationship-diagrams.md).

## ER idea (ShopEase)

```text
customers 1──< orders 1──< order_items
                 │
                 ├──< payments
                 └──< returns  (also FK to order_items)
```

Read: one customer, many orders; one order, many items; one order, many payment attempts; a return belongs to an order and usually a specific item.

## Why BAs must understand keys

| Failure | What you see | Business impact |
|---|---|---|
| No real PK on customers | Two rows, same phone, different ids | Duplicate coupons, split history |
| Orphan orders | `customer_id` not in customers | App crash; "unknown buyer" in ops |
| Orphan payments | Payment with missing order_id | Finance collections ≠ orders |
| Using name as key | "Rahul Sharma" × 40 | Merged or split wrongly |
| Composite needed but ignored | Same SKU twice on one order as one row | Qty wrong |

UAT check: count orphans.

```sql
SELECT COUNT(*) AS orphan_orders
FROM orders o
LEFT JOIN customers c ON c.customer_id = o.customer_id
WHERE c.customer_id IS NULL;
```

## Relationships (cardinality)

| Type | Example |
|---|---|
| 1:1 | order ↔ latest successful payment (often a **view**, not a table) |
| 1:N | customer → orders |
| M:N | orders ↔ products via **order_items** (junction table) |

If someone models M:N by stuffing `sku1,sku2` in one column, you cannot filter "orders that contain SKU X" cleanly.

## 1NF / 2NF / 3NF in one page

**Bad Excel-like table** (denormalised dump):

| order_id | customer_name | phones | sku_list | qty_list | city |
|---|---|---|---|---|---|
| 88 | Asha | 98…, 99… | SHOE,BAG | 1,2 | Pune |

Problems: two phones in one cell, two SKUs in one cell, customer city repeats on every order, cannot sum qty.

**1NF — atomic values, repeating groups become rows**

| order_id | customer_id | sku | qty |
|---|---|---|---|
| 88 | C1 | SHOE | 1 |
| 88 | C1 | BAG | 2 |

**2NF — no partial dependency on a composite key**

If PK is `(order_id, sku)`, `customer_id` depends only on `order_id` → lift customer onto `orders`.

**3NF — no transitive dependency**

`city` depends on customer, not on order → `customers.city`, not copied on every order (unless you **snapshot** shipping city at order time — that is a business choice, then it is an order attribute).

| | Bad dump | Normalised |
|---|---|---|
| Update city | Change 80 order rows | Change one customer (or snapshot rule) |
| Add a line | Rewrite sku_list text | Insert order_items row |
| Report GMV by SKU | Fragile split | `SUM(line_gmv) GROUP BY sku` |

BA takeaway: if the warehouse send you the dump, you may query it, but new requirements should land on normalised tables. Snapshot fields (ship_city at purchase) must be in the requirement if history must not move when the customer relocates.

## Real-world examples

1. **NovaBank**: `account_id` PK; `customer_id` FK. Joint accounts: junction `account_holders` (M:N), not two customer columns.
2. **MediCare+**: `uhid` as business key; still have a surrogate `patient_id` if UHID can be corrected.

## Scenario / Use case

ShopEase finance says some returns have no order. The BA asks for the ER. `returns.order_id` is nullable "for POS walk-in". Walk-in returns were never in `orders`, so collections recon fails. Requirement: either create a dummy order or a `return_source` and a different recon rule. Keys made the product decision visible.

## Weak vs strong

| Weak | Strong |
|---|---|
| "It's all in one Excel" | Tables + keys + grain ("one row = ?") |
| Join on customer name | Join on customer_id |
| Ignore orphans in UAT | COUNT of LEFT JOIN IS NULL |
| Repeat city on every line with no rule | 3NF or explicit snapshot |
| M:N as comma lists | Junction table |

## Notes

- Always ask: **what does one row mean?** That is grain.
- PK should be stable and unique; email is a bad PK (people change it).
- FKs may be missing in analytics replicas — still think as if they exist.
- Normalisation is a design tool; star schemas for BI denormalise on purpose.
- Entry-level BA: you do not need DBA depth; you need keys, grain, and relationships.
- Draw the five ShopEase boxes on paper before writing a JOIN.
- If two teams disagree on "order", they disagree on the PK table.
- Watch: [SQL for beginners](https://www.youtube.com/watch?v=h0nxCDiD-zg) and [how BAs use SQL](https://www.youtube.com/watch?v=94CfbgY8De4). ERD lecture: [Lucidchart ERD](https://www.youtube.com/watch?v=QpdhBUYk7Kk).
