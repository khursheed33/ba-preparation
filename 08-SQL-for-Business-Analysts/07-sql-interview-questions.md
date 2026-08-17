# SQL Interview Questions for Business Analysts

## Definition

Interview SQL for BAs tests whether you can **query**, **join**, **aggregate**, and **validate a business rule** — not whether you can tune indexes or design partitions. Interviewers want to hear you **talk through grain, NULL, and the business question** while you write.

## Why it matters

Many BA JDs list SQL. You will be given a whiteboard or a sample schema (orders, customers). Strong answers sound like: "One row is an order; I will LEFT JOIN payments so I keep unpaid orders."

## How to talk through a query in an interview

1. Restate the question in business words ("customers who never ordered").
2. Name tables and **grain**.
3. INNER vs LEFT and why.
4. Filters (`WHERE` vs `HAVING`).
5. NULL handling.
6. Write SQL slowly; say each clause.
7. Give a sanity check ("count should be ≤ number of customers").

Do not freeze for perfect syntax. `LIMIT` vs `TOP` — say "I'll use LIMIT; in SQL Server I'd use TOP".

## Twelve questions with answers

**1. Second-highest GMV order**

Why they ask: ranking without panicking.

```sql
SELECT MAX(gmv) AS second_highest
FROM orders
WHERE gmv < (SELECT MAX(gmv) FROM orders);
```

Or `DENSE_RANK()` if allowed. Mention ties: two orders share max → second is the next value.

**2. Find duplicate emails**

Why: data quality / keys.

```sql
SELECT email, COUNT(*) AS n
FROM customers
GROUP BY email
HAVING COUNT(*) > 1;
```

Add `email IS NOT NULL`.

**3. Customers with no orders (leftover customers)**

Why: LEFT JOIN / anti-join.

```sql
SELECT c.customer_id, c.email
FROM customers c
LEFT JOIN orders o ON o.customer_id = c.customer_id
WHERE o.order_id IS NULL;
```

**4. Running total lite (GMV by day cumulative)**

Why: they test if you know windows *or* a honest subset.

```sql
SELECT
  d,
  daily_gmv,
  SUM(daily_gmv) OVER (ORDER BY d) AS running_gmv
FROM (
  SELECT CAST(placed_at AS DATE) AS d, SUM(gmv) AS daily_gmv
  FROM orders
  WHERE status = 'DELIVERED'
  GROUP BY 1
) t;
```

If windows are unknown: "I would sum in Excel from a daily GROUP BY" — then learn the OVER clause.

**5. INNER vs LEFT JOIN**

Why: the most failed BA SQL question.

Say: INNER = matches only; LEFT = all from left. Example: orders without payments = LEFT JOIN payments WHERE payment_id IS NULL.

**6. GROUP BY mistake**

Why: they want you to catch `SELECT city, gmv FROM orders GROUP BY city`.

Answer: `gmv` must be `SUM(gmv)` (or also in GROUP BY, which is wrong grain).

**7. NULL: `= NULL` vs `IS NULL`**

Why: silent empty results.

Answer: `WHERE email = NULL` is never true; use `IS NULL`. `<>` does not return NULLs.

**8. DELETE vs TRUNCATE (conceptual)**

Why: they check you will not pretend to be a DBA but you know risk.

| | DELETE | TRUNCATE |
|---|---|---|
| What | Remove rows, can `WHERE` | Empty table, no row filter (typical) |
| Rollback | Yes in a transaction (engine-dependent) | Often not fully logged |
| BA | Never run on prod | Never |

Say: "I would not run either in an interview DB without asking; conceptually DELETE is row-level, TRUNCATE is bulk reset."

**9. COUNT(*) vs COUNT(column)**

Why: missing emails.

`COUNT(*)` = rows; `COUNT(email)` = non-null emails.

**10. HAVING vs WHERE**

Why: filter groups.

"Cities with more than 100 orders" = `GROUP BY city HAVING COUNT(*) > 100`. Date filter = WHERE.

**11. Fan-out / double-counting GMV**

Why: real BA production bug.

"If I join order_items and SUM(orders.gmv), GMV multiplies by line count. I aggregate items first or sum line_gmv."

**12. Explain a query you'd write for X**

Why: product sense + SQL.

Example X: **QuickBite — % late orders by city last 7 days.**

Talk: grain = delivery_order; late = `actual_min > promised_min`; filter last 7 days; `GROUP BY city`; rate = late / all.

```sql
SELECT
  city,
  COUNT(*) AS orders,
  SUM(CASE WHEN actual_min > promised_min THEN 1 ELSE 0 END) AS late_orders,
  SUM(CASE WHEN actual_min > promised_min THEN 1 ELSE 0 END) * 1.0
    / COUNT(*) AS late_pct
FROM delivery_orders
WHERE delivered_at >= CURRENT_DATE - INTERVAL '7 days'
GROUP BY city
ORDER BY late_pct DESC;
```

Other good X: ShopEase return rate by category; NovaBank OTP exceptions > 10,000; MediCare+ patients with no future appt; ShieldSure claims open > 30 days no docs.

## Real-world examples (how interviews map to work)

1. Leftover customers = MediCare+ no next appointment (same anti-join).
2. Duplicates = ShopEase double customer accounts from guest checkout.

## Scenario / Use case

Interviewer: "ShopEase finance says GMV is 20% high vs yesterday's dashboard. What do you query?"

Talk: recon count/sum by status; check cancelled included; check join to items fan-out; check timezone (IST vs UTC date). Write unmatched-status breakdown, not a random `SELECT *`. That answer hires you more than a perfect window function.

## Weak vs strong

| Weak | Strong |
|---|---|
| Silent coding | Grain + join type spoken |
| Memorised 2nd-max only | Ties and NULL mentioned |
| "TRUNCATE is faster" as if you'll use it | "I wouldn't run it; here's the difference" |
| `NOT IN` without NULL talk | LEFT JOIN / NOT EXISTS |
| Fancy SQL, wrong metric | Simple SQL, defined late/GMV |
| Panic on dialect | State PostgreSQL vs SQL Server |

## Notes

- Practice on `customers` / `orders` / `order_items` until joins are muscle memory.
- Entry-level BA: querying, joins, aggregation, and business validation are essential; not DBA depth.
- If you do not know a function, describe the result set you need.
- Ask whether `gmv` includes tax and cancelled orders — that is a BA moving.
- Write keywords in CAPS so the interviewer can scan.
- After the query, propose a check: `SUM(late_pct * orders)` vs overall late %.
- Bring one story: "I found cancelled orders in collections recon" — Phase 8 in one sentence.
