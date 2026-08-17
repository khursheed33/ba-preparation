# Aggregates, GROUP BY, HAVING, and CASE

## Definition

**Aggregate functions** collapse many rows into one value: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`. `GROUP BY` splits the collapse by a dimension (city, status). `HAVING` filters **after** aggregation. `CASE` maps values or **buckets** (TAT 0–1 / 2–3 / 4+).

This is how a BA computes GMV, AOV, return rate, and approval rate in SQL instead of a one-off pivot.

## Why it matters

Stakeholders argue anecdotes. Aggregates with a defined grain ("one row per order") are the shared number. `HAVING` vs `WHERE` mistakes drop the wrong rows.

## Core functions

```sql
SELECT
  COUNT(*)                    AS order_rows,
  COUNT(delivered_at)         AS delivered_with_timestamp,
  COUNT(DISTINCT customer_id) AS unique_customers,
  SUM(gmv)                    AS gmv,
  AVG(gmv)                    AS aov_if_one_row_per_order,
  MIN(placed_at)              AS first_ts,
  MAX(placed_at)              AS last_ts
FROM orders
WHERE placed_at >= DATE '2026-08-01'
  AND placed_at <  DATE '2026-09-01';
```

`COUNT(*)` counts rows. `COUNT(column)` skips NULL. `COUNT(DISTINCT …)` counts unique keys.

## Metrics

| Metric | Idea | Sketch |
|---|---|---|
| GMV | Sum of order value | `SUM(gmv)` on delivered (define cancelled) |
| AOV | GMV / order count | `SUM(gmv)/COUNT(*)` |
| Return rate | Returned / delivered | `SUM(CASE WHEN status='RETURNED' THEN 1 ELSE 0 END)*1.0 / SUM(CASE WHEN status='DELIVERED' THEN 1 ELSE 0 END)` |
| Approval rate | Approved / submitted | ShieldSure claims |

```sql
SELECT
  SUM(gmv) FILTER (WHERE status = 'DELIVERED') AS delivered_gmv,  -- PostgreSQL
  SUM(CASE WHEN status = 'DELIVERED' THEN gmv ELSE 0 END) AS delivered_gmv_ansi
FROM orders;
```

## WHERE vs HAVING

| | WHERE | HAVING |
|---|---|---|
| When | Before groups | After aggregates |
| Example | Only delivered rows | Cities with GMV > 1,00,000 |
| Can use `SUM`? | No | Yes |

```sql
SELECT city, SUM(gmv) AS gmv
FROM orders
WHERE status = 'DELIVERED'      -- row filter
GROUP BY city
HAVING SUM(gmv) > 100000        -- group filter
ORDER BY gmv DESC;
```

Wrong: `WHERE SUM(gmv) > 100000` — SQL error.

Every non-aggregated selected column must be in `GROUP BY`.

## CASE for TAT buckets

```sql
SELECT
  CASE
    WHEN tat_days <= 1 THEN '0-1 day'
    WHEN tat_days BETWEEN 2 AND 3 THEN '2-3 days'
    ELSE '4+'
  END AS tat_bucket,
  COUNT(*) AS claims
FROM claims
WHERE closed_at IS NOT NULL
GROUP BY 1
ORDER BY 1;
```

NovaBank KYC TAT similarly on `NETWORK` days if computed in SQL (`tat_days` as a column or expression).

## Real-world examples

1. **ShopEase** AOV by city: `GROUP BY city` with `WHERE status='DELIVERED'`.
2. **NovaBank** approval rate by channel: `AVG(CASE WHEN status='APPROVED' THEN 1.0 ELSE 0 END)`.

## Scenario / Use case

QuickBite wants restaurant rating buckets for a "boost low-rated" story. Table `restaurants(id, name, city, rating)` where rating is 1.00–5.00.

```sql
SELECT
  CASE
    WHEN rating < 3.0 THEN 'below_3'
    WHEN rating < 4.0 THEN '3_to_4'
    WHEN rating < 4.5 THEN '4_to_4.5'
    ELSE '4.5_plus'
  END AS rating_bucket,
  COUNT(*) AS restaurants,
  AVG(rating) AS avg_rating
FROM restaurants
WHERE is_active = TRUE
GROUP BY 1
ORDER BY 1;
```

Result: 12% `below_3`. PO wanted to boost all below 4.0 — that is 40% of the marketplace (too many). The BA uses `HAVING COUNT(*)` on cities:

```sql
SELECT city, COUNT(*) AS low_rated
FROM restaurants
WHERE is_active = TRUE AND rating < 3.0
GROUP BY city
HAVING COUNT(*) >= 10
ORDER BY low_rated DESC;
```

Scope becomes "cities with at least 10 restaurants below 3" — a requirement change driven by SQL.

## Weak vs strong

| Weak | Strong |
|---|---|
| AOV = `AVG(gmv)` including cancelled | Filter or CASE the denominator |
| `WHERE COUNT(*) > 5` | `HAVING COUNT(*) > 5` |
| `SELECT city, gmv` without GROUP BY | `GROUP BY city` |
| Return rate vs GMV | Count or value — say which |
| `COUNT(email)` as customers | `COUNT(*)` vs `COUNT(email)` vs DISTINCT |
| Buckets in Excel only | `CASE` so BI matches UAT |

## Notes

- Write the metric definition above the query (delivered only? tax in GMV?).
- `AVG` of a 0/1 CASE is a rate — clean and interview-friendly.
- `GROUP BY 1` (ordinal) is handy; some style guides prefer column names.
- NULL `rating` falls into `ELSE` — filter `rating IS NOT NULL` or add a bucket.
- Do not `GROUP BY` a timestamp if you meant a date: `CAST(placed_at AS DATE)`.
- Fan-out joins before `SUM` will explode GMV — next lesson.
- Entry-level BA: GROUP BY + CASE is enough for most interview metric questions.
