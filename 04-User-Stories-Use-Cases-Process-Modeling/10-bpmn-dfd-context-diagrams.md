# BPMN, DFDs, and Context Diagrams

## Definition

**Business Process Model and Notation (BPMN)** is a standard way to draw processes with events, tasks, gateways, pools, and lanes so business and IT share one language.

**Business Process Modeling** is the practice of representing how work gets done — to understand, communicate, improve, and automate. BPMN is one notation; flowcharts are another.

**Data Flow Diagrams (DFD)** show how data moves between external entities, processes, and stores — not who clicks what.

A **context diagram** (often DFD Level 0's parent, "Level C" / Level 0 context) puts **one system in the middle** and **external entities** around it with data/control flows.

## Why it matters

BAs who only write stories miss integration and data. BPMN clarifies parallel work and timers. DFDs catch "payment captured but order store not updated." Context diagrams stop silent scope creep (another system appearing mid-project).

## Concepts

### BPMN basics

| Element | Meaning |
|---|---|
| Start event (thin circle) | Process begins (order placed) |
| End event (thick circle) | Process finishes (delivered / cancelled) |
| Task (rounded rectangle) | Work unit (assign rider) |
| XOR gateway (X) | One path only (payment success or fail) |
| AND gateway (+) | Parallel paths all run (notify customer AND restaurant) |
| Pool | An organization or system (QuickBite platform vs restaurant POS) |
| Lane | Role inside a pool (customer, restaurant, rider, support) |
| Intermediate event | Wait or message (timer: 10 min no rider) |

XOR = exclusive decision. AND = split/join parallel. Do not use AND when you mean "if."

### Mini BPMN description: QuickBite order

**Pool:** QuickBite. **Lanes:** Customer, Restaurant, Rider, Platform.

1. **Start:** Customer places order (start event).
2. **Task:** Platform authorizes payment.
3. **XOR:** Payment OK? No → End (failed). Yes → continue.
4. **AND split:** Notify restaurant **and** create order record.
5. **Task (restaurant):** Accept or reject. **XOR:** Reject → refund → End. Accept → continue.
6. **Task:** Assign rider. **Timer event:** if no rider in 10 minutes, escalate to support lane.
7. **Tasks:** Pick up → deliver. **AND join** not needed if sequential.
8. **End:** Delivered (or cancelled with refund path).

This is a description a BA can later draw in a tool; the point is events, XOR vs AND, and a timer.

### DFD: ShopEase payments (context + level 0)

**Context diagram (system in the middle):**

- **Center:** ShopEase Payments
- **External entities:** Buyer, Payment gateway, Bank/UPI, ShopEase Order service, Finance/GL, Fraud engine
- **Flows:** Buyer → pay request; Payments → gateway charge; Gateway → auth result; Payments → Order service (paid/failed); Payments → Finance (settlement file); Fraud → score / block

**Level 0 (major processes inside Payments):**

| Process | In | Out | Store |
|---|---|---|---|
| P1 Capture intent | Buyer, order id, amount | Intent record | D1 Payment intents |
| P2 Authorize | Gateway | Auth code / decline | D1 updated |
| P3 Settle / reconcile | Gateway settlement | GL entries | D2 Settlements |
| P4 Notify | Status | Order service event | — |

Stores are data at rest (intents, settlements), not "the database server brand."

### Context diagrams — rules

- One system bubble.
- External entities are people or other systems, not internal modules.
- Every flow named (what data, not "integration").
- If an entity is missing (fraud), scope is incomplete.

## Real-world examples

1. **NovaBank:** Context diagram for Digital KYC with OCR vendor, core banking, and regulator reporting as externals.
2. **MediCare+:** BPMN XOR for slot available vs waitlist; AND to SMS patient and update clinic calendar.

## Scenario / Use case

### Context

QuickBite wants "order flow" in Confluence as a cartoon. Payments at ShopEase fail silently between gateway and order service. No context diagram exists.

### Stakeholders

Product, engineering, payments ops, restaurant ops, BA, architect (review, not own the BA model).

### BA actions

1. Agree modeling purpose: handoff and exceptions (BPMN) vs data (DFD) vs scope (context).
2. Draft QuickBite BPMN description with XOR payment and AND notify.
3. Draft ShopEase payments context + level 0 with Order service as external.
4. Walk ops through "authorize success, notify fail."

### Sample artifact

Context diagram list of entities + named flows; Level 0 table; BPMN bullet sequence with gateway types labeled.

### Failure if ignored

AND vs XOR confused: restaurant notified even when payment fails. DFD never drawn: order stays "pending" while the buyer is charged. Context diagram skipped: fraud engine added late as an emergency.

## Weak vs strong

| Weak | Strong |
|---|---|
| BPMN as colorful flowchart with no events | Start/end, XOR/AND, timer |
| DFD that is a UI storyboard | Processes, stores, named data |
| Context with internal microservices as entities | Externals only; system as one bubble |
| Modeling "because the template has a page" | Purpose: improve, integrate, or scope |

## Notes

- BA models for clarity; architects may add technical BPMN (service tasks, messages).
- Level 0 is not code. Stop when stores and interfaces are agreed.
- Pools show company/system boundaries; lanes show roles.
- Name every flow; arrows without nouns are decoration.
- Validate models with an exception walkthrough, not only the happy AND-split.
- Pair DFDs with an [ERD](13-entity-relationship-diagrams.md): stores should match entities.
- Watch: [Lucidchart BPMN 2.0](https://www.youtube.com/watch?v=BwkNceoybvA) and [Lucidchart ERD](https://www.youtube.com/watch?v=QpdhBUYk7Kk).
