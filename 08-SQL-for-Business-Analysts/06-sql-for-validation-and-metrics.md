# SQL for Validation, Reconciliation, and Metrics

## Definition

**Data validation** checks that data obeys rules (mandatory fields, allowed statuses). **Reconciliation (recon)** checks two sources agree (counts, amount sums). **Business metrics in SQL** are defined KPIs (GMV, AOV, conversion). **SQL for reporting** is a stable query pattern with period, grain, and filters. **Requirement validation** uses SQL to find **exceptions** to a stated rule (OTP if transfer > 10,000).

This is the BA's highest-value SQL: not "I can JOIN" but "the requirement is false in 2% of rows".

## Why it matters

Finance will not accept a story that "looks right in UAT" if collections ≠ orders. Exceptions to a business rule are either bugs, undocumented policy, or dirty data — all of which change AC.

## Recon: source vs target

Pattern: count and sum both sides, then diffs.

```sql
-- Source: orders (ShopEase checkout DB)
SELECT COUNT(*) AS cnt, SUM(gmv) AS gmv
FROM orders
WHERE placed_at >= DATE '2026-08-01'
  AND placed_at <  DATE '2026-09-01';

-- Target: warehouse / finance mart
SELECT COUNT(*) AS cnt, SUM(gmv) AS gmv
FROM fin_orders
WHERE order_date >= DATE '2026-08-01'
  AND order_date <  DATE '2026-09-01';
```

Row-level recon (keys in A not in B):

```sql
SELECT s.order_id, s.gmv
FROM orders s
LEFT JOIN fin_orders t ON t.order_id = s.order_id
WHERE s.placed_at >= DATE '2026-08-01'
  AND s.placed_at <  DATE '2026-09-01'
  AND t.order_id IS NULL;
```

Also recon **amounts on matched keys**:

```sql
SELECT s.order_id, s.gmv AS src_gmv, t.gmv AS tgt_gmv
FROM orders s
INNER JOIN fin_orders t ON t.order_id = s.order_id
WHERE s.gmv <> t.gmv;
```

Always recon **grain** (order vs item) and **timezone/date** before you escalate.

## Validate a requirement: OTP if transfer > 10,000

NovaBank AC: "Given a successful transfer amount > 10,000, then an OTP challenge exists."

```sql
SELECT t.txn_id, t.account_id, t.amount, t.created_at
FROM transfers t
LEFT JOIN otp_challenges o
  ON o.txn_id = t.txn_id
 AND o.result = 'PASSED'
WHERE t.status = 'SUCCESS'
  AND t.amount > 10000
  AND o.otp_id IS NULL;
```

Zero rows = rule holds in data (for this period). Non-zero = exceptions: staff override, bug, or "amount in paise". Investigate 10 rows before you file 10,000 bugs.

Also the inverse (OTP on small amounts — extra friction):

```sql
SELECT t.txn_id, t.amount
FROM transfers t
INNER JOIN otp_challenges o ON o.txn_id = t.txn_id
WHERE t.amount <= 10000
  AND t.status = 'SUCCESS';
```

## Reporting query pattern

```sql
-- Header comment: metric, grain, period, owner
SELECT
  CAST(o.placed_at AS DATE) AS dt,
  o.city,
  COUNT(*) AS orders,
  SUM(o.gmv) AS gmv,
  SUM(o.gmv) / COUNT(*) AS aov
FROM orders o
WHERE o.status = 'DELIVERED'
  AND o.placed_at >= :start_ts
  AND o.placed_at <  :end_ts
GROUP BY 1, 2
ORDER BY 1, 2;
```

Reuse: same WHERE as the dashboard. Change a filter in Excel only and you will drift from SQL.

## Real-world examples

1. **MediCare+**: validate "no appointment without UHID" — `WHERE uhid IS NULL`.
2. **QuickBite**: recon vendor payout file SUM vs `SUM(order_value)` for delivered.

## Scenario / Use case

ShopEase finance: **collections ≠ orders**. BA recon:

| Check | Orders DB | Payments SUCCESS | Diff |
|---|---|---|---|
| Count | 50,000 | 46,200 | 3,800 |
| SUM amount | ₹4.2 Cr | ₹3.9 Cr | ₹0.3 Cr |

Exception query:

```sql
SELECT o.order_id, o.status, o.gmv, o.payment_method
FROM orders o
LEFT JOIN payments p
  ON p.order_id = o.order_id
 AND p.status = 'SUCCESS'
WHERE o.placed_at >= DATE '2026-08-01'
  AND o.placed_at <  DATE '2026-09-01'
  AND p.payment_id IS NULL;
```

3,100 are `status = 'CANCELLED'` still included in finance's "orders" extract (they used `placed_at` without status). 700 are COD delivered (no SUCCESS row). Finance extract was **wrong**, not gateway. BA changes the reporting requirement: collections vs **non-cancelled prepaid** + **COD delivered**. New AC on the finance mart story. Cancelled orders were the silent extra GMV.

## Weak vs strong

| Weak | Strong |
|---|---|
| "Totals look close" | Count + sum + unmatched keys |
| AC never tested in prod data | Exception query in UAT and first week live |
| Metric in BI ≠ metric in SQL | One pattern, parameters for dates |
| Assume 3,800 missing payments | Slice by status and method |
| Recon different grains | Order vs item documented |
| OTP rule trusted from demo | Query exceptions > 10,000 |

## Notes

- Recon is a requirement activity: define "order" with finance before you code the story.
- Mask account numbers in saved SQL results.
- Small diffs may be rounding (paise); large diffs are status or timezone.
- Requirement validation SQL belongs on the Confluence story spec.
- You are not a DBA: if the query needs a new index, raise it; do not run heavy SQL on prod at peak without approval.
- Entry-level: validation + recon + metrics beat clever window functions.
- When finance and product disagree, bring the unmatched `order_id` list, not an opinion.
