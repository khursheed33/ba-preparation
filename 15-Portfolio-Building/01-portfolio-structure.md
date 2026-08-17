# BA Portfolio Structure

## Definition

A **BA portfolio** is a small, public (or shareable) set of case studies that prove you can move from a **business problem → analysis → recommended solution**, with artifacts a recruiter can skim.

It is not a dump of every template you ever filled. It is **problem → analysis → solution storytelling**.

## Why it matters

Freshers have no job title to hide behind. In 60 seconds a recruiter decides if you understand BA work or if you pasted a BRD template. Structure is how you survive that scan.

## Recommended folder / site structure

```text
portfolio/
  index.md                 (who you are, 3 cases, contact)
  case-shopease-returns/
    00-story.md            (problem → analysis → solution, 2 pages)
    01-problem-scope.md
    02-stakeholders.md
    03-process-as-is-to-be.md
    04-requirements-excerpt.md   (not 40 pages)
    05-stories-ac.md
    06-wireframes.md
    07-data-sql-bi.md
    08-uat-rtm-excerpt.md
    09-impact.md           (label simulated metrics)
  case-novabank-loans/
    (same skeleton)
  case-medicare-reminders/   (optional third)
  resume.pdf
```

Website can mirror this: Home, Case 1, Case 2, Artifacts, Contact. GitHub repo with the same folders is enough if you have no site yet.

## The 2–3 case studies rule

| Count | Why |
|---|---|
| 1 | Looks thin; one domain only |
| 2 | Minimum: e.g. ShopEase (process + stories) + NovaBank (rules + data) |
| 3 | Ideal cap: add MediCare+ or QuickBite if quality stays high |
| 5+ | Recruiter never opens them; quality drops |

Depth beats volume. Each case needs a full thread: problem, stakeholders, scope, As-Is/To-Be, requirements excerpt, one diagram, stories, one data insight, UAT idea, impact.

## What recruiters scan in 60 seconds

1. Headline: “Business Analyst portfolio — e-commerce returns & banking origination.”
2. One metric per case (even simulated, labelled).
3. Whether you wrote *analysis* or only screenshots of templates.
4. Tools named in context (Jira, SQL, Power BI) — not a shopping list.
5. Link works; no “final_final_BRD.docx” with client secrets.

### Weak vs strong

| Weak | Strong |
|---|---|
| 12 folders of empty templates | 2 complete stories with excerpts |
| “Digital transformation case” with no company | ShopEase / NovaBank named as **practice cases** |
| 40-page PDF as the homepage | 2-page story + “full artifacts inside” |

## Real-world examples

1. Recruiter opens GitHub, sees `ShopEase-returns/00-story.md` with cycle time 9 → 4 days (simulated) and a process map — books you.
2. Recruiter sees 8 random Excel files named `analysis.xlsx` — closes tab.
3. LinkedIn Featured links to the NovaBank story; interview starts at “tell me about loans” instead of “what is a BRD?”

## Scenario / Use case: 60-second scan of your ShopEase folder

**Context.** You apply to a marketplace BA role. Recruiter has 40 tabs. They open your repo.

**What they should see first (`00-story.md`).**

- Problem: prepaid refunds 9 days; 18% tickets are status.
- You: mapped As-Is, found seller approval 2.1 days, recommended auto-approve Size < ₹2,000 + SMS — not a chatbot.
- Artifacts: BPMN, 8 stories, RTM excerpt, Power BI of delay buckets.
- Impact (simulated): cycle 4.2 days; tickets −11%. Labelled simulated.
- Out of scope: chatbot (shows judgment).

**What goes wrong if ignored.** Homepage is a skill cloud. Recruiter cannot retell your story in the debrief. You look like a student who collected files, not a BA who solved something.

## Notes

- Structure is Home + 2–3 cases with the same skeleton, not a template museum.
- Storytelling order is problem → analysis → solution → impact.
- Recruiters scan headline, one metric, and whether analysis exists.
- Practice companies (ShopEase, NovaBank) are fine; never claim them as employers.
- 
