# CityWell Clinics — Duplicate UHID, ABHA Stall, Family-Phone Privacy

> **Sequence: Phase 4, file 12.** After the gate. Best after file `10` so money vs identity are not mixed.  
> Related appointment case (later): `13-Real-World-BA-Projects/04-healthcare-case-study.md`.

**Domain:** Healthcare / identity & privacy. **Company:** CityWell Clinics (illustrative 40-clinic OPD network). **Role:** BA, HIM / EMR. **Grain:** Person / UHID (not claim, not sample).

CityWell: 40 neighbourhood clinics, ~180 doctors, ~6,000 OPD/day network-wide. 12-year HIS; notes often Word/scan. Patients hop clinics; **records do not follow**. ABHA “go-live” was a kiosk poster. SMS “lab ready” deep-links PDFs. Shared family mobiles common. DPO flagged a complaint: relative saw a diagnosis.

Related teaching case: MediCare+ (folder 13) is **appointments**. This case assumes slots exist; identity and consent are still broken — the usual second programme.

## Business problem

**Duplicate active UHID 11.2%** (illustrative extract). Same person billed twice; allergies on the silent duplicate. **ABHA linkage 8%** of OPD; kiosk fails on network and refusal is argued as “non-compliance.” **Results SMS** opens reports without second factor. Doctors will not type EMR because Must fields are 40 screens. Inter-clinic share is USB and WhatsApp.

Sponsor: “ABDM-ready super app and unique ID like Aadhaar for health.”

## Business objective

12 weeks + 8-week adopt, 8 clinics then rollout:

1. Duplicate **create rate ≤ 2%** of new registrations; merge backlog SLA **14 days** for high-confidence matches.  
2. ABHA: **offered 100%**; linkage is **not** a condition of care; refusal reason captured. Linkage **≥ 25%** of eligible (smartphone + consent) — not 100% fantasy.  
3. **Zero** result-by-naked-link; results behind OTP/app login tied to UHID.  
4. Encounter: **Must fields ≤ 8** (allergy, complaint, diagnosis, Rx/orders, follow-up) so notes land in EMR not Word.  
5. Cross-clinic view for same UHID with **consent + audit**.

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| Network COO | H | H | Wants ABDM badge | KPI: duplicates + incidents, not badge |
| HIM / medical records | H | H | Merge fear (wrong merge Sev1) | Privilege + two-person merge |
| Front desk | M | H | Speed vs search | Search UX + training |
| Doctors | H | H | Click fatigue | Template workshop |
| Patients | L | H | Privacy, time | Journey; refusal OK |
| DPO | H | H | DPDP | Consent purposes |
| ABDM / IT vendor | M | M | Sandbox | Offline path |
| Lab vendor | M | M | Result channel | Kill deep link |
| NABH consultant | M | M | Identification | Two IDs |

## Scope

**In:** MPI search/create rules, duplicate suspect queue, merge SOP, consent purposes (reminder / report / share / ABHA), result access, ABHA offer + refusal, EMR Must-field set, cross-clinic break-glass, audit, 8-clinic MVP.

**Out:** National PHR as CityWell product, replacing HIS, appointment rebuild, cashless IPD (ApexCare), AI scribe (Phase 2), Aadhaar as UHID (illegal/unsafe design), denying care without ABHA.

## Assumptions and constraints

**Assumptions:** HIS can add MPI fields or sidecar; SMS vendor can drop deep link; ABDM sandbox credentials exist.  
**Constraints:** DPDP; clinical ethics; ABHA voluntary for care; 12-week MVP; wrong merge is Sev1 — conservative match.

## As-Is process (diagram described)

1. Desk searches name + mobile; if slow, **creates new UHID**.  
2. ABHA kiosk: no signal / no smartphone / patient says no → argument or skip.  
3. Consult: paper or Word; scan to “EMR” folder unmatched.  
4. Lab: SMS link; anyone with the SMS reads PDF.  
5. Other CityWell clinic: new UHID; yesterday’s allergy missing.  
6. Complaint: sister saw report on family phone.

**Problem analysis:** Identity, consent, and EMR adoption are one programme. An ABDM badge on duplicate UHID **spreads the wrong chart**.

