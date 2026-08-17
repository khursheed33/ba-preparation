# Business Case, Organisation, and Change

**Business acumen** for a BA is knowing how the organisation decides, pays, and absorbs change — not becoming a CFO or HR partner.

This file covers four related skills: **business case development**, **ROI and budgeting basics**, **organisational structure**, and **organisational change management**. Cost-benefit and feasibility mechanics live in [cost-benefit, feasibility, and impact](04-cost-benefit-feasibility-impact.md). Agile backlog change lives in [change and continuous discovery](../05-Agile-Scrum-Software-Delivery/08-change-and-continuous-discovery.md). This file is the *sponsor and organisation* view.

## Why it matters

A perfect FRD for video KYC dies if there is no approved case, no budget line, and no plan for branch staff who lose a task. Vendor BAs are often asked to *draft* the case and *trace* the change; Finance and the sponsor *own* the numbers and the decision.

## Business case development

A **business case** argues whether a change is worth doing. A **BRD** specifies what to build once someone said yes. Do not paste FRs into a business case.

| Section | What it contains | NovaBank video KYC |
|---|---|---|
| Problem / opportunity | Baseline metric and who hurts | Digital loan drop-off at “visit branch for KYC” |
| Options | Including do-nothing | A) branch only B) vendor video + fallback C) in-house video |
| Costs | One-time and run (see CBA file) | Build, vendor fee, storage, training |
| Benefits | Cash and non-cash, with assumptions | Conversion, branch minutes, fewer incomplete packets |
| Risks and dependencies | What could kill the case | Legal liveness rules; vendor lead time |
| Recommendation | Go / conditional go / no-go | Conditional go, 14 weeks, salaried residents only |

**Who writes what.** BA structures options and assumptions. Finance models tax, NPV, cost of capital. Sponsor signs. Architecture confirms technical cost bands.

## ROI and budgeting basics

**ROI / payback** — enough to defend a story; not CFA-level. Formulae and sensitivity are in the CBA file.

**Budgeting the BA must understand:**

| Term | Meaning | BA use |
|---|---|---|
| **Capex** | One-time build / licence capitalised | “This is a project budget, not ops overtime” |
| **Opex** | Run cost: vendor per-KYC, support FTEs | Call out year-2 cost so go-live is not a surprise |
| **Cost centre / budget owner** | Who’s money | Digital vs branch vs compliance — whose line? |
| **Benefit owner** | Who is accountable for the KPI moving | Credit ops owns cycle time, not the BA |

You do not set the budget. You prevent a case that counts benefits twice and costs once.

## Organisational structure (so you know who can say yes)

| Pattern | How it feels | BA implication |
|---|---|---|
| **Functional** | Credit, ops, IT in silos | Requirements bounce; you need a named cross-functional sponsor |
| **Matrix** | BA reports to delivery *and* a business line | Two bosses; RACI must be written |
| **Product / tribe** | Aligned to a journey (loans, claims) | PO may be the day-to-day A; legal still C |
| **Vendor / service org** | You sit in an IT firm, client sits elsewhere | Client SMEs are not in your standup; comms plan is the job |

Ask early: **who is Accountable for scope?** In a matrix NovaBank program, the program PM may own timeline while the credit head owns policy. If you only interview IT, you will miss the real A.

Also map **informal power**: a branch cluster head who is not on the org chart can block UAT.

## Organisational change management (people adopting the solution)

Delivery change (CR, backlog restack) is not the same as **people change** (new job, new screen, lost workaround).

A BA supports change; a change manager or ops lead often owns it. You still specify **transition requirements**: training, comms, dual-run, rollback.

| Element | BA contribution | Example |
|---|---|---|
| **Awareness** | Why we are changing (from the case) | “Refund SMS so sellers see auto-approve” |
| **Desire / resistance** | Surface who loses (sellers, RMs, clerks) | RM loses “I walk the file to credit” status |
| **Knowledge** | SOP, job aid, UAT as rehearsal | MediCare+ reminder rules by specialty |
| **Ability** | Time, access, floor support at go-live | Super-user on clinic day 1 |
| **Reinforcement** | KPI, audit, kill old path | WhatsApp no longer accepted as claim pack |

If the To-Be still allows the old side channel, the organisation has not changed — the software just added a path.

## Weak vs strong

| Weak | Strong |
|---|---|
| Business case = list of features | Options, costs, benefits, recommendation |
| “ROI is high” | Payback + who owns the benefit + opex in year 2 |
| Stakeholder list = org-chart paste | Chart + matrix + informal blockers |
| Change management = a training slide | Transition FRs, dual-run, old path retired |

## Scenario / Use case: NovaBank video KYC case meets branch structure

**Context.** Sponsor wants video KYC. Branch network is a powerful functional silo. Budget sits in Digital. CKYC clerks sit in Ops. RMs fear losing customer face-time.

**Stakeholders.** Digital sponsor (budget), credit head (policy), branch ops (jobs), CKYC ops, legal, vendor, BA.

**What the BA produces.**

1. **Case:** Option B, conditional go (see CBA file). Benefit owner: Digital conversion KPI; cost: Digital capex + Ops opex for reviewers.
2. **Structure:** Matrix RACI — Digital PO Accountable for scope; Credit Accountable for policy; Branch Consulted; CKYC Responsible for exception queue.
3. **Change:** Transition requirements — RM script (“video is default, branch is fallback”), clerk capacity model, 30-day dual-run, then retire “mandatory branch KYC” for in-scope segments.
4. **Comms:** Branch cluster heads get a one-pager before rumours hit WhatsApp groups.

**Sample artifact.** Case recommendation box:

> Conditional go. Capex Digital; opex CKYC review team. Benefit: digital conversion. Risk: branch resistance. Transition: fallback remains; mandatory branch retired only for salaried residents after 30-day dual-run.

**What goes wrong if ignored.** Finance approved a build. Branches never send customers to video. Conversion KPI does not move. The BRD was fine; the organisation was not in the case.

## Notes

- Business case decides *whether*; BRD decides *what*.
- ROI/payback are BA-defendable; NPV stays with Finance.
- Org structure tells you who is A vs who is loud.
- Organisational change is transition requirements plus retired old paths — not a kickoff speech.
- Watch: [SWOT](https://www.youtube.com/watch?v=sGrmUvxVrjc), [PESTEL](https://www.youtube.com/watch?v=bYn4CyL3r5w), and [Kniberg product ownership](https://www.youtube.com/watch?v=502ILHjX9EE) for the why / who / value layer of a case.
- 
