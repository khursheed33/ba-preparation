# Conflicts, Ambiguity, Completeness, Quality, Feasibility, and Volatility

A requirement set can be signed and still be dangerous. This file is the quality lens: **conflicts**, **ambiguity**, **completeness**, **quality**, **feasibility**, and **volatility**.

## Why it matters for a BA

ShopEase “fast search” will ship as a full-text query that kills the database while SEO wants every SKU indexed. Nobody was wrong in a meeting; the words were empty and the conflict was hidden. Quality is how you stop that.

## Conflicts

A **conflict** is two (or more) requirements that cannot all be true, or two stakeholders demanding opposite behaviour.

Types:

- Policy vs policy (7-day innerwear vs seller 15-day badge)
- Goal vs goal (SEO completeness vs search latency)
- User vs compliance (fewer KYC clicks vs RBI)
- Functional vs NFR (log every search term vs privacy)

BA process: detect → make visible → options → decision log → update IDs. Do not average two policies into mush.

NovaBank: operations wants fewer screens on UPI mandate setup; finance wants a maker-checker. That is a conflict to resolve, not two stories both marked Must.

## Ambiguity

**Ambiguous** requirements can be interpreted two ways. If QA and the PO would draw different tests, it is ambiguous.

### Words to avoid — and rewrites

| Avoid | Why it fails | Rewrite |
|---|---|---|
| User-friendly | No measure | First-time ShopEase return: ≤ 3 fields; error text names field + fix; WCAG 2.1 AA |
| Fast | No number, no load | Search p95 ≤ 800 ms for 5,000 concurrent users with 2M active SKUs |
| Flexible | Hidden extra scope | Seller may set return window only within platform min/max for that category |
| Intuitive | Unfalsifiable | 8/10 usability-test participants complete checkout without help |
| Seamless | Poetry | No extra login between cart and payment if session is valid |
| Robust | Vague | Recover from payment-gateway timeout: retry once, then show fail + order not created |
| Etc. / and so on | Open list | List the values or say “values in table T_REASON” |
| Support | Noun pretending to be a requirement | Define the exact support actions: view RMA, add note, issue refund |
| Optimal / best | No criterion | Choose the courier with lowest promised TAT among partners with SLA ≥ 95% |
| Real-time | Often false | Status visible within 5 seconds of warehouse scan event |
| 24/7 | Rarely true | 99.5% availability excluding Sunday 02:00–04:00 IST |

ShieldSure: “process claims efficiently” → TAT p95 ≤ 4 business hours from complete pack.

MediCare+: “remind patients properly” → SMS 24h before + email 2h before if email on file; stop if cancelled.

## Completeness

**Complete** does not mean “every future idea.” It means, for the agreed scope, no silent holes.

### Completeness checklist

- [ ] Happy path for each in-scope user task
- [ ] Alternate and exception paths (fail, timeout, duplicate, permission denied)
- [ ] Business rules referenced, not implied
- [ ] NFRs for performance, security, availability that matter in this scope
- [ ] Data: source, validation, retention
- [ ] Roles and permissions
- [ ] Notifications and their triggers
- [ ] Reports / reconciliation if finance is a stakeholder
- [ ] Transition: training, migration, rollback
- [ ] Dependencies, assumptions, constraints listed
- [ ] Out of scope written
- [ ] Each requirement has ID, owner, acceptance idea
- [ ] Conflicts logged or resolved
- [ ] Regulatory obligations in scope are present

Gap example: NovaBank fund transfer FR covers success, not “beneficiary added less than 30 minutes ago” cooling-off — incomplete, not just a missing NFR.

## Quality

Quality attributes of a **single** requirement (writing file in Phase 3 goes deeper):

| Attribute | Test |
|---|---|
| Clear | One reading, one meaning |
| Concise | No essay |
| Testable | A test can fail |
| Measurable | Number, date, or binary condition |
| Unambiguous | Words from the avoid-list are gone |
| Atomic | One test, one ID |
| Consistent | No clash with another ID |
| Traceable | Parent need and child tests exist |

## Feasibility

**Feasibility** asks: can this be done with our time, skill, vendors, data, and law?

- Technical: can the EMR API support hold-the-slot?
- Operational: can 200 sellers attend training before Diwali?
- Legal: can ShopEase offer 15-day innerwear returns?
- Economic: is video KYC for every password reset affordable?

An infeasible Must is a planning defect. The BA raises it early with options (descope, extra time, different solution).

QuickBite: “compensate every order arriving 1 minute late” may be feasible technically and infeasible economically.

## Volatility

**Volatility** is how often a requirement changes.

| Often volatile | More stable |
|---|---|
| Promo rules, UI copy, campaign banners | Core identity (customer cannot see another’s orders) |
| Search ranking boosts, SEO experiments | Regulatory KYC facts (until the circular changes) |
| Notification wording | Accounting: refund to original instrument |
| Thresholds (FOIR %, return days) if hard-coded | The *existence* of a FOIR check |

How to handle volatility:

- Isolate volatile parts as **configuration** (return days, TAT hours), not code-like FRs that need a CR for every tweak — still version the *policy*.
- Shorter cycle for volatile items (feature flags).
- Do not baseline marketing copy in the same document version as security NFRs.
- Watch “unstable stakeholders” as a risk: if the owner changes weekly, freeze decisions in the log.

## Weak vs strong

| Weak | Strong |
|---|---|
| Fast search | p95 ≤ 800 ms under stated load; define what “search” includes |
| Two teams both Must | Conflict log + one decision |
| FRD of 200 pages, no exceptions | Completeness checklist passed for MVP scope |
| “We’ll see if it’s possible in sprint 6” | Feasibility spike *before* Must commitment |

## Scenario / Use case: ShopEase “fast search”

**Context.** SEO team: “Search must return every in-stock SKU including long-tail titles for Google-like completeness; ranking should include popularity.” Performance team: “Search is slow at sale events; we will drop fuzzy match and cap results at 20.” Product says: “Make search fast and user-friendly.” Festival sale in 6 weeks.

**Stakeholders.** SEO, performance/SRE, search engineering, category, buyers, BA, PO.

**What the BA does.**

1. Kill ambiguous words. Rewrite into NFRs and FRs.
2. Expose the conflict: completeness (recall) vs latency (p95).
3. Options: (A) two-tier search — exact + fuzzy only if p95 budget remains; (B) cap 50 results but guarantee in-stock filter; (C) dedicated search cluster (cost/feasibility).
4. Completeness: include out-of-stock behaviour, typo handling, Hindi transliteration — or mark Won’t.
5. Volatility: ranking boosts are config; latency NFR is baselined.

**Sample rewrites.**

| Bad | Good |
|---|---|
| Search must be fast | NFR-SRCH-P01: Search API p95 ≤ 800 ms at 5k RPS during sale, 2M active SKUs |
| User-friendly results | FR-SRCH-04: Results show title, price, delivery ETA, in-stock badge; empty state offers 3 category links |
| Flexible ranking | FR-SRCH-09: Default rank = relevance then popularity; merchandising boosts from config table, max 3 SKUs |

**Decision:** Must = latency NFR + in-stock filter. Should = fuzzy match if p95 headroom ≥ 200 ms. SEO full recall of every SKU in one page = Won’t (pagination + filters instead).

**What goes wrong if ignored.** SEO wins a “return 10,000 hits” FR. Sale day: search p95 is 9 seconds. Conversion collapses. Performance emergency-disables search. Both teams say they followed requirements.

## Notes

- 
