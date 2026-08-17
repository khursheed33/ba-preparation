# Functional, Regression, and Smoke Testing

## Definition

**Functional testing** checks that a feature does what the requirements say: inputs, rules, outputs, errors. “Can NovaBank add a beneficiary within limit?” is functional.

**Regression testing** re-checks *existing* behaviour after a change, so a hotfix or new story did not break what already worked.

**Smoke testing** is a short, shallow pack: “Is the build sane enough to test further?” Login, main journey, no crash. It is a gate, not coverage.

## Why it matters

Releases fail in the untested old path. A NovaBank payment hotfix can smoke-pass (login, one transfer) and still break beneficiary limits. ShopEase can functionally pass “new coupon” and regress checkout tax. The BA must know **when** each type happens and **what they personally verify** in smoke vs full UAT.

## When each happens in a release

| Moment | Smoke | Functional (new/changed) | Regression |
|---|---|---|---|
| Dev complete on a story | Optional local | QA tests the story | Small, related |
| Build to QA env | **Yes — gate** | Full for in-scope stories | Pack / risk-based |
| After defect fix | Re-smoke if build new | Retest the fix | Around the fix |
| Pre-UAT | Smoke on UAT env | Confirm UAT scope still valid | Business-critical pack |
| Hotfix / production patch | **Mandatory** | Only the fix | **Mandatory** on related risk (limits, payments, refunds) |
| Full release | Smoke | All committed stories | Agreed pack (automation + manual) |

Risk-based regression: payments, identity, refunds, clinical safety, claims — always; cosmetic pages — sample.

## What a BA should check: smoke vs full UAT

| | Smoke (BA / PO sanity) | Full UAT (business users) |
|---|---|---|
| Time | 15–45 minutes | Hours to days |
| Depth | Happy path of critical journeys | Happy + exceptions + roles |
| Data | Known test IDs | Realistic volumes, maker-checker, devices |
| Goal | “Don’t waste UAT on a dead build” | “We can run the business” |
| BA action | Confirm env, login, one path per critical process | Facilitate scenarios, defects, not click for users |
| Sign-off | Not sign-off | Formal evidence |

**BA smoke checklist (example)**

- Right environment and version
- Users can log in with intended roles
- One ShopEase order, or one NovaBank transfer, or one MediCare+ book-and-cancel
- No blocker: 500s, blank dashboard, wrong company branding on prod-like env

**BA in full UAT:** exception paths, reports, NFR the business feels (timeout on 4G), and process handoffs — not redoing QA’s functional pack.

### Weak vs strong

| Weak | Strong |
|---|---|
| Smoke = “I opened the app.” | 8–15 named cases, critical money paths |
| No regression on hotfix | Limit, ledger, notification cases in the pack |
| BA repeats all functional tests in UAT | UAT = business process; functional already done by QA |
| “Regression later” | Risk list attached to the release ticket |

## Real-world examples

**ShopEase.** Functional: new return reason code. Regression: refund amount, wallet, GST invoice. Smoke: home → search → pdp → add to cart → login.

**QuickBite.** Functional: new restaurant prep SLA. Regression: assignment, cancellation refund. Smoke: place order, restaurant accept.

**ShieldSure.** Functional: new cashless hospital. Regression: pre-auth limit, claim status SMS. Smoke: login, open a known claim.

**Telecom.** Functional: new prepaid pack. Regression: recharge, validity, tax. Smoke: account view + one recharge.

## Scenario / Use case: NovaBank payment hotfix — smoke passed, regression missed beneficiary limit

**Context.** Production bug: IMPS to a new beneficiary sometimes times out. Dev patches timeout handling. QA runs **smoke**: login, add beneficiary, one ₹1,000 transfer, success. UAT skipped because “tiny hotfix.” Same evening, a corporate ops user adds a beneficiary and transfers ₹8 lakh — over the **new-beneficiary 24-hour limit** of ₹1 lakh. The patch reused a code path that skipped the limit service when the timeout retry fired. Core posted the payment.

**What was missing**

| Test type | Should have included | Actual |
|---|---|---|
| Smoke | Login, one small transfer | Done |
| Functional | Retry after timeout still calls limit check | Not specified in AC for the hotfix |
| Regression | New beneficiary + amount > 24h limit → block | Not in pack |
| UAT | Maker-checker with ops user | Skipped |

**What the BA should have done**

1. Treat payment retry as **behaviour change**, not “infra.”
2. Write AC: “On retry, limit, beneficiary cooling period, and duplicate-detection still apply.”
3. Insist on regression cases: at-limit, over-limit, within cooling period.
4. If business skips UAT, record **known risk** and get risk sign-off — do not silently agree.

**If ignored.** Customer harm, regulator interest, and a war-room that starts with “but smoke was green.”

## Notes

- Functional = this requirement; regression = old requirements still true; smoke = build is alive.
- Hotfixes need *smaller functional + mandatory regression* on money and access.
- BA smoke is a gate for UAT, not a substitute for QA functional tests.
- Full UAT is process and exceptions; do not clone the QA suite.
- Put the regression risk list on the release, especially payments, identity, refunds, clinical.
- Smoke green + regression skipped is a famous production pattern.
- Automation shines on regression; BA still owns the *business* cases that must stay in the pack.
- “Tiny change” is a claim — verify with impact analysis.
