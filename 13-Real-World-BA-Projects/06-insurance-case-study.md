# ShieldSure — Slow Motor Claims

**Domain:** Insurance. **Company:** ShieldSure (illustrative). **Role:** BA, Motor Claims.

## Business problem

Motor own-damage cashless TAT **P50 = 18 days**, **P90 = 29 days** (illustrative). Industry / peer benchmark **7 days P50**. Claims NPS **12**. Customers chase surveyors on WhatsApp. Photos sit outside the claim file. Leakage from goodwill and incomplete surveys.

## Business objective

Two quarters: (1) P50 TAT **7 days**; (2) P90 **12 days**; (3) claims NPS **≥ 35**; (4) 100% survey photos in the claim file (no WhatsApp-only).

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| Chief Claims | H | H | Sponsor | Benchmark pack |
| Surveyor network lead | H | H | Capacity fear | Slot SLA |
| Garage network | M | H | Cashless | Assignment rules |
| Customers | L | H | Angry wait | Journey |
| IRDAI / compliance (style) | H | M | TAT scrutiny | Reports |
| Finance / leakage | M | H | Cost | Dual review |
| Contact centre | M | H | Repeat calls | Status SMS |
| Core claims vendor | M | M | API | FNOL |

## Scope

**In:** digital FNOL, survey appointment < 24h, photo upload (app ≥ 8 photos), garage assignment, status SMS, TAT clock, customer tracker.  
**Out:** AI liability, health claims, legal liability courtroom, full core replacement.

## Assumptions and constraints

**Assumptions:** Surveyors have smartphones; garage list is master data; SMS DLT ready.  
**Constraints:** IRDAI-style TAT expectations (illustrative); 16-week MVP; reuse core claims system; 7-year document retention.

## As-Is process (diagram described)

1. FNOL via call; ticket in core; SMS optional.  
2. Surveyor allocated by phone; **wait 2–5 days**.  
3. Photos on WhatsApp (3 in old app).  
4. Garage start sometimes **before** approval.  
5. Parts quotes email; **wait 4–8 days**.  
6. Repair + payment; customer uninformed.

**Problem analysis:** Wait is survey slot + unstructured photos + garage-before-approval. Portal cosmetics will not move TAT.

**Root cause (Fishbone + benchmark):** People (new adjusters), process (approval after work), tech (3-photo app), data (NCB not applied), external (inflated invoices). Pareto: survey wait + parts approval = majority of the 11-day gap vs industry.

## To-Be process (diagram described)

1. Digital FNOL (app/web/call logged the same).  
2. SMS ack (Kano basic).  
3. Survey slot offered < 24h; photos in-app (up to 12).  
4. Garage assigned after survey complete; cashless approval **before** work.  
5. Parts workflow in system; customer sees status.  
6. Repair complete → payment; TAT clock stops on authorised definition.

## Gap analysis

| Type | Gap | Action |
|---|---|---|
| Process | Survey by phone | Slot booking |
| Tech | 3-photo + WhatsApp | App upload |
| Policy | Goodwill uncapped | BR cap |
| Data | Photos not on claim | Mandatory attach |
| People | Surveyor capacity | Roster + SLA |

## Requirements

| ID | Type | Statement |
|---|---|---|
| FR-CLM-01 | F | Customer/agent can lodge FNOL with policy + incident facts. |
| FR-CLM-02 | F | System sends SMS ack within 5 minutes. |
| FR-CLM-03 | F | Survey slot offered within 24h of FNOL (metro). |
| FR-CLM-04 | F | Surveyor uploads ≥ 8 photos to claim (not WhatsApp). |
| FR-CLM-05 | F | Cashless work cannot start until approval status = APPROVED. |
| FR-CLM-06 | F | Customer tracker: FNOL, SURVEY, APPROVED, REPAIR, PAID. |
| NFR-CLM-01 | NF | FNOL p95 ≤ 3s; photos 10 MB each. |
| NFR-CLM-02 | NF | TAT clock auditable; timezone IST. |

