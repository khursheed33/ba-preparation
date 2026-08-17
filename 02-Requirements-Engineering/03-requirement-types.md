# Requirement Types

Requirements come in **layers**. Mixing them in one list (“the system shall be awesome and also refund in 3 days and use Kafka”) makes prioritization and testing impossible.

BABOK-style layering: business → stakeholder → solution (functional + non-functional) → transition. Technical requirements sit with solution/architecture constraints.

## Why it matters for a BA

ShopEase “returns” is not one requirement. It is a business goal, seller and buyer needs, screens and APIs, speed/security, and a go-live training plan. If you only write functional screens, you miss NFRs and transition. If you only write business goals, developers cannot build.

## The types (learn all of them)

| Type | Answers | Owner typically | Example seed |
|---|---|---|---|
| Business requirements | Why are we doing this? What outcome? | Sponsor / product | Cut return-to-refund cycle |
| Stakeholder requirements | What does a group need from the solution? | Named stakeholder class | Sellers need visibility of return reason |
| User requirements | What must a user be able to do? | End-user role | Buyer can raise a return from My Orders |
| Functional requirements | What must the system do? | BA + PO | System creates RMA and notifies seller |
| Non-functional requirements (NFR) | How well must it do it? | BA + architect + ops | Return search p95 < 2s |
| Transition requirements | What is needed to move from old to new? | Ops + BA + training | Train 200 sellers; migrate open RMAs |
| Technical requirements | Technology, interface, or platform constraints | Architecture / IT | Must use existing returns API v3 |

**User vs stakeholder:** a user interacts with the system (buyer, agent). A stakeholder may not (finance, regulator) but still has requirements.

**Functional vs NFR:** functional is *what*. NFR is *how well* (quality attributes).

**Transition vs functional:** transition is temporary (training, data migration, parallel run). When cutover is done, many transition requirements retire.

**Technical vs functional:** “Must encrypt PAN at rest” can be written as NFR-security; “Must call CIF via ISO 20022” is a technical/interface requirement. Do not hide design opinions as technical requirements unless they are real constraints.

## BABOK-style layering: one ShopEase returns feature

Feature: **Easy Returns** for delivered orders.

| Layer | ID | Statement |
|---|---|---|
| Business | BR-RET-01 | Reduce average return-to-refund time from 9 days to ≤ 4 days within 2 quarters, without increasing fraudulent returns above 1.2% of return GMVs. |
| Stakeholder | ST-RET-01 | Buyers can initiate a return without calling support. |
| Stakeholder | ST-RET-02 | Sellers receive return reason and evidence before the reverse pickup is closed. |
| Stakeholder | ST-RET-03 | Finance can reconcile refunds to original payment instrument. |
| User | UR-RET-01 | A logged-in buyer can request a return from My Orders for an eligible delivered item. |
| Functional | FR-RET-10 | When a buyer submits a return, the system creates an RMA, blocks a second return on the same order line, and notifies the seller. |
| Functional | FR-RET-11 | Refund is triggered only after warehouse scan-in or seller accept, per policy. |
| NFR | NFR-RET-P01 | Return request submit p95 ≤ 2 seconds. |
| NFR | NFR-RET-S01 | Only the order’s buyer account can create the RMA (session + order ownership). |
| Transition | TR-RET-01 | Migrate open RMAs from the old portal; no RMA left in “unknown” status. |
| Transition | TR-RET-02 | Publish seller help article and 15-minute webinar before go-live. |
| Technical | TECH-RET-01 | Reverse pickup must use the existing logistics partner API; no new courier master in this release. |

## NFR categories

Write NFRs with a measure, load, and condition. “Secure” is not an NFR.

| Category | What it covers | Strong example |
|---|---|---|
| Performance | Speed, throughput, latency | MediCare+ slot search p95 ≤ 1.5s for 5,000 concurrent clinic staff at peak 9 a.m. |
| Security | Authn, authz, data protection | NovaBank fund transfer requires 2FA; session idle timeout 5 minutes. |
| Usability | Learnability, errors, accessibility | ShopEase return form: 3 fields default; WCAG 2.1 AA for the flow. |
| Availability | Uptime, planned windows | ShieldSure claims intake 99.5% monthly excluding Sunday 02:00–04:00 IST window. |
| Scalability | Growth without redesign | QuickBite order service handles 3× New Year’s Eve peak without manual sharding. |
| Compliance | Laws, regulators, policy | NovaBank KYC retention per RBI; MediCare+ EMR access logged (audit). |
| Maintainability | Change cost, logs, config | Return window days are config, not hard-coded; change without release. |

NovaBank NFR mix: a loan decision API can be functionally correct and still fail if it is slow (performance), down at month-end (availability), or logs PAN in plain text (security/compliance).

## Weak vs strong typing

| Weak | Strong |
|---|---|
| The returns module should be fast and easy. | Split into UR + FR + NFR-performance + NFR-usability |
| Technical: use React | Not a requirement unless it is a mandated standard; it is design |
| Transition: train people | TR-RET-02: 200 active sellers complete 15-min webinar before cutover; attendance logged |

## Scenario / Use case: MediCare+ appointment booking

**Context.** MediCare+ is rolling a new specialist booking module for 12 clinics. Today: reception books in Excel; doctors’ calendars conflict; patients no-show at 22%. Leadership wants online booking. IT wants it on the existing EMR. Nursing is worried about double-booking of procedure rooms.

**Stakeholders.** Patients, reception, specialists, nursing (rooms), billing, EMR vendor, IT security, clinic admin, training lead.

**What the BA does.** Types the work so nothing is only “a screen”:

- Business: reduce no-shows; fill cancelled slots.
- Stakeholder: doctors control which slots are bookable; billing needs the visit type for tariff.
- User: patient books, reschedules, cancels; reception overrides for walk-ins.
- Functional: hold slot 10 minutes; prevent double-book; send reminder.
- NFR: peak 9 a.m. performance; OTP login; 99.5% availability during clinic hours; ABDM / privacy consent.
- Transition: migrate next-14-days Excel bookings; train reception; parallel run 5 days.
- Technical: must write appointments into EMR API v2; no second calendar of record.

**Sample requirements.**

| ID | Type | Statement |
|---|---|---|
| BR-APT-01 | Business | Reduce specialist no-show rate from 22% to ≤ 12% in 6 months. |
| FR-APT-07 | Functional | Patient can book an available slot for a selected doctor and visit type; system holds the slot for 10 minutes until OTP confirm. |
| NFR-APT-P01 | Performance | Slot grid refresh p95 ≤ 1.5s at 500 concurrent patients. |
| NFR-APT-S01 | Security | Patient sees only their appointments; staff access is role-based and audited. |
| TR-APT-01 | Transition | Import confirmed Excel appointments for T+14 days; duplicates flagged for reception, not auto-merged. |
| TR-APT-02 | Transition | All 12 reception teams complete a 45-minute training and a 10-case sandbox before go-live. |

**What goes wrong if ignored.** The team ships a pretty booking UI (functional only). Excel is not migrated, so Monday is double-booked. Reception was not trained and reverts to paper. Reminders were “someone’s job” (missing NFR + transition). No-shows do not fall. Doctors blame the BA.

## How to use types in a workshop

Put a parking lot: Business / Stakeholder / User / Functional / NFR / Transition / Technical. Every sticky must land in one column. If it lands in two, split it.

## Notes

- 
