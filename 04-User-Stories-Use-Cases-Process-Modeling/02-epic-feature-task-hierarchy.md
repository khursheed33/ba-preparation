# Epic, Feature, Task Hierarchy

## Definition

Work is nested so a large outcome can be delivered in slices:

- **Epic:** a large outcome that will not fit in one sprint and needs splitting.
- **Feature:** a coherent capability under an epic (often a release slice).
- **User story:** a vertical slice of value for one actor.
- **Task:** implementation or analysis work to complete a story (hours, not value).
- **Sub-task:** a split of a task for tracking (e.g. API vs UI vs test data).

## Why it matters

If everything is an epic, nothing ships. If everything is a task, the team loses the user. A BA splits by **value and actor**. A developer splits by **technical work**. Mixing those splits produces "front-end story" and "back-end story" that cannot be demoed.

## Concepts

### How a BA splits vs how a developer splits

| Question | BA split | Developer split |
|---|---|---|
| Unit of value | User can do a job | Component can be coded |
| Demo | Yes, even if limited | Often no (API only) |
| Example | "Retail customer uploads PAN and gets KYC status" | "Build OCR service," "Create KYC tables" |
| Owner of split | BA + PO for backlog shape | Dev team for tasks inside a ready story |

Rule: **stories stay vertical**. Tasks are horizontal. Do not put "create KYC schema" on the product backlog as a user story unless it is a spike with a learning outcome.

### When something is still an epic

Keep it as an epic when:

- Multiple personas or channels are involved.
- You cannot write testable AC without "and also."
- Estimate is "too big to fit a sprint" even after a first split.
- Policy, vendor, or compliance work is still undefined.
- The walking skeleton is not identified.

Promote a story back to epic if refinement keeps adding actors, channels, or rules.

## Real-world examples

1. **ShopEase:** Epic "Marketplace returns" → features for buyer request, seller dispute, support override (see user-story notes). Not one sprint.
2. **QuickBite:** Epic "Track order" is still an epic until live map, ETA, SMS, and restaurant delay are separate stories.

## Full hierarchy: NovaBank "Digital KYC"

**Epic:** Enable retail customers to complete KYC in the mobile app without visiting a branch (regulatory onboarding).

```
Epic: Digital KYC
├── Feature: Identity capture
│   ├── Story: Upload PAN and selfie
│   │   ├── Task: Design capture screens
│   │   ├── Task: Integrate document store
│   │   └── Task: QA image-quality rules
│   │       └── Sub-task: Test data for blur / glare
│   └── Story: Retry when image quality fails
├── Feature: Verification and decision
│   ├── Story: See KYC pending / approved / rejected
│   └── Story: Branch fallback when auto-KYC fails
└── Feature: Audit and consent
    ├── Story: Capture consent text version
    └── Story: Compliance export of KYC trail
```

Sample stories (not tasks):

- As a NovaBank retail applicant, I want to upload my PAN photo and a selfie so that I can open a savings account without visiting a branch.
- As a NovaBank retail applicant, I want a clear reason when KYC is rejected so that I know whether to retry or visit a branch.
- As a compliance officer, I want every KYC decision stored with the consent version so that we can evidence the check to the regulator.

## Scenario / Use case

### Context

NovaBank digital channel wants "Digital KYC" as one sprint story because the vendor demo looked simple. Legal, fraud, and branch ops are not in the room.

### Stakeholders

Retail applicant, product owner, KYC ops, fraud, legal, vendor (OCR), developers, QA.

### BA actions

1. Confirm epic outcome: account can move from "started" to "KYC approved" in-app for a happy path.
2. Split features by customer journey: capture → decision → audit.
3. Protect vertical stories; push schema/OCR work to tasks.
4. Mark remaining bulk (video KYC, NRI, corporate KYC) as later epics, not this one.

### Sample artifact

A hierarchy board: epic → 3 features → 6 stories in Now/Next; corporate KYC explicitly out of scope. DoR: happy-path AC, rejection reasons, consent text owner.

### Failure if ignored

The team takes "Digital KYC" into a sprint as one item. They build PAN upload only. Sprint review shows a screen with no decision, no audit trail, and no branch fallback. Compliance blocks go-live. Leadership thinks KYC "failed Agile."

## Weak vs strong

| Weak | Strong |
|---|---|
| Epic = "KYC screen" | Epic = outcome: in-app KYC for retail savings |
| Story = "Build OCR" | Story = applicant uploads PAN and sees status |
| Feature = a Jira label only | Feature = a demoable capability slice |
| Sub-tasks on the product backlog | Sub-tasks only under a ready story |

## Notes

- If a story needs two personas to succeed, it is probably still an epic or two stories.
- Developers may split tasks however they work; do not copy that split onto the backlog.
- "Still an epic" is a judgment: too many unknowns, too many actors, or no vertical slice.
- Name epics as outcomes, features as capabilities, stories as user jobs, tasks as work.
- Spikes are time-boxed learning stories; they do not replace the KYC outcome.
