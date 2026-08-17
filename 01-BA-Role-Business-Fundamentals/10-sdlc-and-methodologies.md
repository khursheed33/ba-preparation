# SDLC and Delivery Methodologies

## SDLC fundamentals

SDLC = Software Development Life Cycle.

It is the path from idea to live software.

Typical stages:

1. Planning / initiation
2. Requirements
3. Design
4. Development
5. Testing
6. Deployment
7. Maintenance

The BA is most active in requirements, but stays involved through testing, UAT, and change.

## Waterfall

Work happens in sequence. One phase finishes before the next starts.

Requirements → Design → Build → Test → Release

Useful when:

- Scope is clear and stable
- Change is expensive
- Compliance needs heavy documentation

Risk: if requirements were wrong, you find out late.

## Agile

Work happens in short cycles (sprints). Requirements can evolve.

Useful when:

- Needs are not fully known
- Feedback is needed often
- The product will change

The BA in Agile:

- Helps refine the backlog
- Writes user stories and acceptance criteria
- Clarifies requirements just in time
- Supports sprint review and UAT

## Hybrid methodology

Many companies mix both.

Example: high-level BRD in a Waterfall style, then delivery in Scrum sprints.

A BA should not argue "Agile vs Waterfall" as religion. Use what the organization actually follows, and keep requirements clear either way.

## Basic software development lifecycle (from a BA view)

- Understand the problem
- Define requirements
- Confirm design matches requirements
- Support build with clarifications
- Support test and UAT
- Confirm the live system meets the business need

## Basic software testing lifecycle

Testing is not only QA's job. The BA helps define what "correct" means.

Typical flow:

1. Test planning
2. Test scenario / test case design
3. Test execution
4. Defect reporting
5. Retesting
6. UAT
7. Sign-off

BA contribution:

- Acceptance criteria
- Requirement-to-test mapping
- UAT scenarios
- Clarifying expected behavior when a bug is raised

## Real-world examples

| Approach | Fits when | Company example |
|---|---|---|
| Waterfall-ish | Regulator wants a baselined spec | ShieldSure cashless garage pay — IRDAI + legal sign FRD before build |
| Agile / Scrum | Learning by slices | ShopEase auto-approve: one reason code, one price band, then expand |
| Hybrid | Enterprise reality | NovaBank: BRD for loan origination, then 2-week sprints for checklist + SMS + queue |

**BA through SDLC (MediCare+ reminders)**

1. Plan: problem = 22% no-shows.
2. Requirements: consent, 24h/2h, reschedule, specialty suppressions.
3. Design review: BA checks the sequence diagram still matches consent.
4. Build: clarify “what if appointment moved?”
5. Test: QA uses AC; BA supplies UAT clinic scripts.
6. Deploy: transition — reception script change.
7. Maintain: CR when oncology asks to suppress SMS too.

### Weak vs strong

| Weak | Strong |
|---|---|
| “We are Agile so we don’t write requirements” | Stories + AC + rules still exist; they are smaller |
| BRD thrown over the wall in Waterfall | BA stays through UAT even if phases are sequential |
| BA disappears after sprint planning | BA in refinement, review, and defect triage |

## Scenario / Use case: NovaBank hybrid — BRD then sprints

**Context.** NovaBank cannot “just Agile” KYC because compliance wants a signed baseline. Digital wants weekly demos. The BA is stuck between a 40-page BRD request and a Scrum master who wants only tickets.

**Stakeholders.** Compliance, digital PO, Scrum team, credit ops, BA, PM.

**What the BA does.**

1. Hybrid: **baseline** business rules and NFRs that cannot silently change (KYC, OTP, audit log). **Slice** UI and notifications into sprints.
2. SDLC view: requirements for the baseline now; design/dev/test per slice.
3. Testing lifecycle: AC on each story; UAT scenario pack for credit ops at the end of increment 2, not after every commit.
4. Change: anything that touches KYC evidence = CR against the baseline, not a Slack “quick add.”

**Sample artifact.** Trace from methodology to work:

| Baseline (Waterfall-style) | Sprint 1 | Sprint 2 |
|---|---|---|
| FR: document completeness rules | Checklist UI + save draft | Status SMS |
| NFR: audit log of who changed a document flag | Log events | Ops report |
| Out of scope: AI underwriting | — | — |

**What goes wrong if ignored.** Either you fake Agile and skip KYC sign-off (audit finding), or you write a BRD and the team builds something else in Jira. Hybrid is not indecision; it is two speeds with a clear split.

## Notes

- SDLC is the path; Waterfall/Agile/Hybrid is the rhythm. Requirements still need owners in all three.
- BA is thickest in requirements and UAT, present in every other stage.
- Testing lifecycle needs your definition of “correct,” not only QA’s scripts.
- 
