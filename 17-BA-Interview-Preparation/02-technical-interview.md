# Technical Interview (Excel, SQL, Power BI, Jira, Process, Data)

## Definition

A **technical BA interview** tests whether you can **think aloud** on **Excel**, **SQL**, **Power BI**, **Jira**, **process modeling**, and **data analysis** — often with a mini live task, not a certification quiz.

## Why it matters

You will not be hired as a DBA. You *will* be asked to COUNTIFS a stall, explain a JOIN, read a dashboard, and write a story in Jira language.

## How to think aloud (all areas)

1. Restate the question. 2. Name grain/filters. 3. Attempt. 4. Say what you would verify. 5. Caveat.

### Weak vs strong

| Weak | Strong |
|---|---|
| Silent typing | “Grain is application_id; I need DISTINCT” |
| Perfect syntax, wrong question | Right question, messy syntax, then fix |

---

## Excel (4–6)

**Q1. COUNTIFS?** Think: criteria pairs. Live: count ShopEase returns with reason Size and amount < 2000: `=COUNTIFS(C:C,"Size",D:D,"<2000")`.

**Q2. Pivot?** I would put reason in rows, cycle_days in values (average), and volume as COUNT to avoid the “Damaged is worse so it is the problem” trap.

**Q3. VLOOKUP vs XLOOKUP?** I say XLOOKUP if available; otherwise VLOOKUP with false match. Watch duplicate keys (two rows per order).

**Q4. Data quality?** I scan blanks, duplicates, date formats before any insight. NovaBank mobile prefixes (`+91` vs `00`) broke UAT in my case notes.

**Q5. Nested IF vs helper column?** I prefer a helper `AutoApproveFlag` so QC can audit the rule.

**Q6. Live task:** “Flag rows eligible for auto-approve.” I write the boolean column, then COUNTIF the TRUE, then spot-check 5 rows.

---

## SQL (4–6)

**Q1. LEFT JOIN?** “All left rows, matching right or NULL.” NovaBank: all June apps LEFT JOIN bureau so I still see apps with no pull.

**Q2. INNER vs LEFT?** INNER drops apps with no bureau row — that can hide the problem.

**Q3. GROUP BY / HAVING?** Volume by status; `HAVING COUNT(*) > 100` to ignore tiny buckets.

**Q4. DISTINCT vs COUNT(*)?** Status history explodes rows; I `COUNT(DISTINCT application_id)`.

**Q5. WHERE vs ON?** Filter on the many-side in JOIN carefully or you turn a LEFT into an INNER.

**Q6. Live:** Draft JOIN for stalled docs, say “sandbox only,” validate against known 12,400 monthly apps.

Never: run unverified SQL on production.

---

## Power BI (4–6)

**Q1. Fact vs dimension?** Returns fact; reason and seller dimensions. Wrong model double-counts.

**Q2. Filter context?** “Does this card respect the date slicer?” I check.

**Q3. Measure vs calculated column?** Measure for ratios (no-show %); column for static buckets.

**Q4. How do you read this dashboard?** Title, slicers, grain, then the claim. ShopEase: I challenge the reddest bar with volume.

**Q5. Row-level security / PII?** I would not publish patient names on a BA portfolio dashboard.

**Q6. Live:** “What question does this chart answer?” If none, it is decoration.

---

## Jira (4–6)

**Q1. Epic vs story vs task?** Epic = ShopEase auto-approve; story = SMS status; task = copy from legal.

**Q2. Good story?** Role, outcome, AC, out-of-scope note.

**Q3. Story points?** I explain relative size; I do not pretend I ran Scrum as SM.

**Q4. Workflow?** To Do → In Dev → QA → UAT → Done. I do not move to Done without AC.

**Q5. Traceability in Jira?** FR-ID in description; link to Confluence rule table.

**Q6. Live:** Write one story with AC for NovaBank “save draft application.”

---

## Process modeling (4–6)

**Q1. BPMN vs flowchart?** I use BPMN if the team knows gateways; else a clear flowchart with actors.

**Q2. As-Is mistake?** Modeling the hoped process. I timestamp waits.

**Q3. Gateway?** ShopEase diamond: Size AND <2000 AND prepaid → auto-approve else seller.

**Q4. Swimlanes?** Buyer, seller, QC, payments — so handoffs show.

**Q5. When not to model?** If the question is a data definition, I use a table first.

**Q6. Live:** Draw To-Be in 8 boxes + 1 exception (QC fail).

---

## Data analysis (4–6)

**Q1. First step?** Question and grain. “Late orders” is not a question.

**Q2. Average trap?** Size vs Damaged: volume × time.

**Q3. Correlation vs cause?** Monday no-shows: reminder *or* slot mix — I would test.

**Q4. Sample vs population?** I labelled ShopEase n=500 as simulated sample.

**Q5. Conflicting sources?** Dashboard 34% vs ops 28% — I reconcile filters (gold loans in/out).

**Q6. Live:** Given a pivot, speak one insight and one next query.

## Real-world examples

- NovaBank JOIN without DISTINCT → 140% stall rate — they love this story.
- Excel COUNTIFS missed a space in “Size ” — data quality.

## Scenario / Use case: 20-minute mixed live task

**Context.** They share a CSV of 200 ShopEase returns and a blank Jira story.

**What you do.** Clean → COUNTIFS eligible rows → one sentence insight → draw a 6-step To-Be → write the story + AC. Say assumptions out loud.

**What goes wrong if ignored.** You jump to a dashboard screenshot from home and cannot COUNTIFS on their laptop.

## Notes

- Think aloud: grain, filters, verify, caveat.
- Excel COUNTIFS, SQL LEFT JOIN + DISTINCT, Power BI slicers, Jira AC, process exception, insight vs decoration.
- Mini tasks: flag rows, explain JOIN, read a chart, write a story, sketch To-Be.
- No unverified production SQL.
- 
