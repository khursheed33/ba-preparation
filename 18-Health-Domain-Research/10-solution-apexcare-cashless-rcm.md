# ApexCare Hospitals — Cashless Pre-Auth Delay and Claim Denials

> **Sequence: Phase 4, file 10.** After the gate and files `08`–`09`.  
> **Next:** `11-solution-helixlab-sample-tat.md` **or** `12-solution-citywell-abha-emr.md` (one grain at a time). Gen AI SOW is file `13`, after this checklist exists.

**Domain:** Healthcare / RCM. **Company:** ApexCare Hospitals Pvt Ltd (illustrative 3-unit chain). **Role:** BA, Revenue Cycle / HIS. **Grain:** Claim / pre-auth (not OPD slot).

ApexCare: Pune 450 beds, Nashik 250, Kolhapur 150. Occupancy ~63%. ~42% of IPD revenue is insured / TPA / corporate / PM-JAY. HIS is 9 years old (on-prem). TPA desk uses **eight payer portals** plus email. This pack is written as the solution you would take to the COO after two weeks on the floor.

## Business problem

Planned cashless **pre-auth P50 = 6.5 hours** after admission (illustrative). Emergency often **verbal**, pack completed after OT. **Discharge hold P50 = 4.2 hours** waiting for final approval. **Denial + query rate 18%** of cashless files; top reasons uncoded (WhatsApp). Insured **AR days = 52**. Patients NPS at TPA desk **8**. Billing re-keys the same estimate into portals. Implant invoices sit in OT WhatsApp groups. Eligibility is sometimes checked **after** surgery.

Management asked for “a TPA dashboard and AI claim prediction.”

## Business objective

16 weeks + 6-week adopt, Pune first, then replicate:

1. **100%** planned admissions: eligibility status recorded **before** ward transfer (except documented emergency).  
2. Planned pre-auth pack **complete T–24h** for elective listed on OT freeze.  
3. Discharge hold for cashless **P50 ≤ 90 minutes** from “clinically fit” to “financially clear.”  
4. Denial/query **≤ 10%**; **100%** files with a reason code.  
5. AR days insured **≤ 40** (directionally; finance owns the GL).

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| COO / unit heads | H | H | Sponsor; wants dashboard | Weekly denial Pareto |
| Medical Superintendent | H | M | Fear: delay surgery | Emergency exception BR |
| TPA desk lead | M | H | Portal fatigue | Shadow 2 days; co-design pack |
| Ward ICs / nursing | M | H | “Not my job” | Discharge checklist in HIS |
| OT / implant store | M | H | WhatsApp habit | Implant doc in HIS |
| Billing / RCM | H | H | Re-key pain | Single estimate object |
| Patients / attendants | L | H | Lobby wait | Status SMS (no clinical detail) |
| Insurer / TPA (external) | H | M | Incomplete packs | Data contract, not blame |
| HIS vendor | M | M | “No API” | Milestone for status + docs |
| DPO / NABH | H | M | PHI in WhatsApp | Stop clinical docs on WA |
| Finance | M | H | AR days | Clock definition |

## Scope

**In:** eligibility at admission, cashless file in HIS (not Excel), document checklist (planned vs emergency), pre-auth/enhancement/final status, query loop with codes, patient/attendant status (non-clinical), implant/OT document attach, Pune unit MVP, training, audit who submitted.

**Out:** NHCX production cutover (Phase 2 — FHIR mapping spike only), replacing HIS, clinical protocol, AI denial prediction, PM-JAY portal rewrite, OPD appointments (MediCare+), pharmacy e-commerce.

## Assumptions and constraints

**Assumptions:** Payers still require their portals in MVP (HIS stores pack; desk submits or RPA later); planned OT list freeze exists on paper; DLT SMS live.  
**Constraints:** 16-week MVP; no rip-and-replace HIS; DPDP — no diagnosis in SMS; emergency must not wait for portal; illustrative IRDAI-style conduct (do not delay care for paperwork when emergency BR applies).

## As-Is process (diagram described)

1. Admission clerk creates IPD; insurance fields optional.  
2. Ward: surgery proceeds; TPA desk hears at 11:00.  
3. Coordinator builds PDF from WhatsApp + photocopy; **wait 2–8 hours**.  
4. Portal submit; query overnight; coordinator chases.  
5. OT implant invoice photographed to group.  
6. “Fit for discharge” at 14:00; desk starts **final** bill; patient in lobby until 18:00.  
7. Denial discovered at settlement (day 40); reason in email.

**Problem analysis:** Wait is **late eligibility + unstructured pack + implant off-record + final approval serial after clinical discharge**. A dashboard on the same WhatsApp pack does not move AR days.

