# Story Splitting, Refinement, and Prioritization

## Definition

**Story splitting** turns an epic or fat story into small, valuable, testable slices. **Refinement (backlog grooming)** is the recurring session that makes upcoming items Ready. **Prioritization** orders stories by value, risk, and dependency — related to, but not the same as, requirement MoSCoW.

## Why it matters

Unsplit stories hide work until the last day of the sprint. Unrefined backlogs make planning theater. Mixing MoSCoW labels with sprint order without talking about dependencies ships a "Must" that cannot run without a "Could."

## Concepts

### Splitting patterns

| Pattern | How you split | QuickBite / other example |
|---|---|---|
| Workflow steps | One step of the journey | Place order vs track order vs rate order |
| Business rules | One rule variant | Free delivery over ₹499 vs always-paid delivery |
| Data types / variants | One product or channel | Card payment vs UPI vs cash |
| Happy vs exception | Core success first | Track live map vs "rider GPS lost" |
| Operations (CRUD) | One operation | Add address vs edit vs delete |
| SPARNE | **S**pikes, **P**aths, **A**ttributes, **R**ules, **N**egative cases, **E**xamples | Spike map vendor; path "picked up"; attribute ETA; rule 5-min refresh; negative restaurant delay; example peak-hour |
| Hamburger (thin slices) | Layers of the same flow, each demoable | Status list → SMS → live map (not "front end" then "back end") |

Hamburger (also called "elephant carpaccio" / thin vertical slices): do not split UI vs API. Split a thin end-to-end: "status text on order page" before "live map."

SPARNE is a prompt list, not a mandate to create six stories every time. Use it in refinement to find forgotten negatives.

### Story refinement / backlog grooming agenda (45–60 min)

1. Goal: next 1–2 sprints Ready, not the whole backlog.
2. Recap sprint goal and upcoming dates (release, campaign, audit).
3. Walk top 8–12 items: split, AC, open questions.
4. Confirm estimates only after split (re-estimate if the story changed).
5. Flag dependencies (legal, vendor, another team).
6. PO re-orders; BA captures parking lot.
7. Exit: items meeting DoR tagged Ready; owners for unanswered questions.

BA prep: draft splits, example data, known rules. BA is not there to read Jira titles aloud.

### Story prioritization vs requirement MoSCoW

| | MoSCoW (requirements) | Story prioritization (backlog) |
|---|---|---|
| Object | Need or rule | Deliverable slice |
| Labels | Must / Should / Could / Won't | Rank 1..n (and maybe WSJF, value, risk) |
| Time | Release or project | Next sprint and next increment |
| Trap | Everything is Must | Rank ignores dependency |

A Must-have requirement (e.g. "customer can see order status") may still be delivered as four stories ranked in sequence. MoSCoW answers "is this in the release?" Prioritization answers "what do we build first this sprint?"

## Real-world examples

1. **ShopEase:** Split "manage address book" by CRUD: add address first (checkout blocker), edit next, delete later.
2. **NovaBank:** Split "transfer" by happy path vs limit exceeded vs new beneficiary (exception and data type).

## Scenario / Use case: QuickBite "track order" epic

### Context

Marketing wants "live tracking like the big apps" in one sprint. The epic includes map, ETA, SMS, and restaurant delay. Unsplit, it will fail DoR.

### Stakeholders

Customer, rider, restaurant, support, PO, maps vendor, SMS vendor, BA, QA.

### BA actions

1. Identify walking skeleton: status text + timestamps (no map).
2. Apply hamburger: status → SMS → ETA → live map → delay notice.
3. Use SPARNE: negative "restaurant marked delay"; spike if map SLA unknown.
4. Rank by value: customers forgive no map if SMS and status are truthful.

### Sample artifact — split stories (priority order)

| Rank | Story | Split pattern | MoSCoW for release |
|---|---|---|---|
| 1 | See order status and timestamps on the order page | Workflow / hamburger | Must |
| 2 | Receive status SMS at placed / picked up / nearby | Channel variant | Must |
| 3 | See ETA range once a rider is assigned | Attribute | Should |
| 4 | See rider on a live map | Workflow enrichment | Should |
| 5 | See restaurant delay notice with new ETA | Exception / negative | Must if restaurants can pause |

Do not combine 4 and 5. Delay notice has value even if the map vendor slips.

### Failure if ignored

One "track order" story enters the sprint. Map SDK eats the sprint. No SMS, no status, no delay message. Customers call support: "Where is my food?" Support has the same blank screen.

## Weak vs strong

| Weak | Strong |
|---|---|
| Split by layer: API story, UI story | Thin vertical: status page that hits real events |
| Refinement = estimate poker only | Split, AC, dependencies, then estimate |
| MoSCoW = sprint order | MoSCoW for release; rank for sequence |
| SPARNE as six mandatory tickets | SPARNE as a discovery checklist |

## Notes

- If the story still has "and" between user jobs, split it.
- Happy path first is valid; do not ship only happy path forever — schedule the exception.
- CRUD: create often has more value than delete; do not auto-split into four equals.
- Refinement without a PO is a reading club; refinement without a BA is guesswork.
- Prioritize dependencies before "nice map."
