# Flowcharts, Swimlanes, and Decision Trees

## Definition

**Flowcharts** show sequence and decisions in one process. **Swimlane diagrams** add *who* performs each step (role or system). **Decision trees** show how a choice is made from conditions to outcomes (approve / reject / investigate).

## Why it matters

A BA uses diagrams to align stakeholders faster than paragraphs. The wrong diagram hides the real problem: a flowchart without lanes hides queues between teams; a tree without policy references hides arbitrary decisions.

## Concepts

### Flowcharts — symbols and when to use

| Symbol | Meaning |
|---|---|
| Oval | Start / end |
| Rectangle | Process step |
| Diamond | Decision (yes/no or named exits) |
| Arrow | Flow |
| Parallelogram (optional) | Input / output (order id, reason) |
| Document | Artifact produced (cancellation email) |

Use a flowchart when one process, few actors, and you need sequence + branches (ShopEase order cancel). Do not use it as a system architecture picture.

### Swimlanes — who does what

Lanes are roles or systems. Hand-offs are arrows that cross lanes — those are delay and defect magnets. Use when NovaBank-style work crosses customer, RM, credit, and ops.

### Decision trees

Start at a question; each branch is a condition; leaves are actions. Use for policy-heavy decisions (ShieldSure claim outcome). Keep the tree aligned to written business rules; the tree is not the rule's only home.

### Common BA mistakes in diagrams

- Mixing As-Is and To-Be on one page with no label.
- Diamonds with three unlabeled exits.
- Lanes named after software ("API") instead of a responsible role when the question is accountability.
- Happy path only; exceptions in a footnote.
- So much detail it cannot be validated in a workshop.
- Decision tree that duplicates the flowchart poorly (pick one primary view).
- No start, no end, no owner on the legend.
- Drawing every click (that is a wireflow, not a business flowchart).

## Real-world examples

1. **QuickBite:** Flowchart for "restaurant cannot fulfill" — cancel vs reassign rider vs partial refund.
2. **MediCare+:** Swimlanes for lab order: doctor, patient, lab, app — shows who chases results.

## Scenario / Use case

### Context

Three diagrams are needed in one discovery week: ShopEase cancel, NovaBank loan, ShieldSure claim decision. Stakeholders argue from anecdotes.

### Stakeholders

Operations leads, PO, legal/compliance, BA, QA, developers (for system lanes only).

### BA actions

1. Choose diagram type per question (sequence vs ownership vs policy).
2. Draft As-Is; label it; validate in a walkthrough.
3. Keep a legend and rule IDs on trees.
4. Capture mistakes (unlabeled diamonds) in review.

### Sample artifacts

**1) ShopEase order cancel (flowchart, customer-initiated, paid order)**

- Start → Customer taps Cancel → Diamond: shipped?  
  - **No:** Diamond: refund window / payment captured? → Reverse payment → Notify seller → End (Cancelled).  
  - **Yes:** Diamond: delivery status delivered?  
    - **No:** Route to "in-transit cancel policy" (may fail) → End (Cancel rejected or courier intercept).  
    - **Yes:** End (use Returns process, not cancel).

**2) NovaBank personal loan (swimlanes)**

| Lane | Typical steps |
|---|---|
| Customer | Apply, upload docs, e-sign, accept offer |
| RM | Complete file, clarify income, submit to credit |
| Credit | Score, policy checks, approve / reject / extra docs |
| Ops | Disburse, lien, welcome kit |

Handoff RM → Credit is the bottleneck if docs are incomplete (see process analysis). Draw the loop "credit → RM → customer" explicitly.

**3) ShieldSure claim (decision tree)**

```
Covered peril?
  No → Reject (reason: not covered)
  Yes → Documents complete?
    No → Investigate (request docs; SLA clock)
    Yes → Amount within auto-limit and no fraud flag?
      Yes → Approve (straight-through)
      No → Investigate (adjuster / SIU)
```

Leaves: **Approve**, **Reject**, **Investigate**. Each leaf points to a template letter and audit code.

### Failure if ignored

Cancel is built as "always refund." Shipped orders vanish from seller inventory with no courier intercept. Loan swimlanes never drawn; credit blames RM; RM blames the portal. Claims tree lives in one senior adjuster's head; juniors approve inconsistently.

## Weak vs strong

| Weak | Strong |
|---|---|
| Boxes with no decision exits | Named diamond exits |
| Swimlane = one long lane "business" | Customer / RM / credit / ops |
| Tree without reject reasons | Leaves tied to policy codes |
| Diagram as decoration in a BRD | Validated in a workshop, versioned |

## Notes

- One primary diagram per question; link others rather than overlapping everything.
- Crossing a swimlane is a requirement for SLA and notification.
- Decision trees need "else" / investigate; binary yes/no that is actually "maybe" belongs on investigate.
- Label As-Is vs To-Be in the title.
- If developers need sequence of systems, use BPMN or sequence diagrams later — start here for business.
