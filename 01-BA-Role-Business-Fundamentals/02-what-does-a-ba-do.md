# What Does a Business Analyst Do?

## Day-to-day work

A BA helps the organization understand **what** should be built or changed, **why**, and **for whom**.

Typical activities:

- Meet stakeholders to understand problems
- Ask questions and clarify needs
- Document requirements
- Map current (As-Is) and future (To-Be) processes
- Write user stories, use cases, or requirement documents
- Support developers and testers during build
- Help with UAT and sign-off

## BA in an IT organization

In IT, the BA is the link between business teams and technology teams.

```text
Business / Users  →  Business Analyst  →  Developers / Testers / Architects
```

The BA:

- Understands business goals
- Translates them into requirements
- Makes sure the delivered software matches those requirements

## Common BA responsibilities

- Stakeholder identification and communication
- Problem analysis
- Requirement elicitation, analysis, and documentation
- Scope management
- Process modeling
- Requirement traceability
- Change request handling
- UAT support
- Bridging business and technical language

## What a BA owns vs what a BA supports

| Area | BA role |
|---|---|
| Requirements | Owns clarity and completeness |
| Scope of solution | Helps define and protect |
| Project timeline | Supports, PM owns |
| Code quality | Supports, Dev/QA own |
| Business value | Helps define and validate |
| Sign-off | Facilitates stakeholder approval |

## Real-world examples of the same BA activities

| Activity | ShopEase | NovaBank | MediCare+ |
|---|---|---|---|
| Elicit | Interview warehouse QC on why returns fail inspection | Shadow a credit officer for one loan file | Sit with a clinic receptionist during peak hours |
| Analyze | Find that 40% of return delays are seller approval, not logistics | Find that 28% of loan files wait on missing PAN, not underwriting | Find no-shows cluster on Monday specialist slots |
| Document | User stories for return status SMS | FR for document completeness checklist | NFR for SMS reminder consent |
| Support delivery | Clarify QC “damaged vs used” rule with QA | Walk UAT users through OTP reset | Confirm appointment status values with the EMR vendor |

### Weak vs strong day-to-day

| Weak | Strong |
|---|---|
| Sits in every meeting, writes minutes only | Runs elicitation with a goal, then publishes decisions |
| Hands a 40-page BRD and disappears | Stays through build, test, UAT, and first change |
| Accepts “the PO already decided” | Challenges a decision that has no measure or owner |

## Scenario / Use case: NovaBank loan origination — one week in the life

**Context.** NovaBank personal-loan cycle time is 10 days. Target is 3. Product wants “a new loan portal.” The BA is assigned Monday. Go-live is not this week; *clarity* is.

**Stakeholders.** Credit head, branch RM, underwriters, KYC ops, core-banking team, digital PO, compliance, customers who abandoned applications.

**What the BA does (Mon–Fri).**

1. **Mon.** Read last 90 days of application data: 34% stall at “documents pending.” Not a portal problem yet.
2. **Tue.** Interview 4 RMs and 2 underwriters. Map As-Is: apply → KYC → credit score pull → underwriter → sanction → disbursal.
3. **Wed.** Workshop: in-scope = salaried personal loans on web; out-of-scope = gold loans and branch-only products.
4. **Thu.** Draft problem statement + 8 functional requirements (document checklist, status SMS, underwriter queue SLA). Walk through with credit head.
5. **Fri.** Support PO to split into stories. Log assumption: bureau API p95 < 8 seconds (unverified). Raise as a dependency on the data team.

**Sample artifact.** Daily decision log, not a novel:

| Date | Decision | Owner |
|---|---|---|
| Wed | Gold loans out of scope for this release | Credit head |
| Thu | Status SMS at KYC complete, sanction, and disbursal | Digital PO |

**What goes wrong if ignored.** The BA spends the week “gathering requirements for a portal.” Developers design screens. Cycle time does not move because missing PAN still sits in email. The BA was busy, not useful.

## Notes

- A BA’s week is elicit → analyze → document → align → support delivery — in that spirit, even in Agile.
- You own requirement clarity; you do not own the sprint board or the code.
- If you cannot name the process step you improved, you were taking notes, not doing analysis.
- 
