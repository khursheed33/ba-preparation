# Change Requests, RTM, and UAT Documentation

Three artifacts keep delivery honest after elicitation: the **change request (CR)**, the **requirement traceability matrix (RTM)**, and **UAT documentation**.

## Why it matters for a BA

ShieldSure adding “cashless garage” after sprint 3 without a CR will smash the claims baseline. An RTM with a hole will miss an NFR and ship a production bug. UAT without scripts is a tour, not acceptance.

## Change request documentation

A **CR** is the controlled proposal to change baselined requirements (or scope, rules, NFRs).

### Fields (use all of them)

| Field | Purpose |
|---|---|
| CR ID | Unique: CR-SS-17 |
| Date / requester | Who asked |
| Product / baseline | Claims app v1.0 / SRS v1.0 |
| Description | What would change |
| Reason / business need | Why, not only the feature name |
| Proposed solution (optional) | May be refined by BA |
| Requirements impacted | IDs old → new |
| Impact analysis | Stories, tests, data, vendor, training, cost, schedule, risk, ops |
| Priority / urgency | Regulatory vs nice |
| Alternatives | Including “do nothing” |
| Decision | Approve / defer / reject |
| Approvers | Named |
| Implementation version | Target release; catalog versions 1.0 → 1.1 |

### Filled CR — ShieldSure “cashless garage” after sprint 3

| Field | Content |
|---|---|
| CR ID | CR-SS-17 |
| Date | 8 Aug 2026 |
| Requester | Head of Motor Claims |
| Baseline | Motor claims digital v1.0 (sprint 3 shipped FNOL + document upload only) |
| Description | Add cashless repair at network garages: eligibility, estimate, insurer approval, pay garage. |
| Reason | 40% of motor claims are already network repairs on paper; customers still pay cash and wait reimbursement. Renewal season in 11 weeks. |
| Impacted reqs | New BR-CLM-08; FR-CLM-31..40; NFR-CLM-T01; TR-CLM-05 garage training. No change to FR-CLM-10 FNOL except new status CASHLESS_ELIGIBLE. |
| Impact analysis | **Dev:** 5 sprints if garage portal in scope; 3 if portal phase-2 and WhatsApp estimates. **Vendor:** garage master API. **QA:** new UAT pack. **Finance:** payee = garage, not customer. **Risk:** leakage if network table stale. **Training:** 80 claims staff. **Dependency:** network table daily feed (DEP-CLM-09). |
| Alternatives | (A) Full cashless now (B) Eligibility flag + manual cashless in existing ops tool (C) Defer to post-renewal. **Recommended B** for this season, A as 2.0. |
| Decision | Approved option B, 12 Aug. Option A = Won’t this release (decision DL-CLM-11). |
| Approvers | Claims head, Finance, Digital PO, Compliance |
| Versions | SRS 1.0 → 1.1; FR-CLM-31 v1.0 added |

**Weak CR:** “Please add cashless, sprint 4.”
**Strong CR:** the table; impact on payee and network table called out.

## RTM — Requirement Traceability Matrix

An **RTM** is a table that links **business need → functional (or NFR) → story → test case → UAT (and often release)**.

Purpose: coverage (nothing forgotten), impact (what to retest on a CR), audit.

### Typical columns

BR | Req ID | Type | Story | Test case | UAT script | Release | Status

### Sample 8-row matrix (ShieldSure motor claims 1.1)

