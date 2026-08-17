# Use Cases

## Definition

A **use case** describes how an **actor** uses the system to achieve a goal, including main success, alternatives, and exceptions. It is more structured than a user story and is useful when flows, rules, and failures must be explicit (banking, claims, clinical).

## Why it matters

Stories can hide branching. Use cases force preconditions, postconditions, and "what if OTP fails." A BA uses them when audit, operations, and QA need one agreed flow — not as a replacement for stories in every Agile team.

## Concepts

| Term | Meaning |
|---|---|
| **Use case** | Named goal of an actor with the system (e.g. Transfer money to saved beneficiary) |
| **Actor** | Person or system outside the solution that interacts with it |
| **Primary actor** | Who starts the use case to get value (customer) |
| **Secondary actor** | System or person the use case needs (OTP service, core banking, SMS) |
| **Preconditions** | What must already be true |
| **Postconditions** | What is true on success (and sometimes on failure) |
| **Main flow** | Happy path steps |
| **Alternate flow** | Another legitimate success or business-rule branch (limit exceeded → reduce amount) |
| **Exception flow** | Failure that stops the goal (OTP fail, timeout) |
| **Include** | Base use case always uses another (Transfer **includes** Authenticate session) |
| **Extend** | Optional extra behavior (Transfer **extended by** Add new beneficiary — only if chosen) |
| **Generalize** | Shared actor or use case type (Customer generalizes Retail and Corporate) |

### Use case vs user story — when to use which

| | User story | Use case |
|---|---|---|
| Size | Small increment | Whole goal with branches |
| Format | As a / I want / So that + AC | Fully dressed or brief template |
| Best when | Agile delivery, splitting | Complex, regulated, many exceptions |
| Trace | To sprint and AC | To test scenarios and audit |

Use both: epic/goal as a use case; sprint slices as stories that implement main or one alternate.

### Brief vs fully dressed

**Brief:** name, actor, 3–5 sentence summary, success guarantee. Good for backlog shaping.

**Fully dressed:** actors, pre/post, trigger, main/alternate/exception, rules, special requirements. Good for NovaBank transfers, ShieldSure claims, MediCare+ prescriptions.

Do not fully dress every "view FAQ" story.

## Real-world examples

1. **ShopEase:** Use case "Return an item" with alternate "seller dispute" and exception "RMA expired."
2. **MediCare+:** Use case "Book appointment" with exception "slot taken" and alternate "waitlist."

## Scenario / Use case: NovaBank "Transfer money to saved beneficiary"

### Context

Retail app must let customers move money to a beneficiary they already saved. Limits, OTP, and core-ledger posting are non-negotiable. A user story alone was too thin for ops and audit.

### Stakeholders

Retail customer (primary), OTP service, core banking, fraud, SMS, BA, QA, compliance.

### BA actions

1. Confirm primary vs secondary actors.
2. Capture limit rules and OTP retry count from policy, not from the app mock.
3. Write fully dressed use case; map each flow to stories/AC.
4. Walk ops through exception: money must not leave if OTP fails.

### Sample artifact — fully dressed (abridged)

**Name:** Transfer money to saved beneficiary  
**Primary actor:** NovaBank retail customer  
**Secondary actors:** OTP service, core banking, SMS gateway  
**Trigger:** Customer chooses a saved beneficiary and taps Transfer  
**Preconditions:** Customer authenticated; beneficiary active; account not blocked  
**Postconditions (success):** Debit and credit posted; receipt id shown; SMS sent; audit event stored  
**Postconditions (failure):** No ledger posting; customer sees reason; audit event stored

**Main flow**

1. Customer selects saved beneficiary and enters amount.
2. System shows fee (if any) and remaining daily limit.
3. Customer confirms.
4. System sends OTP; customer enters OTP.
5. OTP service confirms success.
6. Core banking posts transfer; system shows receipt.

**Alternate — daily limit exceeded**

4a. Amount + today's transfers > daily limit.  
4a1. System blocks confirm and shows remaining limit.  
4a2. Customer reduces amount (return to step 1) or cancels (end, no post).

**Exception — OTP fail**

5a. OTP incorrect or expired (max 3 attempts).  
5a1. System does not call core posting.  
5a2. Customer sees "Transfer not sent — verify OTP" and may restart.  
5a3. After 3 fails, lock transfer for 30 minutes (policy) and log fraud-relevant event.

**Include:** Authenticate session. **Extend:** Add new beneficiary (out of this use case).

### Failure if ignored

OTP fail still calls core banking; duplicate posts. Or limit is only in the UI and API bypasses it. Audit cannot explain a transfer. Stories said "transfer works."

## Weak vs strong

| Weak | Strong |
|---|---|
| Use case = a stick-figure diagram only | Written flows with pre/post |
| Alternate and exception mixed | Limit = alternate; OTP fail = exception |
| Every story fully dressed | Dress high-risk goals; brief the rest |
| Secondary actor ignored | OTP and core named; failure owned |

## Notes

- Primary actor gets the value; secondary actors are helpers or other systems.
- Include = always; extend = sometimes; generalize = shared type.
- If postcondition on failure is missing, testers will not know whether money moved.
- Map use-case steps to stories so Agile teams still slice.
- Brief is a map; fully dressed is a contract for complex goals.
