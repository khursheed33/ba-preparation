# Scope, Constraints, Assumptions, Dependencies, and Risks

These five items appear in almost every BA document. Learn them together.

## Scope

Scope defines **what is included in this work**.

If scope is unclear, the team will keep adding work. That is called **scope creep**.

### In-scope vs out-of-scope

In-scope: included in this project.
Out-of-scope: deliberately excluded, at least for now.

Example — password reset project:

- In-scope: email-based password reset for retail customers
- Out-of-scope: biometric login, admin user password reset, mobile app changes

Writing out-of-scope is as important as writing in-scope. It prevents hidden expectations.

## Constraints

Limits the solution must respect.

Examples:

- Must go live in 8 weeks
- Budget is fixed
- Must use the existing CRM
- Must follow RBI / HIPAA / GDPR rules
- Cannot change the core banking system in this phase

Constraints are not optional. They shape the solution.

## Assumptions

Things you believe to be true, but have not fully confirmed.

Examples:

- Customers have a valid email on file
- The existing SMS gateway can be reused
- Legal will approve the new consent text

Assumptions are risky. If one is wrong, the plan can break. Track them and convert them into facts as soon as possible.

## Dependencies

Work or decisions this project needs from someone or something else.

Examples:

- Waiting for API from another team
- Waiting for legal approval
- Waiting for data migration from an old system

Dependencies can delay delivery even if your own work is ready.

## Risks

Something that **might** go wrong and hurt the project.

Examples:

- Stakeholders may not agree on the process
- Vendor API may not be ready
- Users may resist the new process
- Requirements may change late

A BA helps identify requirement and business risks. The PM usually tracks overall project risk.

## Quick comparison

| Term | Question it answers |
|---|---|
| Scope | What are we doing / not doing? |
| Constraint | What limits us? |
| Assumption | What are we treating as true? |
| Dependency | What must happen first, or outside our control? |
| Risk | What could go wrong? |

## Real-world examples

| Term | ShopEase returns (phase 1) | NovaBank loans (salaried web) | MediCare+ reminders |
|---|---|---|---|
| In-scope | Prepaid orders < ₹2,000; Size reason; SMS status | Salaried personal loans on web; document checklist | SMS + app for general clinics with consent |
| Out-of-scope | Fashion try-and-buy; international; chatbot | Gold loans; branch-only; AI underwriting | Psychiatry SMS body; WhatsApp |
| Constraint | Must use existing reverse-logistics vendor | Must not change core-banking CIF schema this phase | HIPAA-like consent store already live |
| Assumption | 80% of those returns have reason code Size (unverified) | 92% CIF have valid mobile | Patients who gave consent still have the same number |
| Dependency | Payments team for refund API | Bureau API SLA from data team | SMS gateway + EMR appointment events |
| Risk | Sellers revolt if auto-approve is silent | Incomplete-file % was a seasonal spike | Doctors block SMS for more specialties than expected |

### Weak vs strong

| Weak | Strong |
|---|---|
| Scope: “Returns v2” | In: auto-approve + status; Out: chatbot, international |
| Assumption listed once in a kickoff deck | Assumption ID, owner, date to validate, impact if false |
| Risk: “May be delayed” | Risk: seller pushback → mitigation: 14-day notice + opt-out for two seller tiers |

## Scenario / Use case: ShopEase returns — scope creep in week three

**Context.** Phase 1 in-scope: auto-approve Size returns under ₹2,000 and status SMS. Warehouse lead says, “While you are in the code, add damaged-item photos and change pickup slots.” Marketing wants a chatbot. The PM asks the BA to “just add them to the BRD.”

**Stakeholders.** Warehouse, marketing, sellers, PM, PO, BA, legal.

**What the BA does.**

1. Open the signed in/out list. Photos and pickup slots are **out of scope** unless a CR is raised.
2. Impact: photos need QC rules and seller disputes; pickup slots need logistics vendor — new dependency.
3. Options: (A) CR now, slip date; (B) park in phase 2; (C) replace auto-approve with photos (changes the objective).
4. Recommend B for photos/slots; chatbot stays out. Document the decision.
5. Convert a new assumption: “Size reason codes are accurate” — data to verify this week (risk if sellers misuse Size to dump damaged goods).

**Sample artifact.**

| ID | Type | Statement | Owner |
|---|---|---|---|
| SC-RET-IN-02 | Scope | Auto-approve when reason = Size AND amount < ₹2,000 AND prepaid | PO |
| SC-RET-OUT-04 | Scope | In-app chatbot | PO |
| AS-RET-03 | Assumption | Size is not used as a dump code for damaged goods; validate via 200-row QC sample | BA + QC |
| DEP-RET-01 | Dependency | Refund API v3 from payments by 12 Sep | Payments lead |
| RK-RET-02 | Risk | If AS-RET-03 is false, leakage > 3%; mitigation = QC audit + kill switch | PO |

**What goes wrong if ignored.** Everything “while we are here” lands in sprint. Go-live slips. Auto-approve is half-built. Nobody can say what success was. That is scope creep with a friendly face.

## Notes

- Write out-of-scope on day one. It is a stakeholder alignment tool, not negativity.
- Assumptions must be tested; constraints must be respected; dependencies must have owners and dates.
- BA identifies requirement/business risks; PM rolls them into the project register.
- 
