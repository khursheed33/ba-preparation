# How to Learn a Domain (Without Pretending to Be an Expert)

## Definition

A **domain** is the industry (or function) whose language, money flows, risks, and processes you must understand to write requirements that make sense. Banking is a domain. Claims is a subdomain. “The app” is not a domain.

Learning a domain is **structured context**: enough to ask sharp questions, not enough to replace the actuary, surgeon, or warehouse manager.

## Why it matters — pick ONE domain first

Depth beats a collage of buzzwords. Interviewers and stakeholders trust a BA who can follow a NovaBank KYC conversation more than one who “did a bit of everything.” After you can hold a 30-minute process talk in one domain, a second domain is easier because you already know *what to look for*.

Goal from the roadmap: **enough context for conversations, not industry expert.**

## What to learn (the checklist)

| Area | What “enough” looks like | Example |
|---|---|---|
| Terminology | You can define 20–40 terms without Googling in the meeting | EMI, NPA, cashless, GMV, ASN |
| Processes | You can sketch As-Is 6–12 steps | Order → pick → pack → ship |
| Problems | You know the usual pain | KYC drop-off, claim leakage, no-shows |
| KPIs / metrics | You know 5–8 steering numbers | DPD, combined ratio, on-time % |
| Business model | Who pays, who costs, unit of value | Interest + fees; GMV take rate |
| Customer journeys | Happy path + 2 failure paths | Apply → sanction → disburse |
| Operational processes | Who does the work daily | Maker-checker, QC, triage |
| Regulations lite | Names + what they constrain | KYC, DPDP, IRDAI, PCI |
| Typical systems | Core vs satellite | CBS, OMS, EMR, policy admin |
| Stakeholders | Titles and interests | Underwriter vs agent vs TPA |
| Industry requirements | Recurring FR/NFR types | Audit trail, masking, limits |
| Industry metrics | How they judge success | Churn, occupancy, fill rate |

You do **not** need: to pass CA/medical exams, to code the core, or to memorize every circular.

### Weak vs strong

| Weak | Strong |
|---|---|
| “I can BA any industry.” | “I can run a claims intake workshop and know what I don’t know.” |
| Glossary of 200 unread terms | 30 terms used in a process sketch |
| Only product features | Money + risk + ops + customer |
| Ignore regulation | “This requirement needs compliance in the room.” |
| Expert cosplay | Questions + confirmed terms |

## 30-day learning plan

Assume 45–60 minutes on weekdays, a bit more on two weekends. Pick **one** company type (e.g. NovaBank-style retail bank, or ShopEase-style e-commerce).

| Days | Focus | Output you can show |
|---|---|---|
| 1–3 | Business model | Half-page: who is customer, revenue, cost, unit |
| 4–7 | Terminology | Personal glossary: 25 terms, one sentence each |
| 8–12 | Core process As-Is | One swimlane: 8–15 steps, systems on arrows |
| 13–16 | Customer journey | Happy path + exception (reject, return, claim deny) |
| 17–20 | KPIs | Scorecard: 6 metrics, formula, good/bad direction |
| 21–23 | Systems map | Core + CRM + payments + reporting; what is master |
| 24–26 | Regulations lite | 4 rules: what they stop you from designing naively |
| 27–28 | Stakeholders | Power/interest: 8 roles, what they optimize |
| 29–30 | Mock BA | One problem statement + 5 FRs + 3 UAT scenarios |

**Sources:** annual reports (business model), product help centers, RBI/IRDAI/MoHFW public pages (lite), a friend in ops, job descriptions (systems named), your own as-a-customer journey.

**Not sources:** only YouTube “domain in 10 minutes,” or copying a BRD you do not understand.

## Real-world examples

**Switching later.** A BA who learned ShopEase retail can enter QuickBite faster (catalog, dispatch, SLA) than someone with zero ops vocabulary. Banking → insurance is closer (risk, KYC, ledgers) than banking → hospital floor ops.

**EdTech vs SaaS.** Same subscription mechanics; different “seat” (student vs employee) and content IP. Learn SaaS billing once; add academic calendar.

**Government.** Procurement and citizen identity dominate; your 30 days should include RTI/audit mindset, not only UX.

## Scenario / Use case: first 30 days before a NovaBank project

**Context.** You join a loan origination rebuild in 5 weeks. You have retail e-commerce background only.

**What you do.** Days 1–7: retail vs corporate, secured vs unsecured, EMI, CIBIL, LTV — glossary. Days 8–16: As-Is apply → bureau → underwrite → sanction → KFS → disburse → NACH. Days 17–23: TAT, approval %, first-month bounce, STP %. Days 24–26: KYC, fair practices, data localization *as questions for compliance*, not as legal advice. Day 30: workshop agenda using *their* terms.

**What you do not do.** Redesign credit policy in week one. Pretend you know IRAC norms in depth. Stay silent when “NPA” is used — ask once, write it down.

**If ignored.** You write ShopEase-style “checkout” stories for a regulated credit journey; legal and risk reject the BRD.

## Notes

- Pick one domain first; breadth later.
- Goal: conversation-ready, not expert.
- Learn: terms, processes, problems, KPIs, model, journeys, ops, regs lite, systems, stakeholders, typical requirements and metrics.
- 30 days: model → glossary → As-Is → journey → KPIs → systems → regs → stakeholders → mock artifacts.
- Write terms in your own sentences; unused glossaries die.
- Regulations: know the *constraint type*, bring the specialist.
- Job ads and annual reports beat random blogs for systems and money.
- Your customer-side journey is valid data — then validate with ops.
