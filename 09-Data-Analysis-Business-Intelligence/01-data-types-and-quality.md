# Data Types and Data Quality

## Definition

**Data** is recorded facts about the business. A BA uses data to test claims, size problems, and define what “good” looks like.

**Data types** (for analysis, not programming):

| Type | Meaning | Example |
|---|---|---|
| Quantitative | Numbers you can count or measure | Order value, wait time, claim amount |
| Qualitative | Labels, text, categories | Order status, complaint reason, product category |
| Discrete | Countable integers | Number of items in a cart |
| Continuous | Measured on a scale | Delivery minutes, temperature of a cold-chain van |
| Categorical | Named groups | Payment method: UPI, card, COD |
| Temporal | Dates and times | Order placed at, appointment start |

**Structured vs unstructured**

| Kind | Shape | Examples |
|---|---|---|
| Structured | Rows and columns, fields with meaning | ShopEase `orders` table, NovaBank loan ledger, MediCare+ appointment slots |
| Semi-structured | Some tags or keys, not a full table | JSON from QuickBite rider app, ShieldSure claim XML |
| Unstructured | No fixed fields | Call recordings, emails, product reviews, WhatsApp chats, scanned prescriptions |

A BA often starts with structured tables, then uses unstructured text (reviews, tickets) to explain *why* the numbers moved.

## Why it matters

Bad data produces confident, wrong decisions. Dashboards look official. Leadership acts. The process stays broken.

If unique users are inflated, conversion looks worse than it is. If missing delivery timestamps are treated as on-time, QuickBite “improves” a metric that operations never felt. If ShieldSure claim amounts are inconsistent across systems, reserves and SLAs both lie.

## Data quality dimensions

| Dimension | Question | Failure example |
|---|---|---|
| Accuracy | Is the value true? | ShopEase “delivered” but the parcel is still at the hub |
| Completeness | Are required fields filled? | MediCare+ appointment with no doctor ID |
| Consistency | Do systems agree? | NovaBank core vs CRM show different KYC status |
| Timeliness | Is it fresh enough to act? | Yesterday’s inventory used for today’s ShopEase flash sale |
| Uniqueness | Is each real-world thing counted once? | Two customer IDs for one phone number |

## Data cleaning, missing data, duplicates, outliers, validation

**Data cleaning** is the work of finding and fixing (or flagging) quality issues before you trust a number. BAs do not become data engineers, but they must know *what* to ask for and *what not to believe*.

| Issue | What it looks like | Typical BA response |
|---|---|---|
| Missing data | Null phone, blank GSTIN, no delivery time | Ask: is it optional, a capture bug, or a process skip? Do not silently fill with zero |
| Duplicate data | Same order twice, same customer twice | Define the business key (phone + email, order_id) and a survivorship rule |
| Outliers | One ₹2 crore order in a ₹800 AOV catalog | Split segments (B2B vs B2C) before averaging |
| Validation | Value fails a rule | Status cannot be “shipped” if payment_status is “failed” |

**Validation** is checking data against rules: type, range, mandatory fields, cross-field logic, and source-to-source reconciliation.

### Weak vs strong

| Weak | Strong |
|---|---|
| “The unique user number looks high.” | “Unique users are counted on `customer_id`. 18% of phones map to 2+ IDs. Unique users are inflated ~14%.” |
| “Clean the data.” | “Deduplicate on phone+email; keep the ID with the latest successful order; log merged IDs.” |
| “Some deliveries have no timestamp.” | “12% of delivered orders have null `delivered_at`. Treat as incomplete, not on-time.” |
| “Ignore outliers.” | “Exclude corporate wholesale from B2C AOV; report them on a separate KPI.” |

## Real-world examples

**ShopEase (e-commerce).** Reviews are unstructured. Star ratings are structured. If you only chart average stars, you miss that “late delivery” appears in 40% of 1-star text.

**NovaBank.** Structured core-banking balances plus unstructured call recordings from the collections team. A “promise to pay” in a call is not in the ledger until someone codes it.

**QuickBite.** Rider GPS pings are high-volume structured events. Customer complaint emails are unstructured. On-time % needs both: a timestamp *and* a definition of the promised window.

**Telecom / SaaS.** CDR (call detail records) and subscription invoices are structured. Chat transcripts about “bill shock” are unstructured — that is often where the real requirement lives.

## Scenario / Use case: ShopEase duplicate customer IDs inflate unique users

**Context.** Growth reports “unique monthly users” up 22% after a login redesign. Conversion (orders / unique users) fell. Marketing celebrates traffic. Product panics. Finance says CAC looks worse.

**What is going on.** Guest checkout creates a new `customer_id` every time if the buyer does not log in. The same phone now has 3–7 IDs. A later “link account” feature did not back-merge history. Unique users are not unique people.

**Stakeholders.** Growth, product, CRM, data engineering, finance, customer support.

**What the BA does.**

1. Define the entity: a *customer* is a person identified by verified mobile (primary) and email (secondary), not by `customer_id`.
2. Profile duplicates: count IDs per phone, per email, and IDs with both null.
3. Separate missing vs duplicate vs true new users.
4. Write a quality rule: uniqueness on verified mobile; guest IDs are *sessions*, not users, until merge.
5. Change the KPI definition in the dashboard *and* in the BRD for the identity project.

**Sample finding.**

| Metric (old) | Metric (after dedupe) | Effect |
|---|---|---|
| Unique users 1.20M | Unique people 1.03M | −14% |
| Conversion 2.1% | Conversion 2.45% | Looks healthier |
| Repeat rate 18% | Repeat rate 26% | Loyalty was hidden |

**If ignored.** ShopEase spends more on ads to “acquire” people it already has, builds a loyalty program on broken IDs, and UAT of “my orders” fails because history is split across accounts.

## BA checklist before trusting a number

1. What is the grain (one row = one order, one click, one claim)?
2. What is the business key for uniqueness?
3. What % is missing on each critical field?
4. Which source is master if CRM and core disagree?
5. Are outliers a data error or a real segment?

## Notes

- Structured tables answer *what happened*. Unstructured text often answers *why*.
- Never average across mixed populations (guests vs logged-in, retail vs corporate).
- Completeness is not the same as accuracy: a filled field can still be wrong.
- Duplicates inflate counts (users, tickets) and deflate rates (conversion, repeat).
- Outliers should be investigated, not auto-deleted.
- Validation rules belong in requirements: “order cannot ship if payment_status ≠ captured.”
- Ask for a data dictionary before you argue about a KPI.
- Quality work is a requirement, not a “data team later” afterthought.
