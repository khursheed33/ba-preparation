# SRS and Requirement Specification

An **SRS (Software Requirements Specification)** is a (usually formal) specification of **software behaviour and qualities** for people who must **build, test, or bid** against it: developers, QA, and vendors.

**Requirement specification** is the broader term: any baselined, testable description of requirements (SRS, FRD, catalog). SRS is the classic IEEE-style packaged form.

## Why it matters for a BA

MediCare+ appointment reminders will be implemented by a vendor who never sat in your workshop. If you hand them user-story titles, they will invent timing, channels, and consent. An SRS (or equivalent spec) is the interface with people who were not in the room.

## Audience

| Audience | What they use the SRS for |
|---|---|
| Developers | What to implement; interfaces; rules |
| QA | Test design; coverage against IDs |
| Vendors | Contractual scope; gap analysis; change control |
| Architects | NFRs, integrations, volumes |
| Support / ops (later) | Intended behaviour when incidents happen |
| Business (skim) | Confirm intent — they should have validated earlier; SRS is not their novel |

Do not write the SRS only for the sponsor. If a CIO cannot test a sentence, it does not belong as a functional spec statement.

## Typical IEEE-style sections (explained simply)

IEEE 830-style outlines vary; this is the BA-friendly map.

| Section | In plain language |
|---|---|
| Introduction | What this software is, purpose, scope, definitions (OTP, slot, EMR) |
| Overall description | Product context, users, constraints, assumptions, dependencies |
| External interface | UI, APIs, hardware (SMS gateway, email), other systems (EMR) |
| System features / functional requirements | Numbered “the system shall…” per feature |
| Non-functional / quality attributes | Performance, security, availability, etc. |
| Data | Logical data, validation, retention |
| Other requirements | Compliance, audit, licensing |
| Appendices | Message catalogue, sample reports, trace to BRD |

You do not need the IEEE numbers in the heading. You do need the content. Empty sections are worse than a short SRS that states “N/A with reason.”

## When companies use SRS vs user stories

| Use SRS (or heavy spec) | Use stories + AC |
|---|---|
| Vendor build, fixed-price | In-house Scrum team, high access to BA |
| Medical, banking, insurance audits | Fast product iteration |
| Hardware + software, long test cycles | UI experiments |
| Multiple vendors must integrate | Single team owns the flow |
| Regulator wants a baseline document | PO in the room every day |

Hybrid (common): **SRS for integrations and NFRs** + **stories for UI slices**. MediCare+ reminders: SRS for SMS vendor SLA and consent; stories for “patient edits mobile number.”

**Weak:** SRS of 200 pages no one reads, plus stories that contradict it.
**Strong:** One catalog of IDs; SRS chapters generate from the catalog; stories reference FR-REM-03.

NovaBank core payments to a switch vendor: SRS. ShopEase coupon copy: stories.

## Mini SRS excerpts: MediCare+ appointment reminders

**Product:** MediCare+ Appointment Reminder Service  
**Spec:** SRS-APT-REM v1.0  
**Audience:** EMR vendor, SMS aggregator, QA, clinic IT

### Functional (sample)

| ID | The system shall |
|---|---|
| FR-REM-01 | Send an SMS reminder 24 hours ± 15 minutes before `appointment.start_time` when status is CONFIRMED and `consent.sms` is true and mobile is present. |
| FR-REM-02 | Send an email reminder 2 hours ± 10 minutes before start if `consent.email` is true and email is present; skip email silently if email is absent (do not fail the SMS). |
| FR-REM-03 | Not send reminders if status is CANCELLED or COMPLETED at scheduled send time. |
| FR-REM-04 | Include clinic name, doctor name, date/time IST, and a cancel instruction URL in SMS (max 2 concatenated SMS). |
| FR-REM-05 | Log send result (SENT, FAILED, SKIPPED_NO_CONSENT) against `appointment_id` for 24 months. |
| FR-REM-06 | Retry FAILED SMS once after 5 minutes; then raise ops alert; do not retry email more than once. |

### Non-functional (sample)

| ID | Category | Statement |
|---|---|---|
| NFR-REM-P01 | Performance | Process 10,000 due reminders in ≤ 10 minutes at 07:00 IST peak. |
| NFR-REM-A01 | Availability | Reminder job availability 99.5% clinic days 06:00–21:00 IST. |
| NFR-REM-S01 | Security | SMS body shall not include diagnosis or EMR notes. |
| NFR-REM-S02 | Security | Only reminder-service service account may read `consent` flags. |
| NFR-REM-C01 | Compliance | No send without recorded consent; consent change is audited. |
| NFR-REM-M01 | Maintainability | Lead times (24h / 2h) are configuration, not hard-coded. |
| NFR-REM-U01 | Usability | SMS reading grade: clinic-tested; no URL shortener that looks like phishing (use hospital domain). |

### External interface notes

- SMS aggregator API: already contracted; DLT template IDs required (India).
- EMR: read-only appointment + consent; writes only to reminder log table.
- Email: existing hospital SMTP; from-address `noreply@medicareplus.example`.

### Weak vs strong spec lines

| Weak | Strong |
|---|---|
| The system shall remind patients in a timely manner | FR-REM-01 with 24h ± 15 min and preconditions |
| SMS should be secure | NFR-REM-S01 no diagnosis in body |
| Integrate with EMR | Named read/write entities and direction |

## Requirement specification without the SRS label

If your company forbids “SRS,” still produce: numbered requirements, NFRs, interfaces, glossary, version, trace. The vendor does not care about the acronym. They care that FR-REM-03 exists when they test cancelled appointments.

## Notes

- 
