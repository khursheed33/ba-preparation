# Requirement Lifecycle

The **requirement lifecycle** is the path of a requirement from the first idea until it is implemented, tested, changed, or retired.

A requirement is not “done” when someone writes it in Confluence. It lives as long as the behaviour exists in the product.

## Why it matters for a BA

If you only collect statements and throw them over the wall, nobody owns the requirement through build and change. NovaBank’s “forgot password” complaints sit in a ticket for months, then a developer “fixes login” without tracing back to the original need. The BA is the person who keeps the thread intact.

## The stages (idea → retire)

| Stage | What happens | Typical output |
|---|---|---|
| Idea / trigger | A complaint, regulation, metric, or opportunity appears | Problem statement, ticket, or epic seed |
| Elicit | You pull information from people, systems, documents | Notes, interview records, process facts |
| Analyze | You structure, de-duplicate, find gaps and conflicts | Models, clarified statements, questions |
| Document | You write requirements others can use | Stories, FRD, SRS, rules catalog |
| Validate | Business confirms this is the *right* need | Review comments, “yes, that is the problem” |
| Approve | Named owners baseline the set | Sign-off, sprint commitment, baseline v1.0 |
| Implement | Dev builds against the requirement | Code, config, interfaces |
| Test | QA and UAT check the requirement is met | Test cases, defects, UAT evidence |
| Maintain / change | Live behaviour is updated via controlled change | CR, new version, updated tests |
| Retire | The behaviour is removed or replaced | Decommission notes, redirected traces |

These stages overlap in Agile. You still do all of them; you just do them in smaller slices.

## Who touches a requirement at each stage

| Stage | Who typically touches it | BA role |
|---|---|---|
| Idea | Customer, ops, compliance, product, support tickets | Confirm it is a real problem, not a one-off rant |
| Elicit | Users, SMEs, IT, vendors, legal | Plan sessions, ask, record, probe |
| Analyze | BA, architect, PO, process owner | Decompose, model, resolve conflicts |
| Document | BA (author), reviewers | Write unambiguous, testable statements |
| Validate | Business owner, end-user representatives | Walk through scenarios; check value |
| Approve | Sponsor, PO, compliance (if regulated) | Get named sign-off and a baseline |
| Implement | Developers, architects | Clarify, refuse silent scope adds |
| Test | QA, BA, UAT users | Trace tests to requirements; judge “fail” |
| Change | CR board / PO / change advisory | Impact analysis, version, re-approve |
| Retire | Product + ops + BA | Mark superseded IDs; do not leave orphans |

ShieldSure example: a claims manager’s idea (“pay garage directly”) is elicited from ops and legal, analyzed against existing cashless rules, documented as FR + NFR, validated with claims, approved by product and compliance, implemented with the garage network vendor, tested in UAT, then changed when IRDAI circulars update, and retired when a new cashless platform replaces it.

QuickBite example: “compensate late orders” starts as a support wish. Through the lifecycle it becomes a rule: compensate if restaurant accepted on time and rider delay exceeds SLA — not if the kitchen was late.

## Weak vs strong lifecycle handling

| Weak | Strong |
|---|---|
| Ticket says “fix forgot password” and vanishes into a sprint | Each stage has an owner, an artifact, and a status |
| BA writes FRD and leaves the project | BA stays through UAT and first production change |
| Change is a Slack message | Change is a CR with impact and a new version |
| Old requirement left active after replacement | Retired ID marked superseded by FR-xxx |

## Scenario / Use case: NovaBank “forgot password”

**Context.** NovaBank retail net-banking. Call-centre volume: 1,200 “cannot login” calls per week. 40% are forgotten passwords. Current process: customer visits branch with PAN and gets a printed reset token in 2 days. First complaint logged 11 March by a salary-account holder in Pune who needed to pay rent.

**Stakeholders.** Retail customers, call-centre agents, information security, core-banking (CIF) team, SMS gateway owner, compliance (RBI digital authentication), fraud team, PO for digital channels, QA, branch operations.

**What the BA does at each stage.**

1. **Idea.** Read complaint + volume report. Write problem: customers cannot regain access remotely; branches absorb cost; rent/EMI payments fail.
2. **Elicit.** Interview 5 agents, 3 customers, info-sec, SMS vendor. Observe a branch reset. Read existing “login SOP” PDF (out of date — still mentions ATM PIN reset that was retired).
3. **Analyze.** Conflict: info-sec wants video KYC for every reset; ops wants SMS OTP. Duplicate: two teams already drafted “OTP login” vs “OTP reset.” Gap: what if mobile number is not on CIF?
4. **Document.** FR: registered mobile OTP reset, 10-minute expiry, 3 attempts, then 24-hour lock. NFR: OTP SMS p95 < 30 seconds. Transition: agent script + branch poster that branch visit is no longer required.
5. **Validate.** Walk scenarios with call-centre lead and a customer council. Confirm branch visit remains only when mobile is not registered.
6. **Approve.** Digital PO + CISO + compliance sign baseline v1.0. Assumption logged: 92% of retail CIF records have a valid mobile (to be verified by data).
7. **Implement.** Dev builds against FR-AUTH-014. BA answers: “Does lock apply across app and web?” Yes — one lock store.
8. **Test.** QA tests expiry and lock. UAT: 20 customers. One fail: NRI numbers +91 vs 00 prefix. Defect traced to FR-AUTH-014, not a “random bug.”
9. **Maintain / change.** After go-live, fraud sees SIM-swap cases. CR-17 adds a cooling period for recent mobile-number changes. Version 1.1.
10. **Retire.** Two years later app-based biometric recovery replaces SMS reset for app users. FR-AUTH-014 marked retired for app channel; web still active.

**Sample requirement / artifact.**

> **FR-AUTH-014 (v1.1)** A retail customer whose mobile number has been on CIF for ≥ 72 hours can request a password reset. The system sends a 6-digit OTP to that number, valid 10 minutes, max 3 incorrect attempts. After 3 failures, reset is locked for 24 hours across web and app.

**What goes wrong if ignored.** Someone ships “email reset” because a developer had a template. Half of NovaBank customers never use email. Call volume does not drop. Info-sec is bypassed, a phishing incident occurs, and the feature is rolled back. The original complaint is still open.

## Lifecycle status you can put on a catalog

Draft → In review → Validated → Approved (baselined) → In build → In test → Live → Changed → Retired.

Never leave a requirement in two statuses. If it changed, bump the version and keep the history.

## Notes

- 
