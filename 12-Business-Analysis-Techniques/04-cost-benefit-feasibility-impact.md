# Cost-Benefit, Feasibility, and Impact Analysis

**Cost-benefit analysis (CBA)** compares what a change will cost with the value it returns, in language a sponsor can approve. **Feasibility analysis** asks whether the change *can* be done across technical, operational, economic, legal, and schedule lenses. **Impact analysis** asks what a proposed change (especially a change request) will touch: requirements, process, data, reports, training, and other systems.

## Why it matters

NovaBank “must have video KYC” is not a decision. It is a preference until costs, benefits, feasibility, and knock-on impact are explicit. A BA does not replace Finance or Architecture. A BA *frames* the decision so the wrong option is not chosen because it sounded modern.

## Cost-benefit analysis

List **costs** (one-time and run) and **benefits** (cash and non-cash), then tell a simple ROI / payback story.

| Cost type | What to include | NovaBank video KYC example |
|---|---|---|
| Build | Internal engineering, vendor implementation | App + backend + vendor SDK integration |
| License | SaaS, per-KYC fees, bureau, video vendor | ₹X per successful video KYC |
| Training | Staff, branch, call-centre scripts | RM and CKYC ops training |
| Ops | Support, exception handling, audit storage | 7-year video retention, review team |

| Benefit type | How a BA evidences it | Example |
|---|---|---|
| Time saved | Hours × loaded cost | Branch KYC 45 min → video 12 min customer time |
| Error reduction | Rework, fraud, compliance findings | Fewer incomplete KYC packets returned by ops |
| Revenue / conversion | Extra completed journeys × margin | Drop-off from “visit branch” falls; more loans booked |

**Simple ROI / payback a BA can defend (not CFA-level)**

- **Payback (months)** ≈ one-time cost ÷ monthly net benefit.
- **ROI (year 1)** ≈ (year-1 benefits − year-1 costs) ÷ one-time + first-year run cost.

Example narrative: “Video KYC one-time ₹80 lakh. Run cost ₹18 lakh/year. Branch KYC avoided cost + extra originated loans ≈ ₹4.5 lakh/month net. Payback ≈ 18 months. We are not claiming NPV to two decimals; Finance can model tax and cost of capital. We *are* claiming the volume and time assumptions.”

State assumptions: volumes, adoption %, fully loaded FTE cost, what is *not* counted (brand, option value).

## Feasibility analysis (five lenses)

| Lens | Question | Fail example |
|---|---|---|
| Technical | Can we integrate, scale, store, secure? | Video SDK has no on-prem option; data residency blocked |
| Operational | Can people run it day-2? | No 24x7 review team for failed liveness |
| Economic | Do benefits beat costs at realistic volumes? | Per-KYC fee > contribution on small tickets |
| Legal | Is it allowed with controls we can evidence? | Regulator allows video KYC only with specific liveness + audit trail |
| Schedule | Can we go live by the needed date? | Vendor lead time 16 weeks; sponsor wants 6 |

Feasibility is **go / conditional go / no-go**, not a vibe. Conditional go: “Phase 1 salaried digital loans only; branch KYC remains for NRI and high-risk.”

## Impact analysis for a change request

When someone says “also add…,” map impact before saying yes.

| Impact area | What to check | Video KYC CR example: “add vernacular IVR help during video” |
|---|---|---|
| Requirements | New, changed, retired IDs | New FR for language select; NFR for wait time |
| Process | Extra steps, SLAs, exceptions | Agent barge-in process if video fails |
| Data | New fields, retention, PII | `kyc_language`, longer session logs |
| Reports | Dashboards, regulatory MIS | Drop-off by language |
| Training | Scripts, SOP, UAT users | CKYC ops + branch fallback |
| Other systems | Upstream/downstream | CRM case, LOS, CKYC upload, storage |

## Weak vs strong

| Weak | Strong |
|---|---|
| Benefits: better experience. | Benefits: 28% of drop-offs cite “must visit branch”; assume 40% of those convert; ₹Z extra book. |
| Feasible: yes, other banks do it. | Legal: allowed for resident individuals with liveness; NRI out of scope this phase. |
| Impact: small CR. | Impact: 4 FRs, 1 NFR, CKYC file format, 7-year storage, 2 reports, 1 vendor. |
| ROI: 300%. | Payback 18 months; sensitivity: if adoption < 30%, payback > 3 years — flag to sponsor. |

## Real-world examples

**ShopEase** CBA for reverse-pickup: build + 3PL fees vs lower return-handling cost and higher repeat purchase.

**MediCare+** feasibility for WhatsApp reminders: technical yes, legal (consent) conditional, operational yes if templates approved.

**ShieldSure** impact analysis when IRDAI changes claim TAT: process, reports, SLA clocks, training — not only a banner on the portal.

## Scenario / Use case: NovaBank video KYC vs branch KYC

**Context.** Digital lending conversion dies at “visit branch for KYC.” Product wants video KYC in 8 weeks. Compliance is nervous. Ops has 40 CKYC clerks in two cities. Sponsor asks the BA: “Is this feasible and worth it?”

**What the BA produces.**

1. **Options:** A) status quo branch; B) vendor video KYC + branch fallback; C) in-house video (rejected on schedule).
2. **CBA:** costs (vendor, build, storage, training) vs benefits (time, conversion, fewer branch slots). Payback narrative with volume assumption.
3. **Feasibility:**

| Lens | Verdict | Note |
|---|---|---|
| Technical | Conditional | Vendor SDK + existing LOS; video storage vendor must be India-resident |
| Operational | Conditional | Business hours review; night applications queue to next morning |
| Economic | Go | Payback ~18 months at 35%+ adoption |
| Legal | Conditional | Resident individual, liveness, audit trail; NRI and non-face-to-face high-risk stay branch |
| Schedule | No for 8 weeks | 14-week realistic; recommend phased |

4. **Impact if approved:** KYC requirements rewrite, LOS states, CKYC upload, reports to compliance, RM training, branch still for exceptions.

**Recommendation.** Conditional go: vendor video KYC for salaried resident digital loans; branch remains fallback; 14-week plan; CR process for language pack later.

**If ignored.** Team promises 8-week video KYC, legal blocks go-live, or videos are stored in a non-compliant bucket. Conversion still dies.

## Notes

- CBA: list build, license, training, ops costs against time saved, error reduction, and revenue — with named assumptions.
- Defend payback and simple ROI; hand NPV/IRR to Finance.
- Feasibility is five gates: technical, operational, economic, legal, schedule.
- Impact analysis is mandatory on CRs: requirements, process, data, reports, training, other systems.
- Video KYC vs branch is a feasibility + CBA decision, not a UI decision.
- How this sits in a sponsor pack, budget, and org change: [business case, organisation, and change](09-business-case-org-structure-change.md).
