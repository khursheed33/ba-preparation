# Dashboards, KPIs, and Business Reporting

## Definition

A **KPI** is a defined metric tied to a goal (not any number that is easy to count). A **dashboard** is a one-screen set of KPIs and charts for a decision cadence (daily ops, weekly product). **Business reporting** is the narrative: what changed, why it might have, what to do. **Interpretation** is reading the number in context — mix, seasonality, definition — without pretending you are a data scientist.

A BA often *assembles* the weekly ops view from exports. You are not replacing BI.

## Why it matters

"Sales are down" is not a finding. A BA who can show traffic vs conversion vs AOV vs mix stops the room from fixing the wrong thing.

## KPI examples (define, then calculate)

| KPI | Definition (write this on the sheet) | Excel sketch |
|---|---|---|
| Conversion | Orders / Sessions | `=Orders/Sessions` |
| AOV | GMV / Delivered orders | `=SUMIFS(GMV,Status,"Delivered")/COUNTIF(Status,"Delivered")` |
| NPS proxy | (Promoters − Detractors) / Responses | CSAT 9–10 vs 0–6 if true NPS absent |
| TAT | Median or average working days start→done | `=AVERAGE(TATDays)` + show median if skewed |
| First-contact resolution | Tickets closed on first touch / tickets | `=COUNTIF(FCR,"Y")/COUNTA(TicketId)` |
| Return rate | Returned orders / Delivered orders | `=COUNTIF(Status,"Returned")/COUNTIF(Status,"Delivered")` |
| Late % | Late orders / orders | COUNTIFS (see formulas file) |

Put **period**, **filter** (Android / iOS), and **source file name** next to each KPI. A number without those is not a KPI; it is a rumour.

## How a BA presents a weekly ops report

You are not a data analyst. You are the person who:

1. Agrees definitions with the PO/ops (one page).
2. Pulls the same export every Monday.
3. Refreshes a dashboard sheet (KPIs on top, 3–5 charts, a table of exceptions).
4. Writes **5–8 lines**: what moved, where, what is unknown, what decision is needed.
5. Brings 10 sample rows for any surprising metric.

Structure of the spoken update:

- Headline: "Delivered GMV −6% WoW; traffic flat; Android conversion −1.8 pp."
- Evidence: dashboard, not a tour of 12 pivots.
- Ask: "Do we open a defect on Android checkout or wait for campaign mix?"

Do not present 40 charts. Do not hide the definition in a footnote you skip.

## Misinterpretation traps

| Trap | Example | BA habit |
|---|---|---|
| Correlation as cause | NPS down when GMV down | List other changes (app release, rain, price) |
| Mix effect | AOV up because cheap SKUs stocked out | Show AOV by category, not only total |
| Denominator change | Conversion "up" because bot traffic dropped | Sessions definition |
| Seasonality | Monday always lower than Friday | WoW + vs last year if you have it |
| Survivorship | TAT only on closed tickets | Also show open aging |
| Small N | 3 NPS responses | Show sample size |
| Target without baseline | "2% conversion is bad" | vs last 8 weeks and vs iOS |

## Real-world examples

1. **NovaBank** FCR dashboard: volume up, FCR down — mix shift to dispute tickets, not "agents got worse".
2. **QuickBite** late %: city mix — more orders from a slow city raises the national %.

## Scenario / Use case

ShopEase weekly: "sales down." Marketing wants a sale. Tech wants a war-room.

BA dashboard (Excel, one screen):

| KPI | This week | Last week | Note |
|---|---|---|---|
| Sessions | 1.02M | 1.00M | Traffic OK |
| Conversion (all) | 2.1% | 2.6% | Down |
| Conversion iOS | 2.8% | 2.9% | Flat |
| Conversion Android | 1.6% | 2.4% | Driver |
| AOV | ₹1,140 | ₹1,120 | Not the issue |
| Return rate | 8.1% | 8.0% | Flat |

Line: conversion by day, Android vs iOS. The drop starts the day after Android build `26.08.12`.

Interpretation: do **not** conclude "Android users are poorer." Conclude "Android conversion broke; iOS and traffic did not." Next: Jira bug with the build id, checkout funnel sample of 20 failed pays, not a sitewide discount.

## Weak vs strong

| Weak | Strong |
|---|---|
| 20 KPIs, no owner | 5 KPIs, each with a decision |
| "Sales down" | Traffic vs conversion vs AOV vs mix |
| Dashboard with no date | "Week of 11-Aug-2026, IST" |
| Pie of everything | One headline chart |
| BA invents causality | "Started after build X; cause TBC" |
| Hide sample size | n = 18 NPS is labelled |

## Notes

- Write the KPI formula in a cell comment or a Definitions tab — interviews and audits ask.
- A BA report ends with an ask (investigate, accept, change requirement).
- If BI (Power BI) exists, do not shadow it with a conflicting Excel number.
- Colour: red/green vs last week is fine; do not RAG 30 metrics.
- Screenshot the dashboard into Confluence with the file link; do not only email.
- When mix might explain a KPI, show a simple two-row split (Android/iOS, city, category).
- You can be wrong about cause; you should not be wrong about arithmetic and filters.
