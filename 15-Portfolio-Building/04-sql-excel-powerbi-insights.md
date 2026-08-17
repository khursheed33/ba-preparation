# SQL, Excel, Power BI, and Business Insights

## Definition

In a BA portfolio, **SQL analysis**, **Excel analysis**, and **Power BI dashboards** exist to produce **business insights** — a recommendation a stakeholder could act on — not to prove you know COUNT(*).

## Why it matters

A chart without a question is decoration. One insight per artifact beats five unrelated visuals.

## One insight per artifact

Use the same four-line card on every analysis:

| Line | Meaning |
|---|---|
| Question | What decision this supports |
| Query / sheet | How you got the number (sandbox / sample) |
| Chart | What to look at |
| Recommendation | What to do — and what you still don’t know |

Do not mix ShopEase returns and NovaBank loans on one dashboard “to look busy.”

### Weak vs strong

| Weak | Strong |
|---|---|
| 12 slicers, no sentence | One chart, one sentence, one action |
| SQL dumped with no grain | “Grain: one row per return_id” |
| Insight = “sales are down” | “Size is 70% of volume; Damaged is slower but smaller — auto-approve Size first” |

## Sample ShopEase insight writeup

**Question.** Which return *reason* should phase 1 attack to cut average cycle time?

**Excel / SQL (illustrative, simulated sample n=500 prepaid returns).**

- Sheet `delay_by_reason`: columns reason, volume, avg_days, volume×days (delay hours proxy).
- SQL idea: `SELECT reason, COUNT(*) vol, AVG(cycle_days) FROM returns_sample WHERE prepaid=1 GROUP BY reason`.

**Chart (Power BI).** Clustered bar: volume vs avg days by reason. Caption: Size = 350 rows, 6.2 days; Damaged = 80 rows, 11.0 days.

**Insight.** Size contributes more total wait because of volume, even though Damaged is slower per case. Seller approval sits on Size today (2.1 days). Phase 1 auto-approve Size < ₹2,000 attacks the bigger bucket.

**Recommendation.** Do not start with a Damaged-photo epic. Sequence: Size auto-approve + status SMS; Damaged QC guidance in phase 2. **Caveat:** sample is simulated; validate on 90 days of warehouse data before baseline.

**What you would show in GitHub:** `insight-shopease-reason.md` + `delay_by_reason.xlsx` (fake IDs) + dashboard PNG + DAX/measure list (no prod connection strings).

## Real-world examples

1. **NovaBank.** Question: is TAT a bureau problem or a documents problem? SQL on `status_history` (sandbox) shows 34% of distinct apps idle in DOCUMENTS_PENDING > 48h. Recommendation: checklist before AI underwriting.
2. **MediCare+.** Excel pivot: no-shows by weekday and specialty. Insight: Monday 9 a.m. GPs, not “all clinics.” Recommendation: pilot reminders there first.
3. **QuickBite.** Power BI: late orders split kitchen vs rider. Insight: 70% kitchen. Recommendation: compensation engine scoped to rider-after-ready only.

## Scenario / Use case: interview live-task “read this dashboard”

**Context.** Panel shows your ShopEase PBIX screenshot with a red Damaged bar (11 days). They say, “So Damaged is the problem?”

**What you say.**

1. “Highest average is not highest impact.”
2. Point to volume.
3. Walk the insight card: question, sample, recommendation.
4. Offer the next query: leakage if Size is used to hide damage.

**What goes wrong if ignored.** You built a dashboard that *invites* the wrong conclusion. The BA job is the caption, not the red color.

## NovaBank companion card (same pattern)

**Question.** Is TAT a bureau problem or a documents problem?  
**Query.** `COUNT(DISTINCT application_id)` in DOCUMENTS_PENDING > 48h vs all June salaried-web apps (sandbox).  
**Chart.** Stacked bar of time-in-status.  
**Recommendation.** Completeness checklist before any AI underwriting epic. Caveat: gold loans must stay filtered out.

Put SQL, Excel, and Power BI in the *same case folder* as the process map so recruiters see one story.

## Notes

- One question, one query/sheet, one chart, one recommendation per artifact.
- Label simulated samples; never publish real customer rows.
- SQL/Excel/Power BI are evidence for the case story, not a separate “tech section” with no problem.
- Grain and filters belong in the writeup.
- 
