# Testing Fundamentals and QA vs BA

## Definition

**Software testing** is checking whether the solution behaves as agreed — against requirements, risks, and the real business process — and reporting where it does not.

It is not “click around until it feels OK.” It is planned comparison of **expected vs actual** with recorded evidence.

**QA (Quality Assurance)** owns the quality *system*: test strategy, coverage, environments, automation, regression packs, defect process. Testers/QA engineers design and execute much of the product testing.

**The BA** owns the meaning of “correct” for the business: acceptance criteria (AC), examples, UAT scenarios, and clarification when a defect is really a missing requirement.

## Why it matters

If the BA and QA blur, two failures appear: (1) nobody tests the business path, or (2) the BA becomes an unpaid tester forever and never does analysis. NovaBank hotfixes ship with green QA and red customers. ShopEase “BA tested it” on a laptop is not UAT.

## Testing levels

| Level | Question | Typical owner | BA role |
|---|---|---|---|
| Unit | Does this function/module work in isolation? | Developers | Rarely involved; may share examples |
| Integration | Do modules/APIs talk correctly? | Dev + QA | Clarify contracts, status codes, data meaning |
| System | Does the whole product meet specified requirements? | QA | AC, RTM, clarify expected results |
| UAT | Does it work for the real business in realistic conditions? | Business users, facilitated by BA | Scenarios, data, war-room, sign-off path |

STLC (test lifecycle) in short: plan → design cases → execute → defect → retest → UAT → sign-off.

## QA vs BA responsibilities

| Work | BA | QA | Business user |
|---|---|---|---|
| Problem, scope, requirements | Owns | Consumes | Approves |
| Acceptance criteria | Writes / facilitates | Uses to design tests | Confirms “this is what I meant” |
| Test strategy & coverage | Reviews for business gaps | Owns | — |
| System test cases | Reviews critical paths | Writes | — |
| System test execution | Clarifies, does not replace QA | Executes | — |
| UAT scenarios | Writes with users | Supports environment | Executes |
| UAT execution | Facilitates | Supports | **Must** execute |
| Sign-off | Recommends based on evidence | Reports quality status | Accountable approver |

## RACI (who writes AC, test cases, who executes UAT)

R = Responsible, A = Accountable, C = Consulted, I = Informed.

| Activity | BA | QA | PO / Business owner | End user | Dev |
|---|---|---|---|---|---|
| Write acceptance criteria | R | C | A | C | I |
| Write system test cases | C | R | I | I | C |
| Execute system / integration tests | C (defects) | R | I | I | C (fixes) |
| Write UAT scenarios | R | C | A | C | I |
| Execute UAT | C (war-room) | C (env) | A (sign-off) | R | I |
| Defect triage (business vs bug) | R | C | A on scope | C | C |

### Weak vs strong

| Weak | Strong |
|---|---|
| BA “will test everything.” | QA system-tests; users UAT; BA clarifies AC. |
| AC = “should work fine.” | Given / When / Then with data and error cases. |
| UAT = BA on staging with dummy clicks. | Real roles, real-like data, scheduled scenarios. |
| RACI in someone’s head | Written RACI in the test plan |

## Real-world examples

**ShopEase.** QA tests return refund API (system). Warehouse supervisor UATs “scan return → QC → refund initiated.” BA wrote both AC and the UAT script, did not pretend to be the supervisor.

**NovaBank.** QA tests beneficiary add + limit rules. Branch ops UATs with maker-checker. BA does not “UAT” by adding their own test beneficiary in production.

**MediCare+.** Integration tests: EMR slot ↔ SMS gateway. UAT: front-desk books, patient (or proxy) receives SMS, doctor sees chart.

**Government / HR.** Unit tests on a rules engine; UAT by actual HR ops on payroll cut-off — not the vendor BA alone.

## Scenario / Use case: BA testing on behalf of business forever (anti-pattern)

**Context.** QuickBite’s product owner is “too busy.” For three releases the BA executes UAT, screenshots, and signs “on behalf of ops.” Smoke looks fine. After go-live, restaurant managers cannot mark “food ready” on the device they actually use (old Android, poor network). The BA had tested on a new Pixel on office Wi-Fi.

**Why it is an anti-pattern**

- The BA is not the user; they miss role, device, and incentive.
- Accountability evaporates: ops says “we never accepted this.”
- The BA stops eliciting; they become a bottleneck tester.
- Defects found in production are blamed on “UAT passed.”

**What the BA should do instead**

1. Put RACI in the UAT plan: restaurant success lead **accountable**, 8 restaurant managers **responsible** to execute.
2. BA writes scenarios and sits in the war-room; does not click for them.
3. If users refuse, escalate as a **go-live risk**, not as extra BA overtime.
4. Record: “UAT not executed by business” ≠ “BA tested, so we ship.”

**If ignored.** Every release trains the org that the BA is QA+user. Quality and analysis both degrade.

## Notes

- Testing levels: unit → integration → system → UAT; BA weight increases toward UAT.
- QA owns how to test the system; BA owns what “done” means for the business.
- AC is the BA’s contract with QA; test cases are QA’s contract with the build.
- UAT must be executed by real users, not “the BA who knows the story.”
- RACI prevents the anti-pattern of BA-as-eternal-tester.
- Clarifying a defect is BA work; executing the regression pack is not.
- Integration failures are often contract/requirement issues — stay in the room.
- “I clicked around” is not a test level.
