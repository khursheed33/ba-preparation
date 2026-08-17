# Requirement Prioritization

**Prioritization** is deciding the order and necessity of requirements when you cannot do everything now.

It is not a popularity vote. It is a facilitated trade-off using value, cost, risk, and constraints.

## Why it matters for a BA

If the BA only “asks the PO,” the loudest stakeholder wins. ShopEase marketing will rank a wallet splash screen above refund reconciliation. Legal Must items get labelled Should until a regulator calls. The BA’s job is to make criteria visible and force a decision, not to secretly rank the backlog.

## Factors you must cover

| Factor | Meaning | Question |
|---|---|---|
| MoSCoW | Must / Should / Could / Won’t (this time) | How necessary is this in the agreed scope window? |
| Business value | Outcome: revenue, cost, risk, experience | What metric or risk moves if we do this? |
| Cost | Effort, money, vendor fees, operational load | What does it take to deliver and run? |
| Risk | Delivery risk and business risk of *not* doing it | What happens if we skip or delay? |
| Impact | Breadth and depth of effect on users/process | Who is affected, how often, how severely? |
| Urgency | Time sensitivity | Is there a date (regulation, peak season, contract)? |
| Dependency | Order constraints | What must come first? What do others wait on? |
| Feasibility | Can we do it with current constraints? | Skill, tech, data, vendor, legal — realistic? |

MoSCoW without the other factors is labelling, not thinking. A Must that is infeasible is a project problem, not a font colour on a story.

### MoSCoW rules

- **Must:** solution is not viable without it in this release (including legal Must).
- **Should:** important, painful to omit, but a workaround exists for this release.
- **Could:** nice; do if capacity remains.
- **Won’t:** explicitly not now; prevents silent scope.

Must should be a minority. If everything is Must, nothing is.

### Kano (customer reaction, not a substitute for MoSCoW)

| Type | If missing | If present | BA use |
|---|---|---|---|
| **Basic / Must-be** | Anger | Silence (expected) | Hygiene in the release: SMS ack of a claim, wallet balance visible |
| **Performance** | Disappointment | Satisfaction scales with more | TAT, conversion, fewer clicks — rank with value/cost |
| **Delight** | No anger | Unexpected plus | Proactive garage slot; do **not** make this Must while basics fail |

Kano answers “how will users *feel*.” MoSCoW answers “what is viable in *this* window.” Legal 2FA can be MoSCoW Must even if customers never “delight” in it. Full worked example: [prioritization techniques](../12-Business-Analysis-Techniques/08-prioritization-and-benchmarking.md).

## How a BA facilitates (not “ask the PO”)

1. **Frame the window:** this release / this MVP / this quarter — not “forever.”
2. **Bring evidence:** volumes, cost of delay, incident counts, regulatory dates.
3. **Separate scoring from deciding:** score value, cost, risk on a wall; then apply MoSCoW.
4. **Surface conflicts:** legal Must vs marketing Should in the open.
5. **Use a decision log:** who decided, date, trade-off.
6. **Revisit when facts change:** a CR can reprioritize; do not treat v1 ranks as religion.
7. **Protect Won’t:** write it down so it is not smuggled in as a “small tweak.”

Techniques: 100-point method, pairwise (“A vs B for this sprint”), WSJF-style cost of delay vs job size (even informally), risk-based (compliance first).

NovaBank: feasibility may kill “video KYC for every password reset” even if info-sec *wants* it as Must — capacity and vendor SLA cannot support it. The BA facilitates an alternative Must: OTP + cooling period on SIM change.

QuickBite: urgency of New Year’s Eve scaling (NFR) outranks a Could for new cuisine filters.

## Sample MoSCoW list: ShopEase Wallet

Release window: 12-week “Wallet Pay” MVP for logged-in buyers on Android app. Goal: raise prepaid mix, cut COD cost.

