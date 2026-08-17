# Acceptance Criteria, Definition of Ready, Definition of Done

## Definition

**Acceptance criteria (AC)** are conditions that must be true for a story to be accepted by the business. They describe *behavior*, not implementation.

**Definition of Ready (DoR)** is the team's checklist that a backlog item is clear enough to start.

**Definition of Done (DoD)** is the team's checklist that work is complete enough to release or demo as "done."

## Why it matters

AC without DoR produces stories that look small and explode in the sprint. DoD without AC produces "we coded it" while UAT fails. Test cases without AC invent expected results. The BA owns clarity of AC and helps the team keep DoR/DoD honest.

## Concepts

### Acceptance criteria formats

**Given / When / Then (GWT)** — behavior and rules:

```
Given a MediCare+ patient has a confirmed appointment
When they cancel more than 2 hours before the slot
Then the slot is released and they see "Cancelled — no fee"
```

**Checklist** — useful for UI and data presence:

- Appointment shows doctor, clinic, date, time.
- Patient can add a reason (optional, 200 characters).
- Confirmation SMS is sent within 1 minute.

**Business rules inside AC** — do not hide rules in a side email:

| Rule | In AC |
|---|---|
| Cancellation window | Cancel allowed until 2 hours before start |
| Late cancel | Within 2 hours: mark cancelled, slot may stay blocked, show fee policy |
| Who can cancel | Patient or clinic receptionist; doctor cannot cancel from patient app |

Write the rule once in AC; GWT scenarios prove it. If a rule applies to many stories, put a rule ID (e.g. BR-APT-04) in AC and keep the full text in a rule catalog.

### Sample team DoR (story cannot enter sprint unless)

- Actor, value, and scope boundaries are written.
- AC include happy path plus at least one exception.
- Dependencies (legal text, vendor, data) named or waived.
- UX sketch or flow exists if UI changes.
- Story is small enough for one sprint (team agrees).
- PO is available for questions this sprint.

### Sample team DoD (story cannot be "Done" unless)

- Code merged; AC automated or manually tested.
- NFR checks agreed for the story (e.g. SMS sent).
- Logging/audit if the story touches a decision.
- Product increment demoable on a test environment.
- No open Sev-1/2 defects on this story.
- AC signed off by PO (or BA+PO as designed).

### AC vs DoD vs test cases

| | AC | DoD | Test cases |
|---|---|---|---|
| Level | This story's behavior | Team quality bar for all work | Step-by-step verification |
| Owner | BA + PO + team | Whole Scrum team | QA, with BA review |
| Example | Cancel allowed until T-2h | Tested, logged, demoable | Step 4: cancel at T-1h59, expect fee warning |
| Changes per story | Yes | Rarely | Many per story |

AC are the contract. DoD is the factory standard. Test cases are the inspection script. Do not paste 40 test steps into AC; keep AC intent-level and let QA expand them.

## Real-world examples

1. **ShopEase checkout:** AC "Given a saved card, When the buyer pays, Then the order is placed and inventory is reserved" — DoD still requires PCI logging and no card number in app logs.
2. **NovaBank transfer:** AC cover limit and OTP; DoD requires the audit event even if the UI looks finished.

## Scenario / Use case: MediCare+ book appointment "looked done"

### Context

Story: "As a patient I want to book an appointment so that I can see a doctor." AC listed: pick doctor, pick slot, see confirmation. Team marked Done. UAT: patients cancelled 10 minutes before the slot; clinic still blocked the room; no-show rate and complaints exploded. AC never mentioned a **cancellation window**.

### Stakeholders

Patient, clinic receptionist, doctor, PO, BA, QA, call center.

### BA actions

1. Add rules: cancel until 2 hours before; late cancel behavior; who can cancel.
2. Rewrite AC in GWT for on-time cancel, late cancel, and clinic-side cancel.
3. Update DoR: booking stories must include cancel/no-show policy.
4. Add a follow-up story if waitlist fill is in scope (do not hide it in the same AC).

### Sample artifact (story AC after fix)

```
Given a confirmed appointment more than 2 hours away
When the patient cancels
Then status = Cancelled, slot is released, SMS confirms no fee.

Given a confirmed appointment less than 2 hours away
When the patient cancels
Then status = Late cancellation, slot stays blocked unless clinic releases it,
and the patient sees the clinic's late-cancel policy.

Given the clinic releases a late-cancelled slot
When a waitlisted patient exists
Then that flow is out of scope for this story (new story).
```

### Failure if ignored

UAT fails after "Done." Clinics overbook or refuse the app. Trust in Agile drops because "done" did not mean usable.

## Weak vs strong

| Weak | Strong |
|---|---|
| AC: "User can book." | GWT plus cancellation window rule |
| DoR: "PO said OK" | Checklist: AC, exception, dependency, size |
| DoD = "dev finished" | Tested, demoable, audit, no Sev-1 |
| AC copied from 20 test cases | Intent in AC; detail in tests |

## Notes

- If a tester cannot fail the story using AC, the AC are not testable.
- DoR is a conversation gate, not a document shrine.
- DoD is not AC; a story can meet DoD technically and still fail AC.
- Put policy windows (cancel, refund, OTP expiry) in AC on day one.
- "Looks done" is not Done; UAT uses AC, not screenshots of a happy path.
