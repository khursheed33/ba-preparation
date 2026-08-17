# Stakeholder Management for Requirements

Requirements do not fail only because they are vague. They fail because **people** disagree, disappear, or sign what they did not read.

Stakeholder management for requirements: **identification, influence, interest, expectations, conflicting requirements, negotiation, conflict resolution, communication, sign-off**.

## Why it matters for a BA

NovaBank UPI mandate work will stall when finance, operations, compliance, and the app team each think they “own” the flow. If the BA only writes FRs, the conflict explodes in UAT. Influence and interest tell you who must be in the room *before* the FRD is pretty.

## Identification

List who is affected, who decides, who supplies information, who can block.

For a project, identify:

- Users (do the work)
- Decision makers (can approve)
- Influencers (no formal power, high informal power)
- Constraining parties (legal, risk, vendor)
- Impacted but silent (branch staff, night-shift ops)

ShieldSure cashless garage: claims, garage network, finance, customer, IRDAI-facing compliance, vendor portal team. Missing the garage ops lead is how you get an unusable estimate screen.

Revisit the list when scope changes. Lab integration added to MediCare+ means lab manager is now a stakeholder.

## Influence and interest

**Interest:** how much they care about this requirement set.
**Influence:** how much they can force or block a decision.

### Grid (use it live)

| | Low interest | High interest |
|---|---|---|
| **High influence** | Keep satisfied | Manage closely |
| **Low influence** | Monitor | Keep informed |

### NovaBank UPI mandate project — grid

Context: customers will set UPI AutoPay mandates for loan EMIs and standing instructions. RBI rules apply. App team wants a 3-tap flow.

| Stakeholder | Interest | Influence | Grid | Why |
|---|---|---|---|---|
| Retail digital PO | High | High | Manage closely | Scope and priority |
| Compliance / risk | High | High | Manage closely | Can stop go-live |
| Finance (loan ops) | High | High | Manage closely | Wants extra approval on mandate create |
| Operations (call centre & branch) | High | Medium-high | Manage closely | Live with click-count and exceptions |
| Information security | Medium | High | Keep satisfied | Authn, session, fraud |
| App engineering | High | Medium | Keep informed + involve in feasibility | They build; they do not set policy |
| Customers (represented via research) | High | Low (individually) | Keep informed | Pain is real; they do not sign |
| Marketing | Medium | Medium | Keep informed | Campaigns; not mandate rules |
| Core-banking owner | Low–medium | High | Keep satisfied | Mandate posting dependency |
| Internal audit | Low now | High later | Monitor / periodic | Will ask for evidence at review |

Do not park compliance in “inform.” They have high influence even if they speak little in sprint planning.

## Expectations

Elicit expectations explicitly: “What does success look like for you in 90 days?” Unspoken expectations become UAT surprises.

QuickBite restaurants expect compensation *never* to hit their payout. Finance expects cause-based allocation. If you do not surface that, both will say the BA “missed requirements.”

Reset expectations when MoSCoW says Won’t.

## Conflicting requirements

Treat conflicts as a first-class log, not a personality problem.

| Conflict | Parties | Typical NovaBank UPI example |
|---|---|---|
| Control vs speed | Finance vs operations | Extra approval step vs fewer clicks |
| Safety vs conversion | Risk vs product | OTP every mandate edit vs drop-off |
| Channel vs channel | App vs branch | Branch can waive cooling-off; app cannot |

## Negotiation techniques for BAs

You are not a doormat and not a dictator. You negotiate **options**, not feelings.

