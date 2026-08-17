# Process, Capability, and Stakeholder Analysis

**Process analysis** studies *how work is done*: steps, roles, systems, waits, and exceptions. **Capability analysis** studies *what the organisation can do* as an ability (e.g. “24x7 order operations”), independent of one procedure or one tool. **Stakeholder analysis** (technique, not theory) maps who cares, who decides, and how you will engage them so process and capability work survive contact with real people.

## Why it matters

QuickBite can draw a clean scheduled-order process and still fail at 2 a.m. because **capability** (night ops, restaurant readiness, rider supply) does not exist. A BA who only maps process recommends a workflow tool. A BA who separates process, capability, and system recommends the right mix of people, hours, policy, and software.

## Capability vs process vs system

| Concept | Question | QuickBite scheduled orders |
|---|---|---|
| Capability | What must we be *able* to do? | Promise a slot, hold kitchen capacity, dispatch at T-minus, handle night exceptions |
| Process | How does a case flow? | Customer selects slot → restaurant confirms → hold → dispatch → deliver |
| System | What tool supports it? | App slot picker, restaurant tablet, dispatch engine |

You can have a process on paper and no capability. You can buy a system and still lack both.

## Process analysis (what the BA actually does)

- Map As-Is with time and volume on each step (not boxes only).
- Mark handoffs, loops, and “happy path vs exception.”
- Separate **work time** from **wait time**.
- Ask: which steps exist because of a system limitation vs a real business rule?

## Capability analysis and heat map

Rate each needed capability: current maturity vs importance for the outcome.

**Heat map — capabilities for QuickBite scheduled orders** (I = importance 1–5, M = current maturity 1–5, Gap = I − M)

| Capability | I | M | Gap | Heat |
|---|---|---|---|---|
| Slot promise with kitchen capacity | 5 | 2 | 3 | High |
| Restaurant menu available-by-time | 5 | 1 | 4 | High |
| Rider supply forecasting for slot | 4 | 2 | 2 | Med |
| 24x7 exception desk | 5 | 1 | 4 | High |
| Payment auth hold until slot | 4 | 3 | 1 | Low |
| Customer reschedule self-serve | 3 | 2 | 1 | Low |
| Night-time restaurant support | 5 | 1 | 4 | High |

Red (high gap + high importance) is where requirements and hiring go first — not the slot UI.

## Stakeholder analysis as a technique

Do not stop at a list of names. For each stakeholder, capture influence, interest, attitude, what you need from them, and the engagement move.

| Stakeholder | Influence | Interest | Attitude | Need from them | Technique move |
|---|---|---|---|---|---|
| QuickBite CPO | H | H | Supportive | Priority vs lunch peak | Short decision paper |
| Restaurant ops lead | M | H | Resistant | Slot capacity rules | Workshop + sample P&L |
| Dispatch lead | H | H | Cautious | Rider forecast assumptions | Shadow a night shift |
| Night-shift manager | L | H | “We don’t exist” | Confirm 24x7 gap | Interview; include in RACI |
| Customer (sample) | L | H | Frustrated | Slot trust, reschedule | 5 interviews + journey |
| Finance | M | M | Neutral | Hold vs capture payment | One rules session |
| Legal | M | M | Cautious | Fair cancellation | Review BR only |

**Technique focus:** interviews and shadowing for night ops; workshop for restaurant rules; RACI for who can break a slot promise; influence-interest grid to avoid spending all week with the CPO and zero time with the night manager.

## Weak vs strong

| Weak | Strong |
|---|---|
| Capability: we need a scheduled-order feature. | Capability: hold kitchen capacity by 15-min slot; currently maturity 1/5. |
| Process is fine. | Process steps work at 13:00; capability “24x7 ops” is missing, so 02:00 orders fail. |
| Stakeholder: restaurants. | Restaurant ops lead, resistant; needs P&L of idle kitchen vs rejected slots. |
| Heat map: everything is red. | Three red capabilities; UI reschedule is green-enough — defer. |

## Real-world examples

**NovaBank:** process for loan credit is documented; capability “same-day underwriting without re-key” is missing.

**MediCare+:** process for appointment booking is designed; capability “doctors publish roster weekly” is missing.

**EmployeeHub:** system (HRIS) exists; process for comp-off is tribal; capability “policy interpretation at plant night shift” is missing.

## Scenario / Use case: process looks fine, capability missing

**Context.** QuickBite product shows a scheduled-order flow: pick time, pay, restaurant accepts, rider assigned 40 minutes before slot. UAT in Bangalore at noon is green. Pilot in Hyderabad weekend nights: 31% of scheduled orders cancel or arrive 40+ minutes late. Product says “process is fine, tweak ETA.”

**What the BA finds.**

1. Process analysis: noon happy path is valid. Night path has a hidden step: “WhatsApp the city manager” because no desk is on duty.
2. Capability heat map: 24x7 exception desk and night restaurant support are red; slot UI is not.
3. Stakeholder analysis: night-shift manager was never a stakeholder; dispatch lead assumed restaurants stay open; restaurants assumed QuickBite would not take 1 a.m. scheduled orders.

**To-Be (capability-led).** Either (a) restrict scheduled slots to hours where ops capability exists, or (b) stand up 24x7 exception capability before expanding hours. System changes: hide slots outside capable hours; escalate queue with SLA.

**Requirements from the gap**

| ID | Statement |
|---|---|
| FR-SCH-09 | System offers slots only in windows where city ops status = ACTIVE_24 or within published hours. |
| BR-SCH-02 | If restaurant has not confirmed 3 hours before slot, auto-cancel and full refund; notify 24x7 desk. |
| NFR-SCH-03 | Exception queue first response ≤ 10 minutes, 24x7, for cities in Phase 1. |

**If ignored.** A perfect BPMN and a perfect app, dead at 2 a.m.

## Notes

- Capability = what the org can do. Process = how a case flows. System = the tool.
- Heat-map capabilities by importance vs maturity; fund red cells first.
- Stakeholder analysis is a working technique (grid, RACI, shadowing), not a theory slide.
- If the process is “fine” in daytime UAT, test the night/weekend capability explicitly.
- Missing 24x7 ops is a capability gap — do not disguise it as an ETA bug.
