# Scrum Ceremonies

## Definition

Scrum events (ceremonies):

- **Sprint planning:** choose a sprint goal and the Ready work that can achieve it.
- **Daily stand-up:** 15-minute inspect of progress toward the goal and impediments.
- **Sprint review:** inspect the increment with stakeholders; adapt the backlog.
- **Sprint retrospective:** inspect how the team worked; pick improvements.
- **Release planning:** (common add-on) align several sprints to a release date, marketing, or compliance window.

## Why it matters

Ceremonies fail when they become **status theater**: BA reads Jira, stand-up is a yesterday-today-blocked script to the SM, review is a slide deck of "we did analysis." The BA should bring **decisions, examples, and impediments that block value**.

## Concepts — what the BA prepares and says

| Event | BA prepares | BA says (substance) | Avoid |
|---|---|---|---|
| **Planning** | Ready items, AC, open questions, dependencies | "This story is Ready except legal text; without it we can mock." | Reading 15 tickets aloud |
| **Stand-up** | One impediment or discovery risk | "Blocked on legal for consent copy; OTP story cannot finish AC." | Personal diary of meetings |
| **Review** | Demo script tied to AC; UAT notes | "Here is cancel within window vs late cancel — watch the fee message." | Slide-only "progress" |
| **Retro** | Requirement defects (missed AC, late splits) | "We took two unready stories; UAT bounced." | Blaming the PO |
| **Release planning** | Scope vs date, Must slices, vendor dates | "If core drop slips, we release OTP+UI with mock posting." | Fake certainty |

### Sample stand-up: BA impediment = waiting on legal for consent text

"Impediment: Digital KYC consent story is coded against placeholder text. Legal promised approved wording yesterday; still not in. Risk: we cannot meet DoD for audit. I need PO to escalate to legal today or we drop the story from the sprint goal."

That is useful. "Yesterday I had meetings" is not.

### Review: demo vs slide deck

**Demo:** working software on a test environment, real AC, one failure path. Stakeholders click or watch the BA/PO drive the product.

**Slide deck:** burnup charts, "8 stories Done," screenshots from local host, no exception path. Use slides only for context (metrics, next-rank items), not as a substitute for the increment.

If the increment is not demoable, say so; do not hide it in PowerPoint.

## Real-world examples

1. **ShopEase:** Review demos guest checkout decline path, not a deck titled "Payments 80% complete."
2. **QuickBite:** Release planning maps SMS go-live to a vendor contract date, then sets sprint goals backward.

## Scenario / Use case

### Context

NovaBank digital team: stand-ups are 25 minutes of task-level status. Reviews are decks. Planning starts with unready epics. Retro never mentions AC quality. Legal consent blocks KYC and nobody says it until UAT.

### Stakeholders

PO, SM, BA, developers, QA, legal, compliance (review guests).

### BA actions

1. Coaching with SM: stand-up is toward sprint goal, not a BA status meeting.
2. Bring the consent impediment **daily** until escalated.
3. Planning: only DoR items; KYC consent parked or spiked.
4. Review: demo PAN upload **and** rejection reason; invite compliance.
5. Retro: add "unready items in sprint" as a theme; change DoR enforcement.

### Sample artifact

Ceremony card:

- Planning agenda: goal → Ready list → capacity → risks.
- Stand-up prompt: goal / me / impediment.
- Review script: 3 AC scenarios, 10 minutes.
- Release sketch: Now (OTP login), Next (KYC capture), Later (video KYC).

### Failure if ignored

Legal delay is invisible. Review surprises compliance. Planning commits to Digital KYC epic. Retro blames "Agile." The BA is seen as a secretary taking minutes.

## Weak vs strong

| Weak | Strong |
|---|---|
| Stand-up status theater | One impediment that threatens the goal |
| Review = slides | Review = AC on a shared environment |
| Planning unready epics | Planning Ready stories + explicit risks |
| Retro only about tools | Retro includes requirement quality |
| Release plan = Gantt of hope | Release plan = slices + vendor/legal dates |

## Notes

- BA may skip speaking in stand-up if they have no goal impact — that is fine.
- Minutes belong after, not instead of, the event.
- Release planning is not a Scrum-guide mandatory event; still essential in banks and retail campaigns.
- Invite the users who will do UAT to review, not only managers.
- If demo fails, that is data; do not replace it with a deck of intended behavior.
