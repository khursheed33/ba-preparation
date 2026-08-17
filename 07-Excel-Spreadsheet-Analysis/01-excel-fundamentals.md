# Excel Fundamentals for Business Analysts

## Definition

Excel is a grid of **cells** (column letter + row number, e.g. `B2`) used to store, format, and calculate tabular data. **Data entry** is putting values in correctly. **Data formatting** is how those values display (dates, currency, headers) without changing the true value. A **named range** is a human name (`RefundWindowDays`) that points to a cell or block so formulas stay readable.

A BA uses Excel as a scratchpad for trackers, samples, and recon — not as the system of record.

## Why it matters

Stakeholders send you CSVs and "the list". If you cannot enter, format, freeze, and name ranges, you cannot clean ShopEase seller data or build a requirement tracker the PO will trust.

## BA uses of Excel

| Use | Example | What good looks like |
|---|---|---|
| Requirement tracker | Story id, MoSCoW, status, owner | One row per requirement; no merged cells in the data block |
| Data samples | 20 ShopEase orders for AC | Realistic, masked PII |
| Recon | Payment file vs order GMV | Totals at the top; source timestamps |
| Stakeholder list | Name, role, RACI, contact | Filterable table |
| UAT log | Case, result, defect id | Status validation list |
| Assumption log | ID, statement, impact | Dates as dates, not text |

Do not keep the live product backlog only in Excel if Jira exists. Excel is for analysis and workshops.

## Data entry

- One header row. No blank rows inside the dataset.
- Dates via `Ctrl+;` or `YYYY-MM-DD`, then format. Do not type `12/3` if the file will be shared US/UK.
- Numbers as numbers. `₹1,200` typed as text will break `SUM`.
- IDs as text if they have leading zeros (`00182`) — format the column as Text **before** paste, or prefix `'` .
- Never merge cells in a data range. Merge only in a title row above the table.

Named range example: select `C2`, Formulas → Define Name → `GstRate`. Formula:

```excel
=B2*(1+GstRate)
```

Name a block `SellerList` for `A2:A500` so Data Validation can use `=SellerList`.

## Formatting for readability

| Need | How |
|---|---|
| Header row | Bold, fill, wrap text, filter on |
| Freeze | View → Freeze Panes on `A2` so headers stay |
| Numbers | `#,##0` for counts; `#,##0.00` for money; `%` for rates |
| Dates | `DD-MMM-YYYY` for mixed-region teams |
| IDs | Text format; left aligned |
| Print / PDF | Print titles = header row; fit width |
| Colour | One meaning (e.g. red = missing). Not rainbow. |

Number formats do not change the stored value. `12.6` shown as `13` still calculates as `12.6`.

## Real-world examples

1. **NovaBank** stakeholder sheet: freeze header, named range `BusinessOwners` for a dropdown on the RACI tab.
2. **ShieldSure** claim sample: policy numbers stored as text so `0019` does not become `19`.

## Scenario / Use case

ShopEase sends `sellers_raw.xlsx`: merged title "SELLERS Q1", headers on row 3, city and state in one cell, GMV as `'₹ 12,400`, duplicate header in the middle, phone numbers as scientific notation.

BA cleanup before any analysis:

1. Copy to a new sheet `sellers_clean` (never overwrite the raw file).
2. Unmerge. Delete the title row or move it above row 1.
3. Promote a single header: `seller_id`, `name`, `city`, `state`, `phone`, `gmv`, `onboarded_on`.
4. Split city/state (Text to Columns or Power Query later).
5. `VALUE(SUBSTITUTE(SUBSTITUTE(F2,"₹",""),",",""))` for GMV.
6. Format `seller_id` and `phone` as Text; fix scientific phones by `TEXT` or re-import.
7. Freeze row 1. Name the GMV column range `SellerGmv`.
8. Only then sort, pivot, or send to SQL.

The BA reports "412 sellers, 9 with blank city" from the clean sheet. The raw file stays attached as evidence.

## Weak vs strong

| Weak | Strong |
|---|---|
| Typed `1200` as `'1200` randomly | Numbers numeric; IDs text by design |
| Merged data cells | One cell, one value |
| Header not frozen | Freeze + filter |
| `Sheet1` with no name | `raw` vs `clean` vs `recon` |
| `C2*1.18` magic number | Named range `GstRate` |
| Overwrite the vendor file | Archive raw; work on a copy |

## Notes

- Name workbooks by date and source: `SE_sellers_2026-08-17_clean.xlsx`.
- If Excel "helps" by converting `SEP-1` to a date, you have an ID problem — force Text.
- Named ranges should not include the header if you will `SUM` them.
- Colour is not data; if you need status, use a column, not only cell fill.
- Keep a `Notes` tab: source, extract time, known defects.
- Ctrl+Home should land on a useful corner; do not hide rows 1–20 of junk.
- Shared OneDrive files: one editor at a time for recon sheets, or you will get silent overwrites.
