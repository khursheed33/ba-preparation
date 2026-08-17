# Problem Identification and Problem Statement

## Problem identification

Finding the real problem, not just the symptom.

Symptoms are what people complain about. The root problem is why it happens.

Example:

- Symptom: "Reports are always late."
- Possible root problem: Data comes from 4 systems and is merged manually in Excel.

BA techniques used later: 5 Whys, interviews, process mapping, data analysis.

## Problem statement

A short, clear description of the problem, who it affects, and why it matters.

A good problem statement is:

- Specific
- Evidence-based
- Free of a hidden solution
- Focused on business impact

### Weak problem statement

"We need a mobile app for complaints."

This jumps to a solution.

### Stronger problem statement

"Customer complaints are logged in email and Excel. The support team cannot track status, so 30% of complaints remain unresolved after 7 days, which increases repeat calls and customer churn."

## Template

**Who** is affected  
**What** is happening  
**Where / in which process**  
**Impact** (time, money, risk, customers)  
**Evidence** (numbers if possible)

## Solution vs requirement

These are often mixed up.

| Term | Meaning | Example |
|---|---|---|
| Problem | What is wrong | Users cannot reset password without calling support |
| Requirement | What the solution must do | The system shall allow a user to reset password via email OTP |
| Solution | How it will be done | Build a "Forgot Password" screen using email OTP |

The BA captures requirements. The team may choose among several solutions that satisfy those requirements.

## Real-world examples

| Company | Symptom people shout | Likely root (to verify) | Hidden solution to reject |
|---|---|---|---|
| ShopEase | “Refunds are late.” | Seller approval queue + no status SMS | “Build a chatbot” |
| NovaBank | “Loans take forever.” | 34% files incomplete; underwriter idle | “Buy an AI credit model” |
| MediCare+ | “Patients don’t show up.” | No reminder + hard reschedule | “Build a new patient app” |
| ShieldSure | “Claims are stuck.” | FNOL photos incomplete; garage not on network | “New claims portal” |

### Weak vs strong problem statements

| Weak | Strong |
|---|---|
| We need a mobile app for ShopEase returns. | Prepaid ShopEase buyers wait 9 days for refunds; 18% of support tickets are status chases; seller approval averages 2.1 days. |
| NovaBank should implement AI KYC. | 28% of personal-loan applications stall more than 48 hours because PAN or salary slip is missing from the file. |
| MediCare+ has a no-show problem. | Specialist clinics at MediCare+ Pune have a 22% no-show rate on Monday 9 a.m. slots; patients get no actionable reminder. |

## Scenario / Use case: ShieldSure “claims portal” vs the real problem

**Context.** ShieldSure motor claims TAT is 14 days. Claims head says: “Problem identification is done. We need a new portal. Write the statement as ‘legacy system is old.’” You have one week of access to adjusters and a spreadsheet of 1,200 claims.

**Stakeholders.** Claims head, adjusters, customers, garage network, finance, compliance (IRDAI TAT), BA.

**What the BA does.**

1. Treat “legacy is old” as a *hypothesis*, not a problem statement.
2. Sample 50 delayed claims. Count causes: incomplete FNOL photos (31%), garage not cashless (22%), surveyor calendar (18%), system downtime (9%), other.
3. Five Whys on incomplete FNOL: customer uploads one blurry photo because the SMS link expires in 2 hours and has no example images.
4. Write a problem statement with evidence, no portal inside it.
5. Requirements may later include a better upload flow *or* a longer link *or* agent-assisted capture — several solutions.

**Sample artifact.**

> **Problem statement.** Motor own-damage claims at ShieldSure take a median 14 days against an 8-day target. In a 50-claim sample, 31% of delay hours started when First Notice of Loss photos were incomplete. Customers currently get a 2-hour upload link with no photo guidance. This increases surveyor repeats and IRDAI TAT risk.

**What goes wrong if ignored.** A new portal launches with the same 2-hour link. TAT does not move. The claims head says “we modernized.” The regulator still sees delays. Identification failed because the statement encoded a solution.

## Notes

- Symptoms are complaints; problems have a who, process, impact, and evidence.
- If a “problem statement” names a product, rewrite it.
- Use a small sample (even 50 rows) before you believe a VP’s root cause.
- 