| BR | Req | Type | Story | Test case | UAT | Release |
|---|---|---|---|---|---|---|
| BR-CLM-01 FNOL in app | FR-CLM-10 Capture incident + photos | FR | SS-201 | TC-110 Photo required | UAT-S1 FNOL happy | 1.0 |
| BR-CLM-01 | NFR-CLM-P01 FNOL submit p95 ≤ 2s | NFR | SS-201 | TC-111 load 200 users | UAT-N1 (perf sign-off) | 1.0 |
| BR-CLM-08 cashless | FR-CLM-31 Cashless only if garage in network on incident_date | FR | SS-310 | TC-310 Inactive garage blocked | UAT-S8 cashless eligibility | 1.1 |
| BR-CLM-08 | FR-CLM-32 Upload estimate + photos | FR | SS-311 | TC-312 Estimate PDF + JPEG | UAT-S8 | 1.1 |
| BR-CLM-08 | NFR-CLM-T01 p95 decision ≤ 4 business hours | NFR | SS-312 | TC-390 TAT clock | UAT-N2 TAT | 1.1 |
| BR-CLM-08 | TR-CLM-05 Train 80 claims officers | TR | SS-319 | TC-501 Training attendance | UAT-T1 sandbox 10 cases | 1.1 |
| BR-CLM-02 pay correctly | FR-CLM-40 Pay garage, not customer, when cashless approved | FR | SS-318 | TC-340 Payee = garage_id | UAT-S9 payout | 1.1 |
| BR-CLM-03 leakage control | NFR-CLM-S02 RC copy mandatory before approve | NFR/FR mix — **FR-CLM-33** | SS-313 | TC-333 no RC → cannot approve | UAT-S8 | 1.1 |

Row 2 and row 5 are NFRs **with tests**. If NFR rows are missing, RTM is decoration.

ShopEase Easy Returns would add a row: BR-01 → FR-RET-012 window → SE-88 → TC-RET-07 → UAT-R3.

## UAT documentation

**UAT** is business acceptance that the solution meets the need in a production-like setting. The BA often writes or co-writes the pack; business users execute.

### UAT plan outline

1. Scope of UAT (which reqs / which sites)
2. Entry criteria (dev done, SIT passed, data ready, users trained)
3. Environment and data (no real PAN in logs; masked)
4. Roles: UAT lead, executors, BA, defect manager
5. Schedule and windows
6. Defect severity rules (what blocks sign-off)
7. Exit criteria (all Must scenarios pass; open Sev-2 waived in writing)
8. Trace to RTM
9. Sign-off form

### UAT script sample (ShieldSure)

**Script UAT-S8** — Cashless eligibility  
**Traces:** FR-CLM-31, FR-CLM-33, TC-310, TC-333  
**Tester:** Claims officer  
**Data:** Garage G-992 active; Garage G-118 inactive as of yesterday; claim with RC; claim without RC.

| Step | Action | Expected |
|---|---|---|
| 1 | Create FNOL, choose G-992 | Status allows cashless request |
| 2 | Submit estimate + RC | Status = pending insurer |
| 3 | New FNOL, choose G-118 | Cashless blocked; reason NET-INACTIVE; reimbursement path offered |
| 4 | G-992, estimate, no RC | Approve action disabled; message RC required |

Pass/fail, actual result, evidence (screenshot), tester name, date.

### Sign-off form fields

- Product / version / environment
- Scope statement (what is accepted)
- RTM version
- Open defects (IDs, severity, waivers)
- Statement: “Meets approved requirements for this release”
- Names, roles, dates, signatures (or e-sign)
- Conditions (e.g. NFR-CLM-T01 to be monitored 14 days in production)

**Weak UAT:** “Users clicked around and liked it.”
**Strong UAT:** scripts traced to Must reqs, including NFRs.

## Scenario / Use case: production bug because RTM missed an NFR

**Context.** ShieldSure 1.1 cashless ships. Functional UAT-S8 passed. NFR-CLM-T01 (4-hour decision TAT) was in the SRS but **not in the RTM**, so no TC-390, no UAT-N2. In production, estimates sit 36 hours because the assignment queue was never built (story skipped; no trace from NFR to backlog). Garages complain. IRDAI-facing team asks for TAT evidence. There is none.

**Stakeholders.** Claims, garages, QA, PO, BA, compliance.

**What the BA does after (and should have done before).**

- RTM rule: every NFR has a test type (perf, TAT report, security scan) or an explicit “monitored in prod” with an owner.
- CR not required for the NFR — it was already approved — this is a **coverage defect**.
- Emergency story SS-312, test TC-390, UAT-N2, hotfix release 1.1.1.
- Add RTM review as exit criterion: zero approved reqs with blank test column.

**What goes wrong if ignored.** Business signed UAT on happy-path screens. The quality attribute that justified cashless (speed) never existed. Sign-off was on the wrong evidence.

NovaBank analogue: NFR session timeout 5 minutes missing from RTM → UAT on a laptop that never idled → production shared-kiosk fraud.

## Notes

- 
