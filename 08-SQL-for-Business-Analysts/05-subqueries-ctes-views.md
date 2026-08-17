# Subqueries, CTEs, and Views

## Definition

A **subquery** is a query inside another query (in `WHERE`, `FROM`, or `SELECT`). A **CTE** (`WITH` clause) is a named subquery you can read top-down. A **view** is a saved query the database exposes as a table-like object — a **business-friendly dataset** (e.g. `v_open_claims`).

BAs use these to keep logic readable and to avoid copying 40-line joins into every report.

## Why it matters

Repeat-buyer, aging, and "open and missing document" questions need steps. Nested subqueries in one `SELECT` are how people get the metric wrong and cannot explain it in a review.

## Subqueries

**Filter: customers whose GMV > 10,000**

```sql
SELECT customer_id, email
FROM customers
WHERE customer_id IN (
  SELECT customer_id
  FROM orders
  WHERE status = 'DELIVERED'
  GROUP BY customer_id
  HAVING SUM(gmv) > 10000
);
```

**FROM subquery:** derived table (same idea as a CTE).

**SELECT subquery (correlated):** runs per row — slow; prefer JOIN.

```sql
SELECT o.order_id,
       (SELECT MAX(p.created_at) FROM payments p WHERE p.order_id = o.order_id) AS last_pay
FROM orders o;
```

Fine for small UAT samples; for reporting, join an aggregated payments CTE.

## CTE for readable BA queries (repeat buyers)

```sql
WITH delivered AS (
  SELECT customer_id, order_id, placed_at, gmv
  FROM orders
  WHERE status = 'DELIVERED'
),
buyer_stats AS (
  SELECT
    customer_id,
    COUNT(*) AS delivered_orders,
    MIN(placed_at) AS first_order_at,
    MAX(placed_at) AS last_order_at,
    SUM(gmv) AS gmv
  FROM delivered
  GROUP BY customer_id
)
SELECT c.email, b.delivered_orders, b.gmv, b.first_order_at, b.last_order_at
FROM buyer_stats b
INNER JOIN customers c ON c.customer_id = b.customer_id
WHERE b.delivered_orders >= 2
ORDER BY b.gmv DESC;
```

Talk-through: "First I keep delivered orders, then I count per customer, then I keep count ≥ 2." Interviewers like that.

Chain CTEs instead of nesting five levels.

## Views as business-friendly datasets

```sql
CREATE VIEW v_shop_delivered_orders AS
SELECT
  o.order_id,
  o.customer_id,
  o.gmv,
  o.placed_at,
  o.city,
  c.email
FROM orders o
INNER JOIN customers c ON c.customer_id = o.customer_id
WHERE o.status = 'DELIVERED';
```

BAs often **cannot** CREATE VIEW in prod. You still **use** views: `v_kyc_pending`, `v_claims_open`. Ask the data team for a view when the same join is used in three reports.

| Object | Who changes it | BA use |
|---|---|---|
| CTE | In your query | One-off analysis |
| View | DBA / analytics eng | Stable metric grain |
| Table | Source system | Raw facts |

Do not treat a view as raw: it already filters (e.g. test orders removed). Ask for the view definition.

## Real-world examples

1. **NovaBank**: CTE of `latest_kyc_status` per customer (`ROW_NUMBER` if allowed) then filter pending.
2. **QuickBite**: view `v_late_orders` so ops and BA use one definition of late.

## Scenario / Use case

ShieldSure ops: **claims open > 30 days with no document uploaded.**

Tables: `claims(claim_id, status, opened_at)`, `claim_documents(doc_id, claim_id, uploaded_at)`.

```sql
WITH open_claims AS (
  SELECT claim_id, opened_at, CURRENT_DATE - opened_at::date AS age_days
  FROM claims
  WHERE status IN ('OPEN', 'QUERY')
),
with_docs AS (
  SELECT DISTINCT claim_id
  FROM claim_documents
  WHERE uploaded_at IS NOT NULL
)
SELECT oc.claim_id, oc.age_days
FROM open_claims oc
LEFT JOIN with_docs d ON d.claim_id = oc.claim_id
WHERE oc.age_days > 30
  AND d.claim_id IS NULL
ORDER BY oc.age_days DESC;
```

The BA pastes 87 keys into the war-room. Product writes a story: reminder SMS at day 7 and a dashboard filter. If this query is weekly, request view `v_claims_open_no_docs`.

Subquery form of the same (harder to read):

```sql
SELECT claim_id
FROM claims c
WHERE status IN ('OPEN', 'QUERY')
  AND CURRENT_DATE - opened_at::date > 30
  AND NOT EXISTS (
    SELECT 1 FROM claim_documents d
    WHERE d.claim_id = c.claim_id
      AND d.uploaded_at IS NOT NULL
  );
```

`NOT EXISTS` is often safer than `NOT IN` with NULLs.

## Weak vs strong

| Weak | Strong |
|---|---|
| One 80-line nested SELECT | Named CTEs per grain |
| Correlated subquery on 8M rows | Aggregate then join |
| Secret Excel extract | Shared view definition |
| `NOT IN` (nullable ids) | `NOT EXISTS` or LEFT JOIN |
| View assumed = all rows | Read the WHERE in the view |
| Repeat buyer = two rows in dump | CTE with COUNT ≥ 2 |

## Notes

- CTE is not faster by magic; it is clearer. Clarity prevents wrong metrics.
- You do not need DBA depth; you need to read `WITH` and `CREATE VIEW`.
- `NOT EXISTS` vs LEFT JOIN IS NULL — both are "anti-join"; pick one style.
- If the company forbids `CREATE VIEW`, save SQL on Confluence as the "virtual view".
- Window functions (`ROW_NUMBER`) are a plus, not required for entry-level, but "latest row per id" is a common CTE pattern.
- Document parameters: "open" statuses, 30 calendar days vs business days.
- Re-run the count the day you present; aging queries move every night.
