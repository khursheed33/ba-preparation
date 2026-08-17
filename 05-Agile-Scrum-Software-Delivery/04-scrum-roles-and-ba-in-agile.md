# Scrum Roles and the BA in Agile

## Definition

**Scrum roles:**

- **Product Owner (PO):** maximizes product value; owns the product backlog order and acceptance of increment.
- **Scrum Master (SM):** coaches the framework, removes impediments, protects the team from process abuse.
- **Development Team (Developers):** cross-functional people who build, test, and deliver the increment (includes QA, designers, etc.).

**BA role in Agile:** elicit, analyze, split, write AC, model process/data, support UAT, keep rules current. Scrum does not name a BA; organizations add one to support the PO and team.

## Why it matters

If the BA becomes a **proxy PO** without mandate, the real PO only appears at review and the backlog has no business owner. If the BA only types what the PO dictates, analysis quality dies. Clear RACI prevents both.

## Concepts

### BA vs PO overlap and RACI

| Activity | PO | BA | Devs | SM |
|---|---|---|---|---|
| Product vision / value bet | **A/R** | C | C | C |
| Backlog order | **A/R** | C | I | I |
| Story split, AC, examples | C | **R** | C | I |
| Accept story (business) | **A/R** | C | I | I |
| Technical tasks | I | I | **A/R** | I |
| Facilitation of Scrum events | C | C | C | **A/R** |
| Stakeholder workshops | A | **R** | C | C |
| UAT scenarios | A | **R** | C | I |

R = Responsible, A = Accountable, C = Consulted, I = Informed. Customize, but **do not** make BA Accountable for value if they cannot say no to stakeholders.

### How BA supports PO without becoming a proxy PO

Unless the org **designs** BA-as-PO (some firms do):

- BA drafts stories; PO **orders and accepts**.
- BA brings options and trade-offs; PO chooses the bet.
- BA can facilitate refinement; PO must be in the room for priority calls.
- BA does not privately promise scope to a director.
- BA escalates when PO is absent — does not silently become PO.

Proxy PO symptoms: PO at review only; BA "owns" Jira rank; stakeholders lobby the BA for features; sprint review has no business decisions.

## Real-world examples

1. **QuickBite:** PO owns "reduce cancelled orders"; BA splits restaurant-delay stories and AC; PO ranks map vs SMS.
2. **ShieldSure:** PO owns claims cycle time; BA models verification bottleneck; PO still accepts the slice.

## Scenario / Use case: BA writes all stories, PO only attends sprint review

### Context

MediCare+ patient-app PO is a busy clinic director. BA writes every story, ranks the board, and answers Slack all sprint. PO arrives at review, is surprised by cancellation-window behavior, and rejects the increment. Team is demoralized. SM calls it "Agile."

### Stakeholders

PO (clinic director), BA, SM, developers, QA, clinic ops, patients (via research).

### BA actions (anti-pattern and fix)

**Anti-pattern:** BA = shadow PO. Rank without PO. Accept "Done" without PO. Filter stakeholder requests alone.

**Fix:**

1. Agree RACI with PO and SM in writing.
2. PO office hours twice a week (20 min) for rank and accept.
3. Refinement: PO present for the top 8 items; BA may pre-draft.
4. Sprint review: PO speaks to value; BA supports with AC walkthrough, not a substitute decision.
5. If PO cannot do this, **org design choice:** appoint a delegate PO with authority — do not leave the BA unofficially accountable.

### Sample artifact

RACI table (above) + calendar: "PO rank session Tue/Thu" + rule: no sprint commitment on items the PO has not seen.

### Failure if ignored

UAT/review rejection. Stakeholders treat BA as product. PO is unaccountable. BA burnout. Increment does not match clinical policy.

## Weak vs strong

| Weak | Strong |
|---|---|
| BA proxy PO by accident | Named PO (or named delegate) with authority |
| PO "vision only," never backlog | PO orders; BA analyses |
| SM writing AC | SM coaching; BA/PO/team writing AC |
| Developers excluded from refinement | Three amigos on complex stories |

## Notes

- Scrum Accountable for value is the PO; analysis quality is the BA's craft.
- If you are the PO, say so on the org chart; do not hide it.
- SM is not a BA and not a project manager of tasks.
- Development Team includes testers; BA should not be the only person who understands AC.
- RACI is a conversation starter; revisit when the anti-pattern returns.
