# Project-Based Interview

## Definition

Telling **one project** end-to-end: **business problem**, **your BA role**, **requirement gathering**, **stakeholder handling**, **process improvement**, **challenges**, **decisions**, **business impact**, **lessons learned**.

Use **STAR** (Situation, Task, Action, Result) and two timed pitches: **2 minutes** and **5 minutes**.

## Why it matters

This is where freshers win or sound like they copied a BRD. Practice cases are valid if you say **practice / portfolio** and still own the thinking.

### Weak vs strong

| Weak | Strong |
|---|---|
| Tour of every template | Problem → bottleneck → decision → artifact → metric |
| “We” with no “I” | “I mapped, I recommended, I wrote AC” |
| Fake job at NovaBank | “Portfolio case; I was the BA” |

## STAR examples

**ShopEase (scope fight)**  
**S:** Warehouse wanted photos “while in the code.” **T:** Protect 4-day refund objective. **A:** Impact, options, recommend phase 2, update out-of-scope. **R:** Auto-approve shipped; photos queued; simulated cycle 9 → 4.2 days.

**NovaBank (data vs opinion)**  
**S:** Product wanted AI underwriting. **T:** Find where TAT actually sat. **A:** Status counts; 34% incomplete files. **R:** Checklist scoped; AI parked; complete-file TAT story became 4 days (simulated).

**MediCare+ (missed voice)**  
**S:** Quiet psychiatry constraint. **T:** Make it a rule. **A:** Specialty table, no SMS. **R:** Avoided a consent incident in the design (practice).

---

## ShopEase returns — 2-minute pitch

“This is a **portfolio case**, not employment. ShopEase marketplace refunds took 9 days; 18% of tickets were ‘where is my refund?’ I was the BA. I mapped As-Is and found seller approval averaging 2.1 days — not warehouse as people assumed. I wrote a problem statement without a chatbot inside it. In-scope: auto-approve Size prepaid under ₹2,000 plus status SMS. Out: chatbot and international. I handled sellers late, then added notice and a kill switch. Artifacts: To-Be, rule table, stories, AC, a volume-vs-delay chart. Simulated impact: 4.2-day cycle, tickets down. Lesson: missed stakeholders are missed requirements.”

## ShopEase — 5-minute pitch

Add: stakeholder grid; assumption that Size is not a dump code (QC sample); CR for photos; UAT QC-fail path; RTM line FR-RET-04 → US-12 → UAT-07; you would instrument timestamps on a real job.

## NovaBank loans — 2-minute pitch

“Portfolio case. NovaBank salaried personal loans took 10 days. I pulled a sandbox-style count: 34% of web apps sat in documents-pending over 48 hours. I elicited from RMs and underwriters. Gold loans out of scope. I recommended a completeness checklist and status SMS, not a new AI model. Hybrid: compliance needed a rules baseline; digital got sprint slices. Dependency: bureau API SLA. Simulated result: complete files in 4 days. Lesson: start with the wait state, not the tool.”

## NovaBank — 5-minute pitch

Add: credit vs digital conflict on field count; NRI phone prefix UAT fail; fraud CR cooling period after mobile change; metric reconciliation 34% vs 28% (gold loans in the dashboard); your role vs PM vs PO.

---

## Covering the interview checklist

| They ask | You point to |
|---|---|
| Project explanation | 2-min pitch first |
| Business problem | 9-day refund / 10-day TAT with evidence |
| Your BA role | Elicit, analyze, recommend, write, UAT — not coding |
| Requirement gathering | Interviews + sample data, not only VP |
| Stakeholder handling | Sellers recovery; credit vs digital |
| Process improvement | Remove wait, don’t add chatbot/AI first |
| Challenges | Missed seller; hybrid docs; data mismatch |
| Decisions | Out-of-scope gold loans / chatbot |
| Business impact | Simulated, labelled |
| Lessons learned | Quiet stakeholders; grain of SQL |

## Real-world examples of bad project talks

- 8 minutes of company history, 0 minutes of *your* analysis.
- Claiming you “implemented” core banking.

## Scenario / Use case: “Tell me about a project” at minute 0

**Context.** Interviewer drinks tea. No prompt for 2 vs 5.

**What you do.** Start the **2-minute** ShopEase pitch. Pause: “I can go deeper on stakeholders or on the SQL.” They will pick. If they say “keep going,” expand to the 5-minute structure.

**What goes wrong if ignored.** You start at SDLC theory, they interrupt, you never land the bottleneck. Time-box is stakeholder management.

## Notes

- Always label practice cases; STAR for conflicts and data fights.
- 2-minute = problem, bottleneck, in/out, one decision, metric, lesson.
- 5-minute adds stakeholders, CR/UAT, traceability, what you would do at work.
- Prepare both NovaBank and ShopEase so they can choose a domain.
- 
