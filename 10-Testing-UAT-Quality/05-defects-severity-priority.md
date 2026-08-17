# Defects: Lifecycle, Severity, and Priority

## Definition

A **defect** (bug) is a difference between **expected** (requirement, AC, or agreed behaviour) and **actual**, with enough evidence to reproduce.

The **defect lifecycle** is the path from discovery to close (or won’t-fix).

**Severity** is impact on the business/system (how bad is the failure). **Priority** is order of fix (how soon we must act). They are related but not the same.

**Bug reporting** is writing that evidence so another person can reproduce without a meeting.

## Why it matters

A one-line “map is wrong” on QuickBite can mean “customer cannot find the restaurant” (ship-stopper) or “admin heat-map label off by 2px” (later). Wrong severity burns the team or ships harm. Bad bug reports bounce; the BA sits in the middle translating.

## Defect lifecycle

Typical states (names vary by Jira workflow):

```
New → Open (triaged) → Assigned → Fixed (in build) → Retest → Closed
                                              ↘ Reopen (failed retest or recurrence)
```

| State | Meaning | BA action |
|---|---|---|
| New | Logged, not triaged | Complete the report; attach req ID |
| Open | Accepted as defect (or rejected / duplicate / change) | Argue type: bug vs CR vs working-as-designed |
| Assigned | Developer owns | Clarify expected; provide data |
| Fixed | Code in a build | Know which env/version to retest |
| Retest | QA or UAT user retries | Confirm expected vs actual on that build |
| Closed | Verified or cancelled | — |
| Reopen | Failed retest | New evidence; do not “comment instead of reopen” |

Also: **Deferred / known issue** — accepted for a release with sign-off (see RTM/sign-off notes).

## Severity vs priority (2×2 with examples)

Severity: 1 blocker / 2 major / 3 minor / 4 cosmetic (labels vary).

Priority: P1 now / P2 this release / P3 scheduled / P4 backlog.

| | **High priority (fix soon)** | **Lower priority (can wait)** |
|---|---|---|
| **High severity** | NovaBank: payment posts twice; MediCare+: appointment booked to wrong patient; ShopEase: checkout charges but no order | Rare admin-only crash on a screen used twice a year *if* workaround exists — still high sev, maybe not P1 if workaround and low usage (**rare but severe** still needs a date) |
| **Lower severity** | ShopEase: homepage banner typo on a campaign *today* (cosmetic but P1 for brand) | Cosmetic: ShieldSure admin report column padding; label colour |

More examples:

| Case | Severity | Priority | Why |
|---|---|---|---|
| Payment fail / double debit | Sev1 | P1 | Money + trust |
| QuickBite customer map: pin on wrong street, cannot navigate | Sev1–2 | P1 | Core journey |
| QuickBite admin report map: region boundary 4px off | Sev4 cosmetic | P3–P4 | No customer impact |
| MediCare+ rare admin typo on internal ICD helper text | Sev4 | P4 | Internal, no clinical action |
| NovaBank: wrong interest *display* but correct ledger | Sev2 (trust) | P1 or P2 | Display can cause wrong decisions |
| Button 2px misaligned | Sev4 | P4 | Cosmetic |

**Rule:** Customer-facing money, identity, safety, privacy → high severity. Frequency and workaround drive **priority**. A Sev1 with a solid workaround might be P1 still (safety) or negotiated — never silently downgrade money/safety.

### Weak vs strong

| Weak | Strong |
|---|---|
| “Broken.” | Steps, expected, actual, ID, screenshot, AC-ID |
| Everything Sev1 | 2×2 applied in triage |
| Closed from “dev said fixed” | Retest on named build |
| Map wrong = always P4 | Ask: customer app vs admin report |

## How to write a good bug

| Field | What to put |
|---|---|
| Title | Outcome + where: “IMPS retry posts duplicate debit — retail app” |
| Steps | Numbered, from a clean state |
| Expected | From AC / BRD, not opinion |
| Actual | What happened, including message and timestamp |
| Data | User role, IDs (order, claim, UHID), amounts, env |
| Screenshot / log | UI + correlation ID if any |
| Requirement ID | FR-PAY-04 / AC-3 |
| Severity / priority | Proposed; triage confirms |

Optional: frequency, workaround, browser/device, build number.

## Real-world examples

**ShopEase.** Coupon applies twice at checkout — Sev1, P1. Footer year “2025” — Sev4, P4 unless legal.

**ShieldSure.** Cashless approval SMS to wrong member — Sev1 (privacy + clinical), P1.

**HR / EdTech.** Payslip PDF off-by-one alignment — cosmetic unless figures wrong (then Sev1).

## Scenario / Use case: QuickBite “map wrong”

**Context.** Two tickets titled “map wrong.”

**Ticket A — customer app.** Rider and customer see restaurant pin 1.2 km off. Customers walk to the wrong gate; cancellations spike. **Severity high** (core fulfilment). **Priority P1.**

**Ticket B — admin ops report.** Heat-map of late orders: municipal boundary outline misaligned; used in a weekly PDF. Dispatchers do not use it for navigation. **Severity low (cosmetic / reporting).** **Priority P3.** Same words, different impact.

**BA in triage.** Split tickets; attach FR-MAP-01 (customer navigation) vs RPT-OPS-07 (admin). Do not let Ticket B’s calm tone downgrade Ticket A.

**If ignored.** Engineering “fixes the report” for the louder VP; customers keep cancelling.

## Notes

- Lifecycle: new → open → assigned → fixed → retest → closed / reopen.
- Severity = impact; priority = urgency; use a 2×2, not vibes.
- Cosmetic can be P1 (campaign); rare admin typo is not Sev1.
- Payment / identity / clinical / privacy failures are Sev1 until proven otherwise.
- Good bugs: steps, expected, actual, data, screenshot, requirement ID.
- Retest on a named build; comments are not closure.
- “Map wrong” is not a severity — *who* and *which journey* is.
- Known issues must stay visible, not closed as “won’t fix” without sign-off.
