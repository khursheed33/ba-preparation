# NovaBank — Slow Personal Loan Origination

**Domain:** Banking / FinTech + **loan management**. **Company:** NovaBank (illustrative). **Role:** BA, Digital Lending.

## Business problem

Salaried personal-loan origination averages **9 days** elapsed (illustrative). Customers abandon after “visit branch for KYC.” Credit officers re-key bureau data. Physical Form 16 adds courier wait. Origination drop-off from application-start to disbursal is 61%. Competitors originate in ~1 day.

## Business objective

In 14 weeks + 1 quarter stabilise: (1) P50 origination **≤ 24 hours** for salaried resident digital loans ≤ ₹10 lakh; (2) start-to-disburse conversion **≥ 55%**; (3) re-key rate **0%** on bureau fields; (4) branch KYC only for exceptions.

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| Head of Retail Lending | H | H | Sponsor | Weekly CBA |
| Credit Ops | H | H | Fear fraud | Rules workshop |
| Compliance / KYC | H | H | Conditional | Legal feasibility |
| Branch RM | M | M | Loss of control | Exception RACI |
| Customer (salaried) | L | H | Impatient | Journey tests |
| LOS vendor | M | M | Contract | API dates |
| InfoSec | H | M | Storage | Video retention |
| Finance | M | H | NPA / cost | Cut-off rules |
| QA / UAT credit | M | H | Evidence | UAT scripts |

## Scope

**In:** digital journey for resident salaried; bureau pull; video KYC (vendor) + branch fallback; e-sign offer; LOS statuses; disbursal to customer account; loan management: schedule, EMI, foreclosure quote (view).  
**Out:** NRI, joint, business loans, credit card, collections system rewrite, in-house video build.

## Assumptions and constraints

**Assumptions:** Bureau sandbox in week 2; video vendor India-resident storage; 35%+ of starters will finish if KYC is in-app.  
**Constraints:** RBI-style digital lending & KYC (illustrative); 14-week build; reuse core CBS for account; data localisation; no 8-week fake promise.

## As-Is process (diagram described)

1. App form + OTP (12 min work).  
2. Upload docs (8 min).  
3. **Wait 2–4 days** branch KYC slot.  
4. Credit queue **1 day**; officer **re-keys bureau 25 min**.  
5. Form 16 **courier 2 days**.  
6. Offer e-sign (10 min).  
7. Disbursal ops **1 day** batch.  

**Problem analysis:** ~1.5 hours work vs 9 days elapsed. Drop-off is KYC wait, not form UX.

**Root cause (value stream + 5 Whys):** Why 9 days? KYC wait. Why branch? Video KYC not in policy pack. Why re-key? LOS not consuming bureau API. Why Form 16 paper? Rule never updated for e-docs.

## To-Be process (diagram described)

1. In-app form; income via declared + optional account aggregator.  
2. Bureau pull auto-fills; officer reviews exceptions only.  
3. Video KYC (liveness) or branch if fail/high-risk.  
4. Credit decision engine + officer for borderline.  
5. E-offer, e-sign, e-NACH.  
6. Disbursal two cut-offs/day to CBS.  
7. Loan account: EMI schedule visible in app.

## Gap analysis

| Type | Gap | Action |
|---|---|---|
| Process | Branch-mandatory KYC | Video + fallback |
| Tech | No bureau API in LOS; no video | Vendor + LOS |
| Data | Re-keyed bureau fields | System of record = bureau |
| Policy | Paper Form 16 | E-doc BR |
| People | Officers as typists | Review role + training |

## Requirements

| ID | Type | Statement |
|---|---|---|
| FR-LOS-01 | F | Salaried resident can apply for PL ≤ ₹10 lakh in app. |
| FR-LOS-02 | F | System pulls bureau and maps fields; no re-key on mapped fields. |
| FR-LOS-03 | F | Customer can complete video KYC with liveness; fail → branch case. |
| FR-LOS-04 | F | E-document upload accepted for Form 16 / salary (file types listed). |
| FR-LOS-05 | F | On approve, e-sign offer; on e-NACH success, create loan in CBS. |
| FR-LOS-06 | F | Customer can view EMI schedule and foreclosure quote (indicative). |
| NFR-LOS-01 | NF | Decision path p95 ≤ 30s excluding video. |
| NFR-LOS-02 | NF | Video stored 7 years; India region. |
| NFR-LOS-03 | NF | 5k applications/day peak. |

