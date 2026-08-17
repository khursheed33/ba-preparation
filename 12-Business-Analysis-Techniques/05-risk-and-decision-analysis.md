# Risk Analysis and Decision Analysis

**Risk analysis** identifies what might go wrong, estimates probability and impact, and assigns mitigation and an owner. **Decision analysis** structures a choice: options, criteria, scores, and a recommendation someone can accept or reject. Both stop the BA from writing “TBD” or picking a vendor because the demo was pretty.

## Why it matters

MediCare+ picking SMS vs in-house notifications without criteria will reopen in UAT. ShopEase discount stacking without a decision table will leak margin. Risks that sit only in the PM RAID log never become requirement controls. The BA owns **requirement risks** and feeds **project risks** to the PM.

## Risk analysis

| Step | What you do |
|---|---|
| Identify | Name the risk as “if X, then Y” — not “KYC might be an issue.” |
| Probability | High / medium / low (or 1–5) with a reason. |
| Impact | On objective, compliance, cost, customer, schedule. |
| Mitigation | Reduce probability, reduce impact, transfer, or accept. |
| Owner | Named role, not “team.” |

### Requirement risks vs project risks

| | Requirement risk | Project risk |
|---|---|---|
| About | The *need* is wrong, unstable, untestable, or conflicting | Delivery of an agreed need may fail |
| Example | Video KYC rule unclear for joint accounts → wrong behaviour in prod | Vendor SDK delayed 6 weeks |
| BA action | Clarify, split, add BR, defer, or spike | Flag to PM; add assumption/dependency |
| Typical owner | BA + business owner | PM + vendor / tech lead |

Both can be true on one initiative. Do not dump requirement ambiguity into the project risk register and walk away.

**Sample risk register (NovaBank video KYC)**

| ID | Risk | Type | P | I | Mitigation | Owner |
|---|---|---|---|---|---|---|
| R-01 | Liveness vendor false-fail > 8% | Requirement / vendor | M | H | Fallback to branch; threshold in NFR | BA + InfoSec |
| R-02 | Legal rejects storage location | Requirement / legal | M | H | India-resident storage in constraints | Compliance |
| R-03 | RM bypasses video and paper-KYCs everyone | Requirement (process) | H | M | BR: digital journey cannot complete on paper packet | Ops |
| R-04 | Sprint slips if bureau sandbox late | Project | M | M | Stub + contract dates | PM |

## Decision analysis

1. List **options** (including do nothing).
2. Agree **criteria** and weights with the decision owner.
3. **Score** options (e.g. 1–5) against criteria.
4. **Recommend** with residual risks.

| Criteria (example) | Weight |
|---|---|
| Time to go-live | 20% |
| Cost (3-year) | 20% |
| Control / compliance | 25% |
| Ops effort | 15% |
| Scalability | 20% |

Recommendation is not the highest score if a **must-pass** legal criterion fails.

## Decision table: ShopEase discount stacking

Business question: can coupon, bank offer, and wallet cashback apply together?

| Coupon | Bank offer | Wallet cashback | Stack allowed? | System action |
|---|---|---|---|---|
| N | N | N | — | List price |
| Y | N | N | Yes | Apply coupon |
| N | Y | N | Yes | Apply bank offer |
| N | N | Y | Yes | Apply cashback cap |
| Y | Y | N | **No** | Apply the higher of coupon vs bank; do not add |
| Y | N | Y | Yes | Coupon then cashback on payable |
| N | Y | Y | Yes | Bank offer then cashback on payable |
| Y | Y | Y | **No** | Same as Y/Y/N, then cashback on payable |

**BR-DIS-04:** Coupon and bank offer never add. Cashback applies after the winning cart offer, capped at ₹200.

This table *is* the requirement. A paragraph “stacking should be fair” is not.

## Weak vs strong

| Weak | Strong |
|---|---|
| Risk: vendor. | If SMS vendor DLT templates delayed > 3 weeks, MediCare+ reminders miss go-live (P M, I H). Owner: BA + vendor mgr. |
| Decision: SMS is cheaper. | Scored options; legal must-pass; recommend vendor SMS with in-house failover later. |
| Stacking: apply best offer. | Decision table with 8 rows and one BR ID. |
| Owner: IT. | Owner: Claims Ops Lead (named role in RACI). |

## Real-world examples

**QuickBite:** risk that compensation rules conflict with restaurant SLA — requirement risk, not “ops might be unhappy.”

**ShieldSure:** decision analysis for garage network vs in-house workshops — criteria: TAT, leakage, capital, IRDAI cashless push.

**EmployeeHub:** decision table for overlapping leave types (privilege vs sick vs optional holiday).

## Scenario / Use case: MediCare+ SMS vendor vs in-house

**Context.** Reminders must cut no-shows. IT wants to build a notification service. Ops wants a vendor “next month.” Compliance wants DLT, consent, and audit. Sponsor asks the BA to “just pick.”

**Options.** A) Do nothing. B) Vendor SMS (DLT-ready). C) In-house SMS gateway. D) Vendor now, in-house Phase 2.

**Score (1–5)**

| Criteria | W | A | B | C | D |
|---|---|---|---|---|---|
| Time to go-live | 20 | 1 | 5 | 2 | 5 |
| 3-year cost | 20 | 5 | 3 | 4 | 3 |
| Compliance (DLT, consent, logs) | 25 | 1 | 5 | 3 | 5 |
| Ops effort | 15 | 5 | 4 | 2 | 4 |
| Scalability (WhatsApp later) | 20 | 1 | 4 | 3 | 5 |

Weighted direction: **D** slightly ahead of **B**. Must-pass: compliance — A fails.

**Risks on D:** vendor lock-in (mitigate: message API abstraction); dual run cost in Phase 2 (accept for 12 months).

**Recommendation.** Vendor SMS for appointment reminders now; interface owned by MediCare+; in-house or multi-channel in Phase 2. Do nothing is rejected because no-show cost exceeds vendor fees.

**If ignored.** IT builds a gateway for 5 months, DLT templates still sit with the vendor, no-shows stay at 22%.

## Notes

- Risk = identify, probability, impact, mitigation, owner — in one row.
- Requirement risk = wrong or unstable need. Project risk = delivery of an agreed need.
- Decision analysis = options + criteria + score + recommendation + residual risk.
- Decision tables beat prose for rules like discount stacking.
- Never recommend an option that fails a must-pass legal/compliance criterion.
