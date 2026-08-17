# Supporting Documentation

Requirements do not stand alone. **Business rules, assumptions, constraints, scope, dependencies, and risks** must be written so they can be found, owned, and tested.

They may appear as **sections inside** a BRD/FRD/SRS or as **separate registers** linked by ID. Both are valid. Mixing them as unmarked sentences in a paragraph is not.

## Why it matters for a BA

ShopEase Easy Returns will leak money if the innerwear rule lives only in a Slack thread. NovaBank fund transfer will double-debit if the payment-switch dependency is a rumour. Supporting docs are how you make the hidden environment of a requirement visible.

## Sections vs separate registers

| Item | Inside a document (section) | Separate register | Use when |
|---|---|---|---|
| Business rules | Short list invoked by this FRD | Enterprise rule catalog | Rules reused across products |
| Assumptions | BRD / SRS overall description | Assumption log with review dates | Many teams; long program |
| Constraints | Same | Architecture / compliance constraint register | Org-wide (RBI, HIPAA-like, platform) |
| Scope | Every BRD / release brief | Scope baseline per release | Multiple workstreams |
| Dependencies | Per requirement + summary table | RAID or dependency board | Vendor/API heavy |
| Risks | BRD risk table | RAID log with PM | Project-level tracking |

**Rule of thumb:** if it is reused or lives longer than one project, give it a register and **cite the ID** in the BRD. If it is local to one MVP, a section is enough — still with IDs.

## Business rules documentation

Template fields: Rule ID, statement, type, source, owner, effective dates, scope, exception, related FRs, status.

### Filled — ShopEase

| Field | Content |
|---|---|
| Rule ID | BRULE-RET-007 |
| Statement | Innerwear (category INNERWEAR) is not returnable after 7 calendar days from delivery_date, except DAMAGED_ON_DELIVERY with photos. |
| Type | Constraint |
| Source | Category Policy v3.2 §4.1 |
| Owner | Head of Category Policy |
| Exception | Seller override only if seller_contract.return_override = Y and refund is seller-funded |
| Related | FR-RET-012, FR-RET-020 |

### Filled — NovaBank

| Field | Content |
|---|---|
| Rule ID | BRULE-PAY-04 |
| Statement | Beneficiary added < 30 minutes ago: max transfer ₹5,000 per transaction until cooling-off ends. |
| Type | Constraint |
| Source | Fraud policy 2025-03 |
| Owner | Head of Digital Fraud |
| Exception | None for retail app; branch manager may not waive in app channel |
| Related | FR-03 in FRD-FT-01 |

## Assumptions documentation

Template: ID, assumption, owner, how we will validate, date, impact if false, status (open/confirmed/invalid).

### Filled — ShopEase

| ID | Assumption | Owner | Validate by | If false | Status |
|---|---|---|---|---|---|
| ASM-RET-01 | 90% of delivered orders have a scan event we can use as delivery_date | Logistics BA | Data sample 10k orders, 15 May | Window calculation breaks; need carrier ETA fallback | Open |
| ASM-RET-02 | Seller master has return_override flag for CottonCart | Seller ops | Query seller master | 15-day badge conflict unresolved | Open |

### Filled — NovaBank

| ID | Assumption | Owner | Validate by | If false | Status |
|---|---|---|---|---|---|
| ASM-PAY-03 | 92% of retail CIF records have a valid mobile for OTP | CIF data owner | Query, 1 Jun | 2FA coverage gap; branch fallback volume | Open |

**Weak:** “Assuming SMS works.”
**Strong:** ASM-PAY-03 with a query and a date.

## Constraints documentation

Template: ID, constraint, type (time, budget, tech, legal, operational), source, requirements affected.

### Filled — ShopEase

| ID | Constraint | Type | Source | Affects |
|---|---|---|---|---|
| CON-RET-01 | Must use logistics API v3; no new courier master this release | Technical | Architecture decision AD-44 | Reverse pickup FRs |
| CON-RET-02 | No raw card data in returns service | Legal / PCI | Security standard | Refund-to-instrument design |

### Filled — NovaBank

| ID | Constraint | Type | Source | Affects |
|---|---|---|---|---|
| CON-PAY-01 | Daily IMPS cap ₹2,00,000 for this segment (config) | Policy | Product tariff | FR-02, BRULE-PAY-07 |
| CON-PAY-02 | Go-live before 15 Nov (audit window) | Time | Compliance calendar | Scope of MVP |

## Scope documentation

Template: in-scope list, out-of-scope list, window (release), owner of scope changes (CR).

### Filled — ShopEase Easy Returns (release R1)

**In-scope:** logged-in app + mobile web returns; reason + photos; seller notify; refund original instrument; migrate open RMAs.

**Out-of-scope:** guest returns; international; replacement flow; new couriers; in-store.

**Scope owner:** Head of CX. Changes via CR only after baseline 1.0.

### Filled — NovaBank fund transfer (this FRD)

**In-scope:** debit savings → saved beneficiary; IMPS/NEFT; 2FA; cooling-off cap.

**Out-of-scope:** add-beneficiary UI (FRD-BEN-01); international wires; corporate users.

Write out-of-scope as seriously as in-scope. It is a stakeholder management tool.

## Dependency documentation

Template: ID, this requirement/work, depends on, owner of the other side, needed-by date, status.

### Filled — ShopEase

| ID | We need | From | By | Status |
|---|---|---|---|---|
| DEP-RET-01 | Logistics pickup slot API v3 latency < 2s p95 | Logistics platform team | 1 Jun | In progress |
| DEP-RET-02 | Seller webinar completion list | Seller ops | Cutover −2 days | Not started |

### Filled — NovaBank

| ID | We need | From | By | Status |
|---|---|---|---|---|
| DEP-PAY-01 | Payment switch idempotency key support | Switch vendor | Sprint 4 | Confirmed in interface spec v2.1 |
| DEP-PAY-02 | SMS DLT template approval | Ops + aggregator | 20 May | Open |

FR-05 (timeout/PENDING) is unsafe until DEP-PAY-01 is true.

## Risk documentation

Template: ID, risk, likelihood, impact, owner, mitigation, linked requirements.

### Filled — ShopEase

| ID | Risk | L | I | Owner | Mitigation |
|---|---|---|---|---|---|
| RSK-RET-01 | Seller badge vs 7-day innerwear → legal complaint | M | H | Category + Legal | BRULE-RET-007 exception + listing display FR-RET-020 |
| RSK-RET-02 | Photo upload fails on low network → evidence skipped | H | M | App eng | Compression; retry; block complete without photos for those categories |

### Filled — NovaBank

| ID | Risk | L | I | Owner | Mitigation |
|---|---|---|---|---|---|
| RSK-PAY-01 | Double debit on switch timeout | M | H | Payments BA + vendor | FR-05 pending + idempotency; UAT chaos test |
| RSK-PAY-02 | ASM-PAY-03 false (no mobile) | L | H | Digital PO | Branch fallback FR; volume estimate |

PM may own the RAID log. The BA owns **requirement and process risks** and must still write them.

## How a BA keeps these alive

- Review assumptions weekly until confirmed or replaced by facts.
- Never let a constraint hide inside an FR sentence without a CON ID if it will be argued later.
- When a CR lands, update scope, deps, and risks in the same change.

MediCare+ reminder SRS cites CON (DLT templates), DEP (SMS aggregator), ASM (email present for 40% of patients), RSK (SMS looks like phishing). Those IDs belong in supporting docs, not only in NFR prose.

## Notes

- 
