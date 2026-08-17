# Elicitation Techniques

A technique is a **tool**, not a personality. Use more than one. Interviews alone create confident fiction.

## Why it matters for a BA

NovaBank credit managers will each swear a personal loan takes “about 2 days.” Observation and documents will show 6 days. The BA who only interviews will write the wrong SLA, and UAT will fail.

## How to read this file

For each technique: **when**, **how**, **example**, **pitfall**. Then a comparison table and a full scenario.

### Interviews

- **When:** Deep individual knowledge; sensitive topics (fraud, salary, clinical errors); powerful stakeholders who will not talk in a group.
- **How:** Prepare a guide; 45–60 min; start with their process; ask for a recent real case; end with “what would break if we changed this?”
- **Example:** MediCare+ interview with a senior surgeon about why slots are blocked verbally.
- **Pitfall:** Treating one interview as truth. People describe the ideal, not Tuesday afternoon.

### Stakeholder meetings

- **When:** Status, alignment, decisions among people who already share context. Not for inventing requirements from scratch.
- **How:** Agenda, decisions needed, pre-read. BA records decisions and open questions, not a novel.
- **Example:** ShieldSure weekly claims-IT meeting to confirm pre-auth fields.
- **Pitfall:** Calling a status meeting a “requirements workshop.” No elicitation happens.

### Workshops

- **When:** Cross-functional process, conflicts, end-to-end flow (loan origination, returns, claims).
- **How:** Facilitated, timeboxed, visible notes, parking lot, one process on the wall. Right people in the room (decision maker + doers).
- **Example:** ShopEase returns workshop: buyer ops, seller ops, warehouse, finance.
- **Pitfall:** Too many people; design arguments; no decision owner.

### Brainstorming

- **When:** Early ideas, alternative solutions, risk lists. After the problem is at least sketched.
- **How:** Diverge (no criticism) then converge (vote, cluster). Separate idea generation from evaluation.
- **Example:** QuickBite ideas to cut restaurant accept time (tablet alarms, auto-reject, call).
- **Pitfall:** Brainstorming as a substitute for analysis of current data.

### Surveys

- **When:** Many users, geographic spread, quantitative pulse (satisfaction, feature use).
- **How:** Short, one topic, closed questions + one optional comment. Sample, not “email the company.”
- **Example:** ShopEase survey of 2,000 buyers: why they abandoned return requests.
- **Pitfall:** Biased sample; leading questions; treating 12 responses as statistics.

### Questionnaires

- **When:** Structured information from SMEs who cannot meet (branch managers, clinic admins). More formal than a marketing survey.
- **How:** Numbered questions tied to process steps; definitions of terms; deadline; BA follows up on outliers.
- **Example:** NovaBank questionnaire to 40 branches: steps and time for gold loan disbursal.
- **Pitfall:** Ambiguous questions produce unusable answers. No follow-up interview on odd replies.

### Observation (job shadowing)

- **When:** Workarounds, actual times, UI pain, “we don’t know why it’s slow.”
- **How:** Watch silently first; ask after a cycle; note tools (Excel, WhatsApp). Get consent. Do not “help.”
- **Example:** Sit with NovaBank credit ops while a file moves from login to sanction.
- **Pitfall:** Hawthorne effect (people perform for you). Observe more than one person and one day.

### Document analysis

- **When:** Policies, contracts, SOPs, regulations, old BRDs, training manuals exist.
- **How:** Extract rules, roles, exceptions, dates. Mark contradictions. Version the source.
- **Example:** ShopEase seller MSA vs category return policy (innerwear window).
- **Pitfall:** Trusting an SOP that nobody follows. Always pair with observation or data.

### Existing-system analysis

- **When:** Replacement or enhancement of a live system. “As-is” is in the product, not in people’s heads.
- **How:** Click every state; list fields, validations, reports, integrations, batch jobs; talk to the maintainer.
- **Example:** MediCare+ current appointment Excel + EMR screens before building booking.
- **Pitfall:** Rebuilding every old field “because it exists,” including unused ones.

### Focus groups

- **When:** Attitudes and language of a user class (patients, riders, savings customers). Not for process detail.
- **How:** 6–10 people, moderator, one theme, record themes not votes as facts.
- **Example:** QuickBite customer group on what “late” means to them vs the app timer.
- **Pitfall:** Loudest person dominates; treating opinions as requirements.

