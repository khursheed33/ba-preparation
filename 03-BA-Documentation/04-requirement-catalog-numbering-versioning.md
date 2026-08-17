# Requirement Catalog, Numbering, and Versioning

A **requirement catalog** (requirement register) is the **master list of requirement IDs** with status, version, owner, and source. Documents (BRD, FRD, SRS, Jira) are views. The catalog is the spine.

## Why it matters for a BA

Two BAs on MediCare+ will both invent “FR-01” for different things. QA will test the wrong line. ShopEase returns will have three “the 7-day rule” paragraphs and no ID. Numbering and versioning are how you prevent chaos when the team grows.

## What belongs in the catalog

| Column | Purpose |
|---|---|
| ID | Stable handle |
| Title / statement | Current wording |
| Type | BR / ST / UR / FR / NFR / TR / TECH |
| Module | RET, APT, PAY |
| Source | Workshop, RBI, policy v3.2 |
| Owner | Role |
| Status | Draft / in review / approved / live / retired |
| Version | 0.1, 1.0, 1.1 |
| Baseline | Which pack (SRS v1.0) |
| Trace parent | BR-01 |
| Notes / CR | CR-19 |

Tools: Excel/Sheets, Jira with a Req ID field, Azure DevOps, DOORS, Confluence + database. The tool is secondary. Uniqueness is not.

## Numbering schemes

Pick a scheme and publish it on page one of the catalog. Do not mix schemes in one product.

### Pattern A — type + sequence

`BR-001`, `FR-014`, `NFR-003`

Simple. Gets painful when many modules share FR-014.

### Pattern B — type + module + sequence (preferred for programs)

| ID | Meaning |
|---|---|
| BR-001 | Business requirement 1 (few; can stay global) |
| FR-RET-012 | Functional, Returns module, item 12 |
| NFR-SEC-003 | NFR, security category, item 3 |
| NFR-PER-002 | NFR, performance |
| TR-RET-01 | Transition, returns |
| BRULE-RET-007 | Business rule (rules catalog, linked) |

### Pattern C — project prefix

`SE-FR-RET-012` (ShopEase) when multiple products share a Jira project.

**Rules that prevent chaos**

1. **Never reuse an ID.** If FR-RET-012 is retired, it stays retired. Next is FR-RET-013.
2. **IDs are not ordered by priority.** FR-RET-012 is not “more important” than 011.
3. **Allocate blocks** if two BAs work in parallel: BA-A uses FR-RET-100–199, BA-B 200–299, or a shared ID issuer (even a sheet with `=MAX+1` and a lock).
4. **Do not number by sprint.** Sprint 3’s story can implement FR-RET-012 created in sprint 1.
5. **NFR categories in the ID** (SEC, PER, AVA, USE, SCA, COM, MNT) make test-type obvious.
6. **Stories get their own keys** (SE-441). They **reference** FR IDs; they are not a substitute ID.

NovaBank example: `FR-PAY-01` fund transfer 2FA; `NFR-SEC-003` session timeout — different types, do not both be “FR-99.”

## Versioning

Version the **requirement** and the **document pack**.

| Version | Meaning |
|---|---|
| 0.1 | Draft, elicitation |
| 0.3 | After analysis, not approved |
| 1.0 | **Baseline** — approved sign-off |
| 1.1 | After CR (small additive/corrective) |
| 1.2 | Next CR |
| 2.0 | Major re-baseline (new module or rewrite) |

**0.x** = not approved for build as a contract. **1.0** = build against this. A typo fix in wording that does not change tests can be 1.0.1 if your standard allows; if the test would change, it is 1.1 via CR.

ShopEase: FR-RET-012 v1.0 “reject innerwear after 7 days.” CR-22 adds damaged-on-delivery exception → v1.1. Tests update. Trace stays on the same ID.

## Change history table (example)

Document: FRD-RET Easy Returns

| Version | Date | Author | CR | What changed |
|---|---|---|---|---|
| 0.1 | 02 May | BA A | — | First draft from workshop |
| 0.2 | 09 May | BA A | — | Added seller notify FRs |
| 1.0 | 20 May | BA A | — | Baseline; approved CX + Policy + Finance |
| 1.1 | 12 Jun | BA B | CR-22 | FR-RET-012 exception DAMAGED_ON_DELIVERY; added FR-RET-019 photos |
| 1.2 | 01 Jul | BA A | CR-31 | NFR-RET-P01 p95 2s → 1.5s after sale incident |

Each row must be enough to know **whether tests change**.

Requirement-level history (catalog):

| ID | Ver | Status | CR |
|---|---|---|---|
| FR-RET-012 | 1.1 | Live | CR-22 |
| FR-RET-018 | 1.0 | Retired | superseded by FR-RET-019 |

## Weak vs strong

| Weak | Strong |
|---|---|
| “See latest Confluence” | Catalog row with ID + version + baseline pack |
| FR-1, FR-1 (duplicate) | One issuer; never reuse |
| Version in the filename only (`FRD_final_FINAL2`) | 1.0 / 1.1 in the doc control table |

## Scenario / Use case: two BAs overwrite the same ID

**Context.** MediCare+ program. BA A (appointments) and BA B (billing) both start an FRD. Both use FR-01. BA A: FR-01 = hold slot 10 minutes. BA B: FR-01 = apply tariff for visit type. QA writes TC-01 against “FR-01” from billing. Developers implement appointments FR-01. UAT: billing says tariff is wrong; appointments says slot hold is untested. CIO asks why “FR-01 failed.”

**Stakeholders.** Two BAs, QA, two dev squads, clinic admin, billing, program manager.

**What the BA function should have done.**

- Published numbering: `FR-APT-###` and `FR-BIL-###`.
- Shared catalog with unique constraint on ID.
- Allocated ranges or a request form: “next ID.”
- Peer review: reject any FR without module prefix.

**Sample numbering rule (one paragraph you can paste).**

> Functional IDs are `FR-<MOD>-<nnn>` zero-padded. Modules: APT, BIL, EMR, LAB. Sequences never reset. Retired IDs are not recycled. Drafts use version 0.x; implementation only against ≥ 1.0 unless the story is explicitly spike. New IDs are taken from the catalog sheet; the taker puts their name and timestamp in `allocated_by`.

**What goes wrong if ignored.** Duplicate FR-01, failed UAT, lost traceability, and a week of archaeology. Numbering looks bureaucratic until the day it is not.

QuickBite analogue: `FR-DLV-022` compensation cause vs `FR-DLV-023` customer voucher — if both called “FR-22” in Slack, finance tests the wrong one.

## Notes

- 
