# Scrum and Kanban

## Definition

**Scrum** is a time-boxed framework: sprints, roles, backlog, and ceremonies to deliver a potentially shippable increment.

**Kanban** is a flow system: visualize work, limit **WIP** (work in progress), manage cycle time, and pull the next item when capacity frees — no required sprints.

## Why it matters

Catalog features need a sprint goal and a demo. Production bugs and tiny content changes need flow, not a two-week wait for planning. A BA who forces Scrum on incident work (or Kanban on a multi-story product bet) creates the wrong cadence.

## Concepts

### Scrum vs Kanban

| | Scrum | Kanban |
|---|---|---|
| **Cadence** | Fixed sprint (often 2 weeks): plan, review, retro | Continuous pull; optional replenishment meetings |
| **WIP** | Implicit (sprint commitment) | Explicit WIP limits per column |
| **Roles** | PO, Scrum Master, Developers; BA often supports PO | No mandated roles; BA may own intake quality |
| **Boards** | Sprint board (To do / In progress / Done) reset-ish each sprint | Persistent board (e.g. New / Ready / Doing / QA / Done) |
| **Change mid-cycle** | Discouraged; threatens sprint goal | Normal; expedite lane for Sev-1 |
| **Forecast** | Velocity (points per sprint) | Throughput / cycle time |

### When BA work is Kanban vs Scrum

| Kanban-fit BA work | Scrum-fit BA work |
|---|---|
| Production issues, defects, small copy/rule tweaks | Product increments, new journeys, epics |
| Support-driven "broken checkout tax" | ShopEase catalog search overhaul |
| Ops requests with unpredictable arrival | Roadmap features with a sprint goal |
| Compliance hotfixes that cannot wait for planning | Discovery that still ships a walking skeleton |

Same BA can serve both: **product team Scrum**, **stabilization team Kanban**, with a clear intake so bugs do not silently eat the Scrum sprint.

## Real-world examples

1. **NovaBank:** Digital KYC epic on Scrum; "statement PDF wrong amount" on Kanban ops board with WIP 3.
2. **MediCare+:** Appointment booking MVP in Scrum; clinic "add holiday closure" requests on Kanban.

## Scenario / Use case: ShopEase catalog Scrum + support-bug Kanban

### Context

One team does everything. Sprint goals die because Sev-2 bugs jump the board. Catalog never demos. Support is angry that bugs wait 12 days for sprint planning.

### Stakeholders

Catalog PO, support lead, Scrum Master, developers, QA, BA, merchandising.

### BA actions

1. Split intake: **catalog increment** (Scrum) vs **production defects / tiny tweaks** (Kanban).
2. Define bug vs story (see backlog notes): if it is broken intended behavior → bug on Kanban; if new behavior → story on Scrum.
3. Set Kanban WIP (e.g. 2 in Dev, 2 in QA) and an expedite policy for Sev-1.
4. Protect Scrum: only Sev-1 interrupts the sprint; Sev-2 flows on Kanban capacity (dedicated % or a second board).
5. BA writes AC for Kanban items too (repro + expected) — Kanban is not "no analysis."

### Sample artifact

| Team | Method | Cadence | BA focus |
|---|---|---|---|
| Catalog | Scrum | 2-week sprint, review of search facets | Stories, mapping, sprint AC |
| Support-bug | Kanban | Daily stand-up on stalled columns | Reproduce, expected vs actual, regression AC |

Policies: Sev-1 may pull a Scrum developer with PO+SM agreement; otherwise bugs stay on Kanban.

### Failure if ignored

Everything is "the sprint." Bugs wait; features thrash. Or everything is Kanban with no sprint goal — catalog epics never finish because WIP is unlimited "in progress."

## Weak vs strong

| Weak | Strong |
|---|---|
| Kanban = no priorities | Ordered ready column + WIP limits |
| Scrum = ignore production | Explicit interrupt policy |
| BA only in Scrum ceremonies | BA on Kanban replenishment too |
| One board, mixed policies | Two policies, visible to support and product |

## Notes

- WIP limits make queues visible; if Ready is huge, the BA is producing too far ahead or Dev is stuck.
- Scrum without a sprint goal is a time-boxed Kanban with extra meetings.
- Cycle time on Kanban is a BA metric for "how long until this defect is live."
- Do not copy Scrum roles onto a Kanban ops team unless the org wants them.
- Small changes still need AC: expected result after the fix.
- Watch: [Scrum in under 10 minutes](https://www.youtube.com/watch?v=XU0llRltyFM) and [Kniberg product ownership](https://www.youtube.com/watch?v=502ILHjX9EE).
