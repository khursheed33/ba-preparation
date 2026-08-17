# Storytelling, Basic DAX, Performance, and Sharing Insights

## Definition

**Business storytelling** with data is a sequence: a question the business cares about, evidence that is trusted, an insight (what it means), and a recommendation (what to do). A dashboard without that sequence is a poster.

**DAX** (Data Analysis Expressions) is the formula language in Power BI / Excel Power Pivot for **measures** (and some calculated columns). A BA needs *literacy*: what SUM, DIVIDE, CALCULATE, and YTD *mean* for a KPI — not developer-level optimization.

**Dashboard performance** is how fast a report opens and filters. Slow reports do not get used.

**Sharing and presenting** means the right audience, the right grain, and a decision — not a 40-page PDF dump.

## Why it matters

MediCare+ can have a perfect no-show chart and still change nothing if the BA presents “interesting trends” instead of a process ask. NovaBank IT can reject a report that times out. ShopEase finance will not trust a measure they cannot explain. Story + simple measures + a usable file beat a clever model nobody opens.

## Story structure: question → evidence → insight → recommendation

| Step | Purpose | Example seed |
|---|---|---|
| Question | One decision | Why is specialist utilization down? |
| Evidence | Defined KPI, n, time, splits | No-show 18% (n=4,120) vs 11% last quarter; SMS reminder off for 2 clinics |
| Insight | Mechanism | Patients who get SMS 24h prior no-show 9%; no SMS 24% |
| Recommendation | Owner + action | Turn SMS on; overbook rule for high no-show slots; measure in 4 weeks |

Do not start with the chart type. Start with the decision.

### Weak vs strong

| Weak | Strong |
|---|---|
| Here are 12 slicers. | Question on slide 1; one chart; ask. |
| CALCULATE magic nobody can explain. | DIVIDE(no_shows, bookings) with a written definition. |
| 30 visuals on one page. | 6 visuals, aggregations pre-summarized. |
| Same deck for CIO and clinic admin. | Ops: exception list. IT: refresh, security, model. |

## Basic DAX / calculated measures (BA level)

Think in **measures** (recalculate with filters) not in copied Excel columns for every KPI.

| Pattern | Idea | Sketch |
|---|---|---|
| SUM | Add a numeric column | `Total GMV = SUM( fact_orders[gmv] )` |
| DIVIDE | Safe ratio (handles divide-by-zero) | `Conversion = DIVIDE( [Orders], [Checkouts] )` |
| CALCULATE | Change the filter context | `GMV LY = CALCULATE( [Total GMV], SAMEPERIODLASTYEAR( dim_date[Date] ) )` |
| YTD | Year-to-date using a date table | `GMV YTD = TOTALYTD( [Total GMV], dim_date[Date] )` |

**BA rules of thumb**

- Prefer `DIVIDE(num, den)` over `/` so blank denominators do not explode.
- `CALCULATE` is “this metric, but with a different filter” (paid only, last year, excluding cancelled).
- YTD is wrong without a proper **date dimension** marked as a date table.
- Distinct counts (`DISTINCTCOUNT`) are expensive and also *definitions* (unique users vs unique orders).

You specify the **business formula**; the BI developer writes production DAX. You must still be able to explain the formula in a workshop.

## Dashboard performance basics

| Cause | What the user feels | BA / design fix |
|---|---|---|
| Too many visuals per page | Spinning every slicer | One question; split pages |
| High cardinality in slicers (every order_id) | Slicer hangs | Do not put fact IDs in slicers; use drill-through |
| DISTINCTCOUNT on huge IDs | Slow cards | Pre-aggregate; or accept approximate for ops |
| Bidirectional filters everywhere | Wrong *and* slow | Star schema, single direction |
| Import of unused columns / tick-level GPS | Huge model | Aggregate pings; don’t plot every ping on exec page |
| Live DirectQuery on busy OLTP | Timeouts | Warehouse / import schedule |

**High cardinality** = many unique values (millions of order IDs, rider pings, claim notes). Fine in a fact table; painful as a slicer or as a visual that draws every point.

## Sharing and presenting: business vs IT

| Audience | They need | You bring |
|---|---|---|
| Business (ops, product, clinic head) | Decision, money, risk, next action | Story, KPI vs target, 1–2 options, owner |
| IT / data | Trust, security, refresh, lineage | Source, grain, RLS (who may see PHI), SLA |
| Mixed steering | Both, in that order | 10-min story then 5-min “how the number is built” |

Workspace / sharing (conceptual): app for consumers, workspace for authors, row-level security for NovaBank branch and MediCare+ clinic. Never email a CSV of patient names “for convenience.”

## Real-world examples

**ShopEase.** YTD GMV measure vs finance ledger; BA presents gap as *definition* (cancelled included?) before arguing performance of marketing.

**SaaS.** Churn DAX: cancelled in month / starting logos. Present to CS as playbook, to IT as “event date vs invoice date.”

**Travel.** On-time departure looks good until CALCULATE accidentally includes cancelled flights in the denominator.

## Scenario / Use case: MediCare+ no-show dashboard gets a process change

**Context.** Specialists complain of empty slots. Admin wants a “no-show dashboard.” IT built 14 visuals. Nobody changed booking rules.

**Story the BA presents (20 minutes).**

1. **Question.** Should we change reminder and overbooking policy for cardiology and ortho?
2. **Evidence.** No-show 18% overall; cardiology 26%; patients with SMS 24h prior 9% vs 24% without (n shown). Monday 9 a.m. slots worst. Data: appointments fact, last 12 weeks, exclude cancelled-by-clinic.
3. **Insight.** The gap is process (reminders off in 2 clinics after an SMS vendor change) plus no overbook on historically empty slots — not “patients are careless.”
4. **Recommendation.** Re-enable SMS (ops owner, this week). Pilot overbook +1 on Monday 9 a.m. cardio for 4 weeks. KPI: utilization and wait time; stop if wait median > 20 min. Privacy: dashboard is clinic-scoped (RLS).

**DAX the BA asked for:** `NoShow% = DIVIDE( [NoShow Count], [Booked Count] )` and `NoShow% SMS = CALCULATE( [NoShow%], dim_touch[sms_24h] = "Y" )`.

**Performance:** dropped the visual of every patient name on the exec page; names only on a drill-through with access control.

**Outcome.** Steering approves the SMS restore and the 4-week pilot. That is success — not “dashboard signed off.”

## Notes

- Story: question → evidence → insight → recommendation.
- DAX literacy: SUM, DIVIDE, CALCULATE, YTD idea — you own the formula, not the engine internals.
- DIVIDE protects ratios; CALCULATE changes filters; YTD needs a date table.
- Performance: fewer visuals, no high-cardinality slicers, star schema.
- Present outcomes to business, lineage and security to IT.
- Sharing is an access requirement (PHI, branch, seller data).
- A dashboard that does not change a process is incomplete work.
- Put n and definition on the slide; trust dies in the footnote you omitted.