## Business rules

- **BR-CLM-01:** Goodwill write-off cap ₹5,000 without claims head.  
- **BR-CLM-02:** Dual review if estimate > ₹50,000.  
- **BR-CLM-03:** TAT clock starts at FNOL complete; pauses on customer-caused delay.  
- **BR-CLM-04:** Depreciation table version stamped on estimate.

## User stories (with AC)

1. **As a customer, I want digital FNOL** so I do not only call. **AC:** Policy validated; FNOL number returned.  
2. **As a customer, I want SMS ack** immediately. **AC:** ≤ 5 min.  
3. **As a customer, I want a survey slot in 24h.** **AC:** Metro PIN shows slots.  
4. **As a surveyor, I want to upload 8+ photos in-app.** **AC:** Claim cannot move to estimate without min photos.  
5. **As a customer, I want status** so I do not call. **AC:** Tracker matches FR-CLM-06.  
6. **As claims, I want garage blocked until approval.** **AC:** Cashless job cannot start.

## Use case (fully dressed): UC-CLM-01 Digital FNOL

- **Actor:** Customer. **Pre:** Active motor policy.  
- **Trigger:** Report accident.  
- **Main:** Policy → when/where → third party Y/N → photos optional → submit → FNOL id + SMS.  
- **Alt:** Call centre performs same data capture.  
- **Exception:** Policy lapsed → reject with reason.  
- **Post:** Claim OPEN; survey slot offered.

## Wireframes

1. FNOL wizard. 2. SMS/ack screen. 3. Slot picker (survey). 4. Surveyor camera + count. 5. Customer tracker. 6. Approver estimate + dual review. 7. Garage job (blocked until approved). 8. TAT dashboard vs 7-day benchmark.

## Data, reports, KPIs

**Data:** Claim, Fnol, SurveyAppointment, Photo, Estimate, Approval, GarageJob, TatClock.  
**Reports:** P50/P90 TAT vs industry 7-day; % photos in file; goodwill; repeat calls.  
**KPIs:** TAT 7 / 12; NPS 35; 100% photos on file; % approval-before-work.

## UAT scenarios

- Digital FNOL + SMS.  
- Survey slot 24h metro.  
- < 8 photos cannot complete survey.  
- Garage start blocked.  
- Dual review > ₹50k.  
- Goodwill above cap blocked.  
- Lapsed policy reject.

## RTM

| Req | Story | UC | UAT |
|---|---|---|---|
| FR-CLM-01 | US1 | UC-CLM-01 | FNOL |
| FR-CLM-02 | US2 | UC-CLM-01 | SMS |
| FR-CLM-03 | US3 | — | Slot |
| FR-CLM-04 | US4 | — | Photos |
| FR-CLM-05 | US6 | — | Garage block |
| FR-CLM-06 | US5 | — | Tracker |

## Change request (sample)

**CR-CLM-01:** Add AI photo damage. Impact: model, legal, leakage. **Decision:** Won’t MVP (Kano delight / high effort).

## Risks and dependencies

| Risk | P/I | Mitigation | Owner |
|---|---|---|---|
| Surveyor capacity | H/H | Restrict metros Phase 1; hire | Survey lead |
| Garages ignore block | M/H | Network SLA + audit | Claims |
| Core API delay | M/H | Vendor milestone | PM |

**Dependencies:** core claims, SMS, surveyor app store release, garage master.

## Final business solution

Benchmark-led To-Be: **7-day P50**. MVP = FNOL + 24h survey slot + photos in file + approval before work + tracker + TAT clock. Portal without slot SLA is cosmetics. AI is Won’t.

## Weak vs strong

| Weak | Strong |
|---|---|
| “New claims portal.” | Industry 7-day gap of 11 days; MoSCoW from wait time. |

## Notes

- Insurance portfolio: regulator-style TAT, leakage, network partners.
- Fishbone + benchmarking justify To-Be.
- Illustrative TAT only — not a real IRDAI filing.
