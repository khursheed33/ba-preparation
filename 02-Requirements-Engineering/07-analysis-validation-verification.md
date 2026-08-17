# Analysis, Validation, and Verification

After elicitation you have raw material. **Analysis** structures it. **Validation** checks you captured the right need. **Verification** checks you wrote the requirement correctly.

These three are often mixed in a “review meeting.” Separate them or you will polish a well-written wrong requirement.

## Why it matters for a BA

ShieldSure can implement a beautifully worded claims FR that does not match how claims managers work. QA can pass tests that were never the business need. Analysis without validation is clever fiction. Validation without verification is a handshake on mush.

## Analysis

Analysis is thinking work: decompose, model, find gaps, conflicts, duplicates.

| Activity | Question | Example |
|---|---|---|
| Decompose | Can this be split into smaller testable pieces? | “Manage claims” → intimate, assign, investigate, approve, pay |
| Model | What are the states, flows, data, actors? | ShopEase RMA states: requested → pickup → QC → refund |
| Find gaps | What path is missing? | NovaBank password reset: what if mobile not on CIF? |
| Find conflicts | Do two statements disagree? | Seller 15-day returns vs platform 7-day innerwear |
| Find duplicates | Same need, two IDs? | “OTP on transfer” written in FRD and again in security NFR as a function |

Outputs of analysis: a clean set of requirements, open questions, models (process, data, state), a conflict log.

**Weak analysis:** copy workshop stickies into Jira.
**Strong analysis:** every sticky is typed, sourced, split or merged, and linked to a model.

MediCare+ gap example: booking FRs exist for patient self-book, but no FR for doctor marking “emergency block.” The gap appears only when you model calendar ownership.

QuickBite duplicate example: “show ETA” in customer app, rider app, and restaurant tablet as three unrelated stories. Analysis merges the rule: one promised time, three displays.

## Validation (right need)

**Validation** asks: did we capture the **right** need for the business?

- Does this requirement serve the business objective?
- Would solving this actually change the metric or risk we care about?
- Did the people who live the process recognise the scenario?
- Are we solving a symptom (GPS) or the cause (restaurant accept time)?

Who validates: business owner, process owner, real users — not only the PO, and not QA.

Techniques: walkthrough of scenarios, prototype review against outcomes, trace back to BR IDs, “would you sign this as the problem?”

ShopEase: validating Easy Returns with warehouse QC, not only with marketing. Marketing wanted “returns in one tap.” Warehouse said without photos, fraud explodes. Validation changes the requirement.

## Verification (written correctly)

**Verification** asks: did we write the requirement **correctly** as a quality statement?

Quality checks (also in the quality file):

- Atomic, unambiguous, testable, measurable
- Consistent with other requirements
- Has ID, owner, source
- Acceptance criteria can fail
- No “etc.”, “user-friendly”, “fast” without numbers

Who verifies: BA peer, QA (testability), architect (feasibility), sometimes legal (wording). Verification is a quality gate, not a business-value gate.

NovaBank: “The system shall transfer funds securely and quickly” can be *validated* as the right topic (customers do need transfers) and still *fail verification* (not testable).

## Side-by-side

| | Analysis | Validation | Verification |
|---|---|---|---|
| Focus | Structure and completeness of the set | Right problem / value | Quality of the writing |
| Question | Gaps, conflicts, duplicates? | Is this the need? | Is this a good requirement? |
| Primary audience | BA + architect + PO | Business / users | QA, peer BA, architecture |
| Failure mode | Hidden path, clash, clone | Perfect spec of the wrong thing | Untestable, vague, compound |

## Weak vs strong

| Weak | Strong |
|---|---|
| “Business signed the deck, so we’re validated.” | Scenario walkthrough with the claims manager using a real claim ID |
| QA reviews grammar | QA asks “how would I fail this?” |
| Analysis = pretty Visio | Analysis = decisions, gaps list, merged IDs |

## Scenario / Use case: ShieldSure claims

**Context.** ShieldSure is digitising motor claims. A draft FR: “The system shall allow cashless claims for network garages and process them efficiently.” Product wants to launch before renewal season. QA asks for test cases. Claims managers have not seen the FRD.

**Stakeholders.** Claims manager, garage network ops, finance (payouts), customer, app team, QA, compliance, BA.

**What the BA does.**

**Analysis.** Decompose cashless: eligibility check → cashless request → garage estimate → insurer approval → repair → invoice → payment to garage. Model states. Find gap: no requirement for what happens if the customer pays cash at a network garage by mistake. Find conflict: finance says pay garage in 5 days; network contract says 48 hours. Find duplicate: “upload estimate” in app FR and in garage portal FR as two different data models.

**Validation.** Workshop with claims manager using last month’s claim CLM-88421. Manager: “We cannot approve without photos of damage *and* RC copy. Your FR skipped RC.” Also: cashless is not for out-of-network even if the garage ‘knows someone.’ The *need* is control leakage, not ‘be efficient.’ BA rewrites BR: reduce average cashless TAT to 48 hours *without* increasing leakage above current 3.1%.

**Verification.** QA scores the new FRs:

| ID | Statement | Testability |
|---|---|---|
| FR-CLM-31 | System allows cashless only if garage_id is in the active network table as of incident_date. | Pass — query network table |
| NFR-CLM-T01 | From complete estimate submit to approve/reject decision, p95 ≤ 4 business hours during 09:00–18:00 IST. | Pass — measurable |
| Old text | Process cashless efficiently | Fail — reject |

QA writes a test that can fail: network garage removed yesterday, incident today, expect cashless blocked with reason NET-INACTIVE.

**Sample artifact.** Validation record: “Claims manager R. Mehta, 12 Jun, validated scenarios S1–S6 against CLM-88421; RC copy added as mandatory. Verification: QA testability review 13 Jun, 2 FRs returned for ambiguity.”

**What goes wrong if ignored.** Team ships “efficient cashless.” UAT: claims managers reject because RC is missing. Finance pays the wrong party. QA had green tests against the vague FR. Renewal season is missed anyway because of rework.

## Practical meeting design

Do not run one meeting called “review.” Run:

1. Analysis huddle (BA + architect): gaps and conflicts.
2. Validation walkthrough (business): scenarios.
3. Verification (QA + peer): quality checklist.

If time is short, still use three agendas, even in one hour.

## Notes

- 
