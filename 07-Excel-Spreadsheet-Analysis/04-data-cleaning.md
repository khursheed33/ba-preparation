# Data Cleaning and Transformation

## Definition

**Data cleaning** fixes values so they mean one thing: no stray spaces, one code per city, one row per entity. **Duplicate detection** finds repeated keys (or repeated people). **Missing data** is blanks that should not be blank. **Transformation** is reshaping: split, combine, recode (`MH` → `Maharashtra`), types (text → date).

Cleaning is BA work when you are validating a report, building a sample, or reconciling files. It is not optional "admin".

## Why it matters

Pivots and SQL both fail silently on `Pune ` vs `Pune`. MediCare+ duplicate phones can merge two patients. A BA who publishes uncleaned extracts will defend the wrong KPI.

## Duplicate detection

Excel: Data → Remove Duplicates (destructive — copy sheet first). Safer: flag, then decide.

```excel
=COUNTIF(Patients[Phone],[@Phone])>1
=COUNTIFS(Patients[Phone],[@Phone],Patients[UHID],[@UHID])>1
```

First occurrence vs later:

```excel
=COUNTIF($D$2:D2,D2)>1
```

Business rule first: is duplicate **phone** allowed (family sharing) or duplicate **UHID** (never)? Do not delete until the rule is written.

## Missing data

```excel
=IF([@UHID]="","Missing UHID","OK")
=COUNTA(Patients[UHID])/COUNTA(Patients[RowId])
```

Conditional format blanks on UHID and phone. Missing is not always "fill from another row" — sometimes it is a source-system defect to log.

## Core transforms

| Problem | Formula / action |
|---|---|
| Extra spaces | `=TRIM(CLEAN(A2))` |
| Wrong case | `=PROPER(B2)` for names; `=UPPER` for state codes |
| City + state in one cell | Text to Columns, or `=TEXTBEFORE(A2,",")` / `=TEXTAFTER(A2,",")` |
| `MH` vs `Maharashtra` | Lookup table `CodeMap` + XLOOKUP |
| Mixed dates | `=DATEVALUE(A2)` if Excel sees text; else re-import CSV |
| Numbers stored as text | `=VALUE(A2)` or multiply by 1 |
| Remove duplicates | Flag → review → Remove Duplicates on the **business key** |
| Inconsistent codes | Never find-replace globally without a map; `MH` inside a name can break |

State standardisation:

```excel
=XLOOKUP(UPPER(TRIM([@StateRaw])),CodeMap[Code],CodeMap[StateName],
  XLOOKUP(LOWER(TRIM([@StateRaw])),CodeMap[Alias],CodeMap[StateName],"UNMAPPED"))
```

Keep `UNMAPPED` visible. That is a BA finding.

Split `First Last`:

```excel
=TEXTBEFORE(TRIM([@Name])," ")
=TEXTAFTER(TRIM([@Name])," ",-1)
```

(Older Excel: `LEFT`/`RIGHT`/`FIND`.)

## Real-world examples

1. **ShopEase** seller city: `BOM`, `Mumbai`, `mumbai `. Map to `Mumbai` before "GMV by city".
2. **NovaBank** CIF export: leading zeros stripped. Re-import the column as Text; do not "clean" by making them numbers.

## Scenario / Use case

MediCare+ sends `patients_export.csv` for a reminder-campaign requirement. 8,400 rows.

Findings:

| Check | Result |
|---|---|
| `TRIM` on phone | 120 phones had spaces / `+91` mix |
| Duplicate phone, different UHID | 34 pairs — possible family or dirty data |
| Duplicate UHID | 11 rows — true duplicates; keep latest `updated_on` |
| Blank UHID | 27 rows — cannot send clinical SMS; exclude and raise defect |
| Name case | `PROPER` for display only; keep raw for matching |

BA actions:

1. Sheet `raw` untouched.
2. `clean`: TRIM phones to 10 digits:

```excel
=RIGHT(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE([@PhoneRaw]," ",""),"+91",""),"-",""),10)
```

3. Flag dup phones and dup UHID with COUNTIF.
4. Filter blank UHID → Jira bug "Export omits UHID for walk-in registrations".
5. Campaign file = unique UHID, non-blank, valid 10-digit phone. Duplicate phones listed for ops, not auto-merged.

Requirement validated: "reminders need UHID + phone". Data shows 27 patients would be dropped — product must capture UHID at registration.

## Weak vs strong

| Weak | Strong |
|---|---|
| Remove Duplicates on whole row | Define the key (UHID vs phone) |
| Fill missing UHID with "NA" | Leave blank; count; raise a defect |
| Find-replace `MH` everywhere | Mapping table + UNMAPPED |
| Clean on the only copy | `raw` / `clean` / `exclude` |
| Assume duplicate phone = duplicate person | Business rule + SME |
| Hide messy rows | Document exclusion count in Notes |

## Notes

- Cleaning without a written rule is editing fiction. Write "phone is not a unique patient key".
- `CLEAN` removes non-printing characters from CSVs; use with `TRIM`.
- Never "fix" production by Excel and upload unless ops owns that process.
- Split columns only when the delimiter is reliable; some addresses have extra commas.
- Keep an exclusion log: row id, reason, count — that is UAT evidence.
- Inconsistent codes are a requirements issue (pick-lists) as much as an Excel issue.
- After clean, spot-check 10 rows against the source system, not only against the CSV.
