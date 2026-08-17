# BABOK and the Business Analysis Lifecycle

The **Business Analysis Body of Knowledge (BABOK)** is the International Institute of Business Analysis (IIBA) guide to what BAs do: tasks, techniques, and competencies. It is a **reference**, not a project plan. You do not recite chapter numbers in a vendor interview. You use it so your work has a complete shape: plan, elicit, manage requirements, analyse strategy, specify the solution, and evaluate whether it worked.

This repo is not a BABOK course. BABOK is the map; folders `01`–`18` are how you practise the map on ShopEase, NovaBank, and MediCare+.

## Why it matters

Without a lifecycle, a BA becomes a document typist: BRD in week 1, silence until UAT. BABOK-style work keeps **need, stakeholder, value, and change** in view until the solution is in use. NovaBank “faster loans” that never measures cycle time after go-live is analysis that stopped too early.

## Six core concepts (keep these in every conversation)

| Concept | Meaning for a BA | ShopEase returns example |
|---|---|---|
| **Change** | The controlled difference you enable | Auto-approve Size returns under ₹2,000 |
| **Need** | The problem or opportunity | 9-day refund cycle; NPS drop |
| **Solution** | People + process + software that meet the need | Notifications + auto-approve + seller dashboard — not “a chatbot” |
| **Stakeholder** | Anyone affected or able to influence | Buyer, seller, warehouse, finance, legal |
| **Value** | Why the change is worth it | Cycle time ≤ 4 days; fewer “where is my refund?” tickets |
| **Context** | The organisation, rules, and constraints around the work | Consumer-protection rules; seller contracts; peak festival volume |

If a VP names a **solution** (chatbot), you still owe a **need**, **value**, and **context**.

## Knowledge areas (what the work is)

BABOK groups work into six knowledge areas. They overlap. Agile does not skip them; it slices them smaller.

| Knowledge area | What you actually do | Where this repo practises it |
|---|---|---|
| **Business Analysis Planning and Monitoring** | Who, when, which techniques, how you will trace and report | Stakeholders, RACI, communication plan (`01`, `02`) |
| **Elicitation and Collaboration** | Interviews, workshops, observation; keep people aligned | `02` elicitation; `01` communication |
| **Requirements Life Cycle Management** | Trace, prioritise, approve, change, retire | `02` lifecycle, RTM, change; `03` docs |
| **Strategy Analysis** | Current state, future state, risk, change strategy | Problem statements, SWOT/PESTLE, business case (`01`, `12`) |
| **Requirements Analysis and Design Definition** | Models, stories, specs, design options the business can choose | `03` BRD/FRD; `04` process/UML/ERD; `06` wireframes |
| **Solution Evaluation** | Does the live solution deliver the value? Gaps? | UAT and KPIs (`10`, `09`); post-go-live measures in case studies |

**Underlying competencies** (communication, facilitation, negotiation, critical thinking) sit under all six. They are not optional “soft” extras.

## BA lifecycle / process (how the work sequences)

A practical lifecycle a vendor BA can follow. Stages overlap in Scrum; they still happen.

```text
Plan → Discover (elicit) → Analyse → Recommend / specify
        → Deliver (clarify, trace, test) → Evaluate → (change or retire)
```

| Stage | Outcome | Typical artifact |
|---|---|---|
| Plan | Approach, stakeholders, cadence | RACI, elicitation plan, comms plan |
| Discover | Facts, pain, rules, data | Interview notes, As-Is, samples |
| Analyse | Structured need; conflicts visible | Models, gap, options |
| Recommend / specify | Chosen solution behaviour | BRD/FRD/stories, To-Be, wireframes |
| Deliver | Built behaviour matches the spec | Clarifications, RTM, UAT support |
| Evaluate | Value realised or gap named | KPI vs baseline, lessons, CR or retire |

This is the same spine as the [requirement lifecycle](../02-Requirements-Engineering/02-requirement-lifecycle.md), zoomed out to the **change**, not one FR.

## How a BA uses BABOK without becoming a certification parrot

| Do | Do not |
|---|---|
| Use knowledge areas as a **checklist** (“Did we evaluate after go-live?”) | Quote task IDs in a ShopEase workshop |
| Name techniques (MoSCoW, process model, RACI) when they help a decision | Pretend every project needs all 50 techniques |
| Map IIBA language to the client’s words (epic, FRD, CR) | Force “BABOK templates” onto a Scrum team that lives in Jira |
| Sit ECBA/CCBA/CBAP later if the market asks | Treat a badge as a substitute for a case study |

Certifications are optional in this syllabus. The lifecycle is not.

## Weak vs strong

| Weak | Strong |
|---|---|
| “I follow BABOK” with no artifacts | Plan → elicit → specify → UAT → measure cycle time |
| Lifecycle = “write the BRD” | Lifecycle includes evaluate and retire |
| Knowledge areas as exam flashcards | “We skipped solution evaluation; refund KPI never moved” |
| Copy a BABOK task list into Confluence | Pick three techniques that fit NovaBank’s constraint |

## Scenario / Use case: MediCare+ “patient app” with no lifecycle

**Context.** A clinic chain asks a vendor BA for “a patient app in eight weeks.” The BA writes screens. No planning of stakeholders (psychiatry), no strategy (no-show vs billing), no evaluation plan. App ships. No-shows unchanged.

**Stakeholders.** Ops, doctors, patients, legal (consent), vendor BA, PO.

**What the BA should have done.**

1. **Plan.** RACI: ops accountable for reminder policy; legal consulted on SMS; psychiatry managed closely.
2. **Discover.** Observe reception; count no-shows by specialty.
3. **Analyse.** Need = attendance, not “an app.” Options: SMS, call, deposit.
4. **Specify.** Reminders by specialty; psychiatry in-app only.
5. **Deliver.** UAT with real clinic hours, not office Wi-Fi.
6. **Evaluate.** No-show rate vs baseline in 30 days; CR if psychiatry still leaks.

**Sample artifact.** One-line approach:

> Knowledge areas in play: planning (RACI), elicitation (observation), strategy (no-show vs app), design definition (channel rules), evaluation (no-show %). Requirements lifecycle: baseline v1 reminder rules; retire “SMS all specialties” as a Won’t.

**What goes wrong if ignored.** You delivered a solution that never touched the need. BABOK would have flagged missing strategy analysis and missing solution evaluation — not missing Figma screens.

## Notes

- BABOK is owned by IIBA; this note is a study map, not a substitute for the guide.
- Six concepts: change, need, solution, stakeholder, value, context — test every VP request against them.
- Six knowledge areas are coverage, not a waterfall phase list.
- Lifecycle ends at **evaluate**, not at sign-off.
- Use this file as the index; do the practice in the numbered folders that follow.
- 
