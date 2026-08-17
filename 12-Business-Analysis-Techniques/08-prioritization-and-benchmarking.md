# Prioritization Techniques and Benchmarking

**Prioritization** is how a BA helps the business rank work when not everything can be built. **Benchmarking** compares performance to an internal baseline, a competitor, or an industry KPI so the To-Be target is evidence-based, not a slogan. Together they answer: *what first?* and *how good is good enough?*

## Why it matters

ShieldSure “make claims faster” is not a backlog. If industry motor claim TAT is 7 days and ShieldSure is 18, the gap *justifies* To-Be. If everything is Must, nothing is. Prioritization techniques make trade-offs visible; benchmarking makes the target defensible in a steering meeting.

## Prioritization techniques

### MoSCoW

| Band | Meaning | ShopEase returns example |
|---|---|---|
| Must | Without it, solution fails the objective | Return request + pickup slot + refund status |
| Should | Important, not launch-blocking | Photo upload of damage |
| Could | Nice if capacity remains | Preferred pickup window reminders |
| Won’t (this time) | Explicitly deferred | Instant refund on fashion |

Rule: if > 60% of items are Must, you are not prioritizing — you are labelling.

### Kano

| Type | Customer view | Example |
|---|---|---|
| Basic / Must-be | Expected; absence causes anger | ShieldSure: FNOL number + SMS ack |
| Performance | More is better | Faster claim TAT |
| Delight | Unexpected positive | Proactive garage slot booking |

Do not treat Delight as Must. Basics failing beat any delight feature.

### WSJF lite (Weighted Shortest Job First)

WSJF ≈ (Business value + Time criticality + Risk reduction) ÷ Job size.

Use 1-2-3-5-8. You are not running a bank’s ALM model — you are ranking epics.

| Epic | BV | Time | Risk↓ | Size | WSJF |
|---|---|---|---|---|---|
| Pickup slot | 8 | 5 | 3 | 5 | 3.2 |
| Instant refund fashion | 8 | 3 | 1 | 13 | 0.9 |
| Return reason QA on listing | 5 | 3 | 8 | 3 | 5.3 |

Listing QA outranks instant refund on WSJF lite — matches Pareto on return reasons.

### 2x2 value vs effort

| | Low effort | High effort |
|---|---|---|
| **High value** | Do first (quick wins) | Plan / phase |
| **Low value** | Fill-ins if idle | Avoid |

Plot items with the sponsor in the room so “high value” is not the loudest voice.

## How to choose a technique

| Situation | Technique |
|---|---|
| Release scope fight | MoSCoW + Won’t list |
| Product delight vs hygiene | Kano |
| Agile ranking of epics | WSJF lite |
| Workshop with business + tech | Value vs effort 2x2 |
| Target setting / business case | Benchmarking |

Often: benchmark to set the goal, MoSCoW for MVP, 2x2 for the rest.

## Benchmarking

| Type | Compare to | Example KPI |
|---|---|---|
| Internal | Last year, other city, other product | QuickBite Hyderabad TAT vs Pune |
| Competitive | Named rival (public or mystery shop) | ShopEase refund days vs largest rival app |
| Industry | Regulator, association, research | ShieldSure claim cycle vs IRDAI / industry 7-day cashless repair |

Common KPIs: **delivery TAT**, **NPS**, **claim cycle time**, plus first-contact resolution, no-show %, loan origination days.

**Weak benchmark:** “industry is digital.” **Strong:** “peer motor insurers publish 7-day cashless TAT; we are 18 days P50, 29 days P90.”

## Weak vs strong

| Weak | Strong |
|---|---|
| Everything is Must. | Must = FNOL + survey slot + payment; delight garage tracking is Could. |
| Kano: customers want everything. | Basic = SMS ack; performance = TAT; delight = proactive slot. |
| WSJF with fake decimals. | Relative 1–8 scores; listing QA WSJF 5.3 vs instant refund 0.9. |
| To-Be: world-class claims. | To-Be P50 TAT 7 days to match industry; P90 12 days in 2 quarters. |

## Real-world examples

**NovaBank:** origination 9 days vs digital-bank peers ~1 day — justifies video KYC Must.

**MediCare+:** no-show 22% vs hospital group internal 12% — justifies reminders Must, WhatsApp Could.

**QuickBite:** delivery TAT vs competitor city-level SLA — competitive benchmark, not a press slogan.

## Scenario / Use case: ShieldSure claim TAT vs industry

**Context.** Claims head wants a new portal. COO wants cost down. IRDAI and customers complain about slow motor claims. Industry / peer cashless repair TAT is **7 days P50**. ShieldSure: **18 days P50**, **29 days P90**. NPS claims = 12.

**What the BA does.**

1. **Benchmark pack:** internal (this year vs last), competitive (mystery FNOL on two peers), industry (7-day TAT). Gap = 11 days P50.
2. **Problem / To-Be:** P50 TAT 7 days in two quarters; P90 12 days. Portal is a *means*, not the objective.
3. **Value vs effort:** surveyor appointment SLA (high value, medium effort); customer portal status (high value, medium); AI photo damage (high effort, uncertain value) → Could/Won’t.
4. **MoSCoW MVP:** Must = digital FNOL, survey slot < 24h, garage assignment, status SMS. Should = photo upload. Won’t = AI liability.
5. **Kano check:** SMS ack is Basic — if MVP ships portal without ack, NPS still dies.
6. **WSJF:** survey-slot epic ranks above portal cosmetics.

**Gap → To-Be justification (one paragraph for steering).** “We are 11 days slower than the industry P50 we will be measured against. Closing that gap is the business objective. The portal is in scope only where it cuts wait time (FNOL, slot, status). Features that do not move TAT are Won’t this phase.”

**If ignored.** A glossy portal, same surveyor wait, TAT still 18 days, benchmark unused.

## Notes

- MoSCoW needs a real Won’t list; too many Musts means no priority.
- Kano separates basics from delight — ship basics first.
- WSJF lite ranks by (value + urgency + risk reduction) ÷ size; keep scores coarse.
- 2x2 value vs effort is a workshop tool, not a precision model.
- Benchmark internal, competitive, and industry KPIs; use the gap to justify To-Be, not a tool purchase.
