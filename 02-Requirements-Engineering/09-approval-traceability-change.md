# Approval, Traceability, and Change

Requirements are not official because they exist in a doc. They become official when **approved**, stay trustworthy when **traced**, and stay safe when **change is controlled**.

This file also covers **dependencies, assumptions, and constraints** as attributes you must attach to requirements — not as afterthoughts.

## Why it matters for a BA

MediCare+ will fail UAT when lab integration is added after baseline and nobody traces the new fields to tests. NovaBank will implement a “small” KYC tweak that breaks loan origination because the dependency was never recorded. Approval without a baseline is theatre. A baseline without change control is a rotting document.

## Requirement approval and sign-off

**Approval** is a named person’s decision that this set of requirements is accepted for a defined scope and version.

| Element | Meaning |
|---|---|
| Who | People with authority: sponsor/PO for business, compliance for regulated, architecture for technical constraints, ops for operational Musts |
| Evidence | Signed page, e-mail with version hash, Jira “approved” on a versioned Confluence page, CAB minutes — not a thumbs-up in chat |
| Baseline | The frozen set: IDs + version (e.g. FRD v1.0). Further edits need a CR |
| Scope of approval | What they approved (MVP wallet, not “all future wallet ideas”) |
| Date and version | Always stored together |

**Weak:** “Everyone was in the meeting so it’s approved.”
**Strong:** “Digital PO + CISO approved NovaBank FR-AUTH-014 v1.0 on 4 Apr; baseline stored; distribution list recorded.”

ShopEase: category policy owner must sign return rules; the PO cannot silently override legal.

Who signs depends on risk. A colour change on QuickBite’s cuisine filter may be PO-only. A KYC change needs compliance.

## Traceability

**Traceability** is a chain you can walk in both directions:

Business need → requirement → story → test → release

| From | To | Why |
|---|---|---|
| BR-01 Reduce no-shows | FR-APT-12 Send reminder | Need is not lost in a screen |
| FR-APT-12 | Story MC-441 | Dev knows the requirement ID |
| Story MC-441 | TC-889 SMS 24h before | QA knows what “pass” means |
| TC-889 | Release 2.4 | Ops knows what went live |

Forward trace: is every need covered?
Backward trace: why does this test exist?
If a test has no requirement, it is either extra gold-plating or a missing requirement.

ShieldSure: a payout story with no BR means someone is paying garages without a stated business need — stop.

## Change management

After baseline, change is a **Change Request (CR)**, not a hallway conversation.

| CR field | Purpose |
|---|---|
| CR ID, date, requester | Identity |
| Description | What would change |
| Reason | Need, not solution only |
| Impact analysis | Reqs, stories, tests, data, vendors, training, cost, dates, risk |
| Requirements touched | Old version → proposed version |
| Decision | Approve / defer / reject |
| New baseline version | e.g. 1.0 → 1.1 |

**Impact analysis** is the BA’s core CR skill. “Small change” is not an analysis.

Version the requirement, not only the document: FR-APT-12 v1.1.

## Dependencies, assumptions, constraints

These attach to individual requirements and to the set.

| Term | Definition | Example |
|---|---|---|
| Dependency | Something outside this work that the requirement needs | MediCare+ reminders depend on the SMS gateway vendor SLA and patient mobile in EMR |
| Assumption | Treated as true, not fully proven | 92% of NovaBank CIF records have a valid mobile |
| Constraint | Limit that cannot be wished away | ShopEase returns must use logistics API v3 this release; no new courier master |

**Requirement dependencies** (one req needs another): Wallet pay (FR-WLT-02) depends on settlement (FR-WLT-09). If you ship pay without settlement, finance cannot close the day.

Write them explicitly:

- DEP-01: Lab orders require `patient_id` already in EMR (MediCare+).
- ASM-04: Sellers will complete the returns webinar before cutover (ShopEase) — risky; track it.
- CON-02: RBI 2FA on add-money above threshold (NovaBank/ShopEase wallet analogue).

**Weak:** “Assuming labs will send HL7.”
**Strong:** ASM-07 with owner, date to validate, and impact if false (UAT blocked).

## Scenario / Use case: MediCare+ lab integration after baseline

**Context.** Appointment booking + reminders baselined as SRS v1.0. Two sprints later, the hospital group CIO says lab orders must be placed from the same patient app. A developer adds a “Book lab” button. No CR. No RTM update. UAT for release 2.4 includes appointments and, informally, labs.

**Stakeholders.** Clinic admin, lab manager, EMR vendor, patients, billing (lab tariffs), QA, CIO, BA.

**What the BA should have done.**

1. Treat “Book lab” as CR-19 against baseline 1.0.
2. Impact: new FRs (catalogue, slot, fasting instructions), NFRs (result confidentiality), transition (map old lab codes), dependency on LIS vendor, constraint: NABL identification on reports.
3. Trace: BR-LAB-01 → FR-LAB-04 → story MC-512 → TC-901 → release.
4. Re-approve with lab manager + billing, not only CIO.
5. Baseline 1.1.

**What actually goes wrong if ignored.** UAT script still tests reminders only. Lab booking goes to production. Fasting patients book evening slots. Billing uses the wrong tariff because the visit-type dependency was never traced. Patients get SMS for appointments but no lab prep message — the reminder NFR was never extended. UAT “passed” appointments and leadership is confused why labs are a production incident.

**Sample artifact (trace fragment).**

| Need | Req v | Story | Test | Release |
|---|---|---|---|---|
| BR-APT-01 no-shows | FR-APT-12 v1.0 reminder SMS | MC-441 | TC-889 | 2.4 |
| BR-LAB-01 (missing) | — | MC-512 (orphan) | none | 2.4 (untraced) |

The orphan story is the smell. Traceability would have blocked release or forced the CR.

## Approval vs change in Agile

Sprints still need a baseline for the sprint-committed slice and a CR (or backlog + impact note) for anything that alters a committed or live requirement. “We are Agile” is not a licence to skip impact analysis.

## Notes

- 