**Root cause (privacy incident):** Relative saw diagnosis because SMS was the authenticator. SMS was authenticator because “ease.” Ease because UHID ≠ login. UHID weak because create-is-cheaper-than-search.

## To-Be process (diagram described)

1. Registration: search (name + DOB + mobile + last visit). Suspects listed. Create requires reason if suspects exist.  
2. Consent purposes captured (tick; not a wall of legal).  
3. ABHA offered; success / fail / refuse + reason; **proceed to care**.  
4. Consult: 8 Must fields; save encounter.  
5. Results: notification without values; open via app or OTP to registered channel tied to UHID.  
6. HIM: daily suspect queue; merge with two-person check above threshold.  
7. Cross-clinic: same UHID; other-clinic chart requires purpose + audit; break-glass for emergency.

## Gap analysis

| ID | Type | Gap | Action |
|---|---|---|---|
| G-01 | Data | Create without search | MPI FR |
| G-02 | Policy | ABHA treated as mandatory | BR voluntary |
| G-03 | Tech | Naked result link | OTP/app |
| G-04 | People | 40 Must fields | Cut to 8 with HODs |
| G-05 | Process | No merge SOP | HIM privilege |
| G-06 | Tech | Clinic silo | Shared MPI |
| G-07 | Policy | One consent blob | Purpose-wise |

## Requirements

| ID | Type | Statement |
|---|---|---|
| FR-ID-01 | F | Before create, system shows potential matches (name+DOB+mobile rules). |
| FR-ID-02 | F | Create with open suspects requires reason code. |
| FR-ID-03 | F | HIM can merge UHIDs; two-person approval if confidence ≥ threshold; never auto-merge above clinical risk. |
| FR-ID-04 | F | ABHA offer recorded: LINKED / FAILED / REFUSED / SKIPPED_OFFLINE. |
| FR-ID-05 | F | Care flow must proceed when ABHA = REFUSED or FAILED. |
| FR-ID-06 | F | Consent stored per purpose: REMINDER, RESULT_ACCESS, CLINIC_SHARE, ABHA_LINK, MARKETING. |
| FR-ID-07 | F | Result objects not fetchable by SMS token alone; OTP or authenticated session required. |
| FR-ID-08 | F | Encounter save requires Must-field set (versioned). |
| FR-ID-09 | F | Cross-clinic open: purpose + audit; break-glass with reason. |
| NFR-ID-01 | NF | Search p95 ≤ 2s on 8-clinic data. |
| NFR-ID-02 | NF | Audit log: viewer, UHID, action, clinic; retention per policy. |
| NFR-ID-03 | NF | Break-glass alerts HIM within 15 min. |
| TR-ID-01 | T | Paper register if HIS down; duplicate flag on catch-up. |

## Business rules

- **BR-ID-01:** ABHA is not a condition of treatment.  
- **BR-ID-02:** RESULT_ACCESS consent default **false** until captured; reminders may be separate.  
- **BR-ID-03:** SMS/WhatsApp shall not contain diagnosis or result values.  
- **BR-ID-04:** Wrong-patient suspected → stop, HIM, incident.  
- **BR-ID-05:** Merge reverses only via HIM with audit (compensating).  
- **BR-ID-06:** Marketing consent never implied from care consent.  
- **BR-ID-07:** Minors: guardian consent captured; adolescent confidentiality per clinical policy (HOD + legal — BA does not invent).

## User stories (with AC)

1. **As front desk, I want match list** so I stop creating twins. **AC:** Three suspects shown; create needs reason.  
2. **As patient, I can refuse ABHA** and still consult. **AC:** REFUSED stored; token issued.  
3. **As patient, I want lab results not on a raw link.** **AC:** Link without OTP fails.  
4. **As doctor, I want 8 fields** so I document in HIS. **AC:** Save blocked only on those 8.  
5. **As HIM, I want a suspect queue.** **AC:** Daily list; merge two-person.  
6. **As DPO, I want purpose-wise consent.** **AC:** RESULT false → no result SMS.

## Use case (fully dressed): UC-ID-01 Register returning patient with family mobile

