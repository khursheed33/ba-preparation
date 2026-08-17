# ATS and Resume Keywords

## Definition

An **ATS (Applicant Tracking System)** is software that stores applications, parses resumes into fields, and lets recruiters search/filter. An **ATS-friendly resume** is a file the parser can read and a human can still like.

**Resume keywords** are the nouns and verbs from the job description (JD) that recruiters search — “user stories,” “UAT,” “SQL,” “stakeholder” — mapped honestly to your projects.

## Why it matters

If the parser sees a graphic instead of the word “requirements,” you never reach a BA. If you keyword-stuff “Jira Jira Jira” with no project, the human round fails.

## How ATS works (practical)

1. You upload PDF or DOCX.
2. Parser extracts text, tries to fill Name, Experience, Education, Skills.
3. Recruiters search Boolean: `("business analyst" OR "business analysis") AND (SQL OR Excel)`.
4. Some systems score keyword overlap. Many just *search*. Either way, missing words = invisible.
5. A human still reads the top of the pile. ATS is the gate, not the offer.

It does **not** magically understand your ShopEase story if the words “process mapping” never appear.

## Keyword list from JD → resume mapping

Example JD: “Associate BA, retail, Agile, user stories, acceptance criteria, Jira, SQL, UAT, stakeholders.”

| JD term | Where it goes on *your* resume | Honest source |
|---|---|---|
| Business analysis | Headline + summary | True |
| User stories / AC | ShopEase project bullets | True |
| Jira | Skills + “wrote stories as if for Jira” if you used a board | Don’t claim company Jira admin |
| SQL | NovaBank count + Skills | True if you wrote the query |
| UAT | “Wrote UAT scenarios” | True |
| Retail / e-commerce | ShopEase practice case | Domain practice, not job |
| Banking | NovaBank case | Same |
| Stakeholder management | “Mapped sellers vs CX; recovered missed seller” | True of the case |

Do not add “HIPAA expert” because MediCare+ is in the portfolio unless you studied it.

## Formatting rules

| Do | Don’t |
|---|---|
| Standard headings: Summary, Skills, Projects, Education, Certifications | Textboxes, columns that reorder as “Education” first in parse |
| Simple bullets, consistent dates | Tables for the whole layout (many ATS scramble tables) |
| PDF *or* DOCX as the JD asks; selectable text | Screenshot-of-Canva PDF, icons instead of words |
| Filename `Firstname_Lastname_BA.pdf` | `resume_final2_new.pdf` |
| Skills as text | Skill bars / infographics |

Headers/footers may be ignored. Put phone in the main body.

### Weak vs strong

| Weak | Strong |
|---|---|
| Graphic resume, no copy-paste text | One column, real headings, keywords in context |
| Keyword dump: “BRD FRD SRS BPMN SQL…” | Same words inside project bullets |
| Title “Visionary Ninja” | Title “Aspiring Business Analyst” |

## Real-world examples

1. JD searches `UAT`; your resume says “user testing workshop” only — miss.
2. You add every tool from 20 JDs including Salesforce you never touched — interview collapse.
3. You match “process mapping, user stories, SQL” to ShopEase/NovaBank bullets — pass search and the screen.

## Scenario / Use case: good BA rejected because the resume was a graphic

**Context.** You did strong ShopEase and NovaBank cases. You design a two-column Canva resume: photo, teal skill wheels, icons for phone. You export a flattened PDF. ATS extracts: empty Experience, Skills = “”. Recruiter search for SQL returns other people. You never hear back. A friend pastes your GitHub story into a plain resume and gets the call.

**What the BA does next.**

1. Rebuild one-column DOCX/PDF with selectable text.
2. Headings the ATS expects.
3. Map JD keywords to existing bullets — no fake jobs.
4. Test: copy-paste the PDF into Notepad; if order is garbage, fix.
5. Keep a “pretty” one-pager only as a leave-behind *after* you are in the room, if at all.

**What goes wrong if ignored.** Your analysis never gets a human. ATS friendliness is not “dumbing down”; it is making the words machine-readable.

## Notes

- ATS stores, parses, and searches; keywords must appear as text in context.
- Map JD language to real projects; do not invent tools or employment.
- Avoid layout tables, textboxes, and icon-only contact info.
- Graphic resumes can hide a good BA from the search.
- 
