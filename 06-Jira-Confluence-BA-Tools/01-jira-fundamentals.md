# Jira Fundamentals

## Definition

Jira is an issue-tracking and work-management tool. A **project** is a container for work. An **issue** is one unit of work (epic, story, task, subtask, or bug). The **backlog** is the ordered list of work not yet started. A **sprint** is a time-boxed slice of that backlog the team commits to deliver.

For a BA, Jira is the live source of truth for *what* is requested, *why*, *priority*, and *status* — not a dumping ground for meeting notes.

## Why it matters

If work is not in Jira, it is invisible to Dev, QA, and the Product Owner (PO). Weak tickets cause rework. Strong tickets let the team build the right thing without chasing you on Slack.

## How a BA uses Jira daily

| Time | Typical BA action |
|---|---|
| Morning | Check sprint board, blockers, comments on your stories |
| After standup | Split oversized stories, add acceptance criteria (AC), answer Dev questions |
| Mid-day | Groom backlog with PO: rank, clarify, reject duplicates |
| After workshops | Create/update epics and stories from decisions |
| Before sprint planning | Confirm Definition of Ready (DoR) on candidate stories |
| UAT | Log bugs, link to stories, confirm expected vs actual |

You do **not** assign story points, write code, or close tickets that QA has not verified. You keep requirements current as the team learns.

## Projects and issues

A **project** maps to a product or programme (e.g. `SE` for ShopEase, `NB` for NovaBank). Issue keys look like `SE-142`.

| Type | What it is | BA owns |
|---|---|---|
| Epic | Large outcome spanning many sprints | Outcome, scope, success metric |
| Story | User-facing slice of value | Description, AC, business rules |
| Task | Technical or ops work with no user story | Why it is needed, if business-facing |
| Subtask | Split of a story/task for one person | Rarely; Dev/QA create these |
| Bug | Behaviour that does not match AC or production | Repro steps, expected vs actual, severity |

## Sample issue hierarchy: ShopEase returns

Epic: `SE-200 Allow customer to return an item within 7 days`

| Key | Type | Summary |
|---|---|---|
| SE-201 | Story | As a buyer, I can start a return from Order History |
| SE-202 | Story | As a buyer, I can choose refund to original payment or wallet |
| SE-203 | Story | As a warehouse user, I can mark the item received |
| SE-204 | Task | Configure return reason codes with Ops |
| SE-201-1 | Subtask | API contract for create-return (Dev) |
| SE-205 | Bug | Return window uses calendar days, AC said 7 business days |

Story SE-201 AC (example):

1. Given an order delivered within 7 days, when the buyer taps Return, then eligible items are listed.
2. Given an item marked non-returnable, when the buyer views it, then Return is hidden and a reason is shown.
3. Given a return is submitted, when Ops opens the queue, then the request appears within 1 minute.

## Fields a BA should fill vs leave to Dev

| Field | Who | Why |
|---|---|---|
| Summary | BA | Searchable, one outcome |
| Description | BA | Context, As-Is vs To-Be, links to Confluence |
| Acceptance criteria | BA | Testable rules; QA writes cases from these |
| Priority | BA + PO | Business urgency, not "I want it today" |
| Labels / Components | BA | Reporting and filtering (see next note) |
| Epic link | BA | Traceability |
| Attachments | BA | Wireframes, policy PDFs, sample files |
| Story points | Dev | Estimate; BA must not inflate or deflate |
| Sprint | PO / Scrum Master | Commitment |
| Assignee | Dev lead / SM | Who does the work |
| Technical design | Dev | Implementation |
| Environment / logs | QA or Dev (bugs) | Repro evidence |

**Rule:** if a field answers "what should the product do?", the BA fills it. If it answers "how will we build it?", leave it to Dev.

## Backlog and sprint

The **backlog** is ranked: top items are next. Ranking is a PO decision the BA supports with impact, risk, and dependency notes.

A **sprint** (often 2 weeks) contains only Ready stories. If a ShopEase return story is missing refund-method rules, it stays in the backlog. Pulling unready work into a sprint is how UAT fails.

## Real-world examples

1. **NovaBank** KYC epic: stories for document upload, liveness check, and maker-checker. The BA keeps one epic so compliance can see the whole journey.
2. **MediCare+** appointment bugs: BA files `MC-88` with patient ID masked, steps, expected slot, actual double-book. Dev does not guess from "booking is broken".

## Scenario / Use case

ShopEase Ops wants "faster returns". The BA does not create one giant task. After a workshop, the BA creates epic SE-200, three stories with AC, and a config task for reason codes. In sprint planning, Dev asks whether damaged items get a full refund. The BA updates SE-202 AC the same day, comments on the ticket, and links the Confluence decision log. QA tests from AC, not from Slack. Result: warehouse received-flow ships in sprint 12 without a "what did we mean?" delay.

## Weak vs strong

| Weak | Strong |
|---|---|
| "Fix returns" as one task | Epic + stories with AC and refund rules |
| AC in a chat thread | AC on the story, versioned in comments |
| BA assigns story points | Dev estimates; BA clarifies scope |
| Bug: "not working" | Steps, data, expected vs actual, linked story |
| Everything is a story | Config work is a task; splits are subtasks |

## Notes

- Treat Jira as the contract with the team, not a personal notebook.
- One story = one testable outcome; if AC needs "and also", split it.
- Link bugs back to the story so the PO sees escaped defects.
- Never put PAN, Aadhaar, or full card numbers in tickets; mask sample data.
- If the PO and BA disagree on rank, record both views in a comment and let the PO decide.
- Subtasks do not replace stories; they organise execution inside a story.
- Review your own tickets before standup so you are not the blocker.
