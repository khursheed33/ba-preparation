# Jira Filters, Dashboards, and JQL

## Definition

A **filter** is a saved search. **JQL** (Jira Query Language) is how you write that search. A **dashboard** is a page of gadgets (widgets) fed by filters. **Sprint management** is protecting the sprint goal. **Backlog management** is ranking and slicing work so the next sprint is Ready.

A BA who can query Jira does not answer "how's UAT?" from memory.

## Why it matters

POs, ops, and release managers will ask for counts and blockers in standups and steering. Memory is biased toward the last Slack ping. Filters and dashboards are repeatable evidence.

## Backlog and sprint management (BA view)

| Activity | BA does | BA does not |
|---|---|---|
| Rank backlog | Advise on value, risk, dependency | Override PO rank silently |
| Split stories | Cut along user outcomes | Split by technical layer only |
| Sprint planning | Confirm Ready; flag risks | Force extra stories "just in case" |
| Mid-sprint | Log scope change as a new issue | Quietly expand AC of a committed story |
| Sprint review | Map demo to AC | Hide failed UAT items |

If ShopEase marketing adds "gift wrap" mid-sprint, create a new story. Do not hide it inside checkout AC.

## Eight useful JQL examples

Replace project keys (`NB`, `SE`) and your accountId as needed. Save each as a shared filter.

**1. My open stories**

```
project = NB AND issuetype = Story AND assignee = currentUser() AND statusCategory != Done ORDER BY priority DESC
```

**2. Bugs without acceptance criteria** (empty AC field or description)

```
project = SE AND issuetype = Bug AND (description is EMPTY OR description ~ "TBD") AND statusCategory != Done
```

If you use a custom field `Acceptance Criteria`:

```
project = SE AND issuetype = Story AND "Acceptance Criteria" is EMPTY AND status != Done
```

**3. UAT failed (label or status)**

```
project = NB AND (status = "UAT" OR labels = uat-fail) AND resolution is EMPTY
```

**4. Epics without children**

```
project = SE AND issuetype = Epic AND issueFunction not in hasLinkType("is Epic of")
```

If `issueFunction` is unavailable (no ScriptRunner), use a board swimlane by epic and scan empty ones, or:

```
project = SE AND issuetype = Epic AND statusCategory != Done
```

…then check the epic panel. Flag empty epics in refinement.

**5. Blocked items in the current sprint**

```
sprint in openSprints() AND (status = Blocked OR labels = blocked) AND project = NB
```

**6. Stories Ready but unassigned before planning**

```
project = QB AND status = Ready AND assignee is EMPTY AND issuetype = Story
```

**7. Sev1/Highest bugs older than 2 days**

```
project = MC AND issuetype = Bug AND priority = Highest AND created <= -2d AND statusCategory != Done
```

**8. What is blocking go-live?** (release version + unresolved blockers)

```
project = NB AND fixVersion = "Cards-GoLive-Sep" AND statusCategory != Done AND (priority in (Highest, High) OR labels in (go-live-blocker, blocked, uat-fail)) ORDER BY priority ASC, updated ASC
```

Bonus hygiene:

```
project = SE AND issuetype = Story AND status = Done AND "Acceptance Criteria" is EMPTY
```

Done without AC means you cannot defend the behaviour later.

## BA dashboard widgets

Build a personal dashboard **BA — Delivery Health** with these gadgets, each pointed at a saved filter:

| Widget | Filter / gadget | Decision it supports |
|---|---|---|
| Filter Results | Go-live blockers | What to escalate today |
| Pie chart | Issues by status (current sprint) | Is work stuck in Analysis or QA? |
| Two-dimensional | Component × priority | Which module is risky |
| Created vs resolved | Last 14 days, bugs | Quality trend |
| Assigned to me | Open issues | Your queue |
| Sprint burndown | Scrum gadget | Are we burning scope or hiding it? |
| Activity stream | Project | Comments you missed |
| Filter count | UAT failed | Whether demo is honest |

Share the dashboard with the PO. Do not keep a private "real" list.

## Real-world examples

1. **QuickBite** BA saves `late-partner-onboarding` JQL (`component = Onboarding AND status != Done AND created <= -7d`) and reviews it every Monday with Ops.
2. **ShieldSure** claims dashboard: pie of `component = Claims` by status. Legal sees `blocked-legal` count without opening 200 tickets.

## Scenario / Use case

NovaBank PO asks in the war-room: "What is blocking go-live?" The BA does not recite Slack. She opens dashboard **NB Cards Go-Live**.

Filter 8 returns 6 issues:

| Key | Summary | Why it blocks |
|---|---|---|
| NB-441 | UAT fail: OTP not sent on limit change | Label `uat-fail` |
| NB-418 | Highest bug: duplicate card control | Age 4 days |
| NB-402 | Blocked: vendor SMS template | Status Blocked |
| NB-390 | High: T&C PDF not in app | Compliance |
| NB-455 | Story still in Analysis: dispute SLA | Not Ready |
| NB-460 | Epic "Chargeback phase 2" empty | Out of go-live; PO descope |

The BA says: "Four true blockers, one unready story, one epic to cut from this version." The PO descopes NB-460, legal is pinged with NB-390, Dev takes NB-418. Go-live risk is now a list, not a feeling.

## Weak vs strong

| Weak | Strong |
|---|---|
| "I think UAT is fine" | Filter: UAT + uat-fail = 3 open |
| JQL only on your machine | Shared filters + dashboard |
| Backlog of 400 unranked items | Weekly rank of top 20 Ready |
| Sprint stuffed from memory | Planning from Ready filter |
| One-off Excel export | Repeatable gadget the PO can open |

## Notes

- Learn `statusCategory` (To Do / In Progress / Done) so renamed statuses still work.
- `currentUser()` beats hard-coded names when people change.
- Ask admin which custom fields store AC and severity; JQL uses those names.
- Empty epic JQL varies by Jira Cloud vs Data Center plugins — always test.
- Backlog management is saying no: duplicate, out of scope, or too big.
- Never promise go-live from a burndown alone; pair it with blocker JQL.
- Re-run go-live JQL the morning of release; comments overnight change the list.
