# Jira Boards, Workflows, and Fields

## Definition

A **board** is a visual of issues by status. A **Scrum board** is sprint-scoped. A **Kanban board** is a continuous flow with WIP limits. A **workflow** is the allowed path of statuses (To Do → Done). **Priority**, **labels**, **components**, and **assignee** are fields that help people find, rank, and own work.

The BA's job is to keep status honest and to put **gates** where analysis or UAT must happen before work moves on.

## Why it matters

Wrong board type, skipped statuses, or junk labels hide risk. Teams then "finish" stories that were never analysed or never accepted by business.

## Scrum board vs Kanban board

| | Scrum board | Kanban board |
|---|---|---|
| Time box | Sprint | None |
| Typical use | Feature teams with planning | Ops, support, BAU, production bugs |
| Commitment | Sprint goal | Pull next Ready item |
| BA focus | DoR before planning; UAT in sprint | Cycle time; stop starting, start finishing |

**ShopEase** product squad uses Scrum for the returns epic. **QuickBite** support uses Kanban for restaurant-onboarding tickets that arrive daily.

## Sample workflow with BA gates

Recommended path for a product team:

`To Do → Analysis → Ready → In Progress → QA → UAT → Done`

| Status | Meaning | Who moves it | BA gate |
|---|---|---|---|
| To Do | Captured, not refined | Anyone | None |
| Analysis | BA/PO clarifying | BA | Problem, scope, AC draft |
| Ready | Meets Definition of Ready | BA + PO | AC, dependencies, mock if UI |
| In Progress | Dev coding | Dev | Answer questions same day |
| QA | Test against AC | QA | Clarify expected result |
| UAT | Business validates | BA + business | Sign-off or fail with bug |
| Done | Accepted and in the increment | PO / BA | No open Sev1 on the story |

Do **not** let Dev jump Ready → Done. That skip is how production misses the MediCare+ consent checkbox.

Statuses are not decorations. If a ticket is waiting on legal, it is not In Progress.

## Priorities

| Priority | When to use |
|---|---|
| Highest | Production down, money or safety at risk |
| High | Sprint commitment or regulatory date |
| Medium | Planned value, no date crisis |
| Low | Nice-to-have, tech chore with no user impact |

BA mistake: marking every ShopEase story Highest. Priority then means nothing.

## Labels vs components

| | Labels | Components |
|---|---|---|
| Structure | Free tags, many per issue | Owned list (often by module) |
| Example | `needs-legal`, `release-24.3`, `uat-fail` | `Checkout`, `Wallet`, `Returns` |
| Who maintains | Anyone (risk of spelling chaos) | Project admin / BA with Dev |
| Best for | Temporary flags and cross-cutting themes | Stable product areas and reporting |

Use **components** for "which part of the product". Use **labels** for "what campaign or constraint". Do not create both `returns` as a label and `Returns` as a component unless you have a reason.

## Assignees

Assignee = person currently responsible, not "who cares about this".

- Analysis: BA
- In Progress: Dev
- QA: tester
- UAT: BA or business SME
- Unassigned Ready tickets are a smell before sprint planning

The BA should not stay assignee through coding; that hides who is blocked.

## Real-world examples

1. **ShieldSure** claims Kanban: WIP limit of 5 in "Adjuster review". When the column fills, the BA stops pulling new stories and runs a bottleneck workshop.
2. **NovaBank** Scrum: stories for UPI limits use component `Payments` and label `RBI-circular-2026` so compliance can filter one board.

## Scenario / Use case

NovaBank's cards squad has 14 tickets stuck in **BA Review** (their name for Analysis). Developers idle. Root cause: there is no Definition of Ready. Tickets enter BA Review with a title only ("change MCC blocking"). The BA is expected to invent AC during the sprint.

Fix the BA applies:

1. Add DoR checklist on the board: problem statement, AC, business rules, data fields, open questions = 0, UX link if UI.
2. Workflow: Analysis cannot move to Ready without the DoR checkbox (or a Scrum Master audit twice a week).
3. PO and BA run a 45-minute refinement; 8 tickets go back to To Do as duplicates or out of scope; 6 become Ready.
4. Label `blocked-legal` is added to 2 remaining items so they are not "fake Ready".

Next sprint, BA Review is a queue of 3, not a parking lot. Cycle time drops because work is pulled only when analysable.

## Weak vs strong

| Weak | Strong |
|---|---|
| One status: To Do / Done | Explicit Analysis, Ready, UAT |
| Kanban with no WIP limit | Limit Analysis and In Progress |
| Label `imp`, `Imp`, `important` | Controlled labels + components |
| BA remains assignee forever | Assignee follows the current gate |
| Highest on 40 tickets | Highest only for production/regulatory |
| Skip UAT to hit the date | Fail UAT, log bugs, re-enter QA |

## Notes

- Status should match reality; "In Progress" while waiting on a vendor is a lie — use Blocked or a waiting status.
- DoR is a BA tool; Definition of Done is a team tool. You need both.
- Components beat labels for dashboards that finance or ops will reuse.
- If UAT is always empty until the last day, the workflow is theatre.
- Train stakeholders: comments on the ticket, not WhatsApp screenshots.
- Review labels quarterly; delete one-off tags that never get queried.
- A Scrum board of 80 tickets in one sprint is not ambitious — it is unrefined backlog dumped into a sprint.
