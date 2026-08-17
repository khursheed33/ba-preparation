# How to Build a BA Case Study

A **BA case study** is a complete, fictional-but-realistic pack that shows you can run analysis from problem to solution: process, requirements, rules, stories, UAT, and traceability. It is not a blog post and not a copied BRD from a past employer.

## Why it matters

Hiring managers rarely see your production Confluence. A portfolio case study is the evidence. ShopEase returns or NovaBank loans let you demonstrate the same artifacts you would produce on the job — without waiting for a title.

## How to research when you have no job

| Source | What you extract | Ethics |
|---|---|---|
| Your own customer journeys | Pain, steps, wait, error messages | You may describe public UX; do not scrape private data |
| Company help centres, fee pages, policy PDFs | Business rules, SLAs, KYC, return windows | Public documents only |
| Regulator sites (RBI, IRDAI, NPPA) | Constraints you can cite as fictional policy | Quote the idea, not a stolen internal memo |
| Job descriptions + LinkedIn BA posts | Which artifacts this industry expects | Do not invent “I led X at Y bank” |
| Friends in ops (with permission) | Volume ranges, typical bottlenecks | Anonymise; never use real customer PII |
| News on outages, fines, NPS | Problem statements | Keep numbers labelled **illustrative** |

**Method.** Pick a domain. Mystery-shop the live app as a customer. Write As-Is from that journey. Invent To-Be that closes a measurable gap. Never paste a confidential template from a previous workplace.

## Weak vs strong case study

| Weak | Strong |
|---|---|
| “Amazon-like checkout.” | ShopEase: return cost ₹18/order; 82% of returns from 3 reasons. |
| Screenshots of a real bank’s internal BRD. | Fictional NovaBank with realistic RBI-style constraints. |
| User stories with no AC. | Five stories, each with Given/When/Then. |
| No RTM. | Every FR traces to a test and a story. |
| 40 pages of theory. | 8–12 pages (or a GitHub folder) of artifacts. |

## Artifact checklist (every project file in this folder)

Use this as a definition of “complete.”

| # | Artifact | Done when |
|---|---|---|
| 1 | Business problem | Measurable pain, not a feature request |
| 2 | Business objective | Target metric + date |
| 3 | Stakeholders | Named roles |
| 4 | Stakeholder analysis | Influence, interest, attitude, engagement |
| 5 | Scope | In and out |
| 6 | Assumptions | Testable beliefs |
| 7 | Constraints | Time, money, system, legal |
| 8 | As-Is process | Numbered steps + wait |
| 9 | Problem analysis | Who is hurt, cost of inaction |
| 10 | Root-cause analysis | 5 Whys / fishbone / Pareto — not “legacy” |
| 11 | To-Be process | Numbered steps |
| 12 | Gap analysis | People / process / tech / data / policy |
| 13 | Functional requirements | Testable FRs |
| 14 | Non-functional requirements | SLA, security, volume |
| 15 | Business rules | Decision logic |
| 16 | User stories + AC | ≥ 5 stories |
| 17 | Use case | ≥ 1 fully dressed |
| 18 | Process diagrams described | As-Is and To-Be steps |
| 19 | Wireframes described | Screen-by-screen |
| 20 | Data requirements | Entities and key fields |
| 21 | Reports | Audience + cadence |
| 22 | KPIs | Baseline and target |
| 23 | UAT scenarios | Business path, not only happy path |
| 24 | RTM | Requirement → story → test |
| 25 | Change request | 1 sample with impact |
| 26 | Risks | P/I/mitigation/owner |
| 27 | Dependencies | External teams/vendors |
| 28 | Final business solution | What you recommend, phased |

## How to present: 8–12 pages or a GitHub folder

**Option A — PDF / Doc (8–12 pages)**

1. Cover: company (fictional), problem, your role (BA), date.
2. Page 2: problem, objective, KPIs.
3. Page 3: stakeholders + RACI snippet.
4. Page 4: scope, assumptions, constraints.
5. Pages 5–6: As-Is / To-Be / gaps / root cause.
6. Pages 7–8: FRs, NFRs, rules, one fully dressed use case.
7. Page 9: stories + AC, wireframe descriptions.
8. Page 10: data, reports, KPIs.
9. Page 11: UAT + RTM.
10. Page 12: risks, dependencies, CR sample, solution.

**Option B — GitHub folder**

```
13-Real-World-BA-Projects/02-ecommerce-case-study.md
```

One markdown file per case is enough for study. For interviews, split into `problem.md`, `requirements.md`, `rtm.md` if the reader prefers. Keep a one-page `index` of artifacts — not a marketing README if the course forbids it; a short contents list inside the case file is enough.

**Live walkthrough (15 minutes).** Problem and metric (2 min) → As-Is vs To-Be (3) → one use case + wireframes (4) → RTM and UAT (3) → risks and what you would do in week one on the job (3).

## Ethics

- **Fictional but realistic.** ShopEase, NovaBank, MediCare+ are teaching companies. Numbers are illustrative.
- **No confidential docs.** Do not copy BRDs, data models, or screenshots from a current or former employer.
- **No real customer PII, account numbers, or claim IDs.**
- **Do not impersonate.** “I delivered this at HDFC” when you did not is fraud. “I built a NovaBank-style loan origination case study” is honest.
- **Cite public rules** as “inspired by typical RBI/IRDAI practice,” not as legal advice.

## Real-world examples of good vs bad sources

- Good: IRDAI public circular on claim TAT; your own Swiggy order timeline; a hospital token counter you stood in.
- Bad: a WhatsApp export of production incidents; a client’s Confluence export; a colleague’s signed-off SRS.

## Scenario / Use case: assembling ShopEase without a BA job

**Context.** You are switching careers. You have used ShopEase-like apps. You have never written a BRD.

**What you do.** Mystery-shop a return. Time every wait. Tag three return reasons from the public policy page. Invent volumes (label them illustrative). Write As-Is from your notes. Choose To-Be that cuts the waits you felt. Fill the checklist above. Ask a friend to UAT-read your stories. Put the file in this folder. Practice the 15-minute walkthrough.

**If ignored.** You submit a “case study” that is a UI redesign essay with no RTM, no rules, and a real company’s logo. Interviewers treat it as shallow or unethical.

## Notes

- Research from public journeys, help pages, and regulators — never from stolen internal docs.
- Complete means the 28-artifact checklist, not a long problem essay.
- Present 8–12 pages or a GitHub folder; rehearse 15 minutes.
- Label data illustrative; keep companies fictional; do not claim fake employment.
- Every later file in this folder is a portfolio-ready pack using that checklist.
