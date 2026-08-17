# Agile vs Waterfall

## Definition

**Waterfall** delivers in sequential phases: requirements freeze, then design, then build, then test, then release. **Agile** delivers in short cycles with evolving requirements and frequent feedback. Most organizations run a **hybrid**: stage-gates or vendor contracts in Waterfall, product teams in Scrum.

## Why it matters

A BA who only knows one model will fight the organization. Banks, government, and packaged vendors often still need signed scope. Digital channels may still run Scrum. The BA's job is to keep requirements traceable across both clocks.

## Concepts

### Side-by-side

| Area | Waterfall | Agile (Scrum-like) |
|---|---|---|
| **Planning** | Big plan up front; baseline dates for the whole project | Roadmap + sprint goals; plan the next increment in detail |
| **Requirements** | BRD/FRD signed before build; change control board | Backlog; refinement; AC just in time; change = re-order |
| **Change** | Formal CR; cost/time/scope trade | Expected; PO re-prioritizes; mid-sprint change is costly |
| **Testing** | Test phase after build; UAT at the end | Test each story; UAT each increment; regression continuous |
| **BA role** | Heavy elicitation early; then clarification and UAT | Continuous discovery, refinement, AC, review, UAT slices |

### When Waterfall still appears

- **Banks (NovaBank):** core ledger, payments switches, regulatory releases with fixed windows.
- **Vendors:** package implementation (core banking, policy admin) sold as phases: discover, configure, test, go-live.
- **Government:** tender, signed SOW, acceptance criteria as contract exhibits.
- **Hardware / safety:** change is expensive; documentation is the control.

Waterfall is not "wrong" there. Risk is treating a 200-page spec as finished learning.

### Hybrid reality

Common pattern: **program Waterfall, team Agile.**

- Phase gate: "UAT start date" on a Gantt chart.
- Inside the phase: Scrum sprints producing increments toward that gate.
- BA writes a lightweight BRD/scope for the gate **and** stories for sprints.
- Traceability: epic → vendor requirement ID → story → test.

Hybrid fails when the Gantt assumes all requirements were known at kickoff *and* the Scrum team is forbidden to change anything.

## Real-world examples

1. **ShieldSure:** policy admin vendor waterfall; customer app Scrum. Claims status must match vendor batch cycles.
2. **MediCare+:** hospital EMR vendor waterfall; patient app Agile. Appointment slots depend on EMR interface freeze dates.

## Scenario / Use case: NovaBank core vendor Waterfall + digital channel Scrum

### Context

Core banking vendor runs a 9-month waterfall: design freeze month 3, SIT month 7, UAT month 8. Digital channel (app) runs two-week sprints. Product wants in-app beneficiary transfer **before** core UAT. Core APIs are still "draft."

### Stakeholders

Core program PM, vendor BA, digital PO, digital BA, compliance, QA (both), operations.

### BA actions

1. Map dependencies: which transfer stories need **stable** core postings vs which can mock.
2. Agree a **contract of interfaces** (fields, error codes) as the hybrid artifact — not a full dual BRD.
3. Split digital backlog: UI + OTP now; posting to core when vendor drop is available.
4. Attend vendor change board with impact on sprint forecast.
5. Keep one trace matrix: vendor req → digital story → test.

### Sample artifact

| Vendor waterfall milestone | Digital Scrum implication | BA artifact |
|---|---|---|
| Design freeze | Stop assuming new posting codes | Interface list v1.0 |
| Core SIT drop | Integration stories become Ready | AC for error codes |
| Core UAT | Joint UAT scenarios | End-to-end scripts |
| Core CR after freeze | Digital may need a spike + restack | Impact note |

### Failure if ignored

Digital team "Agiles" a transfer UI that posts with the wrong narrative codes. Core UAT fails. Vendor says "not in design freeze." Digital says "you should have been Agile." Customer gets neither.

## Weak vs strong

| Weak | Strong |
|---|---|
| Agile vs Waterfall as religion | Fit the constraint (vendor, regulator, risk) |
| Hybrid = Scrum with a hidden BRD nobody traces | Explicit gates + living backlog + trace |
| BA disappears after Waterfall sign-off | BA stays through test and change |
| Scrum team ignores vendor freeze | Interface contract and mocked slices |

## Notes

- Ask "what is allowed to change after freeze?" That defines the BA's change path.
- UAT in Waterfall is late; in hybrid, run incremental UAT on digital while core is still in SIT.
- Do not copy 400 vendor requirements into 400 stories blindly — group by user outcomes.
- Planning in Agile is real; it is just rolling wave, not absent.
- The BA is often the translator between the two calendars.
