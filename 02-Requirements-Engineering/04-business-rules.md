# Business Rules

A **business rule** is a statement that defines or constrains some aspect of the business. It is true whether or not software exists.

A **requirement** says what the solution must do about that rule (enforce, calculate, display, override with approval).

## Why it matters for a BA

If you bury rules inside UI notes (“grey out the button after 7 days”), nobody can audit policy, sellers will fight ShopEase, and NovaBank credit policy will drift between two screens. Rules need IDs, owners, and exceptions.

## Rules vs requirements

| | Business rule | Requirement |
|---|---|---|
| Exists without software? | Yes | No — it is about the solution |
| Owner | Policy owner (credit, legal, category, clinical) | Product / BA / sponsor for the solution |
| Change trigger | Regulation, commercial policy, medical protocol | Project or product change |
| Example | Innerwear cannot be returned after 7 days from delivery | System must reject a return request on innerwear SKUs when days_since_delivery > 7 |

ShopEase: the 7-day innerwear rule is policy. The requirement is how checkout, My Orders, seller portal, and support tools all enforce the same policy.

NovaBank: “salaried applicants with FOIR > 50% are ineligible for personal loans” is a credit rule. The requirement is that origination calculates FOIR and stops the application with a defined message and an exception path for credit manager override, if any.

## Types of business rules

| Type | Meaning | Test |
|---|---|---|
| Constraint | Something that must not happen | “Must / must not” |
| Inference | If facts are true, conclude a fact | “If … then classify / consider” |
| Computation | How a number is calculated | Formula, rounding, inputs |
| Action enabler | If a condition holds, an action is allowed or required | “May / shall initiate” |

### Constraint

- ShopEase: No returns on innerwear after 7 days from delivery (category policy).
- NovaBank: A savings account cannot go below ₹0; no unauthorised overdraft.
- ShieldSure: Cashless claim cannot be approved if the hospital is not on the network at admission date.

### Inference

- NovaBank: If FOIR > 50% and employment type = salaried, then application status = ineligible (unless override).
- QuickBite: If restaurant acceptance time > 8 minutes, infer the delay cause = restaurant, not rider.
- MediCare+: If patient has two overlapping appointments in the same clinic, infer a conflict to be resolved by reception.

### Computation

- NovaBank: FOIR = (existing EMI + proposed EMI) / net monthly income, rounded to 2 decimals.
- ShopEase: Refund amount = item price − coupon clawback + return shipping if policy says buyer-pays.
- ShieldSure: Eligible claim amount = min(bill, sum insured remaining, network tariff).

### Action enabler

- ShopEase: If order is delivered and within return window and category is returnable, buyer **may** create an RMA.
- NovaBank: If KYC status = verified and PAN matches, customer **may** open a second savings account digitally.
- MediCare+: If appointment is > 4 hours away, patient **may** cancel in app; otherwise only reception **may** cancel.

## More worked examples

**Loan eligibility (NovaBank).** Constraint: minimum age 21. Computation: FOIR. Inference: FOIR > 50% → ineligible. Action enabler: if eligible, system may send to underwriter.

**Return window (ShopEase).** Constraint: 7 days for innerwear, 10 days for electronics, 30 days for books. Exception: defective items follow warranty, not return window.

**KYC (NovaBank).** Constraint: no debit card dispatch until KYC = verified. Inference: if VKYC failed 3 times, infer status = branch-KYC-required.

**Discount stacking (ShopEase).** Constraint: bank offer and coupon cannot both apply unless campaign flag `stackable = true`. Computation: apply coupon first, then bank discount on payable. Action enabler: if payable < ₹1, payment step is skipped (zero-pay order).

## How BAs document rules

Do not hide a rule in a paragraph of FRD prose. Use a register.

| Field | Why |
|---|---|
| Rule ID | Stable handle: BRULE-RET-007 |
| Statement | One sentence, present tense, no UI |
| Type | Constraint / inference / computation / action enabler |
| Source | Policy PDF, RBI circular, seller contract, medical board |
| Owner | Named role who can change it |
| Effective dates | From / to |
| Scope | Category, product, channel, geography |
| Exception | Who can override, with what evidence |
| Related requirements | FR-RET-10, FR-RET-11 |
| Status | Draft / active / retired |

**Weak:** “Innerwear usually can’t be returned late unless the seller is okay.”
**Strong:** `BRULE-RET-007` Constraint. Innerwear (category = INNERWEAR) is not returnable after 7 calendar days from delivery_date, except DAMAGED_ON_DELIVERY with photo evidence. Owner: Category Policy. No seller override.

## Scenario / Use case: ShopEase innerwear 7-day rule vs seller policy

**Context.** ShopEase category policy: no returns on innerwear after 7 days. A large seller, “CottonCart,” has a storefront badge “15-day easy returns” from an old seller-contract addendum. Buyers raise tickets on day 10. Support sometimes refunds from ShopEase’s pocket. Sellers threaten to leave if ShopEase enforces 7 days on their listings. Legal says platform policy wins unless the seller contract explicitly supersedes.

**Stakeholders.** Category manager (policy owner), CottonCart account manager, buyer support, returns ops, finance (who pays), legal, seller portal product, BA.

**What the BA does.**

1. Pull sources: platform return policy v3.2, CottonCart MSA clause 14, listing-level return window field.
2. Separate platform constraint vs seller-specific exception.
3. Find the conflict: listing UI allows sellers to type any window; enforcement uses category default. Two systems, two truths.
4. Facilitate a decision: either (A) platform rule always wins and seller badge must match, or (B) seller window can be *stricter or more generous* only if `seller_return_override = allowed` and ShopEase is not the refund payer.
5. Document the rule, exception, and who pays.

**Sample artifact.**

| Field | Content |
|---|---|
| Rule ID | BRULE-RET-007 |
| Statement | Innerwear items are not returnable after 7 calendar days from delivery, unless DAMAGED_ON_DELIVERY. |
| Type | Constraint |
| Source | Category Policy v3.2 §4.1 |
| Owner | Head of Category Policy |
| Exception | Seller may offer a longer window only if seller_contract.return_override = Y and refund is seller-funded. Listing must display the actual window. |
| Related FR | FR-RET-19 reject RMA; FR-RET-20 show window on PDP; FR-RET-21 block seller from publishing a window that contradicts policy unless override flag is set |

**What goes wrong if ignored.** Support keeps making goodwill refunds. Finance sees leakage. CottonCart’s 15-day badge is false advertising. A consumer forum case hits ShopEase, not the seller. Engineering “fixes” it by hard-coding 7 days for all categories, which breaks books (30-day) and electronics.

## Rule vs UI vs test

- Rule: 7 days from delivery for innerwear.
- Requirement: system rejects RMA and shows the policy text.
- Test: create delivery_date = today−8, category INNERWEAR, expect reject code RET-WINDOW-EXPIRED.

If the test is written against the button colour, you are testing UI, not the rule.

## Notes

- 
