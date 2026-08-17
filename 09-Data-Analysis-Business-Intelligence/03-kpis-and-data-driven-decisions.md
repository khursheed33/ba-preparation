# KPIs, Metrics, and Data-Driven Decisions

## Definition

A **metric** is any measured number the business can track (page views, tickets opened, GPS pings).

A **business metric** is a metric tied to how the company makes money, serves customers, or controls risk (GMV, NPA, claim ratio, no-show rate).

A **KPI (Key Performance Indicator)** is a small set of metrics chosen because they tell you whether an *objective* is being achieved. “Key” means few, owned, and used to decide.

A **vanity metric** is easy to move and looks impressive, but does not change a decision or outcome (raw downloads, GPS pings, likes).

**Root-cause analysis (RCA)** is a structured hunt for *why* a KPI moved, not a list of guesses.

**Data-driven decision making** means options are compared using evidence and agreed definitions — then someone still makes a judgment. Data informs; it does not replace ownership.

## Why it matters

Teams drown in dashboards and still argue. ShopEase tracks 80 charts; nobody knows if checkout is healthy. QuickBite “improves delivery” by watching rider GPS pings while food sits in the bag. MediCare+ celebrates appointment volume while no-shows destroy doctor utilization.

A BA’s job is to connect **objective → KPI → diagnostic metrics → action**.

## KPI vs metric vs vanity metric

| | Metric | KPI | Vanity metric |
|---|---|---|---|
| Count | Many | Few (3–7 per objective) | Often one flashy number |
| Tied to objective? | Maybe | Must be | Rarely |
| Action if it moves? | Investigate | Yes — owner must respond | Usually “nice” |
| Example | ShopEase sessions | Checkout conversion, on-time ship | Homepage hits |

**Good KPI tests**

| Test | Question |
|---|---|
| Aligned | Does this measure the objective (revenue, risk, experience)? |
| Measurable | Can we get a trusted numerator and denominator? |
| Owned | Named person or team who can change it? |
| Time-bound | Reviewed on a cadence (daily ops vs monthly board)? |
| Limited | If we have 25 “KPIs,” we have none |

Leading vs lagging: rider acceptance time *leads* on-time delivery; monthly NPS *lags*. Use both; do not steer only on lagging praise.

### Weak vs strong

| Weak | Strong |
|---|---|
| Improve delivery. | Raise on-time % (promised window) from 78% to 90% in 8 weeks; owner: logistics lead. |
| Track engagement. | % of riders with ping in last 60s — not a customer KPI. |
| We are data-driven. | Decision log: option A vs B, metric, sample, date, owner. |
| RCA: “ops issue.” | 5 Whys + split by city, restaurant prep vs rider wait vs traffic. |

## Scorecards

Use a short scorecard: objective, KPI, target, owner, diagnostic metrics.

### ShopEase (e-commerce)

| Objective | KPI | Target (example) | Owner | Diagnostics |
|---|---|---|---|---|
| Grow profitable orders | Contribution margin / order | ≥ ₹42 | Finance + category | AOV, discount %, return % |
| Convert demand | Checkout conversion | ≥ 3.2% | Product | Funnel step drop-off |
| Keep promise | On-time dispatch | ≥ 95% | Fulfilment | SLA by warehouse |
| Reduce pain | Return rate (units) | ≤ 8% | Quality + CX | Reason codes |

### NovaBank

| Objective | KPI | Target | Owner | Diagnostics |
|---|---|---|---|---|
| Grow quality book | Disbursal vs plan | ±5% | Credit + sales | Funnel: apply → sanction → disburse |
| Control risk | 30+ DPD in first 6 months | ≤ 2.5% | Risk | Segment, channel, score band |
| Speed | Median sanction TAT | ≤ 48h retail | Ops | Queue time vs decision time |
| Compliance | KYC STP % | ≥ 70% | Ops + compliance | Exception reasons |

### MediCare+

| Objective | KPI | Target | Owner | Diagnostics |
|---|---|---|---|---|
| Use capacity | Slot utilization | 80–90% | Clinic ops | No-show %, overbook % |
| Access | Median days to next slot | ≤ 7 specialist | Admin | By specialty |
| Experience | Wait after check-in | Median ≤ 15 min | Floor manager | Arrival vs start |
| Safety / privacy | Access audit exceptions | 0 Sev1 | IT + compliance | EMR access logs |

## Root-cause analysis (BA pattern)

1. Confirm the KPI definition and data quality.
2. Split: time, geography, segment, channel, product.
3. Walk the process (As-Is) at the worst slice.
4. Separate volume mix vs rate change (NovaBank ticket mix vs true risk).
5. Propose 1–2 interventions with expected KPI movement.
6. Define how you will know it worked (holdout, before/after with caveats).

## Real-world examples

**ShieldSure.** Combined ratio is a true business KPI. “Number of claims logged” is a volume metric. “Dashboard views by executives” is vanity.

**SaaS / EdTech.** MRR and logo churn are KPIs. Login count without learning outcome is often vanity.

**Government / HR.** Time-to-hire can be a KPI; “resumes in the portal” is vanity if quality is unmeasured.

## Scenario / Use case: QuickBite “improve delivery” tracks GPS pings

**Context.** City manager: “Delivery is the problem. Track riders more.” Engineering ships a live map. Ops celebrates 99% of riders sending GPS pings every 10 seconds. Customer on-time % stays 76%. Food is ready 18 minutes before pickup in some kitchens; riders wait; then they speed. Complaints mention cold food, not “no GPS.”

**Vanity vs KPI.**

| Tracked | Type | Why it fails |
|---|---|---|
| GPS pings / rider / hour | Vanity | Measures device health, not customer promise |
| On-time % vs promised window | KPI | Matches the customer contract |
| Food-ready time (kitchen stamped) | Diagnostic | Shows wait is restaurant vs rider |
| Rider wait at store | Diagnostic | Action: batching, prep SLA, pickup SLA |

**What the BA does.**

1. Restate the objective: customers receive food within the promised window, hot.
2. Replace ping volume with on-time % (owned by city ops) and food-ready accuracy (owned by restaurant success).
3. RCA in one city: 41% of late orders had food-ready > 12 min after rider arrival; 29% had no rider assigned in 3 min; 18% rain + distance.
4. Requirements: kitchen “ready” event, promised window on the ticket, alerts on wait > 8 min — not more map dots.

**If ignored.** QuickBite spends on telemetry, riders feel surveilled, restaurants are never measured, and the KPI that customers feel does not move.

## Notes

- A KPI is a chosen metric with an objective, owner, and target — not a synonym for “chart.”
- Vanity metrics are not evil; they are the wrong steering wheel.
- Scorecards beat 40-tile dashboards.
- RCA starts with definition and splits, not with a tool.
- Data-driven means a decision log, not more slides.
- Leading indicators help you act before the lagging KPI prints.
- If nobody owns it, it is not a KPI.
- Never improve a metric by changing its definition without a version note.
