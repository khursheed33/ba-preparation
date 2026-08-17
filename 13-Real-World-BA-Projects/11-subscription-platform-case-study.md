# Subly — Subscription Platform (Failed Payments & Access)

**Domain:** Subscription platform. **Company:** Subly (illustrative memberships for creators). **Role:** BA, Billing & Access.

## Business problem

**19% of renewals fail** card/UPI (illustrative). Access is cut **the same hour**, then support grants manual exceptions. Dunning is one email. Churn tagged “involuntary” is 11% of MRR. Creators blame Subly; members blame “I was charged twice.” Double charge happens when retry overlaps manual pay.

**Related examples:** ShopEase Wallet auto-reload failing then locking checkout; NovaBank standing instruction bounce cutting bill-pay. Same failure: no grace, no idempotent retry.

## Business objective

10 weeks: (1) involuntary churn **≤ 5%** of MRR; (2) dunning **4 retries / 14 days** before cut; (3) access state always matches entitlement; (4) zero double-charge incidents in UAT/prod monitor.

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| Subly CEO / Sponsor | H | H | Take-rate model | Dunning Must |
| Creators (sellers) | M | H | Payout fear | Pause vs cut |
| Members | L | H | Access shock | Journey |
| Payments (Razorpay-style) | H | H | Webhooks | Idempotency |
| Support | M | H | Manual access | Kill Excel |
| Finance | M | H | Revenue rec | Reports |
| Legal | M | M | Auto-renew notice | BR |

## Scope

**In:** plan, subscribe, renew, dunning, entitlement/access, invoices, failed-pay UX, creator pause policy.  
**Out:** custom creator storefront CMS, tax engine rewrite, app store IAP.

## Assumptions and constraints

**Assumptions:** Gateway webhooks reliable with retry; email/SMS templates exist.  
**Constraints:** 10 weeks; take-rate business model (retries are key activity); RBI-style e-mandate notices (illustrative).

## As-Is / To-Be

**As-Is:** Renew fail → access off → one email → support toggles DB. Manual pay + auto-retry = double capture.  
**To-Be:** Fail → PAST_DUE + access **grace** → retry schedule → notify → if still fail, RESTRICT then CANCEL; idempotent pay keys; creator sees member status.

**Problem analysis:** Access is a switch, not an entitlement. Business model (% GMV) dies if dunning is weak.

**Root cause:** No grace; no idempotency key; support bypasses ledger.

## Gap analysis

| Type | Gap | Action |
|---|---|---|
| Process | Instant cut | Grace + dunning |
| Tech | Double charge | Idempotency |
| Data | Access ≠ invoice | Entitlement service |
| Policy | Unclear pause | Creator BR |
| People | Support DB edits | Admin tool only |

## Requirements, rules

| ID | Type | Statement |
|---|---|---|
| FR-SUB-01 | F | Member can subscribe; mandate/card stored per PSP rules. |
| FR-SUB-02 | F | Failed renewal → PAST_DUE; access continues for grace 3 days. |
| FR-SUB-03 | F | System retries 4 times in 14 days with email+SMS. |
| FR-SUB-04 | F | Payment attempts use idempotency key (invoice_id + attempt). |
| FR-SUB-05 | F | Access derived from entitlement, not support flag. |
| NFR-SUB-01 | NF | Webhook processing exactly-once via key. |

**BR-SUB-01:** After 14 days fail → RESTRICT (content off) then CANCEL day 16. **BR-SUB-02:** Creator may gift 7-day access; logged. **BR-SUB-03:** Auto-renew notice 24h before (illustrative).

## User stories (AC)

1. **As a member, I want a grace period** so one fail does not lock me. **AC:** 3-day access after fail.  
2. **As a member, I want retry notices** with update-payment link. **AC:** 4 retries.  
3. **As a member, I must not be charged twice** for one invoice. **AC:** Second attempt same key.  
4. **As a creator, I want to see PAST_DUE vs CANCELLED.** **AC:** Roster statuses.  
5. **As support, I want gift access** without SQL. **AC:** BR-SUB-02 tool.

## Use case (fully dressed): UC-SUB-01 Renew subscription

- **Actor:** System. **Pre:** Period end. **Trigger:** Billing job.  
- **Main:** Charge → SUCCESS → new period + invoice.  
- **Alt:** FAIL → PAST_DUE + schedule retries.  
- **Exception:** Webhook duplicate → ignore (idempotent).  
- **Post:** Entitlement dates updated.

## Wireframes

1. Plan picker. 2. Pay / mandate. 3. Member home (status). 4. Update payment (dunning). 5. Creator member list. 6. Support gift-access. 7. Invoice history.

## Data, reports, KPIs

**Data:** Account, Plan, Subscription, Invoice, PaymentAttempt, Entitlement, GiftGrant.  
**Reports:** involuntary churn; retry success; double-charge monitor; gift usage.  
**KPIs:** involuntary ≤ 5% MRR; 4×14 dunning; access=entitlement 100%.

## UAT, RTM, CR, risks

**UAT:** fail→grace; 4 retries; duplicate webhook no double pay; gift 7 days; cancel after 16.  
**RTM:** FR-SUB-02→US1; FR-SUB-03→US2; FR-SUB-04→US3→UC-SUB-01.  
**CR-SUB-01:** Annual plans with 30-day grace. Impact: BR. **Phase 2.**  
**Risks:** gateway webhook storms (M/H — keys); creators want unlimited gifts (M/M — cap).  
**Dependencies:** PSP, email/SMS, tax display.

## Final business solution

Align **business model** (take-rate) with **dunning as a key activity**: grace, 4 retries, entitlement-based access, idempotent payments, support without SQL. Cutting access on first fail is a product defect, not “strict billing.”

## Weak vs strong

| Weak | Strong |
|---|---|
| “Improve payments UX.” | Involuntary 11%→5%; idempotency; canvas-linked dunning Must. |

## Notes

- Subscription portfolio: entitlements, dunning, idempotency, creator vs member.
- Canvas lite: % GMV makes retry a Must, not Could.
- Illustrative churn only.
