# MediCare+ — Appointment No-Shows and Chaotic OPD

**Domain:** Healthcare. **Company:** MediCare+ (illustrative). **Role:** BA, Patient Access / HIS.

## Business problem

OPD ~800 walk-ins/day. Average wait **95 minutes**. Follow-up no-show **22%** because the next visit is “come Tuesday morning” with no slot. Doctors overbook from memory. Front-desk runs paper tokens. Management asked for “an app.”

## Business objective

In 12 weeks + 8-week adopt: (1) **70%** of OPD visits pre-booked; (2) no-show **≤ 12%**; (3) wait P50 **≤ 30 minutes** for booked patients; (4) walk-in windows explicit (≤ 20% capacity).

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| Hospital COO | H | H | Sponsor | KPI weekly |
| Medical Superintendent | H | H | Roster fear | Roster workshop |
| Front-desk lead | M | H | Token habit | Floor training |
| Specialists | H | M | Mixed | Roster = capacity |
| Patients | L | H | Queue pain | Journey + UAT |
| HIS vendor | M | M | API | Slot contract |
| Privacy officer | H | M | Consent | SMS BR |
| Billing | M | M | Walk-in cash | Payment step |

## Scope

**In:** web/app/phone booking, HIS slot sync, SMS reminder, check-in, no-show, walk-in windows, front-desk override, basic billing link.  
**Out:** teleconsult, inpatient, pharmacy e-prescribe, WhatsApp (Phase 2), AI triage.

## Assumptions and constraints

**Assumptions:** HIS can expose doctor roster and slot API; mobiles unique enough after duplicate flag; DLT SMS templates in 3 weeks.  
**Constraints:** 12-week build; existing HIS (no rip-and-replace); clinical hours 8:00–20:00; patient data confidentiality.

## As-Is process (diagram described)

1. Patient arrives; paper token at specialty counter.  
2. Name in register; no unique ID guaranteed.  
3. Doctor sees token order; VIP inserted.  
4. Follow-up verbal date; no reminder.  
5. Billing after consult. Report = token count only.

**Problem analysis:** Chaos is unscheduled demand + no reminder + no no-show rule. App without roster still fails.

**Root cause:** Policy gap (first-come unwritten) + data gap (no slot entity) + people gap (roster not published) + tech gap (no booking). 5 Whys on no-show ends at: no slot, therefore no reminder, therefore 22% miss.

## To-Be process (diagram described)

1. Patient books named doctor + 15-min slot (or call centre).  
2. SMS confirm + 24h reminder with reschedule.  
3. Check-in at kiosk/desk; status ARRIVED.  
4. 15 min late → NO_SHOW; slot released.  
5. Walk-in only in published windows.  
6. Billing against appointment id.

## Gap analysis

| ID | Type | Gap | Action |
|---|---|---|---|
| G-01 | Process | Token-only | Slot + walk-in windows |
| G-02 | Tech | No booking UI/API | Portal + HIS |
| G-03 | Tech | No reminder | SMS vendor |
| G-04 | People | Clerks on tokens | Training |
| G-05 | Data | Register names | MPI + slot |
| G-06 | Policy | No no-show rule | BR 15 min |
| G-07 | People | Doctors overbook | Weekly roster |

## Requirements

| ID | Type | Statement |
|---|---|---|
| FR-APT-01 | F | Patient books available slot ≥ 24h ahead (or same-day if released). |
| FR-APT-02 | F | Front-desk can book/cancel/reschedule and walk-in into windows. |
| FR-APT-03 | F | Check-in sets ARRIVED; 15 min late → NO_SHOW and release. |
| FR-APT-07 | F | SMS 24h before CONFIRMED if consent=true. |
| FR-APT-12 | F | Unique patient ID required; duplicate mobile flagged. |
| NFR-APT-04 | NF | Confirm ≤ 5s; 99.5% 06:00–22:00. |
| NFR-APT-05 | NF | Audit who overrode a slot. |

