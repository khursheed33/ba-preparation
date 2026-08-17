# Backlog and Sprint Artifacts

## Definition

The **product backlog** is the ordered list of everything known to be needed in the product. The **sprint backlog** is the team's plan for the current sprint: selected items plus tasks to reach the sprint goal.

A **sprint** is a time-boxed increment (often 2 weeks). Backlog items include **epics, features, user stories, tasks, and bugs**. **Backlog prioritization** orders value/risk/dependency. **Backlog refinement** keeps upcoming items Ready.

## Why it matters

If the product backlog is a dumping ground, sprints become random. If the sprint backlog is only Jira tasks with no sprint goal, the review has nothing to demo. A BA helps the PO keep the backlog **DEEP** and helps the team keep bugs, stories, and tasks distinct.

## Concepts

### Artifact map

| Artifact | Contains | Owner |
|---|---|---|
| Product backlog | Epics, features, stories, bugs (product-level), spikes | PO (BA supports) |
| Sprint backlog | Committed stories/bugs + tasks/sub-tasks | Developers |
| Sprint | Goal + timebox + increment | Scrum team |

### DEEP backlog

| Letter | Meaning | BA check |
|---|---|---|
| **D**etailed appropriately | Near-term items have AC; far items are thin | Do not fully dress the 80th idea |
| **E**mergent | New learning changes the list | Discovery notes become stories |
| **E**stimated | Team can size Ready items | Re-estimate after split |
| **P**rioritized | Ordered 1..n, not 20 "High" | PO rank; BA flags dependencies |

### Bug vs story vs task for a BA

| Type | When to use | BA writes |
|---|---|---|
| **Story** | New or changed behavior the user will notice | Actor, value, AC |
| **Bug** | Intended behavior is broken (regression or missed AC) | Repro, expected vs actual, severity, AC of the original story |
| **Task** | Work to complete a story/bug (code, test data, analysis hour) | Rarely a product-backlog item; belongs under the parent |

Do not open a "story" for "fix null pointer." Do not open a "bug" for "we never built guest checkout." That is a story (or forgotten scope).

## Real-world examples

1. **NovaBank:** Epic Digital KYC on product backlog; sprint backlog has "upload PAN" + tasks for store and QA data.
2. **QuickBite:** Bug "ETA shows 0 min" vs story "show restaurant delay notice."

## Sample 10-item ShopEase product backlog

| Rank | Type | Item | Notes |
|---|---|---|---|
| 1 | Story | Guest checkout with card success | Walking skeleton; Must for campaign |
| 2 | Story | Unserviceable pincode stop before pay | Exception; blocks Rank 1 value |
| 3 | Story | Card decline message + no double charge | Payments + QA |
| 4 | Bug | Promo code applies twice on retry | Production Sev-2; keep visible, may Kanban |
| 5 | Story | Saved addresses for logged-in buyer | After guest skeleton |
| 6 | Feature | Returns buyer request (under Returns epic) | Do not pull whole epic |
| 7 | Story | Seller 48h dispute inbox | Depends on Rank 6 |
| 8 | Epic | Marketplace returns (remainder) | Split; not sprint-ready |
| 9 | Story | Order confirmation SMS | Should; SMS vendor |
| 10 | Spike | Wallet provider feasibility (3 days) | Estimable unknown; time-box |

Priorities are ranks, not MoSCoW labels alone. Rank 8 stays epic until split. Rank 4 is a bug: intended promo behavior is broken.

## Scenario / Use case

### Context

ShopEase backlog has 200 "High" tickets mixing tasks ("create table"), bugs, and epics. Sprint planning takes three hours. Nothing is DEEP.

### Stakeholders

PO, BA, SM, developers, QA, support (bug intake).

### BA actions

1. Separate tasks under stories; delete orphan tasks from product backlog.
2. Apply DEEP: detail Rank 1–7; leave Rank 8+ as titles + one-line intent.
3. Tag bugs vs stories; route Sev-2 per Kanban policy if needed.
4. Facilitate PO ranking using dependencies (pincode before campaign ads).

### Sample artifact

The 10-item table above plus a rule: "No task on product backlog without a parent story/bug."

### Failure if ignored

Sprint backlog is a pile of tasks. Review cannot demo guest checkout. Promo bug stays buried. Emergent learning never changes rank.

## Weak vs strong

| Weak | Strong |
|---|---|
| 200 items all High | Ranked, DEEP, few Ready |
| Bug called a story to "look like value" | Honest bug with repro |
| Epic in the sprint as one row | Split features/stories |
| Sprint backlog = leftover product items | Sprint goal + selected Ready work |

## Notes

- Refinement is how the backlog stays DEEP; it is not optional admin.
- Features are optional grouping; some teams use epics only — be consistent.
- Spikes are backlog items with a learning outcome and time-box, not endless research.
- Prioritization without dependency notes is how Rank 1 fails in UAT.
- BA does not silently reorder the product backlog; that is PO accountability.