| ID | Requirement | MoSCoW | Why |
|---|---|---|---|
| FR-WLT-01 | View wallet balance before pay | Must | Without it, users will not trust pay-from-wallet |
| FR-WLT-02 | Pay order fully from wallet if balance ≥ payable | Must | Core value |
| FR-WLT-03 | Partial wallet + other instrument | Should | Value, but full-wallet path is enough for MVP |
| FR-WLT-04 | Add money via UPI | Must | Funding path; India reality |
| FR-WLT-05 | Add money via net banking | Could | Costly integrations; UPI covers most |
| FR-WLT-06 | Wallet refund to original source on return | Must | Finance + RBI-style customer protection; leakage if ignored |
| FR-WLT-07 | Cashback credit to wallet | Should | Marketing value; not viable-without for payments |
| FR-WLT-08 | Gift wallet to another user | Won’t | Fraud/KYC cost; out of window |
| NFR-WLT-S01 | 2FA on add-money above ₹5,000 | Must | Security + compliance risk |
| NFR-WLT-P01 | Pay confirm p95 ≤ 2s | Should | Value/experience; degrade gracefully is possible |
| FR-WLT-09 | Seller settlement from wallet receipts | Must | Dependency: finance cannot operate without it |
| FR-WLT-10 | Animated wallet onboarding video | Could | Low value vs cost |
| FR-WLT-11 | Wallet on iOS | Won’t | Feasibility: team is Android-first this quarter |
| FR-WLT-12 | Auto-pay subscription from wallet | Won’t | Regulatory + mandate complexity |

Notice Must items include a **dependency** (settlement) and **risk** (2FA), not only customer-facing features.

## Weak vs strong prioritization

| Weak | Strong |
|---|---|
| PO ranks in Jira at 6 p.m. | Workshop with finance, legal, ops, eng using evidence |
| All stories Must | Must = viability + legal; rest ranked |
| Ignore cost | A high-value, low-feasibility item is sequenced, not fantasised |
| Ignore dependency | Wallet pay ranked above settlement — finance fails at UAT |

## Scenario / Use case: legal Must vs marketing Should

**Context.** ShopEase Wallet. Marketing campaign booked: “Get ₹200 cashback in wallet” for Diwali. Legal/compliance: storing funds and cashback needs extra disclosures, 2FA above threshold, and refund-to-source. Engineering capacity: 8 Must-sized items max. Marketing wants the campaign story as Must and 2FA as Could “for later.” Legal says no go-live without 2FA and refund-to-source.

**Stakeholders.** Marketing, legal, finance, product, engineering, customer support, BA.

**What the BA does.**

- Puts dates on the wall: Diwali freeze, legal review SLA 10 days.
- Scores: cashback = high value, medium cost, low legal urgency *relative to 2FA*; 2FA = high risk if skipped; refund-to-source = high risk (customer complaint + possible RBI attention).
- Facilitates options: (A) ship pay + add-money + 2FA + refund, delay cashback; (B) delay whole wallet past Diwali; (C) cashback as *Should* on a feature flag after legal text is live.
- Marketing argues urgency (campaign spend). BA shows cost of a regulator or fraud incident vs campaign.
- Decision log: Option A. Cashback is Should, flagged. Campaign rebooked to “pay from wallet, no COD fee” which legal already approved.

**Sample artifact (decision).**

> 18 Sep. Decision: MVP Must = FR-WLT-01,02,04,06,09 + NFR-WLT-S01. FR-WLT-07 Cashback = Should, not in Diwali commit. Owner: Digital PO. Legal: R. Iyer. Marketing informed; campaign brief v3.

**What goes wrong if ignored.** Cashback ships without 2FA. Fraud ring loads stolen cards into wallets. Legal emergency stop. Marketing still blames “tech.” The BA is asked why 2FA was Could.

## A simple scoring sheet you can reuse

Score 1–5 each: value, risk-if-skipped, urgency. Score 1–5 cost and feasibility (invert cost: high cost = low priority unless Must). Flag dependencies in red. Then assign MoSCoW in a group, not alone.

Feasibility of “zero” means it cannot be Must for this window — change the window or the requirement.

## Notes

- MoSCoW without value, cost, risk, and feasibility is labelling.
- Kano protects basics (ack, status, refund path) from being crowded out by delight features.
- Must includes legal and operational viability, not only customer-facing wishes.
- Write Won’t down so it cannot return as a “small tweak.” 
