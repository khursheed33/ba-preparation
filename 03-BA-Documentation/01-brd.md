# Business Requirements Document (BRD)

A **BRD** is a document that states the **business problem, outcomes, scope, stakeholders, and high-level requirements** so sponsors and delivery teams share one baseline of *why* and *what* — not the detailed system design.

## Why it matters for a BA

If ShopEase jumps to screens, “Easy Returns” becomes a button with no success metric. The BRD is where leadership agrees the problem is worth solving. In many Indian IT programs (banks, hospitals, insurers) a BRD is still the gate to funding.

## When used

- Waterfall or hybrid programs that need a funding / steering baseline
- Vendor RFP (vendors bid on business scope, not only stories)
- Cross-department work (returns touches warehouse, finance, sellers)
- Compliance-heavy work where auditors ask “what was approved?”

Less common as a giant static book in pure Scrum — but the **content** still exists as a lean brief, epic outcomes, or Confluence “why.”

## Who writes and who reads

| Role | Relation to BRD |
|---|---|
| BA | Usually authors and facilitates |
| Product owner / sponsor | Owns the business need; signs |
| Business SMEs | Provide process and rules |
| Architecture / IT | Read constraints; do not turn BRD into a design spec |
| PM | Schedule and cost from scope |
| QA | Early view of what “success” means |
| Vendors | Scope of what they must meet |

## Typical sections

| Section | Purpose |
|---|---|
| Document control | Version, authors, approvers |
| Executive summary | One page: problem, ask, outcome |
| Problem / opportunity | Why now |
| Business objectives | Measurable |
| In-scope / out-of-scope | Creep control |
| Stakeholders | Who cares / who signs |
| High-level requirements | Business and stakeholder level, not every field |
| Success metrics | How we know we won |
| Assumptions, constraints, dependencies, risks | Honesty |
| High-level process (optional as-is/to-be) | Shared picture |
| Approval | Baseline |

A BRD is **not** an FRD. It should not list every validation message.

## Mini BRD excerpt: ShopEase “Easy Returns”

**Document:** BRD-RET-001 Easy Returns  
**Version:** 1.0 baseline  
**Author:** BA (Digital CX)  
**Approvers:** Head of CX, Head of Category Policy, Finance controller, Logistics ops

### Problem

Return-to-refund average is 9 days. Buyers call support (22% of return-related contacts). Sellers cannot see return reason before reverse pickup closes. Fraudulent returns are 0.9% of return GMV — any “easier” flow must not push this above 1.2%.

### Objectives

| ID | Objective | Metric | Target | Date |
|---|---|---|---|---|
| OBJ-01 | Faster refunds | Avg return-to-refund | ≤ 4 days | 2 quarters post go-live |
| OBJ-02 | Deflect calls | Return-related contacts | −30% | 2 quarters |
| OBJ-03 | Seller visibility | % RMAs with reason before pickup close | ≥ 95% | Go-live + 30 days |
| OBJ-04 | Control fraud | Fraudulent return GMV | ≤ 1.2% | Ongoing |

### Scope

**In-scope**

- Logged-in buyers: request return from My Orders (app + mobile web)
- Reason codes, photo evidence for selected categories
- Seller notification and reason visibility
- Reverse pickup via existing logistics API v3
- Refund to original instrument after QC or seller accept (per policy)
- Innerwear and other category rules from policy v3.2

**Out-of-scope**

- Guest returns without order login
- International orders
- Replacement-only flow (phase 2)
- New courier partners
- In-store returns

### Stakeholders

| Stakeholder | Interest |
|---|---|
| Buyers | Faster, clearer returns |
| Sellers | Reason + evidence; who pays |
| Warehouse QC | Photos, reason, scan-in |
| Finance | Refund instrument, leakage |
| Support | Deflection, consistent policy |
| Category policy | Rule owner |
| Logistics | Pickup slots |

### High-level requirements

| ID | Statement |
|---|---|
| BR-01 | Buyers can initiate eligible returns without calling support. |
| BR-02 | System enforces category return windows and non-returnable rules, including innerwear 7-day constraint (BRULE-RET-007). |
| BR-03 | Sellers receive reason and evidence before reverse pickup is closed. |
| BR-04 | Refunds go to the original payment instrument after policy QC/accept. |
| BR-05 | Open RMAs migrate from the old portal with no unknown status. |

(Detail belongs in FRD/stories: fields, errors, NFRs.)

### Success metrics

Same as objectives OBJ-01–04; dashboard owned by CX ops; review at 30/60/90 days.

### Assumptions

- ASM-01: 90% of delivered orders have a scannable tracking event (logistics).
- ASM-02: Sellers with override contracts are flagged in seller master (to be verified).

### Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Seller 15-day badge vs 7-day innerwear | Legal + leakage | Decision on override + who pays (see business rules) |
| Photo upload fails on 4G | Incomplete evidence | Compress images; allow retry; NFR on upload |
| Migration of open RMAs | Duplicate refunds | TR-RET-01 dual-run 7 days |

### Constraints

- Must use logistics API v3.
- PCI: no extra card data in returns flow.

## BRD vs Agile artifacts

| BRD world | Agile world | Same job |
|---|---|---|
| BRD objectives | Product goal / epic outcomes | Why |
| High-level BRs | Epics / capabilities | What at altitude |
| Scope in/out | Release MVP + Won’t list | Creep control |
| FRD / SRS | Stories + AC + NFR spikes | Buildable detail |
| Sign-off on BRD | Sprint + release approval | Baseline |

**Weak:** 80-page BRD that includes button colours, then ignored in Jira.
**Strong:** 10–20 page BRD for Easy Returns; FRs in catalog/stories; BR IDs trace to stories.

If the organization is Agile-only, still write a **one-pager BRD equivalent** before a large epic. Do not skip the thinking because the template died.

## Notes

- 
