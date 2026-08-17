# User Acceptance Testing (UAT)

## Definition

**User Acceptance Testing (UAT)** is testing by the people who will live with the process — not by QA and not by the BA “as proxy” — to confirm the solution is fit for business use.

**UAT planning** sets entry/exit, environment, data, schedule, roles, and defect rules *before* execution.

**UAT scenarios** are business-shaped journeys (including exceptions), fewer and fatter than system test cases.

**UAT execution** is scheduled runs with evidence (results, screenshots, IDs) and a war-room for blockers.

## Why it matters

System testing can pass while the front desk cannot complete a MediCare+ walk-in, or NovaBank maker-checker is unusable in the branch time window. UAT is the last chance to catch **fit-for-purpose** gaps: roles, data, devices, SOPs, reports.

## Who should execute

**Real users** (or trained proxies in the same role): branch ops, clinic receptionist, warehouse QC, claims adjudicator, restaurant manager.

Not: the BA, the developer, the intern who “knows the app,” the PO only on a demo call.

The BA **facilitates**. The business owner **accepts**.

## UAT plan contents

| Topic | What to lock |
|---|---|
| Entry criteria | System testing signed as complete for in-scope; env stable; known defects listed; training done |
| Exit criteria | All P0/P1 scenarios pass or waived in writing; no open Sev1/Sev2 without business risk accept; evidence stored |
| Environment | UAT URL, version, integrations (SMS, payment sandbox), who controls refresh |
| Data | Named patients/accounts, clinic calendars, insurance plans — **not** production PHI dumps |
| Schedule | Dates, shifts, which clinic/branch, backup day |
| Defects | Tool, severity rules, 4-hour war-room triage, BA as business interpreter |
| Roles | Executors, backup, approver, BA, QA env support, IT |
| Scope | In / out; which exceptions are in this release |

### Weak vs strong

| Weak | Strong |
|---|---|
| “Users will try it.” | Named executors, 8 scenarios, timeboxed |
| Prod copy with real patients | Masked / synthetic data, consent if needed |
| BA executes, users sign | Users execute, BA logs defects |
| Exit = date arrived | Exit = evidence vs criteria |
| No war-room | Daily stand-up + blocker channel |

## Eight UAT scenarios: MediCare+ appointments (with exceptions)

**Story context.** New booking + reminder + no-show marking for outpatient clinics.

| ID | Scenario | Includes exception? | Executor |
|---|---|---|---|
| UAT-APT-01 | Book future slot for existing patient, confirmed SMS | Happy | Front desk |
| UAT-APT-02 | Walk-in: next available same-day slot | Happy | Front desk |
| UAT-APT-03 | Patient reschedules; old slot frees; new SMS | Exception: change | Front desk |
| UAT-APT-04 | Cancel by patient within policy; slot released | Exception | Front desk |
| UAT-APT-05 | Double-book attempt same doctor/time — second user blocked | Exception: conflict | Two desks |
| UAT-APT-06 | No-show: mark after grace; utilization report updates | Exception | Desk + doctor |
| UAT-APT-07 | Insurance/plan ineligible for that specialty — warning, still book or block per rule | Exception: eligibility | Desk + billing |
| UAT-APT-08 | Reminder SMS failed (vendor down) — staff see failed status, fallback call list | Exception: integration | Desk + ops |

Pass each with: patient test ID, timestamps, screenshot/message ID, and “SOP still matches.”

## BA role during the UAT war-room

- Open with: today’s scenarios, env version, known issues.
- Translate “it’s wrong” into: defect vs training vs data vs change request.
- Keep users on **script + exploratory within role**, not random admin screens.
- Protect scope: new wishes go to parking lot, not silent scope add.
- Update RTM / results log the same day.
- Escalate Sev1 (cannot book, wrong doctor, PHI leak) immediately.
- End of day: go / no-go recommendation, not “we’ll see.”

## Real-world examples

**ShopEase.** Warehouse UAT of returns on handhelds, not only HQ Chrome.

**NovaBank.** Maker-checker UAT with dual users; BA does not approve both sides.

**QuickBite.** Restaurant device on 4G; peak-hour scenario, not office Wi-Fi only.

**Government.** Citizen portal UAT with actual clerks and a sample citizen journey, plus accessibility exception.

## Scenario / Use case: MediCare+ UAT week

**Context.** Go-live in 10 days. QA reports 0 Sev1. Clinics fear the new grid.

**Plan.** Entry: QA complete, SMS sandbox, 50 synthetic patients, two clinics. Exit: UAT-APT-01 to 08 pass at both clinics; Sev2 ≤ 2 with workarounds. Schedule: Tue–Thu execution, Fri retest.

**War-room.** Wednesday UAT-APT-05 fails: two desks book the same slot (cache). BA logs defect vs FR-APT-12, not “training.” Thursday UAT-APT-08: SMS fail flag missing — process fallback written, defect Sev2. Users still execute; BA does not take the mouse.

**If ignored.** Go-live with double-booking; doctors revolt; “UAT was done” means the BA clicked.

## Notes

- UAT = real users, real-like process, scheduled evidence.
- Plan: entry/exit, env, data, schedule, defects — written.
- Scenarios include exceptions (conflict, cancel, integration fail, eligibility).
- BA facilitates the war-room; users execute; owner signs.
- Data is a requirement: synthetic, role-correct, enough volume.
- Exit criteria beat calendar pressure — or risk is explicit.
- Parking lot new features; do not grow scope mid-UAT.
- Failed integration scenarios are first-class, not “nice to have.”
