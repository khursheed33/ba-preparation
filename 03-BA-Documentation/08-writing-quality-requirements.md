# Writing Quality Requirements

A good requirement is **clear, concise, testable, measurable, unambiguous, and atomic**, with **acceptance criteria**, and it has been **validated** with the people who own the need.

This is craft. Templates do not save a vague sentence.

## Why it matters for a BA

QA cannot fail “user-friendly.” Developers cannot implement “flexible.” ShopEase, NovaBank, and MediCare+ all pay for rework when the BA writes essays instead of tests. Quality writing is how analysis survives contact with a sprint.

## The quality attributes

| Attribute | Meaning | Quick test |
|---|---|---|
| Clear | One reading, one meaning | A new tester can paraphrase it |
| Concise | No filler, no design novel | Fits a catalog cell |
| Testable | A test can fail | QA can write a fail condition |
| Measurable | Number, date, count, or binary | You know when it is enough |
| Unambiguous | No banned vague words | Two readers, same test |
| Atomic | One concern per ID | One primary test per ID |
| Acceptance criteria | How we will accept | Given/When/Then or checklist |
| Validated | Right need, not only pretty text | Business walked the scenario |

## SMART and INVEST overlap

You will meet SMART (goals) and INVEST (stories). Requirements sit in the middle.

| Idea | SMART | INVEST | Requirement writing |
|---|---|---|---|
| Specific / Independent | Specific | Independent | Atomic ID; not a bundle |
| Measurable / Valuable | Measurable | Valuable | Traces to a need; has a measure |
| Achievable / Estimable | Achievable | Estimable | Feasible; sized for a slice |
| Relevant / Small | Relevant | Small | In scope; not an epic disguised as FR |
| Time-bound / Testable | Time-bound | Testable | Dates where they matter; always testable |

Do not force every FR to be a SMART goal. BR-01 can be SMART. FR-RET-012 should be testable and atomic. Stories should be INVEST. The overlap is **testable + valuable + small enough to verify**.

## Atomic: one requirement, one test

**Not atomic:** “The system shall let the buyer create a return, notify the seller, and refund to the original instrument after QC.”

That is three tests (create, notify, refund). Split:

- FR-RET-010 create RMA
- FR-RET-011 notify seller
- FR-RET-014 refund original instrument after QC

Compound FRs hide partial fails: notify works, refund does not, and someone marks the story “done.”

Exception: a true transaction that must be atomic in the business sense still gets **one FR for the transaction** plus **child FRs** or AC lines for each side effect — but QA still maps one test per observable.

## Rewrite 10 bad requirements

| # | Domain | Bad | Good |
|---|---|---|---|
| 1 | ShopEase | The site should be user-friendly. | First-time return on mobile web: ≤ 3 input fields besides photos; each error names the field and the fix; flow meets WCAG 2.1 AA. |
| 2 | ShopEase | Search must be fast. | Search API p95 ≤ 800 ms at 5,000 RPS with 2M active SKUs (NFR-SRCH-P01). |
| 3 | ShopEase | Handle returns flexibly. | System enforces category windows from config; seller may not publish a window outside min/max unless `return_override = Y`. |
| 4 | NovaBank | Transfer money securely and quickly. | Debit only after 2FA success; payment confirm p95 ≤ 2.5 s; session idle timeout 5 minutes (split FR + two NFRs). |
| 5 | NovaBank | KYC should be simple. | Salaried digital KYC: 4 screens, VKYC < 8 minutes p95; fail path shows branch appointment link (UR + NFR + FR). |
| 6 | NovaBank | Support all payment types etc. | MVP: IMPS and NEFT to saved beneficiaries. Out of scope: RTGS, international, UPI collect. |
| 7 | MediCare+ | Remind patients properly. | SMS 24 h ± 15 min before CONFIRMED appointments if `consent.sms`; skip if CANCELLED (FR-REM-01, FR-REM-03). |
| 8 | MediCare+ | Booking should not double-book. | System shall not persist two CONFIRMED appointments for the same doctor_id and overlapping start/end; concurrent holds use slot lock (FR-APT-07). |
| 9 | QuickBite | Compensate late orders fairly. | Customer voucher if drop_time > promised_time; cost allocation per BRULE-DLV-12 (split customer vs finance FRs). |
| 10 | ShieldSure | Process cashless efficiently. | From complete estimate submit to approve/reject, p95 ≤ 4 business hours 09:00–18:00 IST (NFR-CLM-T01). |

Banned words in the bad column: user-friendly, fast, flexibly, securely, quickly, simple, all, etc., properly, fairly, efficiently. The good column names actors, conditions, and measures.

## Sample acceptance criteria

### Given / When / Then (NovaBank FR-03 cooling-off)

- **Given** a retail customer added beneficiary B 10 minutes ago  
  **When** they submit a transfer of ₹5,001 to B  
  **Then** the system does not debit and shows FT-E02  
  **And** no accounting entry is created.

- **Given** beneficiary B added 31 minutes ago  
  **When** they submit ₹5,001  
  **Then** 2FA is requested and, on success, debit proceeds (subject to balance and daily cap).

### Checklist style (ShopEase FR-RET-010)

- [ ] Logged-in buyer, eligible delivered item → RMA created, unique RMA ID shown
- [ ] Same order line cannot create a second open RMA
- [ ] Ineligible innerwear day 8 → no RMA, policy message, no seller notify
- [ ] Photos required category without photos → cannot submit

Use GWT for behaviour with state. Use checklists for several pass/fail observables on one screen. Both must be **fail-able**.

MediCare+ GWT: Given CONFIRMED appointment in 24 h and consent.sms true, When the reminder job runs, Then one SMS is sent and log = SENT. Given CANCELLED, Then no SMS and log = SKIPPED.

## Validation walkthrough with business users

Verification is QA’s “is it written correctly?” Validation is business “is it the right need?” A walkthrough:

1. Pick 5–8 real cases (order IDs, claim IDs, appointment IDs).
2. Read the requirement + AC out loud.
3. Ask: “If we do only this, does your problem move?”
4. Act the exception: “Mobile missing — is this acceptable?”
5. Mark changes as new versions, not hallway edits.
6. Record who attended (validation evidence).

Do this **before** a large build, and again on CR-impacted reqs.

**Weak validation:** “Any comments on the FRD?” in email.
**Strong:** claims manager walks CLM-88421 against FR-CLM-31..33.

## Practical writing rules

- Subject: the system or a named role.
- Verb: observable (display, prevent, calculate, send).
- Condition: if / when.
- No UI chrome unless it is the requirement (then it is a UI note, not a BR).
- Reference rules by ID.
- If you need “and,” check atomicity.

## Notes

- 