### Prototyping

- **When:** UI-heavy flows, to validate understanding, not to freeze design on day one.
- **How:** Low-fi first; bind prototype screens to requirement IDs; tell users it is disposable.
- **Example:** ShopEase clickable return flow to confirm reason codes with support.
- **Pitfall:** Stakeholders approve the colour and think requirements are done. Prototype ≠ specification.

### Reverse engineering

- **When:** No documentation, vendor black box, legacy code or reports are the only source of rules.
- **How:** With a developer, extract calculations and decision tables from code/reports; confirm with business.
- **Example:** ShieldSure premium calculation buried in a 12-year-old batch job.
- **Pitfall:** Encoding bugs as “the official rule.” Confirm intent with the rule owner.

### Data analysis

- **When:** Volumes, exception rates, cycle times, where the process actually fails.
- **How:** Define the question first; privacy rules; sample vs census; show distributions not only averages.
- **Example:** QuickBite restaurant accept-time distribution; NovaBank FOIR vs default rate.
- **Pitfall:** P-hacking a metric to support a pre-chosen solution.

## Comparison table

| Technique | Best for | Time cost | Typical output | Pair with |
|---|---|---|---|---|
| Interviews | Depth, politics, exceptions | Medium | Quotes, rules, pain | Observation, documents |
| Stakeholder meetings | Decisions, alignment | Low–medium | Decision log | Workshop notes |
| Workshops | End-to-end + conflict | High | Process + prioritized reqs | Data, prototypes |
| Brainstorming | Options, risks | Low | Idea list | Later analysis |
| Surveys | Scale, trends | Medium | Charts, % | Interviews on outliers |
| Questionnaires | Structured SME facts | Medium | Tabulated answers | Follow-up calls |
| Observation | As-is truth, times | High | Timed process, workarounds | Interviews after |
| Document analysis | Policy, compliance | Medium | Rule extract | Existing-system |
| Existing-system analysis | As-is system behaviour | High | Screen/field inventory | Data, reverse eng. |
| Focus groups | Language, attitudes | Medium | Themes | Surveys |
| Prototyping | UI validation | Medium–high | Feedback on flow | Written FRs |
| Reverse engineering | Hidden logic | High | Decision tables | Rule owner validation |
| Data analysis | Evidence, volume | Medium | Facts that kill myths | Workshop |

## Weak vs strong technique mix

| Weak | Strong |
|---|---|
| Five interviews, write FRD | Interview + observe + read SOP + sample files, then workshop the conflicts |
| Survey only | Survey to find themes, interview to understand them |
| Prototype first | Problem and rules first, then prototype |

## Scenario / Use case: NovaBank loan origination times

**Context.** Product wants a “2-day personal loan” campaign. Interviews with three credit managers: “files take 1–2 days.” Sales says “operations is slow.” Operations says “sales sends incomplete files.” The BA is asked to write an SLA requirement: sanction in 48 hours.

**Stakeholders.** Sales, credit managers, credit ops, compliance (KYC), underwriter, core-banking, customer, PO, QA.

**What the BA does.** Interviews alone are conflicting, so the BA adds techniques:

1. **Document analysis:** SOP says 48 hours *after complete file*. Completeness checklist exists but is not in the CRM.
2. **Observation:** Two days in credit ops. Average file sits 1.5 days waiting for salary slip page 2. “2 days” in interviews meant *their processing time*, not customer-experienced time.
3. **Data analysis:** Median customer-experienced time 6.1 days; 30% of files bounce at least once for documents.
4. **Workshop:** Sales + credit + compliance. Visible timeline on the wall. Decision: SLA clock starts at `file_complete = true`, not at application submit. New FR: CRM completeness gate. NFR: status SMS when documents are missing.

**Sample requirement.**

> **FR-LON-18** The origination clock for the 48-hour sanction SLA starts only when KYC = verified and the document checklist is complete. Incomplete files cannot be submitted to credit ops.

**What goes wrong if ignored.** Marketing publishes “loan in 2 days.” Customers complain. Ops is beaten on a metric they never owned. The BA’s “48-hour” FR is untestable because “start” was never defined.

## Notes

- 
