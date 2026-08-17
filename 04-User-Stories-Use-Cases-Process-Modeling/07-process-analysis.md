# Process Analysis

## Definition

A **business process** is a repeatable set of activities that turns inputs into an outcome for a customer or stakeholder (e.g. settle an insurance claim).

**Process mapping** draws the steps, actors, and handoffs. **Process analysis** studies the map to find delay, rework, risk, and waste. **Process optimization / improvement** changes the design so the outcome is faster, cheaper, safer, or more accurate — without breaking controls.

## Why it matters

Software that automates a bad process makes the mess faster. BAs map work *before* writing stories so the system supports the real path, including exceptions. ShieldSure's four-day document wait is not "an IT ticket"; it is a process problem with a tech slice.

## Concepts

| Term | BA meaning |
|---|---|
| **Bottleneck** | Step whose capacity limits the whole flow (queue grows here) |
| **Inefficiency** | Extra work, rework, waiting, or motion that does not add value |
| **Dependencies** | What this step needs from people, systems, or prior steps |
| **Exceptions** | Paths that leave the standard flow (missing docs, fraud flag) |
| **Process validation** | Check the map against reality (observe, sample cases, metrics) |

### SIPOC lite

SIPOC = Suppliers, Inputs, Process, Outputs, Customers. Lite version for a BA workshop (one page):

| SIPOC | ShieldSure claims (lite) |
|---|---|
| **Suppliers** | Customer, hospital, workshop, broker, internal medical team |
| **Inputs** | Claim form, photos, bills, policy data, FNOL number |
| **Process** | FNOL → register → **verify documents** → assess → decide → pay |
| **Outputs** | Decision letter, payment, audit trail, customer SMS |
| **Customers** | Policyholder, finance, regulator (evidence) |

Use SIPOC to bound the process before drawing 40 boxes.

### Mapping, analysis, optimization (sequence)

1. Map As-Is (what really happens, not the SOP PDF).
2. Validate with volumes, wait times, and a few real cases.
3. Mark bottlenecks, loops, and unclear owners.
4. Design To-Be (people + rules + system).
5. Improve in slices; do not "optimize" by adding a screen that still waits on a person.

## Real-world examples

1. **QuickBite:** Restaurant "mark ready" delay is a bottleneck; riders wait; ETA lies. Process fix: SLA + auto-nudge, not only a prettier map.
2. **NovaBank:** Loan file ping-pongs between RM and credit for missing documents — inefficiency from unclear checklist, not from "slow credit officers" alone.

## Scenario / Use case: ShieldSure claims — document verification bottleneck

### Context

Average time to first decision is 9 days. Operations says "system is slow." Sampling shows **document verification wait is 4 days**. Adjusters sit idle, then batch-review. Customers send photos on WhatsApp that never reach the case file.

### Stakeholders

Policyholder, claims adjuster, document-verification team, medical reviewer, finance, IT, BA, PO, compliance.

### BA actions

1. SIPOC lite in a 45-minute workshop; agree start (FNOL) and end (payment or reject).
2. Map As-Is with wait times on arrows, not only boxes.
3. Validate: 30-case sample — % missing docs, % WhatsApp-only, % rework loops.
4. Name bottleneck: verification queue + unstructured intake.
5. To-Be slice: customer upload portal with a required-doc checklist; verification SLA 1 business day; exception path for medical review.

### Sample artifact

| Step | Actor | Wait / work | Issue |
|---|---|---|---|
| FNOL | Customer / call center | 20 min work | OK |
| Register claim | Ops | 2 hours | OK |
| Collect documents | Customer | 1–5 days | WhatsApp side channel |
| **Verify documents** | Doc team | **4 days wait** | Queue, unclear complete pack |
| Assess | Adjuster | 1 day | Idle then burst |
| Decide and pay | Adjuster / finance | 1 day | Depends on verify |

Metrics to validate improvement: time in "docs incomplete," % first-time-complete packs, verification cycle time (target < 1 day).

### Failure if ignored

A portal is built that still emails the doc team a ZIP. Queue stays 4 days. Leadership blames "the new system." Root issue was intake completeness and queue design, not the claims screen theme.

## Weak vs strong

| Weak | Strong |
|---|---|
| Map the SOP as if it were truth | Map observed work; validate with cases |
| "Optimize" = more fields | Remove wait, rework, and dual intake |
| Bottleneck = "people are slow" | Bottleneck = capacity + arrival + completeness |
| SIPOC as a poster | SIPOC as scope fence before mapping |
| Exceptions as footnotes | Exceptions as drawn paths with owners |

## Notes

- Process analysis is not only drawing; it is measuring wait vs work.
- Dependencies (medical report, police FIR) belong on the map or they become "random delay."
- Validation: if staff say "we never skip this" and the sample shows skips, believe the sample and investigate.
- Improvement without a To-Be owner fails; name who verifies completeness.
- Software is one lever; checklist and SLA are others.
- Named wastes and DMAIC: [Lean and Six Sigma basics](12-lean-six-sigma-basics.md).
- Watch BPMN: [Lucidchart BPMN 2.0](https://www.youtube.com/watch?v=BwkNceoybvA) and [BA Doctor process map](https://www.youtube.com/watch?v=BFeHAONDDtw).
