# Elicitation, Gathering, and Discovery

People say “gather requirements” as if they were fruit on a tree. Real BA work is three related activities: **elicitation**, **gathering**, and **discovery**. They overlap. They are not identical.

## Why it matters for a BA

If you only *gather* what stakeholders volunteer, you will automate their current workarounds. If you only *elicit* answers to your script, you will miss the problem they cannot name. If you skip *discovery*, QuickBite will pay late-delivery compensation forever while restaurants sit on the accept button.

## The three terms

| Term | Meaning | BA posture | Risk if used alone |
|---|---|---|---|
| Gathering | Collecting already-stated needs, documents, tickets, metrics | Receiver / compiler | You copy noise and duplicate wish lists |
| Elicitation | Actively drawing out information that is not sitting in a folder | Facilitator / questioner | You get polished opinions, not observed facts |
| Discovery | Finding the real problem, hidden process, and unknown constraints | Investigator | You may delay delivery if you never time-box it |

**Gathering** answers: what is already written or said?
**Elicitation** answers: what do people know that is not written?
**Discovery** answers: what is actually true, and what is the problem behind the request?

NovaBank example: gathering = read the existing “loan SOP.” Elicitation = interview credit managers about exceptions they never wrote down. Discovery = sit with a file and see that 30% of “policy rejects” are missing salary slips, not FOIR.

MediCare+ example: gathering = clinic brochure of “online booking.” Elicitation = ask reception why they still use Excel. Discovery = doctors block slots verbally in the corridor; Excel is not the real calendar.

## Preparation, session, follow-up

Every elicitation event has three parts. Skipping any one wastes the other two.

### Preparation

- Purpose: one sentence (“understand why late-delivery compensation is rising”).
- Scope: what we will and will not cover.
- People: who must be in the room vs who we interview separately (power dynamics).
- Inputs: tickets, process maps, sample orders, policies, system screenshots.
- Questions: open first, closed later; avoid leading (“You want GPS, right?”).
- Logistics: time, tools, recording consent, parking lot template.
- Success test: what artifacts we need by the end (list of causes, current process, rules).

### Session

- Recap purpose and timebox.
- Separate facts, opinions, and ideas (three columns).
- Listen for workarounds (“we usually WhatsApp the rider”).
- Capture exact examples: order IDs, timestamps, amounts.
- Do not design the solution in the first 20 minutes unless the session is a design workshop.
- End with: decisions, open questions, owners, dates.

### Follow-up

- Same-day notes (see documentation phase).
- Confirm quotes with SMEs (“did I hear FOIR threshold as 50% or 55%?”).
- Trace each statement to a source.
- Convert notes into requirements, rules, and questions — not a transcript dump.
- Book the gap sessions (legal, data, vendor) instead of guessing.

**Weak:** show up, ask “what do you want?”, type a story.
**Strong:** read 50 compensation tickets, map the process, then elicit with evidence on the table.

## Sources of requirements

Never use only users. Users describe symptoms.

| Source | What you get | Example |
|---|---|---|
| Users | Tasks, pain, workarounds | QuickBite customer: “I waited 70 minutes.” |
| Systems | Actual behaviour, data fields, errors | Order events: `restaurant_accepted_at` vs `rider_assigned_at` |
| Documents | Policy, contracts, SOPs, old BRDs | Compensation SOP v1.4: 30% off coupon if > 45 min |
| Data | Volumes, exceptions, true cycle times | 61% of compensated orders had restaurant accept > 8 min |
| Regulations | Non-negotiable constraints | NovaBank: RBI authentication; MediCare+: patient consent for SMS |

ShieldSure: users say “claims are slow.” Documents say TAT is 7 days. Data says 7-day median but 22-day tail for missing discharge summary. Regulation says cashless needs pre-auth. The requirement is not “make claims faster”; it is “capture discharge summary at admission and block submit until attached.”

## Combining the three in practice

1. Gather: tickets, SOP, last quarter metrics.
2. Discover: observe or query where time is spent.
3. Elicit: take the finding back to stakeholders — “the data says X; is that acceptable?”
4. Gather again: the new policy they write after they see X.

## Scenario / Use case: QuickBite late-delivery compensation

**Context.** QuickBite product owner: “Customers are angry about late food. We need better rider GPS so we can compensate fairly.” Compensation cost is up 18% quarter-on-quarter. Riders say GPS already works. Restaurants say riders arrive late to pickup.

**Stakeholders.** Hungry customers, riders, restaurant partners, support agents, logistics, finance (compensation budget), product (delivery experience), data analyst, BA.

**What the BA does.**

*Preparation.* Pull 500 compensated orders. Columns: promised time, restaurant accept time, ready time, pickup, drop, GPS pings, compensation reason code. Read SOP. Book a kitchen observation at two restaurants and a rider ride-along.

*Discovery (not GPS).* 61% of compensated orders: restaurant `accepted_at` minus `placed_at` > 8 minutes. Kitchen ready time after accept is normal. Rider GPS shows the rider reached pickup on time and waited. Support reason code is almost always “rider delay” because the form default is that value.

*Elicitation session.* Workshop with ops and restaurants. Fact: some restaurants accept immediately then cook late; others ignore the tablet. Opinion: “riders are lazy.” Data kills the opinion for this slice.

*Gathering.* Existing SOP never defined “late” relative to restaurant accept. It used promised customer time only.

**Sample requirement / artifact.**

| ID | Statement |
|---|---|
| BR-DLV-04 | Compensation is paid only when delay is attributable to QuickBite logistics, not restaurant accept/cook delay. |
| BRULE-DLV-12 | If `restaurant_accepted_at − placed_at` > 8 minutes, cause = RESTAURANT; no rider penalty; customer still informed. |
| FR-DLV-22 | Support form default reason must not be RIDER_DELAY; reason is suggested from event timestamps. |
| FR-DLV-23 | Customer compensation decision uses promised time; cost allocation uses delay cause. |

**What goes wrong if ignored.** Engineering spends a quarter on GPS replay maps. Compensation keeps rising. Riders churn because they are penalised for kitchen delay. Restaurants never see a tablet SLA. The PO still thinks the need was “better GPS.”

## Practical rule

If a stakeholder brings a solution (“we need GPS”), write it as a **proposed solution**, then elicit the **need**, then discover **evidence**. Gathering without discovery is how BA work becomes stenography.

## Notes

- 
