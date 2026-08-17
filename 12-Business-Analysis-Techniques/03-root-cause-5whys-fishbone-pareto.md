# Root-Cause Analysis, 5 Whys, Fishbone, and Pareto

**Root-cause analysis (RCA)** finds the underlying cause of a problem so the solution fixes the cause, not the symptom. **5 Whys** drills a single chain by asking “why” until the actionable cause appears. **Fishbone (Ishikawa)** maps many cause categories around one effect. **Pareto analysis** ranks causes so you attack the vital few (often ~80% of impact from ~20% of causes).

## Why it matters

QuickBite paying compensation for every cancellation treats the symptom. ShieldSure tightening auditor checks on every claim burns cost if leakage sits in three categories. ShopEase “improve returns UX” wastes a sprint if three return reasons already explain 82% of volume. The BA uses RCA to write the *right* problem statement and the *right* requirements.

## When each technique is the right one

| Technique | Best when | Weak when | Typical output |
|---|---|---|---|
| 5 Whys | One visible failure, linear chain, ops incident | Many independent causes; people stop at “human error” | Cause chain + one or two actions |
| Fishbone | Complex outcome with people, process, policy, tech, materials | You fill bones with guesses, no data | Cause map + hypotheses to test |
| Pareto | You have counts or cost by reason code | Reasons are free text / “other” = 40% | Ranked bar + cumulative % |
| Full RCA | Recurring, costly, or safety/compliance issue | One-off anecdote | Problem, evidence, root cause, corrective action |

Use **5 Whys** for a sharp incident. Use **Fishbone** to avoid tunnel vision. Use **Pareto** to choose *which* causes to fix first. Combine: Pareto to pick the top reasons, Fishbone or 5 Whys on those reasons.

## Weak vs strong

| Weak | Strong |
|---|---|
| Why? Staff are careless. | Why? No SLA clock after restaurant accept; rider not assigned for 11 min median. |
| Fishbone bone: “technology.” | Fishbone: “surveyor app cannot store more than 3 photos; rest go on WhatsApp.” |
| Pareto: we should fix all return reasons. | Pareto: size, damaged-in-transit, and “item different” = 82%; fix those three first. |
| Root cause: lack of awareness. | Root cause: BR never defined stacking; system allows coupon + bank offer + wallet cashback together. |

## Real-world examples

**5 Whys — QuickBite high cancellation after restaurant accept**

Problem: 14% of orders cancel after the restaurant taps Accept (target < 5%).

1. Why do customers cancel after accept? They see ETA jump from 25 to 55 minutes.
2. Why does ETA jump? Rider is assigned late; batching waits for a second order.
3. Why late assignment? Dispatch holds the order to improve rider utilisation.
4. Why does dispatch hold after accept? Rule: “do not dispatch until kitchen time + 5 min,” but Accept does not capture kitchen-ready time.
5. Why is kitchen-ready time missing? Restaurant app has Accept only — no “food ready” event.

**Root cause:** process + tech — no food-ready signal; dispatch optimisation fights the customer-visible ETA.

**Action / requirement:** restaurant must send `food_ready`; do not show a tight ETA until rider is assigned; cancel-after-accept reason codes.

**Fishbone — ShieldSure claim leakage**

Effect (head): motor claim leakage (paid amount > policy entitlement).

| Bone | Candidate causes |
|---|---|
| People | New adjusters; garage relationship pressure; no dual review above threshold |
| Process | Cashless approval after work starts; no parts-vs-labour split check |
| Policy / rules | Depreciation table outdated; “goodwill” write-off with no cap |
| Technology | Surveyor app 3-photo limit; WhatsApp photos not in claim file |
| Data | Old NCB not applied; duplicate claim on same accident not flagged |
| External | Inflated garage invoices; parts price list not matched to OEM |

**Pareto — ShopEase return reasons (last 90 days, 100k returns)**

| Rank | Reason | Count | % | Cumulative |
|---|---|---|---|---|
| 1 | Size / fit | 41,000 | 41% | 41% |
| 2 | Damaged in transit | 28,000 | 28% | 69% |
| 3 | Item different from listing | 13,000 | 13% | **82%** |
| 4 | Changed mind | 8,000 | 8% | 90% |
| 5 | Late delivery | 6,000 | 6% | 96% |
| 6 | Other | 4,000 | 4% | 100% |

Three reasons = 82%. BA recommendation: size charts + try-and-buy rules; packaging SLA with 3PLs; listing image QA — not a generic “returns portal redesign.”

**NovaBank** uses 5 Whys on “loan files stuck in credit.” **EmployeeHub** uses Pareto on leave-request errors (wrong leave type = 60%).

## Scenario / Use case: QuickBite cancellation war room

**Context.** Support spend on post-accept cancellations is ₹1.8 Cr/quarter. Product wants “better cancellation UI.” Ops wants to punish restaurants. The BA is asked for root cause in 5 days.

**What the BA does.**

1. Pareto on cancel-reason codes: “ETA too long” 61%, “wrong items fear” 12%, “payment fail after accept” 9%.
2. 5 Whys on the 61% slice (chain above).
3. Light fishbone to check other bones (payment, menu photos) so the team does not overfit one chain.
4. Requirements: `food_ready` event; ETA not promised before rider assign; restaurant SLA clock from accept; compensation rule only if kitchen was on time and rider late.

**If ignored.** A prettier cancel button increases cancellations. Restaurants get fined for rider delay. Leakage moves; the root cause stays.

## How a BA writes RCA into BA artifacts

| RCA output | Where it goes |
|---|---|
| Problem + evidence | Problem statement, BRD context |
| Root cause | Gap analysis, not a feature |
| Corrective action | Requirements, rules, training, vendor SLA |
| Pareto cut-off | MoSCoW: Must = top 80% causes |

Stop at a cause the business can change. “Customers are impatient” is not a root cause. “We displayed 25 min before a rider existed” is.

## Notes

- Symptom vs cause: compensation, fines, and UI tweaks often treat symptoms.
- 5 Whys: one chain, evidence at each why; never stop at “human error.”
- Fishbone: categories to generate hypotheses; still need data to confirm.
- Pareto: fix the vital few; do not wait to boil the ocean.
- Combine Pareto (what to attack) with 5 Whys or Fishbone (why it happens).
- Trace root cause → requirement ID so UAT tests the cause, not the slogan.
