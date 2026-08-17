# Change and Continuous Discovery

## Definition

**Continuous requirements discovery** is ongoing learning about users, process, and risk while delivery continues — not a single "requirements phase."

**Change management in Agile** is how the team absorbs new evidence (market, incident, regulator) by restacking the backlog and, when needed, replanning the sprint — with visible impact.

**Stakeholder collaboration in Agile** is frequent, lightweight involvement (not a sign-off ceremony at the end).

## Why it matters

If discovery stops when sprint 1 starts, the backlog goes stale. If every mid-sprint idea is stuffed into the increment, nothing finishes. If stakeholders only appear at UAT, they reject work they never shaped. Dual-track and collaboration patterns keep learning and shipping in parallel.

## Concepts

### Discovery vs delivery (dual track)

| Track | Goal | BA work | Output |
|---|---|---|---|
| **Discovery** | Reduce uncertainty | Interviews, mapping, prototypes, spikes, metrics | Validated problems, thin stories, killed ideas |
| **Delivery** | Ship a Done increment | Ready AC, refinement, UAT support | Working software |

Same BA often works both tracks in one week: morning delivery questions, afternoon discovery on Next. Dual-track fails when discovery is only slide research with no path onto the backlog, or delivery has no time for learning.

### Handling a mid-sprint scope change

1. Capture the request; do not implement from Slack.
2. PO + team: does it threaten the **sprint goal**?
3. If no: park on product backlog; rank in refinement.
4. If yes (regulator, Sev-1, legal): PO **replans** — drop or shrink committed items; make the swap visible.
5. BA: impact analysis (stories affected, AC, tests, downstream teams).
6. Do not "just add it" and keep the old goal.

### Collaboration patterns

| Pattern | What it is | BA use |
|---|---|---|
| **Office hours** | Fixed drop-in for stakeholders | Clinic directors, ops, sellers — 30 min, twice a week |
| **Three amigos** | BA + Dev + QA on a story | Ambiguous rules, edge cases, test ideas before coding |
| Workshops | Time-boxed mapping | New epics |
| Review | Increment inspect | Not the first time stakeholders see the idea |

Three amigos prevent "BA wrote AC, QA disagrees, Dev built a third thing."

## Real-world examples

1. **ShopEase:** Discovery finds guest checkout abandonment; delivery already in flight on logged-in-only — restack Next, do not silently expand the sprint.
2. **MediCare+:** Three amigos on cancellation window before coding (avoids the UAT failure in AC notes).

## Scenario / Use case: ShieldSure regulator change mid-release

### Context

Two sprints from a claims-app release. Regulator issues a notice: **claim decision letters must show a specific appeal paragraph and a reference number format within 10 days of decision.** Current stories print a generic letter. Marketing still wants a "live claim map" feature in the same release.

### Stakeholders

PO, BA, compliance, claims ops, developers, QA, legal, regulator liaison, marketing.

### BA actions

1. **Impact analysis:** which stories, templates, data fields, and audit logs are affected; what is not (map feature).
2. Gap: people (letter owners), process (when number is generated), tech (template), data (reference format), policy (10-day rule).
3. Dual-track: discovery workshop same day with compliance (example letters); delivery team stops new map work if PO agrees.
4. **Backlog restack:** new Must stories — appeal paragraph, reference number, audit; map feature to Later.
5. Mid-sprint: if the current sprint goal was "map," PO cancels or swaps goal; BA rewrites AC; QA joins three amigos.
6. Communicate to marketing: release outcome changed; date may hold with a thinner increment.

### Sample artifact — impact + restack

| Item | Before | After regulator notice |
|---|---|---|
| Decision letter template | Generic | Appeal paragraph + reference id |
| Reference number | Optional internal id | Mandatory format per notice |
| Live claim map | Release Now | Later |
| Sprint goal | Map MVP | Compliant decision letter |
| Tests | Map pins | Letter content + 10-day clock |

### Failure if ignored

Map ships; letters fail audit; regulator penalty. Or the team "does both" and neither is Done. Stakeholders hear about the law at UAT. Discovery was not continuous — it was a surprise.

## Weak vs strong

| Weak | Strong |
|---|---|
| Discovery phase then freeze | Dual-track learning onto the backlog |
| Mid-sprint add with same goal | Replan, drop, visible trade-off |
| Stakeholders only at UAT | Office hours + review + three amigos |
| Change = update a BRD in silence | Impact analysis + restack + communication |

## Notes

- Continuous discovery is not endless research; time-box spikes.
- Collaboration without a PO decision-maker is a talk shop.
- Regulator and Sev-1 changes are valid sprint interrupters; feature envy is not.
- Three amigos on every tiny copy change is overhead — use it when AC are ambiguous.
- Write down the restack so marketing and ops see what moved to Later.