## Business rules

- **BR-APT-03:** NO_SHOW after 15 minutes past start if not ARRIVED.  
- **BR-APT-04:** ≤ 20% slots marked WALKIN_WINDOW per doctor-session.  
- **BR-APT-05:** SMS only with recorded consent.  
- **BR-APT-06:** Roster published by Thursday for next week or slots freeze.

## User stories (with AC)

1. **As a patient, I want to book a slot** so I do not take a token. **AC:** Given published roster, When I pick slot, Then confirmation SMS.  
2. **As a patient, I want a reminder** so I remember. **AC:** 24h before, SMS with reschedule link.  
3. **As a patient, I want to reschedule** once without calling. **AC:** Link works until 2h before start.  
4. **As front-desk, I want walk-in windows** so overflow is legal. **AC:** Cannot book walk-in into specialist Must slots.  
5. **As a doctor admin, I want to publish roster.** **AC:** Unpublished week → no patient slots.  
6. **As ops, I want no-show marked automatically.** **AC:** 15 min rule fires without clerk.

## Use case (fully dressed): UC-APT-01 Book appointment

- **Actor:** Patient (or desk on behalf). **Pre:** Registered / new registration with ID + mobile + consent.  
- **Trigger:** Selects Book.  
- **Main:** Specialty → doctor → day → slot → confirm → SMS.  
- **Alt:** No slots → waitlist Could (out of MVP).  
- **Exception:** Duplicate mobile flag → desk merge.  
- **Post:** Appointment CONFIRMED; HIS slot locked.

## Wireframes

1. Find doctor/specialty. 2. Calendar. 3. Confirm + consent. 4. My appointments (reschedule/cancel). 5. Desk calendar + walk-in. 6. Kiosk check-in PIN. 7. Roster admin. 8. No-show dashboard.

## Data, reports, KPIs

**Data:** Patient, Consent, Roster, Slot, Appointment, CheckIn, SmsLog.  
**Reports:** % pre-booked; no-show; wait (check-in to consult); walk-in mix; SMS fail.  
**KPIs:** 70% pre-booked; no-show ≤ 12%; wait P50 ≤ 30 min booked.

## UAT scenarios

- Book + reminder + check-in.  
- No-show auto at 15 min.  
- Walk-in blocked on Must slot.  
- Consent false → no SMS.  
- Duplicate mobile flag.  
- Roster unpublished → no slots.

## RTM

| Req | Story | UC | UAT |
|---|---|---|---|
| FR-APT-01 | US1 | UC-APT-01 | Book |
| FR-APT-07 | US2 | — | Reminder |
| FR-APT-03 | US6 | — | No-show |
| BR-APT-04 | US4 | — | Walk-in |
| FR-APT-12 | US1 | UC-APT-01 | Duplicate |

## Change request (sample)

**CR-APT-01:** Add WhatsApp reminders. Impact: vendor, consent, templates. **Decision:** Phase 2; SMS Must now.

## Risks and dependencies

| Risk | P/I | Mitigation | Owner |
|---|---|---|---|
| Doctors refuse roster | H/H | COO mandate + freeze slots | MS |
| HIS API delay | M/H | Vendor milestone | PM |
| Shared family mobile | H/M | Duplicate flag + desk | BA + desk |

**Dependencies:** HIS slot API, SMS DLT vendor, identity/MPI.

## Final business solution

Online appointments **plus** roster policy, 15-min no-show, 20% walk-in windows, SMS, MPI. The app is not the solution by itself. Success = mix, no-show, wait — tokens become overflow, not the default.

## Weak vs strong

| Weak | Strong |
|---|---|
| “Implement appointment app.” | 70% pre-booked; gaps G-01–G-07 each traced to FR/BR/TR. |

## Notes

- Healthcare case: people + policy gaps dominate technology.
- Consent is an NFR/BR, not a footer.
- Illustrative volumes only.
