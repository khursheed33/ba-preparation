# RTM, Business vs Production Validation, and Sign-off

## Definition

A **Requirement Traceability Matrix (RTM)** maps each requirement to design, tests, and results so nothing in-scope is untested and extra tests are visible.

**Requirement-to-test mapping** is the RTM core: Req ID → AC → test scenario/case IDs → result.

**Business validation** is confirmation that the solution meets the business need in UAT (or equivalent) — process works for users.

**Production validation** (often **hypercare**) is confirmation after go-live with real volume, real integrations, and real customers — dashboards, reconciliations, support queues.

**Sign-off** is a named person’s recorded acceptance of a scope, with date, version, and exceptions (known issues). It is a control, not a vibe in a meeting.

## Why it matters

Without an RTM, ShieldSure ships with an untested cashless exception. Without hypercare, UAT “green” hides a payment switch that only fails at 7 p.m. Without honest sign-off, known Sev3s become “someone said we were live.” Politics will pressure partial approval — the BA’s job is to make that **visible**, not to pretend it is full acceptance.

## RTM sample

| Req ID | Requirement (short) | AC | Test IDs | Level | Result | Defect | Evidence |
|---|---|---|---|---|---|---|---|
| BR-01 | Reduce missed first notice for claims | — | KPI report UAT-RPT-01 | UAT | Pass | — | Screenshot 12-Aug |
| FR-CLM-04 | Duplicate claim_id rejected | AC-2 | TC-CLM-12, TC-CLM-13 | System | Pass | — | QA run 10-Aug |
| FR-CLM-07 | Cashless pre-auth within network | AC-1–3 | TC-CLM-20–24, UAT-CLM-05 | Sys+UAT | Pass | — | — |
| FR-CLM-09 | SMS on status change | AC-1 | TC-CLM-30 | System | Fail | BUG-441 | Retest pending |
| NFR-02 | Pre-auth p95 < 8s | AC-1 | PERF-03 | NFR | Pass | — | Report |
| FR-CLM-11 | Reopen closed claim (maker-checker) | AC-1 | — | — | **Gap** | — | No test mapped |

The last row is the point of an RTM: **gaps scream**.

### Weak vs strong

| Weak | Strong |
|---|---|
| Excel of stories, no tests | Every FR/NFR has ≥1 test or a waiver |
| Sign-off = “LGTM” on chat | Version, scope list, known issues, name, date |
| UAT pass = production ready | Hypercare checklist + recon |
| Hide Sev3s to get a signature | Document, residual risk, owner, date to fix |

## Business validation vs production validation (hypercare)

| | Business validation (UAT) | Production validation (hypercare) |
|---|---|---|
| Data | Synthetic / masked | Real (with controls) |
| Volume | Sample | Peak, batch jobs, night files |
| Integrations | Sandbox | Live SMS, payment, TPA, 3PL |
| Users | Trained UAT users | All shifts, real customers |
| Success | Scenarios pass | KPI, defect inflow, recon, rollback unused |
| BA | War-room, RTM | War-room, compare prod to expected, CR vs bug |

Hypercare window (example): 1–2 weeks, daily severity review, named on-call, success metrics (e.g. failed IMPS < 0.2%, claim SMS fail < 1%).

## Sign-off checklist (and political reality)

**Checklist before recommending sign-off**

- Scope list matches what was built (and what was dropped)
- RTM: no unmapped in-scope FR; P0/P1 tests pass or waived
- Open defects: no Sev1/Sev2 **or** accepted in writing with workaround
- Known Sev3/Sev4 listed with owner and target date
- UAT evidence stored; executors named
- NFR: performance, access, audit — as agreed
- Support / SOP / training done
- Rollback / hypercare plan exists
- Approver is the **business owner**, not only the BA

**Political reality**

- **Partial sign-off:** “We accept claims capture; reports in phase 2.” Write it. Do not imply full.
- **Known issues:** shipping with 2 Sev3s is common; shipping without listing them is malpractice.
- Calendar go-live ≠ quality go-live. If leadership overrules, the BA records **risk acceptance** (who, what, residual).
- Never forge user UAT. Never “sign on behalf of” silently.

## Real-world examples

**NovaBank.** Business validation: maker-checker UAT. Production: first payday salary credits recon vs core.

**ShopEase.** UAT of flash-sale flag. Hypercare: inventory oversell at 12:00 launch.

**Government.** UAT on sample applications. Production: midnight filing spike.

## Scenario / Use case: ShieldSure go-live with 2 known Sev3s

**Context.** Cashless module must go live for a hospital network contract. Two Sev3s remain: (1) admin CSV export truncates long hospital names; (2) status filter “on hold” label shows as “hold” — users trained on it. No Sev1/Sev2. RTM complete except a deferred report FR (out of this release, on the partial sign-off).

**What the BA prepares**

| Item | Content |
|---|---|
| Sign-off form | Version 3.2.1, scope: pre-auth + SMS; out: MIS export v2 |
| Known issues | BUG-512 Sev3 export; BUG-518 Sev3 label; owner BI team; fix sprint+1 |
| Residual risk | Ops uses on-screen names; CSV is weekly workaround: copy from UI |
| Hypercare | 10 days; TPA recon daily; SMS fail %; war-room 9 a.m. |
| Approvers | Claims head (business), IT release manager, BA recommendation attached |

**If ignored.** Six months later “who approved the truncated export?” has no paper. Or go-live is blocked forever on cosmetics while the contract penalty runs.

## Notes

- RTM: requirement → test → result; gaps are the product.
- Requirement-to-test mapping is not optional for regulated domains (banking, insurance, health).
- Business validation = UAT fit-for-purpose; production validation = hypercare with real load.
- Sign-off is named, dated, versioned, and exception-listed.
- Partial sign-off and known issues are legitimate if written.
- The BA recommends; the business accepts residual risk.
- Do not close known Sev3s as “not a bug” to clean the dashboard for go-live.
- Hypercare KPIs belong in the same family as UAT exit criteria, not as a surprise.
