# Confluence for Business Analysts

## Definition

Confluence is a wiki for **team knowledge**. A **space** is a project or domain site. **Pages** hold requirements, meeting notes, decisions, and how-to knowledge. **Templates** make those pages consistent. **Collaboration** is comments, @mentions, and version history — not editing in silence and emailing PDFs.

Jira tracks work items. Confluence explains the *why*, the process, and the signed decision behind those items.

## Why it matters

People leave. Slack scrolls away. If MediCare+ onboarding lives only in a BA's head, every new joiner costs two weeks of "who knows how appointments work?"

## Recommended space tree for a BA project

Example space: `MediCare+ Appointments`

```text
Home (purpose, contacts, links to Jira board)
├── 01 Discovery
│   ├── Problem statement
│   ├── Stakeholder map
│   └── Research notes
├── 02 Requirements
│   ├── BRD / product outline
│   ├── Process (As-Is / To-Be)
│   ├── Story specs (or index of Jira epics)
│   └── Data dictionary
├── 03 Decisions
│   └── Decision log (one page, table, or child pages)
├── 04 Meetings
│   └── Dated notes (YYYY-MM-DD topic)
├── 05 UAT & Release
│   ├── UAT plan / scripts
│   └── Release notes (business)
└── 06 Knowledge base
    ├── How appointments are booked (ops)
    └── FAQ / known limitations
```

Keep **one space per product** (or per programme). Do not create a new space per meeting.

## Page organization rules

| Rule | Practice |
|---|---|
| Names | `YYYY-MM-DD UAT readout` not `Notes final 2` |
| One topic | Split "process + stories + UAT" into three pages |
| Status | Label `draft` / `approved` or a status macro |
| Owner | Page owner in the header |
| Archive | Move dead pages to `99 Archive`; do not delete history |

## Page templates

**Story spec** (when the story is too rich for Jira description):

- Jira key (smart link)
- User / job to be done
- Scope in / out
- Business rules
- Acceptance criteria
- Data fields and validations
- Errors and empty states
- Open questions

**Process page:**

- Purpose and trigger
- Actors
- As-Is steps (numbered)
- To-Be steps
- Exceptions
- Systems touched
- Diagram (exported image + source file link)

**Decision log row / page (ADR-lite):**

- Date, decision owner
- Context
- Options considered
- Decision
- Consequences
- Linked Jira keys

**Meeting notes:**

- Date, attendees, absentees
- Agenda
- Decisions (copy to decision log)
- Actions with owner and date
- Parking lot

## Linking Jira issues on Confluence pages

Use **Jira issue/filter macros** or paste the issue URL so it renders as a smart link (`MC-102`).

| Link type | Use |
|---|---|
| Single issue | Story spec header |
| Filter macro | "Open UAT defects for this epic" live table |
| Epic link | Requirements index |

When AC changes, update Jira first, then one line on Confluence: "AC source of truth: MC-102". Do not maintain two conflicting AC lists.

## Collaboration

- @mention the SME on the paragraph they must confirm.
- Resolve comments when the page is updated; do not leave 40 open threads.
- Restrict legal pages; do not lock the whole space.
- Watch the space if you own it; unwatch noise.

## Real-world examples

1. **ShopEase** returns: process page + story spec index. Warehouse trainers use Confluence, not the BA's laptop.
2. **NovaBank** KYC: decision log records "liveness vendor = Vendor A until FY27". Audit asks "why this vendor?" — the page is the answer.

## Scenario / Use case

MediCare+ hires a new BA on a Monday. Old pattern: 11 Slack channels, three "final" BRDs in email, and a process that only the ops lead remembers.

New pattern: space home says "start here". She reads Discovery → problem statement, Requirements → To-Be booking process, Decision log → "double-book prevention = lock slot for 90 seconds", and Knowledge base → how call-centre books for elderly patients. Jira filter macro on the epic page shows current stories. By Wednesday she can run a refinement without asking "what is UHID?"

Cost of the space: the previous BA spent 2 hours a week keeping pages current. Cost of not having it: 10 days of shadowing and two missed rules in UAT.

## Weak vs strong

| Weak | Strong |
|---|---|
| 12 untitled "Meeting notes" | Dated template with actions |
| BRD PDF emailed once | Living requirements + Jira links |
| Decisions in chat | Decision log with owner and date |
| AC on Confluence *and* Jira, different | Jira AC; Confluence context |
| Space dump of 400 pages | Tree + archive + labels |
| New joiner pings 8 people | Home page path in 30 minutes |

## Notes

- Confluence is for understanding; Jira is for tracking. Duplicate AC at your peril.
- Put sample data on pages; never real patient names, account numbers, or OTPs.
- A knowledge base page is written for the next stranger, not for you.
- If a meeting produces no decision and no action, you still record "no decision — waiting on legal".
- Templates only help if you actually use them; pin them on the space home.
- Link Draw.io/Lucid sources, not only a screenshot that nobody can edit.
- Review the space at release: archive superseded As-Is so people do not implement the old process.
