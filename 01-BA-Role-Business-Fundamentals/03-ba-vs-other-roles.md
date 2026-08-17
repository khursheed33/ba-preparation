# BA vs Other Roles

A BA often works with all of these roles. The difference is **ownership**.

## BA vs Data Analyst

| | Business Analyst | Data Analyst |
|---|---|---|
| Focus | Business problems and requirements | Data, trends, and insights |
| Output | BRD, user stories, process maps | Reports, dashboards, analysis |
| Question | What should we build or change? | What does the data tell us? |

Overlap: both may use Excel, SQL, and KPIs. A BA uses data to support decisions and requirements. A Data Analyst goes deeper into statistics and reporting.

## BA vs Product Manager

| | Business Analyst | Product Manager |
|---|---|---|
| Focus | Requirements and solution fit | Product vision, strategy, and market |
| Time horizon | Current project / change | Long-term product |
| Output | Requirements, processes, UAT | Roadmap, prioritization, product success |

In many companies, especially startups, one person may do both jobs.

## BA vs Project Manager

| | Business Analyst | Project Manager |
|---|---|---|
| Focus | What and why | When, who, and how much |
| Owns | Requirements, scope clarity | Plan, budget, timeline, risks of delivery |
| Success | Right solution is defined | Project is delivered on time and budget |

They work closely: the PM manages delivery; the BA manages requirements.

## BA vs Product Owner

| | Business Analyst | Product Owner |
|---|---|---|
| Focus | Analysis and documentation | Backlog ownership and value |
| Decision power | Recommends | Prioritizes and accepts work |
| Agile role | Supports the team | Accountable for product backlog |

In Scrum, the Product Owner decides priority. The BA often helps the PO write stories, refine the backlog, and clarify requirements.

## BA vs QA

| | Business Analyst | QA / Tester |
|---|---|---|
| Focus | What the business needs | Whether the system works correctly |
| Output | Requirements, acceptance criteria | Test cases, bug reports |
| Question | Is this the right thing to build? | Was it built correctly? |

The BA defines acceptance criteria. QA tests against them. Both care about quality, from different angles.

## Quick memory aid

- **BA**: What should we build and why?
- **PM**: How do we deliver it on time?
- **PO**: What is most valuable next?
- **QA**: Does it work as specified?
- **Data Analyst**: What do the numbers say?

## Real-world examples (same meeting, different jobs)

**ShopEase returns war-room**

- BA: “Seller approval is the delay. Requirement: auto-approve returns under ₹2,000 if the reason is Size.”
- Data Analyst: “Auto-approve would hit 41% of return lines; refund leakage risk is 2.3% based on last quarter QC fails.”
- PM: “If we slice auto-approve this sprint, UAT needs two extra warehouse days. I will re-plan.”
- PO: “Do auto-approve before the chatbot. Value is cycle time, not a new channel.”
- QA: “I need a rule table: reason codes that qualify, and what happens if QC later fails.”

**NovaBank vs MediCare+ overlap traps**

| Confusion | What happens | Fix |
|---|---|---|
| BA writes SQL dashboards all week (NovaBank MIS) | Requirements for the loan portal stall | BA uses data to *support* requirements; DA owns the recurring report |
| PO at MediCare+ writes stories with no exceptions | Doctors reject UAT | BA adds clinical exceptions; PO still prioritizes |
| PM at ShopEase “freezes scope” without out-of-scope list | Sellers assume pickup *and* reverse-logistics redesign | BA writes in/out; PM tracks dates |

### Weak vs strong role clarity

| Weak | Strong |
|---|---|
| “I can also be the PM this sprint” (silently) | Named owners: BA = requirements, PM = plan |
| Fighting the PO in stand-up over priority | Recommend; PO decides; you document the decision |
| QA asks you to write all test cases | You provide AC and UAT scenarios; QA designs tests |

## Scenario / Use case: MediCare+ appointment reminders — who owns what

**Context.** Specialist no-show rate is 22%. COO says “BA, PM, and the data team should just figure it out.” A Slack channel with 18 people forms. Nobody owns the problem statement.

**Stakeholders.** COO (sponsor), clinic ops, doctors, patients, EMR vendor, SMS gateway, legal (consent), PM, BA, data analyst, PO for patient app.

**What the BA does.**

1. Propose a RACI in writing. BA: problem, process, requirements, UAT scenarios. DA: no-show by clinic/day. PM: vendor dates and cutover. PO: backlog order. QA: test against AC.
2. Refuse to “also project-manage” the SMS vendor. That is the PM.
3. Use the DA’s finding (Monday 9 a.m. slots drive no-shows) as *evidence*, then write: reminder 24h + 2h, with reschedule link, only if `consent.sms = true`.
4. Hand AC to QA. Do not write 40 test cases.

**Sample artifact.** One-page role card attached to the kickoff deck.

| Decision | Owner | BA does |
|---|---|---|
| Which clinic goes first | COO / PO | Options + impact |
| SMS vendor contract dates | PM | Dependency list |
| Exact reminder copy | Ops + legal | Requirement + review |
| “Does it work?” | QA + UAT doctors | Expected behaviour |

**What goes wrong if ignored.** The BA becomes a coordinator. The DA builds a dashboard nobody asked to act on. The PM schedules a vendor. Doctors never confirmed that SMS is allowed for certain specialties. Go-live is “successful”; no-shows do not move. Leadership cannot tell who failed because ownership was soup.

## Notes

- Learn neighbouring roles so you can hand off cleanly, not so you can do everyone’s job.
- In startups one person may wear BA + PO. Still say which hat you are wearing in the email.
- Data supports BA work; it does not replace a requirement.
- 