**Root cause (5 Whys on discharge hold):** Lobby wait because final approval missing → approval missing because query on implant → implant not in file → file assembled after OT → **no BR that cashless completeness is a discharge dependency with a named owner.**

## To-Be process (diagram described)

1. Admission: policy/corporate ID captured; **eligibility = ELIGIBLE / NOT / UNKNOWN / EMERGENCY_OVERRIDE**.  
2. Planned: TPA pack template in HIS; Must docs attached **T–24h** or OT listing cannot stay CONFIRMED (MS exception).  
3. Emergency: care first; pack SLA **T+4h** from admission with override reason.  
4. OT close: implant invoice + sticker photo **attached to IPD file** before OT status = CLOSED.  
5. Queries: coded; owner; clock pauses only on defined codes.  
6. Clinically fit **and** financially clear (copay estimate shown); then discharge.  
7. Patient SMS: status labels only (SUBMITTED / QUERY / APPROVED / PAY_GAP / REJECTED).  
8. Denial Pareto weekly; top codes become BR/training.

## Gap analysis

| ID | Type | Gap | Action |
|---|---|---|---|
| G-01 | Process | Eligibility after OT | Admission mandatory insurance block |
| G-02 | Process | Pack in WhatsApp | HIS cashless file |
| G-03 | Policy | No T–24h rule | BR + MS exception |
| G-04 | Data | No denial codes | Code list (completeness, medical, limit, other) |
| G-05 | Tech | Estimate re-keyed | Single estimate object → print/portal |
| G-06 | Tech | No patient status | SMS/kiosk status API |
| G-07 | People | OT docs not owned | RACI implant attach |
| G-08 | Policy | PHI on WhatsApp | Ban clinical images on WA for cashless |
| G-09 | Tech | Eight portals remain | MVP: HIS as system of record; portal is channel |

## Requirements

| ID | Type | Statement |
|---|---|---|
| FR-RCM-01 | F | Admission cannot complete for non-emergency IPD if payer type IN_NETWORK and eligibility status is blank. |
| FR-RCM-02 | F | System stores cashless file against IPD with checklist by payer type (planned/emergency). |
| FR-RCM-03 | F | Planned OT status cannot be CONFIRMED if cashless pack completeness < 100% unless MS override with reason. |
| FR-RCM-04 | F | OT CLOSED requires implant/consumable invoices attached when implant flag = true. |
| FR-RCM-05 | F | Desk records SUBMITTED / QUERY / APPROVED / ENHANCEMENT / REJECTED / PAID with timestamp. |
| FR-RCM-06 | F | Query requires a reason code from the controlled list. |
| FR-RCM-07 | F | Attendant can see financial status (no diagnosis) after OTP tied to registered mobile. |
| FR-RCM-08 | F | Copay / non-payable estimate displayed before financial clearance. |
| FR-RCM-09 | F | Emergency override captured: user, reason, time; alert to TPA lead. |
| NFR-RCM-01 | NF | Status update visible in HIS ≤ 5s; 99.5% 07:00–22:00. |
| NFR-RCM-02 | NF | Audit: who viewed/uploaded cashless docs; 7-year retention (policy). |
| NFR-RCM-03 | NF | SMS body contains no clinical terms (template approved). |
| TR-RCM-01 | T | Paper pack + register if HIS down; catch-up < 4h after restore. |

## Business rules

- **BR-RCM-01:** Emergency: care is not delayed for eligibility. Override mandatory within 30 minutes of admission.  
- **BR-RCM-02:** Planned cashless pack 100% complete 24h before OT freeze.  
- **BR-RCM-03:** No clinical documents on personal WhatsApp for cashless (HIS attach only).  
- **BR-RCM-04:** Financial discharge requires APPROVED or documented PAY_GAP collected.  
- **BR-RCM-05:** Denial/query without code cannot be saved.  
- **BR-RCM-06:** SMS only if consent_reminders = true; results never in this flow.

## User stories (with AC)

1. **As admission clerk, I want eligibility captured** so surgery is not a surprise denial. **AC:** Given in-network planned, When eligibility blank, Then save blocked.  
2. **As TPA coordinator, I want a HIS checklist** so I do not hunt WhatsApp. **AC:** Planned template shows Must docs; % complete visible.  
3. **As OT nurse, I want to attach implant invoice** so query does not hit at discharge. **AC:** OT CLOSED blocked if implant flag and no attach.  
4. **As attendant, I want status without calling** so I am not in the lobby. **AC:** OTP → status label only.  
5. **As RCM lead, I want coded queries** so we fix the top five. **AC:** Weekly report by code; uncoded count = 0.  
6. **As MS, I want emergency override** so we do not harm. **AC:** Override logged; care path unblocked.

