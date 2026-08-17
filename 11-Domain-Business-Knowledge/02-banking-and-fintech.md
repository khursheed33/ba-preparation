# Banking, Finance, and FinTech

## Definition

**Banking** takes deposits, makes loans, and moves payments under a license. **Finance** (broader) includes lending, markets, insurance-adjacent wealth. **FinTech** is technology-led delivery of those activities (UPI apps, account aggregators, digital KYC) — still bound by banking *outcomes* even when the brand is not a bank.

NovaBank in these notes is a retail + SME bank with a digital channel.

## Why it matters

Wrong KYC, limit, or ledger requirements create regulatory and customer harm. A BA who thinks “payment is like placing an order” will miss maker-checker, cooling periods, and reconciliation.

## Business model

| Stream | How money is made | BA implication |
|---|---|---|
| Net interest | Lend at higher rate than cost of funds | Ticket, tenure, risk grade, NPA |
| Fees | Cards, NEFT/IMPS, account services | Fee rules, waivers, GST |
| Float / payments | Transaction rails, merchant acquiring | Time-out, duplicate, refund |
| FinTech take-rate | Facilitation, not always balance-sheet lending | Who is licensed, who holds funds |

## Key processes (As-Is lite)

**Retail loan (unsecured)**

1. Lead / apply (app or branch)
2. KYC + bureau + bank statement
3. Credit decision (STP or underwriter)
4. Sanction letter / KFS, e-sign
5. Disbursal to account
6. NACH/e-mandate, collections if bounce

**Payment (IMPS/UPI)**

1. Add beneficiary (cooling / limit)
2. Authenticate (PIN/OTP)
3. Core posts debit; rail acknowledges
4. Recon; fail = reverse or investigate

**KYC:** collect ID, verify (CKYC/Aadhaar/video as applicable), periodic update, freeze if expired.

## Stakeholders and systems

| Stakeholders | Interest |
|---|---|
| Customer, RM | Speed, clarity |
| Credit / underwriting | Risk, policy |
| Operations | STP, queues |
| Compliance / AML | KYC, STR |
| Finance / recon | Ledger truth |
| IT / CBS vendor | Stability |
| Regulator (context) | Conduct, prudential |

| System | Role |
|---|---|
| Core banking (CBS) | Accounts, ledger, products |
| LOS / LMS | Origination / servicing |
| Payments switch / UPI | Rails |
| CRM | Leads, complaints |
| AML / fraud | Monitoring |
| Channel: mobile, branch, ATM | Experience |

## Regulations lite (not legal advice)

- KYC / AML, customer due diligence
- Fair practice / KFS-style disclosures on loans
- Payment limits, 2FA, cooling on new beneficiaries
- Data protection and localization expectations
- Outsourcing and incident reporting in spirit

BA action: **flag** when a story touches identity, money movement, or marketing of returns; pull compliance.

## KPIs and common BA projects

| KPI | Why |
|---|---|
| Sanction TAT (median) | Experience + drop-off |
| STP % | Ops cost |
| Approval % by segment | Mix vs quality |
| First-period bounce / 30+ DPD | Early risk |
| KYC STP / exception % | Onboarding |
| Payment success % | Rails + UX |
| NPA / SMA (aware of, not owner) | Portfolio |

**Common projects:** digital onboarding, loan origination rebuild, beneficiary and limits, statement/MIS, collections workspace, FinTech partnership (who holds the account).

### Weak vs strong

| Weak | Strong |
|---|---|
| Instant loan, no KYC story | KYC states, exceptions, freeze |
| “Transfer money” one AC | Limit, cooling, duplicate, reverse |
| Average ticket as sole KPI | Segmented book + TAT + risk |
| FinTech = no compliance | License and fund-flow map |

## Real-world examples

**NovaBank** retail EMI vs **corporate** bilateral loan — same word “loan,” different process and stakeholders.

**FinTech wallet** vs bank account — outstanding is a liability with different rules; BA must map who is the regulated entity.

**SaaS payroll** paying salaries through NovaBank file — file format, cut-off, partial fail are requirements.

## Scenario / Use case: NovaBank KYC blocking disbursal

**Context.** Digital personal loan: sanction in 20 minutes, disbursal fails 18% because KYC “pending” in CBS while LOS shows approved. Customers see “money today.”

**As-Is gap.** Video-KYC vendor success does not update CBS customer status before disbursement API. Ops patches manually next day.

**BA work.** Sequence diagram: LOS → KYC → CBS. FR: disbursement blocked unless CBS KYC = verified; user message honest; ops queue for exceptions. UAT: maker-checker on exception, not BA-only. KPI: % sanctioned-not-disbursed for KYC.

**If ignored.** Complaints, mis-selling perception, recon breaks.

## Notes

- Banking = ledger + identity + rails; FinTech still touches those.
- Learn: loans, payments, KYC, core banking — as processes, not slogans.
- Maker-checker, limits, recon are default patterns.
- KPIs: TAT, STP, bounce, payment success — not only “app ratings.”
- Always ask: which system is master for customer and for money.
- Compliance is a stakeholder, not a footnote.
- Segment retail / SME / corporate before averaging tickets.
- “Instant” is a promise that maps to a state machine.
