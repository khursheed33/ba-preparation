# Functional Requirements Document (FRD)

An **FRD** specifies **what the system must do** — functions, business rules to enforce, UI notes, validations, and error messages — so developers and QA can build and test without inventing behaviour.

It sits **below** the BRD. The BRD says *why* and *what outcome*. The FRD says *what the solution does* in testable statements.

## Why it matters for a BA

NovaBank fund transfer will be built wrong if the BRD only says “customers can send money.” Without validations and errors, QA cannot fail a test, and a ₹5 lakh transfer might skip 2FA. The FRD (or equivalent story set) is the contract for behaviour.

## FRD vs BRD

| | BRD | FRD |
|---|---|---|
| Altitude | Business | Solution behaviour |
| Language | Outcomes, scope, stakeholders | System shall / user can + rules |
| Audience | Sponsors, SMEs, vendors (scope) | Dev, QA, architects |
| Change | Rare after funding | More detail; still baselined |
| Example | BR-01 Customers can transfer to added beneficiaries | FR-01 System credits beneficiary only after 2FA success and cooling-off |

If you copy the BRD into the FRD and add “the system shall” in front of objectives, you do not have an FRD.

## Typical FRD sections

- Document control and traces to BR IDs
- Actors and preconditions
- Functional requirements (numbered)
- Business rules invoked
- UI notes (not a full visual design)
- Validations
- Error / message catalogue
- Non-functional pointers (or a separate NFR section)
- Out of scope for this function
- Open questions

## Mini FRD excerpt: NovaBank fund transfer

**Document:** FRD-FT-01 Retail fund transfer (own bank + IMPS/NEFT)  
**Version:** 1.0  
**Traces to:** BRD-PAY-02 “Retail payments,” BR-01

### Actors

Retail customer (authenticated), beneficiary (passive), fraud engine (system), SMS gateway.

### Preconditions

Customer session is valid; KYC = verified; at least one beneficiary exists or customer adds one (add-beneficiary is FRD-BEN-01, out of this excerpt except cooling-off).

### Functional requirements

| ID | Statement | Trace |
|---|---|---|
| FR-01 | After the customer confirms a transfer, the system authenticates with 2FA (OTP to registered mobile) before debit. | BR-01 |
| FR-02 | The system debits the selected savings account only if available balance ≥ amount + applicable charges. | BR-01 |
| FR-03 | If the beneficiary was added fewer than 30 minutes ago, the system allows a transfer of at most ₹5,000 until cooling-off ends (BRULE-PAY-04). | BR-01, risk |
| FR-04 | On success, the system posts an accounting entry, shows a reference ID, and sends SMS + in-app notification within 60 seconds. | BR-01 |
| FR-05 | On payment-switch timeout, the system retries once; if still unknown, it marks the transaction PENDING and does not allow a duplicate submit of the same idempotency key. | BR-01 |
| FR-06 | The customer can view PENDING/SUCCESS/FAILED in transaction history the same day. | BR-01 |

### Business rules (invoked)

| Rule ID | Statement | Type |
|---|---|---|
| BRULE-PAY-04 | New beneficiary cooling-off: 30 minutes; during cooling-off, cap ₹5,000 per transaction. | Constraint |
| BRULE-PAY-07 | Daily IMPS cap for this segment: ₹2,00,000 (config). | Constraint |
| BRULE-PAY-11 | Charge: NEFT as per published tariff table T_CHARGE. | Computation |

### UI notes

- Amount field: numeric, 2 decimals, Indian grouping on blur.
- Beneficiary list: last-used first; show masked account (last 4).
- Do not show “success” until FR-04 conditions are met; PENDING has its own screen.
- 2FA: 6-digit OTP, 3 attempts (align FR-AUTH lock policy).

These notes constrain behaviour; pixel-perfect layout lives in design files.

### Validations

| Field | Rule | When |
|---|---|---|
| Amount | > 0, ≤ available balance, ≤ remaining daily cap | On continue |
| Remarks | Optional, max 50 chars, no emoji | On continue |
| Account | Must belong to customer, status = active | On load |
| OTP | 6 digits, match, not expired | On verify |

### Error messages

| Code | Condition | Message (customer) |
|---|---|---|
| FT-E01 | Amount > balance | Insufficient balance. Available: ₹X.XX |
| FT-E02 | Cooling-off cap | You can send up to ₹5,000 until 30 minutes after adding this beneficiary. |
| FT-E03 | Daily cap | Daily transfer limit reached. Try tomorrow or use branch. |
| FT-E04 | OTP wrong | Incorrect OTP. Attempts left: N |
| FT-E05 | Timeout pending | Transfer is being processed. Do not retry. Reference: {id} |
| FT-E06 | Debit account frozen | This account cannot send money. Call 1800-… |

**Weak message:** “Error occurred.”
**Strong message:** FT-E02 states the rule the customer can act on.

## Trace from BRD BR-01 to FR-01

**BRD BR-01:** Retail customers can transfer funds from their NovaBank savings account to a saved beneficiary, with fraud controls appropriate to RBI guidelines.

| BR | FR | Story (illustrative) | Test idea |
|---|---|---|---|
| BR-01 | FR-01 2FA before debit | NB-221 Confirm + OTP | No debit if OTP cancelled |
| BR-01 | FR-02 balance check | NB-222 | Amount = balance+0.01 → FT-E01, no debit |
| BR-01 | FR-03 cooling-off | NB-223 | Beneficiary age 10 min, amount ₹5,001 → FT-E02 |
| BR-01 | FR-04 notify | NB-224 | SMS within 60s of SUCCESS |
| BR-01 | FR-05 timeout | NB-225 | Switch timeout → PENDING, second click no double debit |
| BR-01 | FR-06 history | NB-226 | PENDING visible in history |

If FR-03 is missing, BR-01’s “fraud controls” is not met — the trace makes the hole visible.

## FRD in Agile shops

You may not produce a Word FRD. You still need the same content: FR IDs, rules, validations, errors, traces. Often: Confluence FR catalog + stories with AC. The name changes; the discipline does not.

ShopEase analogue: Easy Returns FRD would list RMA create, window check, seller notify — each traced to BR-01–05 in the BRD excerpt.

## Notes

- 
