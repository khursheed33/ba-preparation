# SaaS, EdTech, and Telecom

## Definition

**SaaS** (Software as a Service) sells access to software on a **subscription**: seats, usage, or tiered **plans**. **EdTech** is SaaS (or content + SaaS) aimed at learners and institutions: batches, academic calendar, content rights. **Telecom** sells **connectivity plans** (prepaid/postpaid), usage (voice/data/SMS), devices, and often bundles. All three share **recurring billing, plans, and churn** — different regulators and “units of value.”

## Why it matters

A BA from e-commerce will design “buy once.” Subscriptions need **start, renew, upgrade, downgrade, prorate, dunning, churn**. Telecom adds usage rating and number portability. EdTech adds academic sessions and “student vs payer” (parent). Wrong churn definition ships a happy dashboard and a dying book.

## Business models

| Domain | Unit | Revenue | Cost / risk |
|---|---|---|---|
| SaaS | Seat, workspace, usage | MRR/ARR, expansion | CAC, support, infra |
| EdTech | Student, course, school license | Sub + one-time courses | Content, teachers, refunds |
| Telecom | MSISDN / connection | ARPU, packs | Network, interconnect, churn |

## Key processes (As-Is)

**Subscribe / change plan (SaaS)**

1. Trial or paid start
2. Entitlement (features by plan)
3. Invoice / charge (card, NACH)
4. Upgrade (immediate) / downgrade (end of term) + prorate rules
5. Failed pay → dunning → suspend → cancel

**EdTech extra:** enrol in batch; teacher assignment; exam window; refund of course vs seat.

**Telecom extra:** SIM/eSIM activate; pack validity; usage against cap; bill shock; recharge; port-out.

## Stakeholders and systems

| Domain | Stakeholders |
|---|---|
| SaaS | Buyer (admin), end user, CS, finance, product |
| EdTech | Student, parent, teacher, school admin, content |
| Telecom | Subscriber, retailer, network ops, billing, TRAI-facing compliance |

| System | Role |
|---|---|
| Billing / subscription | Plans, invoices, dunning |
| Identity / SSO | Seats |
| Product analytics | Activation, engagement |
| CRM | Churn save |
| Mediation / rating (telecom) | Usage to money |
| LMS / content (EdTech) | Courses, progress |
| BSS/OSS (telecom) | Customer + network |

## Regulations lite

- SaaS: data residency, DPDP, B2B contract, uptime SLA in MSA
- EdTech: advertising of outcomes, child data extra care, refunds
- Telecom: TRAI-style tariff transparency, KYC of SIM, spam, QoS, portability

## KPIs (industry metrics)

| KPI | Formula idea | Watch-out |
|---|---|---|
| MRR / ARPU | Recurring revenue / connections | Mix of plans |
| Logo vs revenue churn | Lost customers vs lost $ | Expansion can hide logo loss |
| Net retention | Starting MRR + expansion − churn | SaaS health |
| Activation | % seats using core feature in 7 days | Vanity: logins only |
| EdTech completion / attendance | Learners who finish / attend | Not the same as login |
| Telecom: MoU, data GB, recharge | Usage | Bill shock complaints |
| Grace / suspend rate | Failed payments | Dunning design |

**Common BA projects:** plan catalog, self-serve upgrade, dunning emails, student–parent accounts, pack recommender, bill redesign, number portability journey, school admin rostering.

### Weak vs strong

| Weak | Strong |
|---|---|
| Churn = cancelled this month | Cohort + voluntary vs involuntary (payment fail) |
| Seat = email | Seat = entitled user; shared logins policy |
| EdTech “engagement” | Attendance + assignment submit |
| Telecom “unlimited” | Fair use + speed throttle as disclosed rules |
| Prorate “later” | Upgrade/downgrade rules in AC |

## Real-world examples

**B2B SaaS HR tool:** buyer is HR, user is employee — two journeys (see HR primer).

**EdTech live class:** entitlement lapse must not delete history; recorded vs live is a business rule.

**Telecom prepaid:** validity vs balance — two clocks; BA must not merge them.

**ShopEase seller SaaS** (subscription for ads): same billing patterns on an e-commerce platform.

## Scenario / Use case: EdTech involuntary churn looks like “product hate”

**Context.** Leadership: “Churn is 8%; fix content.” Data: 55% of churned logos had **failed auto-pay** after card expiry; students still tried to join class and saw a generic “access denied.” CS had no dunning playbook. Product roadmap filled with new videos.

**BA work.** Split **voluntary** (cancel intent) vs **involuntary** (payment). FR: dunning sequence, in-class message “update card,” grace 3 days, parent vs student who pays. KPI: involuntary churn %, recoveries. UAT: failed charge → banner → pay → class unlock.

**If ignored.** Content spend; revenue still leaks at billing.

## Notes

- Subscriptions: plan, entitlement, invoice, dunning, churn — learn this once, reuse.
- Churn must split voluntary vs payment-fail.
- EdTech: learner ≠ payer; academic calendar ≠ monthly SaaS month.
- Telecom: usage rating + packs + KYC; “unlimited” is a disclosed rule.
- Activation beats vanity logins.
- Proration and downgrade timing are classic missed AC.
- Net retention and ARPU need mix awareness.
- Compliance: child data, SIM KYC, tariff transparency — bring specialists.
