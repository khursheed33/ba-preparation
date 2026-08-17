# GitHub, Website, and Presentations

## Definition

How you **publish** BA work: a clean **GitHub** repo, a simple **portfolio website**, and two talk tracks — a **project presentation** and a **case-study presentation**.

## Why it matters

A recruiter will open one link. Broken images, `password.txt`, and a 40-slide dump all say “not production-ready.” Hygiene is part of the BA brand.

## GitHub hygiene for BA work

| Do | Do not |
|---|---|
| Markdown stories, PNG/SVG diagrams | `.env`, API keys, connection strings |
| Fake/sample CSVs labelled `sample_` | Real PAN, phones, patient IDs |
| `README` per case: problem, your role, how to read | Empty repo named `BusinessAnalyst` |
| License + “practice case, not a real client” | Claiming ShopEase employed you |
| Reasonable file names `03-process-to-be.png` | `scan0001.jpg` of a whiteboard only |

Optional: GitHub Pages from the same markdown. Keep secrets out of history (once pushed, rotate keys — better never to commit).

## Website sections

1. **Hero:** name, “Aspiring / Junior Business Analyst,” 1 line of domains (e-commerce, banking).
2. **Selected work:** 2–3 cases with one metric each.
3. **How I work:** problem → analysis → solution (5 lines).
4. **Artifacts:** links into GitHub folders.
5. **Contact:** email, LinkedIn, GitHub. No 12 social icons.

If you cannot build a site yet, a well-structured GitHub *is* the website.

## 5-minute presentation outline (case-study)

| Min | Content |
|---|---|
| 0–0.5 | Problem + metric (ShopEase 9-day refunds) |
| 0.5–2 | As-Is bottleneck (seller 2.1 days) + evidence |
| 2–3.5 | Options + recommendation + in/out scope |
| 3.5–4.5 | One diagram + one story/AC + one insight chart |
| 4.5–5 | Simulated impact + what you would do in week 1 on the job |

## 15-minute presentation outline (project)

| Min | Content |
|---|---|
| 0–2 | Context, stakeholders, your BA role (you, not a fake employer) |
| 2–5 | Problem statement, goals, scope, assumptions |
| 5–8 | Process As-Is/To-Be, root cause |
| 8–11 | Requirements excerpt, rules, stories, wireframe |
| 11–13 | Data insight, UAT idea, risks |
| 13–15 | Impact, lessons, questions |

Practice with a timer. Cut jokes. Leave 2 minutes if they want Q&A inside the 15.

### Weak vs strong

| Weak | Strong |
|---|---|
| 30 slides of definitions | 8 slides, all on one case |
| GitHub full of course certificates | Two cases with diagrams |
| Website as a skill constellation | Website as two stories |

## Real-world examples

1. Recruiter clones the repo on a phone; `00-story.md` renders; they forward the link to the hiring manager.
2. You screen-share the 5-minute ShopEase deck; they interrupt at options — that is success.
3. You accidentally commit a NovaBank “sample” that still has real-looking account numbers — interview cancelled.

## Scenario / Use case: 5-minute vs 15-minute for the same NovaBank case

**Context.** Round 1: “Walk me through a project, five minutes.” Round 2 panel: “Fifteen minutes, then questions.”

**5-minute:** TAT 10 days → 34% incomplete files → checklist + SMS, gold loans out of scope → one SQL count → simulated 4-day complete-file TAT.

**15-minute:** Add stakeholder map (credit head vs core-banking freeze), assumption 92% mobile, UAT NRI prefix defect, CR for fraud cooling period, lesson: hybrid BRD + sprints.

**What goes wrong if ignored.** You use the 15-minute deck in round 1, get cut off at slide 4 (SDLC theory), and never reach the bottleneck. Matching time-box is a BA communication skill.

## Notes

- GitHub: markdown, images, sample data, no secrets, practice-case disclaimer.
- Website: hero, 2–3 cases, method, contact — GitHub can substitute.
- 5-minute = problem-evidence-recommendation; 15-minute = full BA thread.
- Never present ShopEase/NovaBank as employment.
- 
