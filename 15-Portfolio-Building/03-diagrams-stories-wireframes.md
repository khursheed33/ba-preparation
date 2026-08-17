# Diagrams, Stories, Use Cases, and Wireframes

## Definition

**Process diagrams**, **user stories**, **use cases**, and **wireframes** are different views of the *same* change. A portfolio set that tells **one story** beats four unrelated pretty files.

## Why it matters

Interviewers test coherence: if the BPMN says seller is skipped, the story cannot say “wait for seller,” and the wireframe cannot have a “Seller approve” button as the only path.

## Present them as one set

**One ShopEase thread (auto-approve Size < ₹2,000 prepaid):**

```text
Process (As-Is / To-Be)
  → Use case (buyer submits return)
    → User stories (auto-approve, SMS, seller notify, QC fail)
      → Wireframes (status screen, no fake chatbot)
```

Caption every artifact with the same ID prefix (`RET-`) and the same in-scope line.

| Artifact | Job in the story | Keep it small |
|---|---|---|
| Process diagram | Where time is lost; what changes | One As-Is, one To-Be; happy + 1 exception |
| Use case | Actor, trigger, main flow, alts | 1 primary use case, not 20 |
| User stories | Delivery slices | 5–8, not 40 |
| Wireframes | UI implications of rules | 3–5 screens, annotated with rules |

### Weak vs strong

| Weak | Strong |
|---|---|
| BPMN from the internet, stories from a blog, Figma from Dribbble | All four drawn from the same problem statement |
| Wireframe with extra menu items “for completeness” | Out-of-scope chatbot omitted on purpose |
| Use case 12 pages | Main success + QC fail + amount ≥ 2000 |

## How to caption (example)

**Diagram:** “To-Be: seller approval removed only when reason=Size AND amount<2000 AND prepaid. Else As-Is.”

**Story:** `US-RET-12` maps to To-Be box “Auto-approve service.”

**Use case alt flow:** amount ≥ 2000 → seller queue (matches diagram diamond).

**Wireframe:** status = AUTO_APPROVED; helper text “Seller was notified; pickup next.” No Approve button for this path.

## Real-world examples

1. **NovaBank.** Process: document wait. Use case: submit application. Stories: checklist, SMS. Wireframe: missing-PAN banner — same rule.
2. **MediCare+.** Process: reminder. Use case: send SMS. Story: suppress psychiatry. Wireframe: staff see “SMS off for this specialty” — doctors trust you.
3. **QuickBite.** If the process says kitchen delay is out of scope, the wireframe must not be a “compensate everyone” button.

## Scenario / Use case: portfolio review where the set disagrees

**Context.** You present ShopEase. Panelist points at To-Be BPMN (no seller). Then opens wireframe with a big “Waiting for seller” default. Then a story “As a seller I want to approve every return.”

**What you should have done when building the set.**

1. Freeze the rule table first.
2. Draw To-Be from the table.
3. Write the use case main flow from To-Be.
4. Slice stories from the use case.
5. Wireframe last, annotating fields from AC.
6. Peer check: “Find one contradiction.”

**Repair in interview (if you find it live):** “That’s an As-Is leftover; To-Be hides that button when auto-approve applies. I would log it as a documentation defect.” Honesty beats bluffing.

**What goes wrong if ignored.** The panel concludes you collected artifacts, not that you analyzed a process. Coherence *is* the BA skill on display.

## Mini checklist before you publish the set

| Check | Pass looks like |
|---|---|
| Same in-scope sentence on all four | Prepaid Size < ₹2,000 |
| Exception exists in all four | QC fail after auto-approve |
| No chatbot in wireframe if out of scope | Button absent, not greyed “coming soon” |
| IDs cross-link | US-RET-12 in the diagram note |

NovaBank set uses the same checklist: document-pending wait in the process, checklist fields on the wireframe, story AC matching the CIF rule.

## Notes

- One problem, one rule table, then diagram → use case → stories → wireframes.
- Annotate wireframes with business rules; pretty UI without rules is UX homework.
- Use cases carry exceptions that stories often drop — keep both.
- Contradiction between artifacts is a defect, same as a wrong FR.
- 
