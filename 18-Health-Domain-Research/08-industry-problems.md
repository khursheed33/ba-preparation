# Industry Problems and BA Opportunities

> **Sequence: Phase 3, file 08.**  
> **Stop.** Open this only after the gate in `00-how-to-use-this-pack.md` (files `01`–`07` done).  
> **Next:** `09-research-methods-and-use-cases.md`. Pick **one** problem. Do not read all solution files the same day.

These are the problems you will be hired to analyse. Each row is a **business problem** (measurable), not a feature request. Map it to people / process / tech / data / policy before you write a single FR.

Volumes are **illustrative industry patterns**. Replace with the client’s HIS/LIS extract on a real job.

---

## Problem catalog

| ID | Problem | Who hurts | Typical metric (illustrative) | Usual false solution | Real BA lever |
|---|---|---|---|---|---|
| P-01 | OPD chaos / no-show | Patient, doctor, revenue | Wait 90+ min; no-show 18–25% | “Build an app” | Roster + slot + reminder + walk-in windows |
| P-02 | Duplicate / wrong UHID | Clinical safety, billing | Duplicate 5–15% | “Search better” | MPI rules, merge, privilege to merge |
| P-03 | Cashless pre-auth delay | Patient, TPA desk, AR | Pre-auth hours; discharge hold 2–6 h | More TPA staff | Eligibility at admit + structured pack + status |
| P-04 | Claim denial / query loop | CFO, patient gap | Denial 12–20%; AR 45–70 days | “Follow up harder” | Coded reasons, completeness checklist, NHCX path |
| P-05 | Package vs item leakage | Finance, patient trust | Unbilled or overbilled extras | Training memo | Package BOM in HIS, exception BR |
| P-06 | Bed not ready / delayed discharge | Occupancy, OT | Bed turnaround 6–12 h | Buy more beds | Discharge-before-noon + pharmacy + TPA parallel |
| P-07 | Lab TAT miss | Clinician, aggregator SLA | 20%+ past committed TAT | Blame courier | Clock start/stop, barcode, analyser worklist |
| P-08 | Sample mix-up | Patient safety | Mismatch / recollection 1–4% | Extra sticker | Accession ID, two-identifier rule |
| P-09 | Home-collection no-show | Cost, TAT | 15–20% | Overbook randomly | Slot + reminder + geo slot + fee rule |
| P-10 | Pharmacy stock vs bill | Margin, NABH | Expiry write-off; ward leakage | CCTV | Indent–issue–bill triangle, NDPS dual control |
| P-11 | e-Rx not reaching pharmacy | Patient, leakage | Paper Rx still 40%+ | Mandate overnight | Privilege, template, allergy alert *owner* |
| P-12 | Results SMS on family phone | Privacy, DPDP | Incidents | “Add disclaimer” | Consent class + OTP/app, not naked link |
| P-13 | ABHA linkage stall | Strategy, scheme | Linkage << footfall | Banner in lobby | Script, offline path, refusal reason, not force |
| P-14 | EMR clicks vs 5-min consult | Doctors, adoption | Notes after clinic in Word | Bigger EMR | Encounter template, scribe/dictation, Must fields only |
| P-15 | HIS–LIS–PACS islands | Orders, billing | Order without result; result without charge | “One vendor” | Order ID across systems, HL7 contract |
| P-16 | Downtime with no paper SOP | Safety | Last outage: lost orders | Hope | Transition requirements: paper + catch-up |
| P-17 | OT first-case delay | Utilisation, ARPOB | Start +40 min | WhatsApp OT list | Freeze list, equipment, consent, ICU bed |
| P-18 | Critical value not called | Safety | Missed call | SOP poster | LIS alert + recorded call + EMR ack |
| P-19 | Corporate/PM-JAY package mapping | Rejection | High query % | Excel mapping | Empanelment master, photo/ID, package code |
| P-20 | M&A two-HIS | Duplicate everything | Two bills, two allergies | “We’ll migrate later” | MPI, code-set, TPA IDs, cutover plan |
| P-21 | Notes after hours / unstructured EMR | Doctors, RCM, NABH | Same-day structured note % low | “ChatGPT for doctors” | HITL scribe; doctor is author; eval (file `13`) |
| P-22 | Cashless PDFs in WhatsApp | TPA desk, AR | Pack assemble hours | Unsupervised PDF chatbot | Checklist in HIS first; then IDP + confirm |
| P-23 | Shadow AI (staff paste PHI) | DPO, MSA | Incidents | Ban posters only | Enterprise tenant, DLP, BA redaction rule |

---

## Root-cause patterns (use these in workshops)