- **Actor:** Front desk, patient. **Pre:** Clinic HIS up.  
- **Trigger:** Arrives for OPD.  
- **Main:** Search → select existing UHID → verify second factor (DOB/last visit) → capture/update consent → offer ABHA → book/consult.  
- **Alt:** New patient, no suspects → create.  
- **Exception:** Suspects exist, desk unsure → do not create; HIM/supervisor same day or temporary encounter with flag.  
- **Post:** One UHID; consent; ABHA status; audit.

## Wireframes

1. Search (not “new” as first button). 2. Suspect cards. 3. Consent purpose ticks. 4. ABHA offer (skip). 5. Doctor 8-field encounter. 6. Result unlock OTP. 7. HIM merge. 8. Break-glass. 9. Duplicate dashboard.

## Data, reports, KPIs

**Entities:** Person, UHID, MatchSuspect, MergeEvent, ConsentPurpose, AbhaEvent, Encounter, ResultAccess, AuditEvent, Clinic.

**Reports:** Duplicate create %; merge lag; ABHA funnel (offered/linked/refused/failed); result access fail; Word-upload residual; break-glass count.

**KPIs:** Objectives. Incident count = 0 naked-link after go-live.

## UAT scenarios

- Create blocked without reason when suspects exist.  
- REFUSED ABHA still gets consult.  
- Offline SKIPPED_OFFLINE.  
- Naked SMS token cannot download PDF.  
- Family phone: OTP to number on UHID; change-of-number SOP.  
- RESULT consent false.  
- Doctor save with 7 of 8 fields blocked.  
- Clinic B opens Clinic A chart — audit + purpose.  
- Wrong merge drill on training data only.

## RTM

| Req | Story | UC | UAT |
|---|---|---|---|
| FR-ID-01 | US1 | UC-ID-01 | Search |
| FR-ID-02 | US1 | UC-ID-01 alt | Create reason |
| FR-ID-05 | US2 | — | Refuse ABHA |
| FR-ID-07 | US3 | — | Naked link |
| FR-ID-08 | US4 | — | Must fields |
| FR-ID-03 | US5 | — | Merge |
| FR-ID-06 | US6 | — | Consent |
| BR-ID-01 | US2 | — | Care continues |

## Change request (sample)

**CR-ID-01:** Force ABHA for all billed visits (marketing). **Decision:** Rejected. Violates BR-ID-01 and public evidence that network/smartphone/refusal dominate. Capture funnel instead.

## Risks and dependencies

| Risk | P/I | Mitigation | Owner |
|---|---|---|---|
| Wrong merge | M/H | Two-person; conservative rules; training tenant drills | HIM |
| Doctors stay on Word | H/H | 8 fields; MS mandate; measure Word uploads | MS |
| ABDM sandbox flaky | H/M | FAILED path; care continues | IT |
| Shared phone | H/H | OTP + number-change SOP | Desk + DPO |
| Staff shame refusers | M/M | Script + mystery shop | COO |

**Dependencies:** HIS MPI, ABDM APIs, lab result portal, SMS vendor, DPO notices, HOD Must-field sign-off.

## Final business solution

**MPI with disciplined create, voluntary ABHA, purpose-wise consent, results behind real authentication, and a tiny EMR Must set.** The super-app is Phase 2 on a clean UHID. Success = duplicate rate, zero naked-link incidents, notes in HIS, ABHA funnel honesty.

**Phasing.** W1–2 extract duplicates + consent workshop. W3–6 search/create/merge. W7–8 result access. W9–10 EMR fields. W11–12 ABHA offer + UAT. Rollout 8 → 40.

## Weak vs strong

| Weak | Strong |
|---|---|
| “Unique health ID like Aadhaar” | MPI + voluntary ABHA + no care denial |
| ABDM badge | Funnel + FAILED/REFUSED |
| 40 EMR fields | 8 Must, HOD-owned |
| SMS deep link | OTP tied to UHID |

## Notes

- Public ABHA hurdle pattern (network, smartphone, refusal) is designed in, not treated as user stupidity.  
- Identity errors are clinical safety.  
- Do not use real patient data in portfolio screenshots.  
- Illustrative % only.
