# Descriptive Statistics and Metrics

## Definition

**Descriptive statistics** summarize a set of numbers so a human can see the pattern: typical value, spread, mix, and change over time. They describe what *did* happen. They do not, by themselves, prove *why*.

A BA uses them to size a problem, challenge a slogan, and define targets.

| Term | Meaning | BA use |
|---|---|---|
| Mean | Arithmetic average | Fine when the distribution is not skewed |
| Median | Middle value when sorted | Better for skewed money and time |
| Mode | Most frequent value | Common ticket size, common delay bucket |
| Percentage | Part / whole × 100 | Mix, conversion, SLA hit rate |
| Growth rate | Change vs a prior period | MoM, YoY, WoW |
| Ratio | One quantity divided by another | Orders per rider, claims per policy |
| Trend | Direction over time | Rising no-shows, falling AOV |
| Correlation | Two things move together | Clue, not proof of cause |

## Why it matters

Leaders quote “average.” Average hides the customer the process actually serves. NovaBank’s “average loan ticket” can look like a healthy SME book while 90% of files are tiny personal loans and a few corporate deals dominate the mean. QuickBite’s “average delivery time” can look fine while the median is acceptable and the tail (p95) is destroying ratings.

If you pick the wrong summary, you write the wrong requirement.

## Mean, median, mode — when median beats mean

Use **median** when the distribution is skewed or has outliers: loan ticket size, delivery time, claim amount, hospital bill, property price.

Use **mean** when values are similar and you care about the total divided by count (e.g. cost per order if you will actually pay the average).

Use **mode** when the business cares about the *most common* case (most frequent SKU size, most common appointment slot).

| Situation | Prefer | Why |
|---|---|---|
| NovaBank loan ticket (many small + few huge corporates) | Median + segment means | Mean is not a typical file |
| QuickBite delivery minutes | Median + p90/p95 | Mean hides late tail |
| ShopEase item quantity per order | Mode | Ops stocks the common case |
| MediCare+ wait time | Median | A few 3-hour waits wreck the mean |

### Weak vs strong

| Weak | Strong |
|---|---|
| Average delivery is 32 minutes. | Median 24 min; p90 51 min; 8% of orders > 60 min in rain zones. |
| Average ticket ₹18 lakh. | Median ticket ₹2.4 lakh; corporate (n=12) mean ₹4.1 cr. |
| Sales grew. | GMV +12% MoM; order count +3%; AOV +8.7%. |
| Ads and sales are correlated so ads work. | Correlation 0.62; also summer seasonality; run a geo holdout. |

## Percentage, growth rate, ratios, trends

**Percentage** = (part / whole) × 100. Always name the denominator. “Returns are 8%” of *orders* is different from 8% of *GMV*.

**Growth rate (simple)**

- Period growth = (new − old) / old
- MoM % = (this month − last month) / last month
- YoY % = (this month − same month last year) / same month last year

CAGR (when someone quotes multi-year growth): \(\text{CAGR} = (V_{end}/V_{start})^{1/n} - 1\).

**Conversion ratio** = desired actions / eligible opportunities.

| Ratio | Formula | Company |
|---|---|---|
| Checkout conversion | Orders / checkout starts | ShopEase |
| KYC pass rate | KYC approved / KYC started | NovaBank |
| Show-up rate | Arrived / booked | MediCare+ |
| On-time delivery | On-time orders / delivered orders | QuickBite |
| Claims acceptance | Paid claims / submitted claims | ShieldSure |

**Trends.** Plot the same definition over weeks. A one-week spike is noise until you know seasonality (payday, festivals, monsoon).

## Correlation basics — correlation ≠ causation

**Correlation** means two series move together (positive) or opposite (negative). It is a clue for investigation, not a requirement to “do more of X.”

Classic pattern: ice cream sales and drowning both rise in summer. Heat is the hidden driver. Ads and ShopEase sales both rise in Diwali. Season and promotions are confounders.

**BA example (ads vs sales).** ShopEase spends more on ads in weeks when it also runs 20% off. Sales rise. Marketing claims ads caused GMV. The BA splits weeks: promo-only, ads-only, both, neither. Promo explains more than ads. Requirement: measure incremental GMV with a holdout, not a correlation slide.

NovaBank: branches with more relationship managers have higher deposit growth. That may be because large branches get more RMs *and* already have richer catchments — not because “hire more RMs everywhere.”

## Real-world examples

**QuickBite.** Mean delivery 31 min looks on SLA. Median 22 min; mode 18 min; p95 64 min. The requirement is to cut the tail in rain and during restaurant prep delay, not to shave the mean by 1 minute.

**ShieldSure.** Mean claim paid looks stable. Median falls (many small cashless OPD) while a few large hospitalization claims hide in the mean. Reserving and fraud rules need segments.

**EdTech / SaaS.** Average session length is pulled by a few power users. Median session and % of students who return in 7 days are better product metrics.

## Scenario / Use case: NovaBank average ticket is misleading

**Context.** Credit leadership wants to “raise average ticket” as a growth KPI. The mean personal+SME+corporate blended ticket is ₹18.2 lakh, up 40% YoY. Sales is told to chase bigger files. Retail RM morale drops; they cannot produce corporate-sized tickets. Risk says concentration is rising.

**Facts the BA pulls.**

| Segment | Count | Mean ticket | Median ticket |
|---|---|---|---|
| Personal loans | 8,400 | ₹1.9 lakh | ₹1.6 lakh |
| SME | 620 | ₹42 lakh | ₹28 lakh |
| Corporate | 14 | ₹6.8 crore | ₹4.1 crore |
| Blended | 9,034 | ₹18.2 lakh | ₹1.7 lakh |

**What the BA does.**

1. Kill the blended mean as a steering KPI.
2. Set segment KPIs: median personal ticket, SME count, corporate pipeline *separately*.
3. Show that 14 corporate files moved the mean; retail volume is the franchise.
4. Write requirements for the MIS: filters for segment, and always show n, mean, median.

**If ignored.** RMs inflate ticket with weak large files; NPA risk rises; the “growth” KPI is an artifact of mix, not capability.

## Notes

- Always ask: mean of *what*, over *which population*, with *what n*.
- Median beats mean for money and time when a few giants exist.
- Name the denominator of every percentage.
- Growth rate without mix (price vs volume vs new users) is a slogan.
- Correlation is a prompt to find confounders (season, promo, mix).
- Trends need a stable definition; changing “on-time” mid-year fakes a trend.
- Mode is useful for ops design (what happens most).
- Report p90/p95 for SLAs; customers live in the tail.
