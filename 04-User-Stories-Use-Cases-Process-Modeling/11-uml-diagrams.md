# UML Diagrams for Business Analysts

## Definition

**UML (Unified Modeling Language)** is a family of diagrams for structure and behavior. A BA uses a **small subset** to explain actors, flows, time-ordered interactions, and lifecycle — not to replace solution architects.

Relevant types:

- **Use case diagram:** actors and goals (bubbles) plus relationships.
- **Activity diagram:** workflow, decisions, parallel (similar intent to BPMN/activity flow).
- **Sequence diagram:** messages over time between actors/systems.
- **State diagram:** how one object changes status (appointment, claim, order).

**Basic UML** for a BA means: correct actors, readable flows, named messages, and complete states — not every UML 2.5 feature.

## Why it matters

Stories do not show time. Flowcharts do not show message order (OTP). Tables do not show illegal transitions (complete a cancelled appointment). UML fills those gaps when stakeholders must agree on behavior before build.

## Concepts — when a BA uses each (not instead of architects)

| Diagram | BA uses it for | Architect / tech lead uses it for | Skip when |
|---|---|---|---|
| Use case | Scope of goals and actors | System-of-systems use cases | You only have one actor and three stories |
| Activity | Business workflow, swimlanes | Detailed service orchestration | BPMN is already the team standard |
| Sequence | OTP, payment, "who calls whom" | Protocol, retries, timeouts at API level | No integration conversation yet |
| State | Status model and allowed transitions | Persistence, event sourcing | Status is a single flag with no rules |

BA rule: if the diagram needs class attributes and design patterns, hand it to architecture. Keep BA UML at **business objects and interactions**.

## System design collaboration (architects and developers)

Solution assessment is **shared**, not thrown over the wall.

| You bring | They bring | Joint output |
|---|---|---|
| Behaviours, rules, exceptions, volumes | Constraints, patterns, NFRs that are technical | Options the business can choose (not one secret design) |
| Conceptual ERD, DFD, state model | Physical schema, APIs, sequence at protocol level | Agreed grain, error codes, “who owns the source of truth” |
| Wireframes / AC | Feasibility and effort | Split stories; spike vs Must |

Cadence: three amigos on each thick story; architecture review when a new system or store appears. Do not wait for a “design phase” if you are in Scrum — bring the diagram to refinement.

Data model detail: [ERD](13-entity-relationship-diagrams.md). Process/integration: [BPMN and DFD](10-bpmn-dfd-context-diagrams.md).

## Real-world examples

1. **ShopEase order states:** placed → paid → packed → shipped → delivered / cancelled / returned. Illegal: shipped → placed.
2. **NovaBank transfer sequence:** App → OTP service → App → Core banking (no core call before OTP success).

## Mini examples

### MediCare+ appointment states

States: **Requested, Confirmed, Completed, No-show, Cancelled.**

| From | To | Trigger |
|---|---|---|
| Requested | Confirmed | Clinic/doctor accepts slot |
| Requested | Cancelled | Patient or clinic declines before confirm |
| Confirmed | Completed | Visit occurred (clinic marks done) |
| Confirmed | No-show | Slot time passed; patient did not attend |
| Confirmed | Cancelled | Cancel within policy window |
| Cancelled / Completed / No-show | (none) | Terminal — no return to Requested |

AC must forbid "mark completed" from Cancelled. This is why a state diagram exists.

### Sequence: OTP login (NovaBank or ShopEase — same pattern)

Actors/objects: User, Mobile app, Auth service, OTP/SMS gateway.

1. User → App: enter mobile number.
2. App → Auth: request OTP.
3. Auth → OTP gateway: send SMS.
4. OTP gateway → User: SMS (out of band).
5. User → App: enter OTP.
6. App → Auth: verify OTP.
7. Auth → App: session token **or** fail (attempts remaining).
8. App → User: home screen or error.

BA callout: after fail, **no session**. Timeout is an alternate message Auth → App.

### Use case diagram actors (MediCare+ appointments)

- **Primary:** Patient, Clinic receptionist, Doctor (limited).
- **Secondary:** SMS gateway, Calendar/EMR, Payment (if deposits).
- **Use cases:** Book appointment, Cancel appointment, Confirm appointment, Record no-show, Send reminder (**include** from Confirm or a scheduler).
- **Extend:** Pay deposit extends Book when clinic requires it.

## Scenario / Use case

### Context

MediCare+ developers implement "status = string on the appointment." Support marks no-show on cancelled visits. OTP login on a patient app lets users in when SMS is delayed because the sequence was never agreed.

### Stakeholders

Patient, clinic, doctor, BA, PO, QA, app team, EMR vendor (secondary).

### BA actions

1. Facilitate a state workshop; list legal transitions only.
2. Draw a simple sequence for OTP with fail/timeout.
3. Sketch use case diagram to confirm doctor is not a booking primary actor on the patient app.
4. Give diagrams to architecture for technical depth; keep BA versions in Confluence.

### Sample artifact

State table (above) + sequence steps 1–8 + actor list. Title: "BA behavior model — not system design."

### Failure if ignored

No-show metrics include cancelled visits. OTP race issues. Doctor "use cases" appear on the patient app. Architects redraw everything because BA UML tried to specify classes.

## Weak vs strong

| Weak | Strong |
|---|---|
| Use case diagram with 40 bubbles | Few goals, clear primary vs secondary |
| Sequence of UI pages only | Named systems and messages |
| State list without transitions | Table of from → to + trigger |
| BA producing class diagrams | BA producing behavior; architect designs structure |

## Notes

- Activity diagrams: use if the team does not speak BPMN; do not maintain both for the same process.
- Every state needs an owner of the transition (who may click "no-show").
- Sequence diagrams are for tricky timing (OTP, payment, dual write) — not for "user opens menu."
- Include/extend on use case diagrams should match written use cases.
- Label diagrams As-Is or To-Be.
- Design is collaborative: BA owns behaviour and grain; architect owns physical structure.
