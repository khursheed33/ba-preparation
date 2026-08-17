# Test Scenarios, Test Cases, and Acceptance Criteria

## Definition

**Acceptance criteria (AC)** are conditions that must be true for a requirement or user story to be accepted. They are written *before* build, in business language, and they define “done.”

A **test scenario** is a high-level situation to verify (happy path or exception): “Customer returns a delivered item within window.”

A **test case** is a specific, executable check: numbered steps, test data, expected result. Many cases sit under one scenario.

**Requirement-based testing** means every requirement/AC maps to at least one scenario and case (and vice versa — extra tests should be justified). That mapping is the start of an RTM.

## Why it matters

Vague AC produces vague tests. QA guesses. ShopEase refunds the wrong amount. The BA says “that’s not what I meant.” Writing AC and reviewing cases is how the BA helps QA **without becoming QA**.

## Scenario vs case vs AC

| Artifact | Grain | Contains | Owner |
|---|---|---|---|
| AC | Story / requirement | Rules, outcomes, boundaries | BA (+ PO) |
| Test scenario | Situation | One business path or exception | QA, BA contributes UAT ones |
| Test case | Atomic check | Preconditions, steps, data, expected | QA (system); BA/users (UAT scripts) |

Example chain:

- **AC:** If return is approved and payment was UPI, refund to source within 5 days; if COD, refund to ShopEase Wallet.
- **Scenario:** COD order return approved.
- **Case:** COD + partial return (1 of 3 items) → wallet credit equals item net of coupon rules.

### Weak vs strong

| Weak | Strong |
|---|---|
| AC: User can return products. | AC: Eligible SKU, within 7 days of delivery, unopened unless listed as try-and-buy… |
| Scenario: Test returns. | Scenario: In-window return of prepaid order; out-of-window rejection. |
| Case: Click return. | Steps, SKU, order_id, expected refund ₹X, status Returned. |
| BA writes 200 system cases | BA writes AC + 8 UAT scenarios; QA writes system cases |

## How BAs help QA without becoming QA

- Give **examples** (Given/When/Then) and **boundary data** (day 7 vs day 8).
- Walk **negative paths**: expiry, wrong state, duplicate submit, no inventory.
- Review QA cases for **missing business rules** (GST, wallet vs source, QC fail).
- Do **not** copy-edit every locator and every UI step unless the story is yours for UAT.
- Join **triage** to say: bug vs change vs working-as-designed.

## Sample: one ShopEase return story → 6 test cases

**Story.** As a delivered-order buyer, I can request a return so I get money back under policy.

**AC (abridged)**

1. Return allowed if `delivered_at` ≤ 7 days ago and SKU `returnable = Y`.
2. Prepaid (UPI/card) → refund to source in 5 days after QC pass.
3. COD → refund to Wallet after QC pass.
4. QC fail (damaged / used beyond policy) → return rejected, no refund, item disposition per warehouse rule.
5. Duplicate return request on same item → rejected with message, no second refund.

**Scenario A — happy prepaid.** **Scenario B — COD.** **Scenario C — policy reject.** (Cases below.)

| ID | Type | Preconditions | Steps (short) | Expected |
|---|---|---|---|---|
| TC-RET-01 | Positive | Order delivered 3 days ago, UPI, SKU returnable | Request return → warehouse QC pass | Status Refund initiated; amount = item net; destination = UPI source |
| TC-RET-02 | Positive | COD order, delivered 2 days ago | Request return → QC pass | Wallet credit = item net; no bank payout |
| TC-RET-03 | Negative | Delivered 8 days ago | Request return | Blocked; message: window expired; no RMA |
| TC-RET-04 | Negative | SKU `returnable = N` (innerwear) | Request return | Blocked; policy message; no RMA |
| TC-RET-05 | Negative | QC fail: item used, stains | Buyer ships → QC fail | No refund; status Rejected; CX template sent |
| TC-RET-06 | Negative | Return already approved for line | Submit second return | Error: duplicate; refund count remains 1 |

QA will add more (GST breakup, partial qty, replacement vs refund). The BA ensured **negatives and money rules** exist.

## Real-world examples

**NovaBank.** AC: beneficiary add requires OTP and daily limit. QA cases: at limit, over limit, OTP expiry. BA does not write the Selenium script.

**MediCare+.** AC: cannot book overlapping slots for same doctor. Scenario: double-book attempt. Case: two front-desk users, same slot, second gets conflict.

**ShieldSure.** AC: cashless pre-auth within network. Negative case: out-of-network hospital.

**EdTech.** AC: subscription lapse blocks live class, not recorded library. Negative: grace period day 0 vs day 1.

## Scenario / Use case: ShopEase return story in a sprint

**Context.** PO wants “returns like Amazon.” QA asks the BA for test cases tomorrow. The BA writes AC with finance (COD vs prepaid) and warehouse (QC). QA turns AC into 18 system cases. The BA reviews the 6 money-and-policy cases above, adds TC-RET-06 after a past double-refund incident. UAT: warehouse QC lead runs TC-RET-05 on real devices.

**If the BA had written all 18 system cases instead of AC.** Analysis of the next story slips; cases go stale when UI labels change; QA is deskilled.

**If the BA had only written happy-path AC.** Duplicate refund ships; finance finds it in reconciliation.

## Notes

- AC = done conditions; scenario = situation; case = executable steps + expected.
- Requirement-based testing starts from AC, not from the UI mock.
- Always include negatives: time window, eligibility, duplicate, QC fail.
- BA helps QA with rules and examples, not by replacing the test team.
- One story can spawn many cases; six is a minimum when money moves.
- Expected result must include **data** (₹ amount, status), not “success.”
- Map case IDs back to AC IDs (mini-RTM).
- UAT scripts stay fewer and business-shaped; system cases can be granular.
