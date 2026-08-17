# Health Domain Landscape

> **Sequence: Phase 1, file 03 of 06.** After `02-abbreviations-and-full-names.md` (sections A–C at least).  
> **Next:** `04-glossary-kpis-regulations.md`. Look up every unknown short name in file `02`. Do not jump to `08` or `10`.

## Definition

**Healthcare** as a BA domain is the set of organisations that **prevent, diagnose, treat, bill, and record** care. The unit of work is not “a screen.” It is an **encounter** (OPD visit, admission, sample, claim, discharge) that must be identified, consented, documented, charged, and audited.

India’s organised hospital industry is still expanding: ICRA’s listed-chain sample ran occupancy around **62–64%** into FY2026–27, with ARPOB still growing (slower in tier-II than metros). That is the money context. The BA context is that occupancy, cashless, diagnostics TAT, and privacy all fail in **process + master data**, not in a missing calendar widget.

## Why it matters for a BA

A loan origination BA can be wrong and the bank retries. A healthcare BA who collapses identity, consent, and billing into “the app” produces wrong-patient charts, SMS leaks, and claim denials. Interviewers and COOs test whether you know **four parallel processes**: access (appointments/beds), clinical record (EMR), revenue (billing/RCM), and privacy (who may see what).

## The value chain (where money and risk sit)

```
Prevention / wellness
    → Primary care (clinic, GP, teleconsult)
        → Diagnostics (lab / radiology)
            → Secondary / tertiary hospital (OPD → IPD → OT / ICU)
                → Pharmacy / consumables
                    → Rehab / home care
                        → Payer (self-pay, insurer, TPA, PM-JAY)
```

| Stage | Who pays | Typical BA failure |
|---|---|---|
| Prevention | Employer, insurer, patient | Wellness package billed as clinical; no consent for results SMS |
| Primary | Patient / OPD package | Slot without roster; duplicate UHID |
| Diagnostics | Patient / hospital / aggregator | Sample ID ≠ order; TAT clock starts at wrong event |
| Hospital | Mix of cash + insurance | Discharge held for final approval; bed not released |
| Pharmacy | Patient / package | Stock vs prescription mismatch; NDPS items without dual control |
| Payer | Premium / tax | Pre-auth pack incomplete; denial with no coded reason |

## Subdomains you must not mix

| Subdomain | Unit of work | System of record | Example players |
|---|---|---|---|
| Multi-specialty hospital | Bed-day + procedure | HIS / EMR | Apollo, Fortis, Max, Medanta, Narayana |
| Single-specialty | Procedure / programme | HIS + specialty EMR | HCG (oncology), Rainbow (paeds), Shalby (ortho), Cloudnine |
| Clinic / polyclinic | Slot / consult | Clinic EMR / HIS-lite | Practo-powered clinics, neighbourhood chains |
| Diagnostics | Sample / accession | LIS (+ RIS/PACS for imaging) | Dr Lal PathLabs, Metropolis, Thyrocare, Vijaya |
| Retail pharmacy | SKU + Rx | Pharmacy POS + inventory | Apollo Pharmacy, MedPlus |
| Health insurance / TPA | Policy + claim | Policy admin + claims | Star Health, Niva Bupa, TPAs |
| Public schemes | Beneficiary + empanelment | PM-JAY / state portals | NHA, state trusts |
| Digital health / marketplace | Lead / order / consult | App + partner HIS | Practo, Tata 1mg, Apollo 24/7, PharmEasy |
| Home care | Visit / device reading | Scheduling + clinical log | Portea-style, hospital home-health |

If you write ShopEase “checkout” stories for a cashless discharge, the TPA desk will reject the BRD.

## Business models (how they actually make money)

| Model | Revenue idea | Cost / risk the BA will hear |
|---|---|---|
| Hospital (fee-for-service) | ARPOB × occupancy × beds | Empty bed is lost; insurance mix delays cash |
| Hospital (package) | Fixed price for procedure | Leakage when extras are not in package rules |
| Diagnostics hub-spoke | Test price × volume; spoke feeds hub | Logistics + repeat test + aggregator discount |
| Pharmacy | Margin on drug + private label | Expiry, theft, substitution |
| Insurer | Premium − claims − expense (combined ratio) | Leakage vs delay; network hospital fights |
| Marketplace | Commission / slot fee / diagnostic take-rate | Doctor supply, discount wars, quality complaints |
| SaaS HIS | Licence or per-bed / per-clinic | Implementation, ABDM, integration, support |

**ARPOB** (average revenue per occupied bed) is the hospital steering number. **Occupancy** without payer mix is a vanity metric: 75% occupancy with 50-day insured receivables can starve cash.

## How care is paid (India)

| Channel | What happens | BA implication |
|---|---|---|
| Self-pay / cash | Bill at discharge or after OPD | Estimate accuracy; package vs item |
| Insurance cashless | Hospital + TPA/insurer settle; patient pays gap | Pre-auth, enhancement, final bill, denial codes |
| Reimbursement | Patient pays, claims later | Documents, TAT, query loop |
| PM-JAY / state | Package rates, empanelment, portal | Rate list, photo/ID, claim form, rejection |
| Corporate / TPA | Empanelment + pre-auth | Eligibility file, employee ID |
| International | Package + facilitator | Passport, estimate, forex, medical visa docs |