| Technique | How | Example |
|---|---|---|
| Interest vs position | Ask why, not only what | Finance’s position: “always two approvers.” Interest: prevent fraudulent high-value mandates |
| Options, not ultimatums | Bring A/B/C with impacts | Threshold: 2FA always; second human approval only above ₹X |
| Objective criteria | Policy, data, regulator, SLA | RBI mandate rules; fraud rate last quarter |
| Timebox the decision | Decision date in the log | “Friday 4 p.m. or we descope from this release” |
| Split the difference in *scope*, not in *safety* | Phased release | Phase 1: new mandates; Phase 2: edit flow |
| BATNA awareness | What if we do nothing | Keep existing NACH; no UPI mandate this quarter |
| Separate people from the problem | Attack the process, not Ops vs Finance | “The click count vs control trade-off,” not “Ops is lazy” |
| Written confirmation | Repeat the deal in the decision log | Stops “that’s not what I said” |

**Weak:** “Please compromise.”
**Strong:** “Here are three designs, cost, fraud exposure, and click counts. You choose; I record it.”

## Conflict resolution

1. Name the conflict in one sentence.
2. Evidence on the table (volumes, incidents, circulars).
3. Options with impacts.
4. Escalate only with a pack, not with gossip.
5. Record the decision and the *rejected* alternatives (stops re-litigation).

ShopEase seller vs platform return window is the same pattern: sources, who pays, then a rule.

## Communication

Match channel to grid:

- Manage closely: workshops, weekly working group, decision log
- Keep satisfied: short brief + “any constraint we missed?”
- Keep informed: digest after decisions, not a debate forum
- Monitor: monthly check-in

Same message, different depth. Do not send a 40-page FRD to marketing and a slogan to compliance.

## Sign-off

Sign-off is stakeholder management made visible.

- Right signers (influence + accountability)
- Versioned pack they actually saw
- Time to read (not “sign in the meeting while we watch”)
- Dissent recorded if someone signs with conditions

If operations never signed the click-count, they will fail UAT on purpose or by freeze.

## Scenario / Use case: extra approval vs fewer clicks

**Context.** NovaBank UPI mandate for EMIs. Finance: every new mandate needs a second supervisor approval in the back office (maker-checker). Operations: customers already drop at OTP; a day-long checker queue will explode call-centre volume. Product wants Diwali campaign “pay EMI via UPI AutoPay.”

**Stakeholders.** Finance, operations, compliance, digital PO, app team, customers, BA.

**What the BA does.**

- Identifies finance and ops as high interest / high influence; both must be managed closely.
- Maps expectations: finance = zero unauthorised mandates; ops = < 4 customer screens; compliance = RBI-compliant authentication.
- Negotiation: interest of finance is fraud above a value, not humiliation of ops. Option A: checker for all. Option B: checker only if amount > ₹25,000 or if beneficiary is new. Option C: no checker; step-up OTP + 30-min cooling-off + SMS alert with cancel link.
- Data: 88% of EMIs are below ₹25,000; last year fraud on standing instructions clustered above that.
- Decision log (sample below).
- Sign-off: PO + finance controller + ops head + compliance on FR set v1.0 including the threshold.

**Sample artifact — decision log row.**

| Field | Content |
|---|---|
| Decision | Maker-checker required only when mandate amount > ₹25,000 or payee not previously paid from this account. Below that: 2FA + 30-min cooling-off + SMS cancel. |
| Date | 3 Oct |
| Owner | Digital PO (A. Shah), Finance (K. Rao), Ops (M. Iyer) |
| Alternatives | (A) checker all (B) no checker (C) adopted hybrid |
| Impact | App: extra status “pending checker.” Ops: queue only ~12% of volume. Finance: residual risk accepted on small EMIs. |

**What goes wrong if ignored.** Finance wins politically; every mandate queues. Campaign conversion dies. Or ops wins; a large fraudulent mandate hits the papers. Either way the BA “wrote what they were told” and still failed.

## Notes

- Influence vs interest tells you *who must be in the room* before the FRD is pretty.
- Negotiate options with evidence (volumes, fraud cluster), not volume of opinion.
- Sign-off is named owners on a baseline, not a meeting that “felt aligned.”
- RACI and the communication plan are taught in [stakeholders](../01-BA-Role-Business-Fundamentals/09-stakeholders.md); use them here when finance and ops both think they own the flow. 
