# AI for Requirements

## Definition

**AI-assisted requirements work** means using an LLM to draft, summarize, classify, or critique requirements — while a BA still elicits, validates, and baselines them.

It covers gathering support, documentation drafts, summarization, classification, user stories, acceptance criteria, conflict detection, and quality checking.

## Why it matters

Speed is real. So is generic sludge. ShopEase will get Amazon-shaped stories if you do not feed ShopEase facts. The only safe workflow is **AI draft → human validate**.

## Good workflow: AI draft → human validate

```text
Facts you gathered → prompt with constraints → AI draft
        → BA edit (rules, exceptions, IDs)
        → SME walkthrough → baseline
```

Never reverse it (AI invents → you “confirm” in a meeting without users).

## Prompts, sample outputs, BA edits (ShopEase returns)

**Facts to paste (redacted):** prepaid; reason code Size; amount < ₹2,000; seller approval today 2.1 days; out of scope: chatbot, international.

### User story generation

**Prompt:** “Role: Agile BA. Using only the facts below, write 3 user stories in As a / I want / So that. Flag any gap as [QUESTION]. Do not invent SLAs.”

**Sample AI output (too generic):**

> As a customer, I want to return items easily so that I am happy.

**BA edit (strong):**

> As a prepaid ShopEase buyer, I want a Size return under ₹2,000 to auto-approve without waiting on the seller so that refund starts after pickup/QC only, not after a 2-day seller queue.  
> **AC:** see AC-RET-04. **[QUESTION]:** Does “Size” include Size+Color?

### Acceptance criteria generation

**Prompt:** “Given/When/Then for auto-approve. Include one negative path. Do not add store drop-off.”

**AI output (invented rule):** “Given the customer is Prime… When they scan a QR at a store…”

**BA edit:** Delete Prime and QR. Keep: Given prepaid AND reason=Size AND amount<2000 When return is submitted Then status = AUTO_APPROVED and seller is notified within 15 minutes.

### Requirement summarization

Use on *your* interview notes, not on a secret BRD in a public tool. Output: decisions, open questions, owners. Check that a quiet dissent was not dropped.

### Requirement classification

Ask the model to bucket statements into business / stakeholder / functional / NFR / transition / business rule. **You** still correct “Must feel premium” (wish, not NFR).

### Requirement conflict detection

**Prompt:** “These two rules conflict? Rule A: auto-approve Size. Rule B: seller must confirm every return in 24 hours.”

AI should flag the conflict. BA resolves with PO: B does not apply when A is true; update the seller SOP.

### Requirement quality checking

Ask: “Which of these are untestable?” AI will catch “user-friendly.” It will not catch a missing psychiatry-style exception it never saw.

### AI-assisted gathering (not replacing interviews)

Good: draft an interview guide for warehouse QC.  
Bad: skip QC and let the model “describe a typical warehouse.”

## Dangers

| Danger | What it looks like | Defence |
|---|---|---|
| Generic stories | “Easily,” “seamlessly,” no user, no measure | Force As a *named role* + so that *outcome* |
| Missed exceptions | Happy path only | Prompt: “list exception questions”; then ask humans |
| Invented rules | Prime, 30-day window, store QR | “Use only facts below” + red-pen every SLA |
| Fake conflicts resolved | Model “picks” a winner | BA + PO decide; document |

### Weak vs strong

| Weak | Strong |
|---|---|
| One-shot “write all stories for returns” | Facts → draft → edit → SME → Jira IDs |
| Accepting AI AC with extra features | Delete scope creep the model added |
| Classification without reading | Spot-check every bucket |

## Real-world examples

1. **NovaBank.** AI writes “user can upload any document.” BA adds file types, size, virus scan NFR, and “PAN mandatory before bureau pull.”
2. **MediCare+.** AI classifies “remind all patients” as FR. BA splits FR (send) vs rule (specialty suppress) vs NFR (consent).
3. **ShieldSure.** AI “detects no conflicts” in two claims SLAs that disagree on weekend hours — because both were vaguely worded. BA rewrites with calendar rules, then re-runs the check.

## Scenario / Use case: ShopEase returns pack in one afternoon

**Context.** PO wants stories tomorrow. You have a 40-minute QC interview and a metric: seller approval 2.1 days.

**What the BA does.**

1. Type facts into an approved tool. Prompt for stories + AC + quality critique.
2. Delete invented chatbot stories.
3. Add exception: damaged item wrongly coded Size — QC fail reverses auto-approve; seller dispute path.
4. Conflict check vs existing SOP “seller confirms all returns.”
5. Walk QC and one seller through the edited set. Then Jira.

**Sample quality table after AI + BA:**

| ID | AI draft issue | BA fix |
|---|---|---|
| US-1 | Generic “easy returns” | Named buyer + amount + reason |
| AC-2 | Missing negative path | QC fail after auto-approve |
| BR-1 | Invented 30-day window | Removed; 7-day innerwear stays as existing policy (verified) |

**What goes wrong if ignored.** Sprint fills with Amazon-like stories. Exceptions explode in UAT. You cannot tell the interviewer what *you* analyzed.

## Notes

- Workflow is always AI draft → human validate → SME confirm → baseline.
- Generic stories, missed exceptions, and invented rules are the three default failure modes.
- Use AI for questions and critique as much as for prose.
- Classification and conflict detection help only if the input statements are specific.
- 
