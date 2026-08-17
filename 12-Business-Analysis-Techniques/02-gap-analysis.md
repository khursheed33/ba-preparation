# Gap Analysis

**Gap analysis** compares **current state (As-Is)** with **future state (To-Be)**, names the **gap**, and proposes **actions** that close it. A gap is not a wish list. It is a measurable difference between how work happens today and how it must happen to hit the objective.

## Why it matters

Requirements written without a gap are often “nice to have.” MediCare+ does not need “an app” because apps are fashionable. It needs to close the gap between walk-in tokens and booked slots so no-shows and queue chaos drop. The BA’s job is current → future → gap → action → requirement.

## Method: current, future, gap, action

| Step | Question | Typical evidence |
|---|---|---|
| 1. Current (As-Is) | How does it work today, with numbers? | Process map, volumes, TAT, error rate, policy |
| 2. Future (To-Be) | What must be true to hit the objective? | Target process, SLA, roles, data, policy |
| 3. Gap | What is missing or broken between 1 and 2? | People, process, technology, data, policy |
| 4. Action | What will close each gap? | Requirement, training, vendor, rule change |

Do not skip measurement. “We use tokens” is a fact. “Tokens cause 38% of OPD patients to wait > 90 minutes” is a usable current state.

## Five gap types a BA must separate

| Type | Meaning | MediCare+ example | Typical action |
|---|---|---|---|
| People | Skills, roles, capacity, behaviour | Front-desk cannot reschedule; doctors not rostered to slots | Role design, training, hiring |
| Process | Steps, handoffs, SLAs, exceptions | Walk-in token is the only path; no reminder, no no-show rule | New process + business rules |
| Technology | Systems, integrations, channels | HIS has billing, no patient-facing booking | Portal / SMS / HIS API |
| Data | Fields, quality, master data, history | Patient mobile missing or shared across family | Data rules, cleanup, unique ID |
| Policy | Rules the org or regulator imposes | “First come, first served” unwritten; no cancellation fee | Written policy + BR |

One problem can have all five gaps. If you only log a “system gap,” you will buy software and keep the same queue.

## Weak vs strong

| Weak | Strong |
|---|---|
| Gap: no online booking. | Process gap: 100% of OPD starts as walk-in token; To-Be: 70% pre-booked slots by month 3. |
| Action: implement app. | Action: HIS slot API + SMS confirm + front-desk override + no-show policy. |
| People gap: staff need training. | People gap: 12 desk clerks have never used slot calendar; 2-day training + floor walker for 2 weeks. |
| Link to requirements: “booking.” | Gap G-03 (no reminder) → FR-APT-07 send SMS 24h before confirmed slot. |

## Real-world examples

**ShopEase returns.** Current: buyer prints a form, drops at courier, refund in 14 days. Future: in-app pickup in 48 hours, refund in 3 days. Gaps: process (no pickup slot), tech (no reverse-logistics API), data (return reason not coded), policy (open-box not defined).

**NovaBank personal loan.** Current: 9 days average origination. Future: 24-hour in-app decision for salaried customers. Gaps: people (credit officers still re-key bureau data), tech (no video KYC), policy (physical Form 16 still mandatory).

## Scenario / Use case: MediCare+ walk-in tokens → online appointments

**Business context.** MediCare+ multi-speciality hospital. OPD sees ~800 walk-ins/day. Average wait 95 minutes. No-show for follow-up is 22% because follow-up is “come next Tuesday morning.” Doctors overbook mentally. Management wants “online appointments.”

**Current (As-Is)**

1. Patient arrives, takes a paper token at the specialty counter.
2. Clerk writes name in a register; HIS billing happens after the consult.
3. Doctor sees patients in token order, with VIP walk-ins inserted.
4. Follow-up: doctor says a day; no slot, no reminder.
5. Reports: daily token count only; no-show not measured for follow-ups.

**Future (To-Be)**

1. Patient books a 15-minute slot on web/app/phone for a named doctor.
2. SMS/WhatsApp confirmation + 24-hour reminder with reschedule link.
3. Front-desk can book, cancel, and walk-in overflow into published “walk-in windows.”
4. Doctor roster in HIS drives available slots.
5. No-show marked after 15 minutes; slot released; KPI dashboard.

**Gap register (worked)**

| ID | Type | Current | Future | Gap | Action |
|---|---|---|---|---|---|
| G-01 | Process | Token-only arrival | Slot booking + walk-in windows | No booking process | Design To-Be OPD process; BR for overflow |
| G-02 | Technology | HIS billing only | Patient channel + HIS slots | No booking UI or slot API | FR: book/cancel/reschedule; HIS integration |
| G-03 | Technology | No reminders | SMS 24h before | No notification service | FR: reminder + consent |
| G-04 | People | Clerks run tokens | Clerks manage calendar + exceptions | Skill and role gap | Training; new SOP; floor support |
| G-05 | Data | Name + phone in register | Unique patient ID, mobile, slot_id | Duplicate patients, no slot entity | Master patient index; slot data model |
| G-06 | Policy | Unwritten first-come | Written no-show and walk-in policy | No approved rules | BR: no-show after 15 min; 20% walk-in capacity |
| G-07 | People | Doctors overbook in head | Roster = capacity | Roster not maintained | Doctor admin must publish weekly roster |

**Linking gaps to requirements**

| Gap | Requirement ID | Statement |
|---|---|---|
| G-01, G-02 | FR-APT-01 | Patient can book an available slot for a doctor and specialty at least 24 hours ahead. |
| G-03 | FR-APT-07 | System sends SMS 24 hours before `status=CONFIRMED` if SMS consent is true. |
| G-05 | FR-APT-12 | Booking requires a unique patient ID; duplicate mobile must be flagged, not silently merged. |
| G-06 | BR-APT-03 | If patient is not checked in 15 minutes after slot start, status = NO_SHOW and slot is released. |
| G-04 | TR-APT-01 | Front-desk completes slot-calendar training before go-live (transition requirement). |
| G-02 | NFR-APT-04 | Booking confirmation within 5 seconds; 99.5% availability 6:00–22:00. |

**What goes wrong if ignored.** Vendor delivers a pretty app. Tokens continue because doctors never publish rosters (G-07). Reminders fail because mobiles are shared (G-05). Walk-ins still jump the queue because policy was never written (G-06). The “gap” was treated as a shopping list for software.

## How a BA runs a gap workshop

1. Map As-Is with ops on the wall (or Miro) using real volumes.
2. Agree To-Be with sponsor *before* features.
3. Tag each gap People / Process / Technology / Data / Policy.
4. Write one action and one requirement (or training/policy item) per gap.
5. Put residual gaps in out-of-scope or a later phase — do not hide them.

## Notes

- Always four steps: current, future, gap, action. Skipping current makes To-Be fantasy.
- Tag every gap as people, process, technology, data, or policy.
- A technology gap without a process and policy gap is usually incomplete.
- Each in-scope gap should trace to at least one requirement, rule, or transition item.
- Numbers belong in current and future (“800 walk-ins,” “70% pre-booked”), not only in the KPI slide.
