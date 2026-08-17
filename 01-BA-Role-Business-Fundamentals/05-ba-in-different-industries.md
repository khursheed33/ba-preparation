# Business Analyst in Different Industries

A BA's core skills stay the same. The **domain language, processes, regulations, and systems** change by industry.

## Why industry knowledge matters

Stakeholders speak in domain terms. If you do not understand those terms, you cannot write good requirements.

Example: in banking, "KYC", "loan origination", and "settlement" are everyday words. In healthcare, "claim", "EMR", and "patient journey" matter.

## How the BA role changes by industry

| Industry | Typical BA work |
|---|---|
| Banking / FinTech | Payments, loans, KYC, compliance, core banking |
| Insurance | Claims, underwriting, policy admin |
| Healthcare | Patient records, billing, appointments, compliance |
| E-commerce / Retail | Orders, inventory, returns, customer journey |
| Logistics / Supply Chain | Shipments, warehouses, tracking |
| Manufacturing | Production, inventory, quality, ERP |
| Telecom | Plans, billing, network-related processes |
| SaaS | Features, onboarding, subscriptions |
| EdTech | Courses, enrollments, assessments |
| HR | Hiring, payroll, employee lifecycle |
| Travel | Bookings, cancellations, inventory |
| Government | Citizen services, compliance, approvals |
| Real Estate | Listings, transactions, property workflows |

## What to learn for any industry

- Industry terminology
- Main business processes
- Common problems and KPIs
- Typical software systems
- Key stakeholders
- Basic regulations

## Study tip

Pick **one domain first**. Learn its language well. You can switch domains later; the BA method stays reusable.

## Real-world examples across the five companies

| Company | Industry | Domain terms you must not fake | Typical BA problem |
|---|---|---|---|
| ShopEase | E-commerce / marketplace | RTO, QC, seller SLA, GST invoice, COD vs prepaid | Returns cycle time and refund visibility |
| NovaBank | Banking | KYC, CIF, bureau, sanction, disbursal, NPA | Loan origination cycle time and completeness |
| MediCare+ | Healthcare | EMR, consent, no-show, clinical specialty rules | Appointment reminders without violating consent |
| QuickBite | Food ordering | Prep time, rider SLA, restaurant accept, compensation | Late orders and who pays |
| ShieldSure | Insurance | FNOL, underwriting, cashless, IRDAI, garage network | Claims cycle and cashless hospital/garage pay |

### Weak vs strong industry behaviour

| Weak | Strong |
|---|---|
| Using ShopEase language in a NovaBank interview (“cart,” “SKU”) | Learning 20 domain terms and one end-to-end process |
| Claiming “I can do any domain” with no process map | One deep case + honesty about what you would learn in week 1 |
| Ignoring regulation | Asking compliance in the first week (RBI, IRDAI, clinical consent) |

## Scenario / Use case: MediCare+ BA hired from ShopEase

**Context.** You did a ShopEase returns case. MediCare+ hires you as a Functional BA for outpatient appointments. On day 3 a doctor says, “Don’t SMS psychiatry follow-ups.” You almost copy-paste ShopEase “notify the customer at every status change.”

**Stakeholders.** Doctors, clinic ops, patients, legal, EMR vendor, you (BA), PO.

**What the BA does.**

1. Keep the *method*: problem → process → rules → requirements. Change the *content*.
2. Elicit specialty-level constraints. Psychiatry, some oncology, and VIP rooms may suppress SMS body content.
3. Write a rule table, not a slogan: `IF specialty IN (restricted) THEN send in-app only`.
4. Add a transition requirement: staff training so receptionists do not promise “you will get a text” for those clinics.
5. Log a question for legal: what is allowed in SMS vs app for each specialty.

**Sample artifact.**

| Specialty | SMS allowed | App push | What the message may contain |
|---|---|---|---|
| General medicine | Yes, if consent | Yes | Clinic, time, reschedule link |
| Psychiatry | No SMS | Yes, generic | “You have an appointment” — no specialty name |
| Lab collection | Yes | Yes | Slot + fasting instruction |

**What goes wrong if ignored.** You ship ShopEase-style notifications. A clinical constraint mentioned once is missed. Trust with doctors collapses; compliance opens an incident. Industry knowledge was the requirement, not a nice-to-have.

## Notes

- Method travels; vocabulary and regulation do not. Study one domain’s happy path and exceptions.
- Interviewers test whether you ask about compliance early.
- Use ShopEase, NovaBank, and MediCare+ as your three “I have seen a process” stories even as a fresher.
- 
