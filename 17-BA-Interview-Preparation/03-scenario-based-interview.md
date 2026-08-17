# Scenario-Based Interview

## Definition

Interviews that put you in a messy situation: **ambiguous requirements**, **conflicting or difficult stakeholders**, **changing requirements**, **missed requirements**, **scope creep**, **tight deadlines**, **production issues**, **requirement conflicts**, and **data inconsistencies**.

Strong answers follow: **clarify → options → recommendation → communication → documentation**.

## Why it matters

They are not asking if you have a template. They are asking if you stay structured when people are loud.

### Weak vs strong

| Weak | Strong |
|---|---|
| “I would escalate immediately” as the whole answer | Clarify facts, give options, recommend, write it down |
| Taking a side in a conflict | Name the decision owner |

Use this spine every time:

1. **Clarify** the goal, users, in/out, evidence.  
2. **Options** (at least two) with impact.  
3. **Recommendation** with why.  
4. **Communication** who hears what.  
5. **Documentation** decision, CR, AC, RTM.

---

## Ambiguous requirements

**Scenario.** ShopEase PO: “Make returns like Amazon.”  
**Answer.** Clarify what “like” means (window, pickup, refund speed). Options: status SMS vs auto-approve vs chatbot. Recommend auto-approve Size < ₹2,000 based on 2.1-day seller wait. Communicate out-of-scope Amazon features. Document IDs, not the slogan.

## Conflicting stakeholders

**Scenario.** NovaBank credit wants more documents; digital wants fewer fields.  
**Answer.** Clarify the risk each is protecting (NPA vs drop-off). Options: progressive disclosure vs two products. Recommend mandatory PAN/salary slip, optional extra docs. Workshop both; PO/credit head signs. Document the mandatory list.

## Changing requirements

**Scenario.** Mid-sprint, MediCare+ ops wants WhatsApp not SMS.  
**Answer.** Clarify: channel vs message rules (psychiatry still suppressed?). Options: CR this sprint (slip) vs next increment. Recommend park WhatsApp; keep SMS+app. Communicate date impact. Document CR even if rejected.

## Difficult stakeholders

**Scenario.** ShopEase warehouse lead talks over everyone and calls your BRD “theory.”  
**Answer.** Clarify their KPI (QC fail rate). Invite a floor walk. Options: they co-own the QC-fail AC vs stay a reviewer. Recommend co-own. Communicate privately first, then in the decision mail. Document their rule in the table so they see themselves.

## Missed requirements

**Scenario.** UAT: psychiatry SMS went out; Dr. Mehta said “don’t” once in a workshop.  
**Answer.** Clarify incident vs spec gap. Options: hotfix suppress + RCA. Recommend hotfix same day; add specialty table; legal review. Communicate apology + timeline to doctors. Document missed stakeholder/requirement in RTM and a lesson.

## Scope creep

**Scenario.** “While you are in the code, add pickup-slot redesign.”  
**Answer.** Clarify if it serves the 4-day refund objective. Options: CR+slip vs phase 2. Recommend phase 2. Communicate to PM/PO. Document out-of-scope list update.

## Tight deadlines

**Scenario.** NovaBank demo in 10 days; BRD requested 40 pages.  
**Answer.** Clarify must-have for demo (checklist happy path). Options: thin baseline + stories vs fake 40 pages. Recommend hybrid: rules one-pager + 5 stories. Communicate compliance what is *not* in the demo. Document assumptions and demo scope.

## Production issues

**Scenario.** ShopEase auto-approve live; leakage spike; sellers furious.  
**Answer.** Clarify metric (false Size vs true Size). Options: kill switch vs tighten amount cap. Recommend kill switch for top seller tier tonight; sample QC. Communicate sellers and CX. Document incident, CR, new rule, UAT for the fix.

## Requirement conflicts

**Scenario.** Rule A: auto-approve Size. Rule B: SOP “seller confirms all returns in 24h.”  
**Answer.** Clarify which SOP is authoritative. Options: B exception when A true vs kill A. Recommend update SOP + seller notice. Communicate seller-ops. Document rule precedence.

## Data inconsistencies

**Scenario.** Dashboard says 34% NovaBank stall; ops says 28%.  
**Answer.** Clarify filters (gold loans? date? DISTINCT apps?). Options: one definition of “stall.” Recommend status_history DISTINCT + product code. Communicate both numbers until reconciled. Document the metric spec.

## Real-world examples (compressed)

QuickBite compensation: CX vs finance leakage cap — same spine. ShieldSure TAT vs incomplete FNOL photos — do not jump to a portal.

## Scenario / Use case: panel stacks two at once

**Context.** “Stakeholders conflict *and* the deadline is Friday.”  
**What you do.** Still the spine: you cannot skip clarify because of Friday. Recommend an MVP slice both parties can live with (NovaBank: PAN mandatory, extra docs later). Document the Friday demo as *not* the baseline.

**What goes wrong if ignored.** You pick the louder person and ship WhatsApp to psychiatry. Structure is the product you are selling in this round.

## Notes

- Spine: clarify, options, recommendation, communication, documentation.
- Cover all ten situation types with a named company and a decision owner.
- Missed requirements and production issues need RCA + artifact updates, not blame.
- Data fights are definition fights until proven otherwise.
- 