Cashless is **insurance process inside the hospital**. It is not a billing screen.

## Operating grain (get this wrong and every FR is wrong)

| Setting | Grain | Example KPI |
|---|---|---|
| OPD | Slot / encounter | No-show %, wait after check-in |
| IPD | Bed-day | Occupancy, ALOS, bed turnaround hours |
| OT | Theatre minute | First-case start delay, utilisation |
| Lab | Sample / accession | TAT by test, recollection %, barcode mismatch |
| Radiology | Modality slot | Report TAT, machine downtime |
| Claims | Claim / pre-auth | Denial %, AR days, pre-auth TAT |
| Identity | UHID / ABHA | Duplicate rate, merge time, consent coverage |

MediCare+ (roadmap folder `13-Real-World-BA-Projects`, **after this pack’s gate**) is OPD grain. In this pack Phase 4: ApexCare is claim grain (`10`). HelixLab is sample grain (`11`). CityWell is identity grain (`12`).

## India-specific digital stack (conversation depth)

| Layer | What it is | BA must ask |
|---|---|---|
| ABHA | Citizen health ID | When is it captured? What if patient refuses? |
| HPR / HFR | Doctor and facility registries | Is the hospital HFR-linked? |
| PHR / HIE-CM | Consent-based record exchange | Who is data fiduciary? Where is consent stored? |
| UHI | Open protocol for digital health services | Booking vs record share — different APIs |
| NHCX | Claims exchange (FHIR-style) | Are we still on 8 TPA portals or one gateway? |
| DPDP Act | Personal data law | Purpose, consent, access, retention, breach |

Public research (AIIMS Kalyani OPD, 2024): among ABHA integration *hurdles*, network and no-smartphone dominated; refusal was material. Technology readiness without a front-desk script still fails.

## Stakeholders you will meet on day one

| Role | Optimises | Typical conflict |
|---|---|---|
| COO / unit head | Occupancy, wait, cost | Wants app; will not freeze doctor roster |
| Medical superintendent | Clinical safety, privileges | Fears EMR clicks add consult time |
| Nursing / ward in-charge | Bed, MAR, handover | Downtime SOP on paper |
| Front desk / TPA desk | Throughput, cashless honour | Eight portals, no status for patient |
| Billing / RCM | Leakage, AR days | Package vs item fights |
| Lab / radiology HODs | TAT, quality | HIS order ≠ analyser worklist |
| Pharmacy | Stock, expiry | Ward indent vs billing |
| IT / HIM | Uptime, HIS vendor | “Just an API” that does not exist |
| DPO / compliance / NABH | Audit, consent | Privacy as afterthought |
| Insurer / TPA | Leakage | Queries that look like delay to the patient |
| Patient / attendant | Access, wait, bill surprise | Family phone, language, literacy |

## Typical BA programmes (what you will actually be hired for)

1. OPD scheduling + no-show policy (already in MediCare+).
2. Cashless / RCM desk (ApexCare).
3. LIS barcode + TAT (HelixLab).
4. MPI / ABHA / consent (CityWell).
5. IPD bed management and discharge.
6. e-prescription + pharmacy linkage.
7. Patient app / CRM on top of HIS (not instead of HIS).
8. NABH / NABL evidence in the system, not in a binder.
9. Downtime SOP (paper + catch-up) as a transition requirement.

## Weak vs strong

| Weak | Strong |
|---|---|
| “Healthcare is EMR” | Four processes: access, chart, money, privacy |
| One KPI: downloads | Occupancy + ARPOB + denial % + no-show + duplicate UHID |
| Global Epic story in an Indian 200-bed hospital | HIS already there; contract, don’t rip-and-replace |
| Ignore payer | Cashless is in-scope for any IPD programme |
| “HIPAA later” | Role-based access + audit in MVP (DPDP + clinical ethics) |

## Scenario / Use case: first week on a hospital programme

**Context.** Sponsor says “build a patient super-app like Apollo 24/7.”

**What you do.** Day 1–2: map which HIS is system of record, how UHID is issued, how TPA desk works, what SMS already fires. Day 3: pick **one** measurable problem (wait, denial, TAT, duplicates). Day 4: write in/out scope that keeps clinical protocol with HODs. Day 5: workshop roster or pre-auth pack — not screens.

**If ignored.** You deliver an app on a duplicate UHID base. Reports go to the wrong phone. Cashless still takes six hours. The app is blamed; the process was never the app.

## Notes

- Learn occupancy, ARPOB, ALOS, cashless, UHID, ABHA, TAT, denial — then processes.
- Do not mix hospital, diagnostics, and marketplace business models in one BRD.
- India: ABDM + DPDP + NABH/NABL + IRDAI-style cashless are constraints, not optional modules.
- BAs do not design treatment. They design who is identified, who consents, who is billed, and who is audited.
- Public industry numbers (ICRA occupancy, EY growth) are for context. Your project KPIs come from the client’s HIS extract, labelled and dated.
- **Next file:** `04-glossary-kpis-regulations.md`. Do not open `08` yet.
