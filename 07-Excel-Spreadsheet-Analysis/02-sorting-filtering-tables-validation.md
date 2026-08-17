# Sorting, Filtering, Tables, Validation, and Conditional Formatting

## Definition

**Sorting** orders rows. **Filtering** hides rows that do not match. An **Excel Table** (`Ctrl+T`) is a named, expanding range with structured references. **Data validation** restricts what can be entered (lists, numbers, dates). **Conditional formatting** changes appearance from rules (SLA breach, blanks, duplicates).

These are how a BA makes a 5,000-row UAT log usable in a meeting.

## Why it matters

A range that looks like a table but is not will drop formulas when someone pastes row 5001. Unvalidated Status columns become `Open`, `open`, `WIP`, and your `COUNTIF` lies.

## Excel Tables vs ranges

| | Normal range | Excel Table |
|---|---|---|
| Name | `A1:G200` | `DefectLog` |
| New row | You must extend formulas | Auto-expands |
| Formulas | `=SUM(G2:G200)` | `=SUM(DefectLog[AgeDays])` |
| Filter / sort | Manual | Built-in |
| Charts / pivots | Break when rows added | Source can be the table |

Always convert analysis data to a Table. Keep a raw sheet as a range if you must, then Table the clean sheet.

Structured reference examples:

```excel
=COUNTIF(DefectLog[Status],"Open")
=[@OpenedOn]          @ means this row
=DefectLog[[#Headers],[Severity]]
```

## Sorting and filtering

- Sort by **Severity** then **OpenedOn** — Data → Sort, two levels.
- Filter: Status = Open, Severity = Sev1.
- Do not sort a single column only (that shreds row integrity). Select the table; Excel Tables prevent this.
- Custom list sort: MoSCoW order Must → Should → Could → Won't (File → Options → Advanced → Custom Lists, or sort by a helper rank).

Helper for MoSCoW rank:

```excel
=SWITCH([@MoSCoW],"Must",1,"Should",2,"Could",3,"Won't",4,9)
```

## Validation lists for status, priority, MoSCoW

Create a sheet `Lists`:

| A (Status) | B (Priority) | C (MoSCoW) |
|---|---|---|
| Open | Sev1 | Must |
| In Progress | Sev2 | Should |
| Fixed | Sev3 | Could |
| Retest | Sev4 | Won't |
| Closed |  |  |
| Cannot Reproduce |  |  |

Name ranges `StatusList`, `PriorityList`, `MoscowList`. On the log:

Data → Data Validation → List → `=StatusList`

Also useful: whole-number Age ≥ 0; date OpenedOn ≤ TODAY(); `seller_id` length = 6 using custom formula:

```excel
=LEN(A2)=6
```

Invalid entries should **Stop**, not Warning, on UAT logs.

## Conditional formatting

| Rule | Formula (applies to table column) | Meaning |
|---|---|---|
| Blank owner | `=AND($E2="",$C2="Open")` | Open defect, no owner |
| Duplicate ticket id | Home → Conditional Formatting → Duplicate Values on `Key` | Paste error |
| SLA breach Sev1 open > 2 days | see below | War-room red |
| Status = Open | Text that contains `Open` | Optional; prefer formula so Closed is not red |

Sev1 open more than 2 days (row 2 is first data row; column C = Severity, D = Status, B = OpenedOn):

```excel
=AND($C2="Sev1",$D2="Open",TODAY()-$B2>2)
```

Format: red fill. Use `NETWORKDAYS` if SLA is business days:

```excel
=AND($C2="Sev1",$D2="Open",NETWORKDAYS($B2,TODAY())>2)
```

## Real-world examples

1. **ShopEase** backlog Excel for a workshop: Table + MoSCoW validation so marketing cannot type `asap`.
2. **MediCare+** appointment export: filter `status = No-show`, sort by clinic, conditional format blank UHID.

## Scenario / Use case

NovaBank UAT for cards: 180-row defect log in email. The BA pastes into `DefectLog` Table, applies Status/Severity lists, and this rule:

```excel
=AND([@Severity]="Sev1",[@Status]="Open",TODAY()-[@OpenedOn]>2)
```

Filter: Severity Sev1, Status Open. Three rows light up red, all opened 4–6 days ago, all assigned to "TBD". In the war-room the BA does not say "UAT is messy". She says "three Sev1 open beyond 2-day SLA; keys NB-UAT-12, 19, 41." PO reassigns before go-live talk continues.

A fourth row was `Sev 1` with a space — validation later blocks that. Until then, a TRIM helper column saved it:

```excel
=TRIM([@Severity])
```

## Weak vs strong

| Weak | Strong |
|---|---|
| Sort one column | Sort the Table |
| Status typed freely | Validation list |
| Pink rows "because important" | Rule: Sev1 + Open + age |
| Range `A1:G999` with empty tail | Table that grows |
| Filter forgotten on, sent as PDF | Clear filter; state the filter in the email |
| Duplicates found by eye | Duplicate-values rule on Key |

## Notes

- Convert to Table before you write `SUMIF`, or you will forget to extend ranges.
- Validation does not fix old bad data; clean first, then lock the list.
- Conditional formatting is a signal, not a data column — still keep `AgeDays` as a value.
- `TODAY()` in SLA rules makes screenshots date-sensitive; record "as of 17-Aug-2026".
- Custom sort lists must be on the machine or in the workbook's custom lists — document them.
- Do not filter and then delete "hidden" rows without checking; you may delete the rest of the universe.
- One Table per sheet for UAT logs; extra calculations go to the right or a summary sheet.
