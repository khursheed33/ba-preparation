# Case Studies and Documentation

## Definition

A **project case study** is a narrative plus selected **requirement documentation** and **project documentation** that prove you did BA work — not a 40-page BRD uploaded as the portfolio.

## Why it matters

Hiring managers believe excerpts they can read on a phone. They do not read your full FRD. If you hide the thinking inside 40 pages, they assume there is no thinking.

## How to show BRD / FRD excerpts without dumping 40 pages

Pick **one slice** of the thread:

| Include | Skip (or link as appendix) |
|---|---|
| Problem statement + in/out scope | Every appendix and version history |
| 8–15 requirements with IDs | 200 copied “system shall” lines |
| 1 rule table | Full legal policy paste |
| RTM for that slice only | Entire product RTM |
| Change-request example (1) | All comments from Confluence |

**Label the rest:** “Full pack available on request (practice case, no real client data).”

Cover sheet on every excerpt: company (practice), your role (you were the BA), what is simulated, date.

## Before / after metrics (even if simulated)

Always **label simulated** or **illustrative**. Inventing a job at ShopEase is fraud; simulating impact on a practice case is honest if labelled.

| Case | Before | After (simulated) | How you would measure for real |
|---|---|---|---|
| ShopEase returns | 9-day refund; 18% tickets | 4.2 days; tickets −11% | Ticket tag + cycle timestamp |
| NovaBank loans | 10-day TAT; 34% incomplete | 4-day complete-file TAT | Status_history hours |
| MediCare+ | 22% no-show | 13% no-show | EMR attendance flag |

Put the metric in the story, not only in a dashboard PNG.

### Weak vs strong documentation

| Weak | Strong |
|---|---|
| Full BRD PDF as the case | 2-page story + 3-page excerpt + diagrams |
| Metrics with no source | “Simulated from As-Is sample of 50 returns” |
| Documentation with no decisions | Excerpt includes one CR and one out-of-scope fight |

## Project documentation that belongs in a case

- Problem, objectives, scope, assumptions, risks (one pager)
- Stakeholder map (one grid)
- As-Is / To-Be
- Requirements excerpt + stories + AC
- UAT scenarios (5–8)
- RTM excerpt
- Lessons learned (honest)

That *is* project documentation. Status reports and RAID logs can be a half-page sample, not a 12-week archive.

## Real-world examples

1. **ShopEase.** Excerpt shows FR-RET-04 auto-approve plus the seller-notice transition requirement — proves you did not only write buyer stories.
2. **NovaBank.** Excerpt shows completeness rules and the gold-loan out-of-scope line — proves control.
3. **ShieldSure.** One CR: “weekend hours for TAT” — proves change handling.

## Scenario / Use case: interviewer asks for “your BRD”

**Context.** You bring a laptop. Interviewer says “open the ShopEase BRD.” If you open page 1 of 40, they skim headings and ask nothing deep. If you open `00-story.md` then jump to the rule table, they ask about sellers.

**What you do.**

1. Start with the story (2 minutes).
2. Show scope in/out.
3. Show 5 FRs and 2 NFRs.
4. Show RTM line: FR-RET-04 → US-12 → UAT-07.
5. Say: “The 40-page training pack is how I practiced completeness; the excerpt is what I would take to a steering committee.”

**What goes wrong if ignored.** You either dump 40 pages (unread) or have only slides with no IDs (untraceable). Excerpts are the professional middle.

## Notes

- Case study = story + thin, traceable excerpts, not a document landfill.
- BRD/FRD: show a slice with IDs, rules, and one CR.
- Label every metric simulated unless you measured it.
- Project documentation is the decision trail, not every email.
- 
