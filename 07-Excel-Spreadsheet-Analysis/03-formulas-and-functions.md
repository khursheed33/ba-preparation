# Formulas and Functions for Business Analysts

## Definition

A **formula** starts with `=` and calculates from cells. **Logical** functions return TRUE/FALSE or branch (`IF`, `AND`, `OR`). **Lookups** fetch a value from another table (`XLOOKUP`, `VLOOKUP`, `INDEX`/`MATCH`). **Text** functions parse IDs and names. **Date** functions measure aging and TAT. **Statistical** functions count and average. **Error handling** (`IFERROR`, `IFNA`) stops `#N/A` from breaking a tracker.

You do not need every Excel function. You need the set below, written against a business question.

## Why it matters

BAs answer "how old is this refund?" and "% late in Pune?" before SQL access exists. Wrong `IF` logic becomes a wrong go-live slide.

## Must-know formulas (with business questions)

Assume a Table `Orders` unless noted.

### Logical: IF, AND, OR

ShopEase: refund still inside 7-day window?

```excel
=IF(AND(TODAY()-[@DeliveredOn]<=7,[@Status]="Delivered"),"Eligible","Not eligible")
```

NovaBank: KYC can auto-pass?

```excel
=IF(OR([@RiskBand]="Low",AND([@DocScore]>=80,[@Liveness]="Pass")),"Auto","Manual")
```

### Error handling: IFERROR / IFNA

```excel
=IFERROR(XLOOKUP([@City],Rate[City],Rate[Fee]),"No rate")
=IFNA(VLOOKUP([@Sku],SkuMap!A:B,2,FALSE),"Unmapped SKU")
```

### Lookups: XLOOKUP, VLOOKUP, INDEX/MATCH

Prefer `XLOOKUP` (Excel 365). `VLOOKUP` needs the key in the left column.

```excel
=XLOOKUP([@SellerId],Sellers[SellerId],Sellers[City],"Missing seller",0)
=VLOOKUP([@SellerId],Sellers!A:D,3,FALSE)
=INDEX(Sellers[City],MATCH([@SellerId],Sellers[SellerId],0))
```

Business question: "What city is this order's seller in?" — lookup, do not type it again.

### Text: LEFT, RIGHT, MID, TRIM, TEXT

MediCare+ UHID `MC-2026-00881`:

```excel
=TRIM(A2)
=LEFT([@UHID],2)              → MC
=MID([@UHID],4,4)             → 2026
=RIGHT([@UHID],5)             → 00881
=TEXT([@ApptOn],"DD-MMM-YYYY")
```

### Dates: TODAY, DATEDIF, NETWORKDAYS

Refund aging (calendar days) and KYC TAT (working days):

```excel
=TODAY()-[@RefundOpened]
=DATEDIF([@KycStart],[@KycEnd],"d")
=NETWORKDAYS([@KycStart],[@KycEnd],Holidays[Date])
```

Question: "How many working days from KYC start to complete?"

### Statistical: SUM, COUNT, COUNTA, COUNTIF, SUMIF, AVERAGE

```excel
=SUM(Orders[Gmv])
=COUNT(Orders[Gmv])                 numeric only
=COUNTA(Orders[OrderId])            non-blank
=COUNTIF(Orders[Status],"Returned")
=SUMIF(Orders[City],"Pune",Orders[Gmv])
=AVERAGE(Orders[Gmv])
=COUNTIFS(Orders[City],"Pune",Orders[Late],"Y")
=SUMIFS(Orders[Gmv],Orders[City],"Pune",Orders[Status],"Delivered")
```

Appointment no-show % (MediCare+ `Appts`):

```excel
=COUNTIF(Appts[Outcome],"No-show")/COUNTA(Appts[ApptId])
```

Format as `%`.

## Scenario / Use case

QuickBite PO asks: **"% of late orders by city last week."** Columns: `City`, `PromisedMin`, `ActualMin`, `OrderDate`.

Helper:

```excel
=[@ActualMin]>[@PromisedMin]     → TRUE/FALSE, or
=IF([@ActualMin]>[@PromisedMin],"Y","N")
```

City summary (Pune row):

```excel
=COUNTIFS(Orders[City],$A2,Orders[OrderDate],">="&$G$1,Orders[OrderDate],"<="&$G$2)
=COUNTIFS(Orders[City],$A2,Orders[Late],"Y",Orders[OrderDate],">="&$G$1,Orders[OrderDate],"<="&$G$2)
=B2/A2
```

Where `$G$1`/`$G$2` are week start/end. The BA shows Pune 18% late vs Hyderabad 7%. Ops investigates kitchen load in Pune — not "riders nationwide".

## Real-world examples

1. **ShieldSure** TAT bucket with nested IF (or see Pivot file for groups): `=IF([@Days]<=1,"0-1",IF([@Days]<=3,"2-3","4+"))`
2. **ShopEase** AOV: `=SUMIF(Orders[Status],"Delivered",Orders[Gmv])/COUNTIF(Orders[Status],"Delivered")`

## Weak vs strong

| Weak | Strong |
|---|---|
| Nested VLOOKUP copies | XLOOKUP or INDEX/MATCH + IFNA |
| `% late` by eye | COUNTIFS / COUNTIF ratio |
| `=A2+B2` across 10k rows typed | Table structured refs |
| `#N/A` on the PO slide | IFERROR with a label |
| Dates as text `"17/08/26"` | Real dates + NETWORKDAYS |
| `IF` for 12 cities | COUNTIFS + city table |

## Notes

- `COUNT` ignores text; use `COUNTA` for IDs.
- `VLOOKUP` approximate match (`TRUE`) is a silent killer — always `FALSE` unless you intend ranges.
- `DATEDIF` exists but is poorly documented; `NETWORKDAYS` is clearer for TAT SLAs.
- Division by zero: wrap `%` as `=IF(A2=0,"-",B2/A2)`.
- Keep helper columns visible in analysis files; hide them only in a polished printout.
- Recalculate (`F9`) if a file is set to manual calc before you send numbers.
- Formulas answer questions; they do not replace a written definition of "late" (promised vs actual).
