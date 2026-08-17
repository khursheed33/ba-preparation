# Business Problems, Goals, Outcomes, and Value

## Business problems vs technical problems

A **business problem** is a difficulty the organization faces in achieving its goals.

Examples:

- Customers abandon checkout
- Loan approval takes 10 days
- Support team cannot track complaints

A **technical problem** is a system limitation or defect.

Examples:

- API timeout
- Database is slow
- Button does not save data

Rule: start with the business problem. Technology is a possible solution, not the starting point.

Bad: "We need a new dashboard."
Better: "Managers cannot see weekly sales by region, so they make slow decisions."

## Business objectives

An objective is what the business wants to achieve.

Example: Reduce customer onboarding time.

## Business goals

A goal is a broader aim. Objectives are more specific steps toward a goal.

- Goal: Improve customer experience
- Objective: Cut onboarding from 5 days to 1 day

## Business outcomes

An outcome is the result after the change.

Example: 80% of customers complete onboarding in one day.

Outcomes are more useful than outputs.

- Output: "We launched a new form"
- Outcome: "Onboarding time dropped by 60%"

## Business value

Value is the benefit the business or customer gets.

Value can be:

- More revenue
- Lower cost
- Less risk
- Better customer experience
- Faster operations
- Compliance

A BA should always ask: **What value does this change create?**

## Simple chain to remember

```text
Problem → Goal / Objective → Solution → Outcome → Value
```

## Real-world chain examples

| Layer | ShopEase returns | NovaBank personal loans | MediCare+ no-shows |
|---|---|---|---|
| Problem | Buyers wait 9 days for refunds; support load 18% | Sanction takes 10 days; 34% files stall on documents | 22% specialist no-shows; idle doctor time |
| Goal | Trustworthy post-purchase experience | Faster, safer credit for salaried customers | Higher clinic utilization |
| Objective | Return-to-refund ≤ 4 days for prepaid < ₹2,000 | Cycle time 10 → 3 days for complete files | No-show ≤ 12% in 90 days |
| Solution (one option) | Auto-approve + status SMS | Completeness checklist + status SMS | 24h + 2h reminder with reschedule |
| Outcome | Cycle time 4.2 days (simulated) | Complete-file cycle 4 days (simulated) | No-show 13% (simulated) |
| Value | Fewer tickets, better NPS, lower COD distrust | Lower drop-off, less branch load | More filled slots, revenue |

### Weak vs strong

| Weak | Strong |
|---|---|
| Goal: “Digital transformation” | Goal: Improve post-purchase trust; objective: 4-day refunds |
| Value: “We launched the app” | Value: Support tickets −11% and refund NPS +8 |
| Problem: “Need AI underwriting” | Problem: Files wait on missing PAN; AI is a possible later solution |

## Scenario / Use case: QuickBite “we need a compensation engine”

**Context.** QuickBite late-order complaints spike on Friday nights. Marketing wants a “compensation engine like the big apps.” Finance fears leakage. The BA is asked to write an epic called `compensation-engine`.

**Stakeholders.** CX, finance, restaurants, riders, customers, PO, BA.

**What the BA does.**

1. Name the **business problem**: customers experience late delivery; trust and repeat orders drop. Not “we lack an engine.”
2. Split **technical problem** (no rule service) from **business problem** (unclear who pays when kitchen vs rider is late).
3. Write objective: “Paid compensation for rider-caused delays > 15 min after restaurant ready, with leakage ≤ 1.5% of GMV in a 6-week pilot.”
4. Outcome metric: repeat-order rate in the pilot city; ticket volume for “late.”
5. Value: retained customers minus compensation cost. If leakage > value, do not scale.

**Sample artifact.**

| Term | Statement |
|---|---|
| Problem | Friday-night orders arriving > 15 min late drive complaints and churn in Pune. |
| Objective | Cut late-order tickets 30% in 6 weeks without leakage > 1.5% GMV. |
| Out of scope | Restaurant-caused delays (kitchen SLA) — separate workstream. |

**What goes wrong if ignored.** A generic engine pays everyone. Finance kills it. The original problem (rider delay after ready) is still unsolved. The BA documented a solution name, not value.

## Notes

- Start every intake with problem → objective → outcome → value. Park solutions until the first three are named.
- Outputs (screens, engines, apps) are not outcomes.
- Label simulated metrics as simulated in portfolio work.
- 