**5 Whys — cashless discharge hold**

1. Patient still in lobby at 16:00.  
2. Final approval not in.  
3. TPA queried “implant invoice missing.”  
4. Implant billed in OT but document sat in WhatsApp.  
5. No rule: cashless file completeness **before** ward sends discharge.

Root: **policy + data**, not “slow TPA.”

**Fishbone — lab TAT**

- People: night technician shortage.  
- Process: TAT starts at registration, not at sample-in-lab.  
- Tech: analyser not on worklist (manual result entry).  
- Data: barcode reprint without void.  
- External: aggregator surge 07:00–09:00.

**Pareto — OPD wait**

Usually: unscheduled walk-in + doctor late + missing file + billing after consult. An app that does not publish roster does not move P50 wait.

---

## People / process / tech / data / policy (how you classify gaps)

| Type | Example | Artifact |
|---|---|---|
| People | Doctors overbook from memory | Roster workshop, RACI |
| Process | Eligibility after surgery | As-Is/To-Be, BR |
| Tech | No HIS slot API | FR + vendor dependency |
| Data | Duplicate mobile = identity | MPI rules, merge SOP |
| Policy | No 15-min no-show | BR signed by MS/COO |

If your gap list is 100% “tech,” you have not been on the floor.

---

## What good looks like (targets you can propose, then baseline)

Propose targets only after a 2-week measurement. These are **starting hypotheses**:

| Area | Baseline pattern | Target pattern |
|---|---|---|
| OPD pre-booked | 20–40% | 70% (MediCare+ style) |
| No-show | 18–25% | ≤ 12% with reminder + rule |
| Duplicate UHID | 5–15% | ≤ 2% active; merge SLA |
| Cashless planned pre-auth | Same-day chaos | Pack complete T–24h; TAT clock |
| Denial | Uncoded | 100% reason code; top 5 fixed |
| Lab TAT | Argument | Clock definition + % met by test |
| ABHA | Forced at counter | Offered; refusal captured; no care denial |
| Privacy | SMS with diagnosis | Results behind auth; audit |

---

## Opportunity map by company type

| If the client is… | First problem to pick | Why |
|---|---|---|
| 200–800 bed hospital | P-03 / P-06 | Cash and beds; COO will sponsor |
| Clinic chain | P-01 / P-02 / P-12 | Identity and access |
| Diagnostics | P-07 / P-08 / P-09 | Sample grain |
| Insurer | Query TAT + leakage | Different system of record |
| Marketplace | Partner SLA + order state | You do not own HIS |
| Post-merger group | P-20 | Everything else is noise until MPI |
| Services firm + Gen AI CoE | P-21 / P-22 / P-23 | SOW a HITL use case; full copilot BRD is file `13` after file `10` |

---

## BA projects vs non-BA work

| You own | You facilitate | You refuse to invent |
|---|---|---|
| Process, rules, FRs, UAT, RTM | Clinical protocol with HOD | Drug dose, ICD assignment as “BA opinion” |
| Consent capture, access matrix | Legal wording with DPO | “HIPAA-like later” |
| Slot/TAT/denial KPIs | Finance formula for ARPOB | Fake precision without extract |
| Vendor API contract (fields, SLA) | Architecture choice | Secret exploit / “hack the HIS” |

---

## Scenario / Use case: sponsor wants AI triage

**Context.** Board saw a demo. Ask: “Put AI on symptoms in the app.”

**What you do.** Ask what happens today at 02:00 for chest pain (ER redirect). Write out-of-scope: diagnosis. In-scope: emergency disclaimer, nurse protocol, audit of advice. NFR: no AI advice as record without clinician. UAT: chest-pain path must **not** book a dermatology slot.

**If ignored.** Liability and wrong-patient routing. This is a Sev1 design error, not a model-tuning task.

## Weak vs strong

| Weak | Strong |
|---|---|
| 20 problems in a slide | One problem, one grain, one KPI, 12-week MVP |
| “Digitise the hospital” | P-03 with eligibility + pack completeness |
| Feature list from vendor brochure | Gaps G-01… with type tags |
| Ignore policy | No-show and consent as signed BRs |

## Notes

- Pick one problem from this catalog; run the 28-artifact checklist (folder 13).
- Safety problems (wrong ID, mix-up, critical value, privacy) outrank NPS cosmetics.
- Cashless and diagnostics TAT are where CFOs fund BAs.
- P-21 to P-23 are how a **services + Gen AI** account usually starts. Process first; copilot second (`13-solution-nimbus-genai-note-copilot.md` — only after the gate).
- Measurement week is part of the project, not a delay.