## Use case (fully dressed): UC-RCM-01 Planned cashless admission to pre-auth submit

- **Actor:** Admission clerk, TPA coordinator. **Pre:** Patient registered; policy number; consent captured.  
- **Trigger:** IPD admission with payer = INSURED_CASHLESS.  
- **Main:** Eligibility check recorded → file created → Must docs uploaded → completeness 100% → coordinator submits portal → status SUBMITTED → SMS to attendant.  
- **Alt:** Eligibility NOT → convert to self-pay or reschedule (patient choice logged).  
- **Exception:** HIS portal timeout → status UNKNOWN + manual task; emergency path N/A here.  
- **Post:** File ID; audit; OT listing may confirm.

## Wireframes

1. Admission: payer + eligibility. 2. Cashless file checklist. 3. Upload + viewer. 4. OT close implant attach. 5. Status board (desk). 6. Attendant status (mobile, labels only). 7. Copay estimate. 8. Denial Pareto. 9. MS override.

## Data, reports, KPIs

**Entities:** InpatientStay, Payer, EligibilityCheck, CashlessFile, CashlessDocument, StatusEvent, QueryCode, ImplantFlag, Consent, SmsLog, Override.

**Reports:** Pre-auth TAT (clock: admission eligible → SUBMITTED); pack completeness at T–24h; discharge financial wait (clinically_fit → financially_clear); query codes; AR ageing insured.

**KPIs:** See objectives. Clock definitions in data dictionary; finance signs AR.

## UAT scenarios

- Planned: eligibility blank blocked.  
- Planned: incomplete pack cannot CONFIRM OT (no override).  
- MS override allows OT; audit exists.  
- Implant missing blocks OT CLOSED.  
- Query without code blocked.  
- Attendant OTP; SMS has no diagnosis.  
- Emergency override; care not blocked.  
- Consent false → no SMS; desk still works.  
- Downtime: paper catch-up TR-RCM-01.

## RTM

| Req | Story | UC | UAT |
|---|---|---|---|
| FR-RCM-01 | US1 | UC-RCM-01 | Eligibility blank |
| FR-RCM-03 | US2 | UC-RCM-01 | Incomplete pack |
| FR-RCM-04 | US3 | — | Implant |
| FR-RCM-06 | US5 | — | Query code |
| FR-RCM-07 | US4 | — | Attendant OTP |
| FR-RCM-09 | US6 | — | Emergency |
| BR-RCM-03 | — | — | No WA policy (SOP + training) |
| NFR-RCM-03 | US4 | — | SMS content |

## Change request (sample)

**CR-RCM-01:** Auto-submit to Portal A via RPA. Impact: vendor, brittle UI, credentials. **Decision:** Phase 2; HIS file is Must now. NHCX spike in parallel.

## Risks and dependencies

| Risk | P/I | Mitigation | Owner |
|---|---|---|---|
| Surgeons ignore T–24h | H/H | MS freeze + exception report | MS |
| Payer still slow | H/M | We control pack quality; publish our clock | RCM |
| WhatsApp shadow process | H/H | Block OT close; spot audit | Nursing + BA |
| HIS vendor delay | M/H | File in HIS even if portal manual | PM |
| PHI in SMS | M/H | Template + DPO UAT | DPO |

**Dependencies:** HIS document store, SMS DLT, payer portals (external TAT), implant store billing, OT list freeze process.

## Final business solution

Make the **cashless file the system of record in HIS**, with eligibility at admission, T–24h completeness for planned OT, implant documents at OT close, coded queries, and attendant status **without clinical content**. Do not start with AI or a dashboard on WhatsApp PDFs. Phase 2: RPA/NHCX. Success = discharge hold, denial codes, AR direction — not portal count.

**Phasing.** W1–2 measure clocks. W3–6 admission + file. W7–10 OT implant + status. W11–14 attendant + reports. W15–16 UAT/NABH doc control. Nashik/Kolhapur copy playbook.

## Weak vs strong

| Weak | Strong |
|---|---|
| “TPA dashboard + AI” | Eligibility + pack BR + implant attach + coded denials |
| Blame the insurer | Control completeness; contract the rest |
| SMS the diagnosis “for convenience” | Status labels + OTP |

## Notes

- Pattern matches every Indian private hospital TPA desk; numbers illustrative.
- Emergency override is a safety BR, not a loophole to skip all files.
- NHCX is the industry direction; MVP still works if portals remain.
- Do not claim this was delivered at a named chain.
