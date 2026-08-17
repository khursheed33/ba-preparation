# AI for Process, Data, SQL, and Dashboards

## Definition

Using generative AI to **draft** process questions, interpret tables, suggest SQL, and narrate dashboard insights — then **verifying** every number and join on real data you are allowed to use.

This is assistance, not automated analysis. The warehouse, CIF, and EMR do not live inside the model.

## Why it matters

A BA who can move from a messy pivot to a question, a query, and a recommendation is valuable. A BA who pastes unverified SQL into production is a risk incident.

**Never run unverified SQL on production.** Draft in a sandbox or against a snapshot. Read the plan. Check counts. Get a DBA/data-owner OK for anything that writes or scans huge tables.

## Process analysis with AI

Use AI to draft **As-Is questions**, not the As-Is itself.

**Prompt:** “I am mapping ShopEase returns. Generate 15 questions for warehouse QC and seller ops. Cover start/end, wait states, exceptions, systems, SLAs.”

You still sit with QC. AI has never seen their exception “box torn but item unused.”

## Data analysis with AI

Paste a **small aggregated** pivot (not raw PII) and ask: “What cuts are missing? What could explain this without jumping to a solution?”

**ShopEase pivot (illustrative):** return cycle time 9 days; by reason, Size = 6.2 days, Damaged = 11 days.

AI might say “focus on Damaged.” Critical thinking: Size is 70% of volume — auto-approve Size may move the average more. **You** do the volume × time math.

## SQL assistance

Workflow: **draft SQL → explain it back in English → run on non-prod → compare counts to a known total → then maybe prod read replica if policy allows.**

**Never:** `UPDATE`, `DELETE`, or unscoped `SELECT *` on prod because the model said so.

### Weak vs strong

| Weak | Strong |
|---|---|
| Run AI SQL on prod “just this once” | Sandbox + COUNT checks vs known application volume |
| Trust JOIN because it “looks right” | State grain (one row per loan? per customer?) before joining |
| Dashboard story from AI with no filter check | Re-read slicers, date range, and excluded statuses |

## Dashboard insight generation

Ask: “Given this screenshot description, what 3 questions should a BA ask before recommending?” Not: “Write the insight as if it is fact.”

One insight structure: **question → evidence (chart/query) → recommendation → caveat.**

## Real-world examples

1. **ShopEase.** AI interprets “returns up 20%” as quality failure. BA checks: GMV up 25% — rate is flat. Insight dies; no false “QC crisis.”
2. **MediCare+.** AI drafts SQL joining appointments to SMS logs. It uses `patient_name`. BA strips PII, joins on `appointment_id`, filters `consent_sms = 1`.
3. **QuickBite.** AI says “compensate all late orders.” Pivot shows kitchen-caused delay is 70%. Recommendation changes.

## Scenario / Use case: NovaBank BA drafts a JOIN, then validates counts

**Context.** Product claims 34% of personal-loan applications stall on documents. A dashboard shows “pending” but mixes salaried web and gold loans. You need a clean count for the BRD.

**Stakeholders.** Digital PO, credit ops, data team, BA, info-sec (query access).

**What the BA does.**

1. Write the question in English: “Of salaried personal-loan applications started on web in Jun, how many sat in DOCUMENTS_PENDING > 48 hours at least once?”
2. Ask AI for a JOIN sketch: `applications` ⋈ `status_history` ⋈ `product`.
3. **Think aloud on grain:** `status_history` is multiple rows per application. A bad JOIN explodes the count.
4. AI draft (logical):

```sql
-- DRAFT ONLY — run on sandbox, not prod
SELECT COUNT(DISTINCT a.application_id) AS stalled_apps
FROM sandbox.applications a
JOIN sandbox.product p ON p.product_id = a.product_id
JOIN sandbox.status_history h ON h.application_id = a.application_id
WHERE p.code = 'PL_SALARIED_WEB'
  AND a.started_at >= '2026-06-01' AND a.started_at < '2026-07-01'
  AND h.status = 'DOCUMENTS_PENDING'
  AND h.hours_in_status > 48;
```

5. **Validate:**  
   - Count distinct applications in June (denominator) vs ops’ known 12,400. If SQL says 80,000, the JOIN duplicated.  
   - Spot-check 10 IDs in the UI.  
   - Confirm gold loans excluded.  
6. Only then put 34% in the problem statement, with query ID and date.

**What goes wrong if ignored.** AI uses `COUNT(*)` on the history table. You publish 140% stall rate. Credit head stops trusting BA numbers. Or someone runs the draft on prod and locks `status_history`.

**Dashboard follow-on.** AI caption: “Documents are the problem.” BA adds: “Among stalled, missing PAN vs salary slip split still unknown — next query.” Insight stays honest.

## Notes

- Draft As-Is *questions* with AI; draft As-Is *maps* with people and timestamps.
- Interpret pivots with volume, not only the reddest cell.
- SQL assistance ends at a sandbox and a count check; production is not a playground.
- Dashboard text is a hypothesis until filters and grain are verified.
- Never paste raw customer rows into a public model.
- 
