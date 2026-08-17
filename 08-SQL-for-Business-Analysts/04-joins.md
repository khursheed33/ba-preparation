# SQL Joins for Business Analysts

## Definition

A **JOIN** combines rows from two tables using a key. **INNER JOIN** keeps matches only. **LEFT JOIN** keeps all left rows and matching right rows (NULL if none). **RIGHT JOIN** is the reverse (BAs rarely need it — swap tables and LEFT). A **self join** joins a table to itself (manager, original order). **Multiple-table queries** chain joins along the ER path.

Joins implement the relationships from the database fundamentals note.

## Why it matters

"Customers with orders" vs "orders without payments" are different joins. The **fan-out trap** (row explosion) makes GMV look 3× because you joined `order_items` and then `SUM(orders.gmv)`.

## Venn-style meaning

| Join | Keeps |
|---|---|
| INNER | In both (customers who placed at least one order) |
| LEFT | All left + matches (all orders, payment if any) |
| RIGHT | All right + matches |
| FULL OUTER | All from either (less common in BA work) |

There is no "OUTER JOIN" without LEFT/RIGHT/FULL. People say "outer" meaning LEFT.

## ShopEase examples

**INNER: customers with orders**

```sql
SELECT c.customer_id, c.email, o.order_id, o.gmv
FROM customers c
INNER JOIN orders o ON o.customer_id = c.customer_id;
```

Customers with zero orders disappear.

**LEFT: orders without a successful payment**

```sql
SELECT o.order_id, o.gmv, o.status, p.payment_id, p.status AS pay_status
FROM orders o
LEFT JOIN payments p
  ON p.order_id = o.order_id
 AND p.status = 'SUCCESS'
WHERE p.payment_id IS NULL;
```

Note: the `SUCCESS` filter is on the **ON** clause, not WHERE. If you put `p.status = 'SUCCESS'` in WHERE, the LEFT JOIN becomes an INNER JOIN (NULL status fails the WHERE).

**LEFT vs INNER for payments**

```sql
-- All orders, pay info if present
FROM orders o
LEFT JOIN payments p ON p.order_id = o.order_id;

-- Only orders that have some payment row
FROM orders o
INNER JOIN payments p ON p.order_id = o.order_id;
```

**RIGHT JOIN** (same as LEFT with flipped tables):

```sql
SELECT *
FROM payments p
RIGHT JOIN orders o ON p.order_id = o.order_id;
```

Prefer LEFT for readability.

## Self joins

**NovaBank employees: staff and manager**

```sql
SELECT e.emp_id, e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m ON m.emp_id = e.manager_id;
```

LEFT so the CEO (no manager) still appears.

**ShopEase returns vs original order** (or replacement order):

```sql
SELECT r.return_id, orig.order_id AS original_order, repl.order_id AS replacement_order
FROM returns r
INNER JOIN orders orig ON orig.order_id = r.order_id
LEFT JOIN orders repl ON repl.order_id = r.replacement_order_id;
```

Self join is "same table, two roles".

## Multiple-table query

```sql
SELECT
  c.email,
  o.order_id,
  i.sku,
  i.qty,
  p.status AS pay_status
FROM customers c
INNER JOIN orders o ON o.customer_id = c.customer_id
INNER JOIN order_items i ON i.order_id = o.order_id
LEFT JOIN payments p ON p.order_id = o.order_id AND p.status = 'SUCCESS'
WHERE o.placed_at >= DATE '2026-08-01';
```

Grain is now **order line**, not order. Do not `SUM(o.gmv)` here.

## Fan-out trap (row explosion)

`orders` 1 row GMV = 1000, two `order_items`, three `payments` attempts.

```sql
SELECT o.order_id, SUM(o.gmv) AS wrong_gmv
FROM orders o
JOIN order_items i ON i.order_id = o.order_id
GROUP BY o.order_id;
```

`wrong_gmv` = 2000. You summed the order GMV once per item.

**Fix:** aggregate children first, then join; or `SUM(i.line_gmv)`; or `COUNT(DISTINCT o.order_id)` with `SUM(DISTINCT o.gmv)` — `SUM(DISTINCT)` is dangerous if two orders share GMV. Prefer:

```sql
SELECT o.order_id, o.gmv, COALESCE(s.item_count, 0) AS item_count
FROM orders o
LEFT JOIN (
  SELECT order_id, COUNT(*) AS item_count
  FROM order_items
  GROUP BY order_id
) s ON s.order_id = o.order_id;
```

If GMV looks "too big" vs finance, suspect fan-out before suspecting fraud.

## Real-world examples

1. **MediCare+**: patients LEFT JOIN next appointment — uncovered in SELECT file.
2. **QuickBite**: restaurants INNER JOIN orders — inactive restaurants with no orders drop out; use LEFT if you need zero-order restaurants.

## Scenario / Use case

ShopEase finance: "Paid orders missing from collections." BA runs LEFT JOIN payments SUCCESS. 600 COD orders have no payment row (COD settles later). 40 prepaid orders have only FAILED attempts. Requirement: collections metric = SUCCESS payments + COD in `DELIVERED`. Join taught the metric, not "SQL is wrong".

## Weak vs strong

| Weak | Strong |
|---|---|
| Filter right table in WHERE on a LEFT JOIN | Filter in ON, then `WHERE right.key IS NULL` |
| `SUM(order.gmv)` after joining items | Aggregate to order grain first |
| INNER when you need "without" | LEFT + IS NULL |
| Join on names | Join on ids |
| RIGHT JOIN for style | LEFT JOIN, left table = the one you keep |

## Notes

- Say the grain after every join: order, item, or payment attempt.
- Multiple SUCCESS payments (retries) can also fan-out — `DISTINCT ON` / qualify latest payment.
- Draw two circles; pick INNER vs LEFT before you type.
- `USING (order_id)` is shorthand when names match.
- Self join aliases must be readable (`e`, `m`).
- Entry-level BA: INNER, LEFT, and fan-out awareness are the interview bar.
- If counts jump after a join, you exploded rows — do not publish.
