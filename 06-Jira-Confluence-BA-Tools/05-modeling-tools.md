# Modeling Tools: Draw.io, Lucidchart, Miro, and Visio

## Definition

**Draw.io** (diagrams.net) is a diagram editor, often embedded in Confluence/Jira. **Lucidchart** is a similar cloud diagram tool with stronger collaboration and templates. **Miro** is an infinite whiteboard for workshops, sticky notes, and messy thinking. **Microsoft Visio** is the desktop (and web) diagram tool still standard in many banks, insurers, and government accounts.

A BA uses these to make **process, journey, and system-lite pictures** that stakeholders can correct. You are not the enterprise architect.

## Why it matters

Text-only process descriptions hide loops and handoffs. A picture in a workshop gets "that's not how warehouse actually receives returns" in five minutes. That sentence is worth more than a 20-page BRD written alone.

## Purpose and when to use which

| Tool | Best for | Weak for | Typical BA moment |
|---|---|---|---|
| Miro | Workshops, affinity mapping, journey drafts, voting | Versioned baseline diagrams | QuickBite ops in a room (or Zoom) |
| Draw.io | As-Is/To-Be process, flowcharts, simple ER, swimlanes | Live multiplayer energy | Baseline after the workshop |
| Lucidchart | Same as Draw.io; shared libraries, comments, Lucid cards | Teams with no licence | Cross-vendor process with many reviewers |
| Visio | Client-mandated BPMN/swimlanes, stencils, print packs | Cheap collaboration if only one licence on a laptop | NovaBank/ShieldSure PMO that files `.vsdx` in the share |

**Rule of thumb:** diverge in Miro, converge in Draw.io, Lucidchart, or Visio, publish in Confluence. Visio vs Draw.io is an **account standard**, not a skill contest — same swimlanes, same legend, same versioned file.

You do not need to master every shape library. You need a readable swimlane, a decision diamond, and a legend.

## BA workflows

**1. Process map workshop (Miro)**

1. Frame the question: "How does an order become a delivered meal today?"
2. Columns = steps or swimlanes = roles (Customer, Rider, Restaurant, Support).
3. Silent sticky storm (5 min), then cluster.
4. Walk the happy path, then exceptions (cancel, rider reassign).
5. Dot-vote pain points.
6. Photograph / export; list decisions and open questions.

**2. Whiteboard (Miro or physical)**

Use for scope: in/out boxes, stakeholder map, or "what is an order vs a shipment?" Do not pretty it. Capture and move on.

**3. Architecture-lite (Draw.io / Lucidchart)**

Boxes for systems (App, Order service, Payment, SMS). Arrows labelled with events ("payment_success"). No server sizes, no Kubernetes. Enough for "OTP is sent by which system?"

## Workshop facilitation on Miro

| Facilitation move | Why |
|---|---|
| Timer on every activity | Stops the loudest person owning the board |
| One board, frames named | Discovery vs To-Be vs Parking lot |
| Private mode for stickies | Reduces groupthink |
| Parking lot frame | Protects the main thread |
| Explicit "not a solution yet" | Ops will jump to app features |
| End with owners | Who confirms the As-Is by Friday |

Invite 6–8 people, not 25. For QuickBite, that is Ops lead, one rider-ops, one restaurant success, support lead, PO, BA.

## Exporting diagrams into BRD / Confluence

| Step | Practice |
|---|---|
| Source of truth | Keep `.drawio` / Lucid doc linked on the Confluence page |
| Image | Export PNG/SVG into the page for readers who will not open the tool |
| Version | File name `QB-order-to-delivery-v3-To-Be.drawio` |
| Call-outs | Number steps on the diagram; same numbers in the page text |
| Permissions | Viewers of Confluence must be able to see the image without a Lucid licence if possible |

Never paste a screenshot as the only copy. In six months nobody can edit it.

## Real-world examples

1. **ShopEase** returns: Draw.io swimlane Customer → CS → Warehouse → Finance. Finance spots that refund starts before QC — policy bug.
2. **ShieldSure** FNOL: Lucidchart with comments from legal on the "admit liability" decision box.

## Scenario / Use case

QuickBite late-delivery complaints rise. Ops swears "riders are slow". The BA runs a 90-minute Miro workshop.

Frame 1: As-Is stickies. Restaurant "food ready" often fires when the item is still on the grill. Rider is auto-assigned too early, waits 12 minutes, then the SLA clock looks like rider delay.

Frame 2: pain votes. Highest: false "ready" signal.

The BA exports the board PDF to Confluence that afternoon. Overnight she redraws a clean As-Is in Draw.io with timestamps. To-Be is a separate page: restaurant cannot mark ready until pack photo or POS status. Stories go to Jira with the Draw.io embedded.

Ops agrees the problem was not "hire more riders". The workshop picture changed the backlog.

## Weak vs strong

| Weak | Strong |
|---|---|
| Miro board as permanent spec | Miro for workshop; Draw.io for baseline |
| 200 undecorated boxes | Swimlanes, legend, happy vs exception colour |
| BA draws As-Is alone | Workshop then confirm with one SME |
| Screenshot only | Editable source + published image |
| "Architecture" with 40 microservices | 6 boxes the business can read |
| No facilitation | Timer, parking lot, named decisions |

## Notes

- Purpose and workflow beat tool mastery; pick one diagram tool and one whiteboard and go deep enough.
- Visio, Draw.io, and Lucidchart are interchangeable for BA swimlanes — follow the account standard.
- Label every arrow with a business event, not "data".
- If two systems share a box, you are hiding a handoff — split it.
- Print or PDF the As-Is for warehouse/hospital floors that will not open Miro.
- Store vendor licence limits: do not build the only copy in a tool the company will cancel.
- Architecture-lite supports requirements; it does not replace a solution architect.
- Revisit the diagram at UAT: if testers walk a different path, the picture is wrong.
