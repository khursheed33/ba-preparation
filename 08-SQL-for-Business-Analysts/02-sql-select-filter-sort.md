# SQL SELECT, Filter, Sort, and NULL

## Definition

**SQL** is the language to ask a relational database questions. `SELECT` lists columns. `FROM` names the table. `WHERE` filters rows. `ORDER BY` sorts. `DISTINCT` removes duplicate result rows. `LIMIT` / `TOP` / `FETCH` cap rows. **Operators** compare values (`=`, `<>`, `>`, `IN`, `LIKE`, `BETWEEN`). **NULL** means unknown — it is not `0` and not `''`.

A BA uses SQL to pull evidence: who is active, what failed, what is missing.

## Why it matters

Exports to Excel go stale. A saved query answers "failed payments yesterday" in seconds. NULL mistakes (`= NULL`) make you report zero missing emails when thousands are missing.

## SQL fundamentals (shape of a query)

```sql
SELECT column_or_expr
FROM table
WHERE condition
ORDER BY column
LIMIT n;
```

Logical order to think: FROM → WHERE → SELECT → DISTINCT → ORDER BY → LIMIT. (GROUP BY comes later.)

## Ten queries a BA actually runs

ShopEase / generic names; adjust schema.

**1. Active users (logged in last 30 days)**

```sql
SELECT customer_id, email, last_login_at
FROM customers
WHERE last_login_at >= CURRENT_DATE - INTERVAL '30 days'
ORDER BY last_login_at DESC;
```

**2. Orders last 7 days**

```sql
SELECT order_id, customer_id, gmv, status, placed_at
FROM orders
WHERE placed_at >= CURRENT_TIMESTAMP - INTERVAL '7 days'
ORDER BY placed_at DESC;
```

**3. Failed payments**

```sql
SELECT payment_id, order_id, amount, method, failure_code, created_at
FROM payments
WHERE status = 'FAILED'
ORDER BY created_at DESC
LIMIT 100;
```

**4. Null email**

```sql
SELECT customer_id, phone, created_at
FROM customers
WHERE email IS NULL;
```

**5–10. Distinct, IN, LIKE, high-value, date range, not cancelled**

```sql
SELECT DISTINCT status FROM orders ORDER BY 1;

SELECT txn_id, account_id, amount FROM transfers
WHERE amount > 10000 AND status = 'SUCCESS';          -- NovaBank

SELECT return_id, order_id, reason FROM returns
WHERE reason LIKE '%damaged%';

SELECT order_id, city FROM delivery_orders
WHERE city IN ('Pune', 'Mumbai', 'Hyderabad')
  AND delivered_at IS NOT NULL;                       -- QuickBite

SELECT * FROM orders
WHERE placed_at >= DATE '2026-08-01'
  AND placed_at <  DATE '2026-09-01';                 -- prefer over BETWEEN on timestamps

SELECT order_id, gmv FROM orders
WHERE status <> 'CANCELLED' AND gmv >= 500;
```

## Operators and NULL traps

| Predicate | Matches NULL? |
|---|---|
| `email = NULL` | **Never.** SQL result is unknown. Use `IS NULL`. |
| `email <> 'a@b.com'` | Does **not** include NULL emails. |
| `email IS NULL` | Missing emails. |
| `email IS NOT NULL` | Present emails. |
| `COALESCE(email, 'unknown')` | Display substitute, not a stored fix. |
| `status IN ('A', NULL)` | NULL in IN is a trap; avoid. |

```sql
-- WRONG: always empty
SELECT * FROM customers WHERE email = NULL;

-- RIGHT
SELECT * FROM customers WHERE email IS NULL;
```

`WHERE city = 'Pune' OR city IS NULL` if you need Pune plus unknown city.

`LIMIT 100` on exploration; never assume the first 100 are random — `ORDER BY` first.

## Real-world examples

1. **ShopEase** CS: list orders `status = 'DELIVERED'` and `delivered_at IS NULL` — data bug.
2. **ShieldSure**: policies `expiry_date < CURRENT_DATE` AND `status = 'ACTIVE'` — stuck status.

## Scenario / Use case

MediCare+ ops: "Patients without a next appointment." Tables: `patients(patient_id, uhid, status)`, `appointments(appt_id, patient_id, starts_at, status)`. Prefer LEFT JOIN over `NOT IN` (NULL in the subquery can empty the result).

```sql
SELECT p.uhid, p.patient_id
FROM patients p
LEFT JOIN appointments a
  ON a.patient_id = p.patient_id
 AND a.starts_at > CURRENT_TIMESTAMP
 AND a.status IN ('BOOKED', 'CONFIRMED')
WHERE p.status = 'ACTIVE'
  AND a.appt_id IS NULL;
```

The BA finds 1,204 patients. SME says some are "follow-up not required". New requirement: `care_plan.needs_followup = TRUE`. The query was the workshop, not the final KPI.

## Weak vs strong

| Weak | Strong |
|---|---|
| `WHERE email = NULL` | `IS NULL` |
| `SELECT *` in production reports | Explicit columns |
| `BETWEEN` timestamps | `>= start AND < next day` |
| `NOT IN` with nullable column | `LEFT JOIN … IS NULL` |
| No `ORDER BY` with `LIMIT` | Sort then cap |
| Distinct by eye in Excel | `SELECT DISTINCT` |

## Notes

- Confirm date timezone with the DBA (UTC vs IST) before "yesterday".
- `LIKE '%x%'` cannot use indexes well; fine for BA exploration, not a 10M-row habit without help.
- `<> 'CANCELLED'` drops NULL statuses; include `OR status IS NULL` if needed.
- Save queries in Confluence with the business question above them.
- `LIMIT` is for sampling; counts need a full `COUNT(*)`.
- Entry-level BA: filtering and NULL literacy matter more than fancy SQL.
- Always run `COUNT(*)` of the same WHERE before you send a list to ops.