## Business rules

- **BR-LOS-01:** Video KYC only resident individual; NRI out of scope.  
- **BR-LOS-02:** High-risk score → mandatory branch KYC.  
- **BR-LOS-03:** Offer cooling-off displayed before e-sign (digital lending).  
- **BR-LOS-04:** Disbursal only if CKYC upload status = SUCCESS or queued with SLA.

## User stories (with AC)

1. **As a salaried customer, I want in-app KYC** so I skip branch. **AC:** Given resident + liveness pass, Then KYC=VERIFIED without branch.  
2. **As a customer, I want a same-day decision** for vanilla cases. **AC:** Given complete file + low risk, Then decision ≤ 24h.  
3. **As a credit officer, I want bureau fields locked** so I do not re-type. **AC:** Mapped fields read-only; override needs reason.  
4. **As a customer, I want EMI schedule after disbursal.** **AC:** Given LOAN_ACTIVE, Then schedule visible.  
5. **As compliance, I want video audit trail.** **AC:** Given completed video, Then playable file + timestamp + agent id stored.  
6. **As ops, I want two disbursal windows.** **AC:** Files before 11:00 and 16:00 same-day CBS.

## Use case (fully dressed): UC-LOS-01 Video KYC

- **Actor:** Customer. **Pre:** Application SUBMITTED; KYC pending.  
- **Trigger:** Starts Video KYC.  
- **Main:** Consent → liveness → capture ID → match → VERIFIED.  
- **Alt:** Poor network → reschedule.  
- **Exception:** Liveness fail x3 → BRANCH_KYC case; RM notified.  
- **Post:** KYC status set; LOS unlocked for credit.

## Wireframes

1. Loan amount + tenure. 2. Personal + employment. 3. Bureau consent. 4. Video KYC room. 5. Offer (APR, cooling-off). 6. E-sign + NACH. 7. Schedule / foreclosure quote. 8. Officer queue (exceptions).

## Data, reports, KPIs

**Data:** Application, BureauSnapshot, KycSession, Offer, LoanAccount, EmiSchedule.  
**Reports:** funnel; P50/P90 TAT; video fail %; exception queue age; NPA early (watch).  
**KPIs:** origination P50; conversion; re-key %; % video vs branch; drop-off at KYC.

## UAT scenarios

- Vanilla salaried, video pass, 24h disburse.  
- Liveness fail → branch.  
- High-risk → branch mandatory.  
- Bureau timeout → retry + message.  
- Cooling-off text present.  
- Foreclosure quote visible post-disburse.

## RTM

| Req | Story | UC | UAT |
|---|---|---|---|
| FR-LOS-03 | US1 | UC-LOS-01 | Video pass/fail |
| FR-LOS-02 | US3 | — | Locked fields |
| FR-LOS-05 | US2, US6 | — | Disburse windows |
| FR-LOS-06 | US4 | — | Schedule |
| NFR-LOS-02 | US5 | UC-LOS-01 | Storage |

## Change request (sample)

**CR-LOS-01:** “Add vernacular IVR during video.” Impact: FR language, vendor, reports. **Decision:** Phase 2; English/Hindi UI first.

## Risks and dependencies

| Risk | P/I | Mitigation | Owner |
|---|---|---|---|
| Legal blocks storage | M/H | India-resident vendor in contract | Compliance |
| Vendor 16-week lead | M/H | 14-week plan already; no 8-week | PM |
| Fraud via video | M/H | Liveness + high-risk branch | Credit |

**Dependencies:** bureau API, video vendor, CBS disbursal, CKYC, NACH.

## Final business solution

**Conditional go:** vendor video KYC + bureau-integrated LOS + e-docs + twice-daily disbursal. Branch remains exception. Loan management MVP = schedule + indicative foreclosure. Success = 24h P50 and conversion — not a prettier form.

## Weak vs strong

| Weak | Strong |
|---|---|
| “Digital loans like fintechs.” | 9 days → 24h P50; 0% re-key; feasibility 14 weeks. |

## Notes

- This file covers Banking/FinTech **and** loan management (origination + EMI/foreclosure view).
- Feasibility vs branch KYC is the decision spine.
- Label all volumes illustrative.
