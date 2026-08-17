# Healthcare Domain Primer

## Definition

**Healthcare** delivery (as a BA domain) is the operational system around **care encounters**: appointments, clinical records, billing, and privacy. An **EMR/EHR** (electronic medical record) is the system of record for clinical documentation. **Billing** converts encounters into charges (self-pay, insurance, packages). **Privacy** is legal and ethical control of who may see what (role, consent, audit).

MediCare+ in these notes is a multi-clinic outpatient + day-care provider with diagnostics.

## Why it matters

A “booking app” that ignores slot rules, doctor leave, and consent still harms patients. Privacy is not an NFR footnote: wrong-patient chart or SMS to the wrong number is a Sev1. Billing fights (package vs itemized) become requirements if you listen only to IT.

## Business model

| Stream | Idea |
|---|---|
| Consults / procedures | Fee per visit or package |
| Diagnostics | High volume, slot + machine capacity |
| Pharmacy / consumables | Margin + clinical protocol |
| Insurance / TPA | Cashless or reimbursement; empanelment |
| Occupancy / utilization | Unused slot is lost revenue |

## Key processes (As-Is)

**Appointments**

1. Patient identified (UHID) or registered
2. Specialty / doctor / slot chosen
3. Confirmation (SMS) + prep instructions
4. Check-in, vitals, queue
5. Consult; follow-up slot
6. No-show / cancel / reschedule rules

**EMR**

1. Open encounter for the right UHID
2. Notes, orders (lab/rx)
3. Results in; doctor reviews
4. Close encounter; access logged

**Billing**

1. Services from encounter + orders
2. Package vs item; insurance eligibility
3. Collect copay / full; invoice / GST as applicable
4. Claim to payer if insured

## Stakeholders and systems

| Stakeholders | Interest |
|---|---|
| Patient / attendant | Access, wait, bills |
| Front desk | Throughput, errors |
| Doctor / nurse | Chart, queue, legal record |
| Billing / TPA desk | Leakage, denials |
| Clinical admin | Protocols, privileges |
| IT / HIM | EMR, downtime |
| Compliance / DPO | Privacy, retention |

| System | Role |
|---|---|
| HIS / EMR | Chart, orders |
| Scheduling | Slots, resources |
| LIS / RIS | Lab / radiology |
| Billing / RCM | Charges, claims |
| CRM / app | Reminders |
| Identity | UHID, ABHA-style IDs where used |

## Regulations lite

- Patient privacy and consent (DPDP-style + clinical ethics)
- Who may access EMR; audit logs
- Prescription / record retention
- Insurance empanelment rules
- Not medical advice: BAs do not design clinical protocols alone

## KPIs and common BA projects

| KPI | Use |
|---|---|
| Slot utilization | Capacity |
| No-show % | Access + revenue |
| Median wait after check-in | Experience |
| Days to next specialist slot | Access |
| Claim denial % | Billing quality |
| Duplicate UHID rate | Master data |
| EMR access exceptions | Privacy |

**Projects:** appointment + SMS, UHID merge, queue management, e-prescription, TPA desk, patient app, no-show overbook policy.

### Weak vs strong

| Weak | Strong |
|---|---|
| Calendar widget only | Conflict, leave, room, equipment |
| One patient phone = identity | UHID merge rules |
| “HIPAA-like later” | Role-based access + audit in MVP |
| Utilization without no-show | Pair the two KPIs |

## Real-world examples

**MediCare+** double-book (see UAT notes) vs **inpatient** bed management — different grain.

**Diagnostics:** machine calendar is a resource like a doctor.

**Pharmacy:** allergy and interaction are clinical; BA captures *who is alerted*, not the algorithm.

## Scenario / Use case: MediCare+ privacy on family phone

**Context.** Many patients share a family mobile. SMS with doctor name + time goes to a shared phone. A new “lab results ready” SMS includes a deep link that opens reports without a second factor. Complaint: relative saw a diagnosis.

**BA work.** Consent: which numbers receive what. FR: results require app login or OTP tied to UHID, not only SMS link. Audit: who viewed. UAT: family-phone exception scenario. Legal/privacy in the room.

**If ignored.** Privacy incident; trust loss; possible regulatory event.

## Notes

- Appointments, EMR, billing, privacy are four processes — do not collapse into “the app.”
- UHID quality is a data requirement (duplicates, merges).
- Cashless/TPA is insurance process inside the hospital.
- Utilization and no-show must be designed together.
- Access control and audit are functional for healthcare, not optional polish.
- BAs facilitate clinicians; they do not invent treatment rules.
- Wait time and slot access are the usual “why we are here” problems.
- Downtime SOP (paper) is a transition requirement.
