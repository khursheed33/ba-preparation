# Prompt Engineering for Business Analysts

## Definition

**Prompt engineering** is structuring instructions so an LLM drafts a useful artifact — role, context, format, constraints, examples — then iterating with a critique pass.

It is not magic words. It is briefing a junior BA who has no memory of your last workshop unless you paste it.

## Why it matters

Vague prompts produce generic Amazon/Netflix stories. Tight prompts still need human validation, but they waste fewer cycles.

## Patterns

| Pattern | What you specify | Example |
|---|---|---|
| Role | Whose quality bar | “You are a BA writing for developers and QA.” |
| Context | Only verified facts | ShopEase prepaid, Size, < ₹2,000 |
| Artifact format | Table, Given/When/Then, IDs | “Markdown table: ID, statement, type” |
| Constraints | What not to do | “Do not invent SLAs. Use [QUESTION] for gaps.” |
| Examples | One weak vs one strong line | Show a good AC |
| Critique pass | Second prompt | “List ambiguities and missing exceptions.” |

**Iteration:** Draft → you red-pen → “Here is my edit. Apply this bar to stories 4–8.” Do not start a new chat for every sentence if the facts are stable.

### Weak vs strong prompts

| Weak | Strong |
|---|---|
| Write user stories for loans | Role + NovaBank salaried web + in/out scope + format + do not invent bureau SLAs |
| Make it better | “Rewrite AC so each line is testable; no adjectives” |

## Eight reusable BA prompts

Copy, then paste **your** facts. Never paste secrets or full client BRDs into public tools.

### 1. BRD section

> Role: BA. Context: [facts]. Write section “In-scope / Out-of-scope / Assumptions” as tables. Flag unknowns as [QUESTION]. Do not recommend vendors.

### 2. User stories

> Role: Agile BA. Facts: [ ]. Write 5 stories As a / I want / So that. Each story one outcome. Add [QUESTION] where a rule is missing. No chatbot, no AI features unless in facts.

### 3. Acceptance criteria

> For story [text], write Given/When/Then: 1 happy, 2 exceptions, 1 NFR if relevant. Testable. No new scope.

### 4. 5 Whys

> Symptom: [ ]. Ask 5 Why questions I should take to [role]. Do not answer the Whys as fact.

### 5. Process steps

> Draft an As-Is step list as: Actor, Action, System, Wait, Exception. Facts: [ ]. Mark invented steps as [GUESS] — I will delete those.

### 6. Interview guide

> 20 questions for [SME] on [process]. Mix open, closed, probe. End with exception and volume questions.

### 7. NFR list

> Given this FR: [ ]. List NFR questions (performance, security, audit, availability) as questions, not fake numbers.

### 8. RTM

> Columns: Req ID, statement, source (interview/metric), story ID, UAT idea. Fill only from [pasted IDs]. Leave blank don’t invent links.

**Critique pass (use after any of the eight):**

> Critique the draft. List: untestable lines, implied scope, missing actors, conflicts, where I must verify with a human.

## Real-world examples

1. **ShopEase.** Prompt 2 without constraints invents “return at 2,000 stores.” With constraints, it asks [QUESTION] for pickup vs drop-off.
2. **NovaBank.** Prompt 7 on document upload yields “virus scan? size limit? PII at rest?” — better than fake “response time 200ms.”
3. **ShieldSure.** Prompt 5 marks [GUESS] on surveyor allocation; BA replaces it after sitting with claims.

## Scenario / Use case: iterating AC for ShopEase auto-approve

**Context.** First prompt: “Write AC for auto-approve.” Output mentions Prime and 30 days.

**Iteration 1 — constraints:** “Facts only: prepaid, Size, <2000. Delete loyalty programs.”

**Iteration 2 — example:** “Match this bar: Given/When/Then with fields you can test in UAT.”

**Iteration 3 — critique:** Model admits it still missed QC-fail-after-approve. You add AC-RET-09 and stop.

**Sample final AC (BA-owned):**

| ID | Criteria |
|---|---|
| AC-RET-04 | Given prepaid AND reason=Size AND amount<2000 When submitted Then AUTO_APPROVED |
| AC-RET-09 | Given AUTO_APPROVED When QC=fail_damaged Then seller dispute path opens; refund does not release |

**What goes wrong if ignored.** One-shot prompts become the spec. Iteration is the actual engineering.

## Notes

- Patterns: role, context, format, constraints, examples, critique — then iterate.
- The eight prompts cover BRD slice, stories, AC, 5 Whys, process, interviews, NFRs, RTM.
- [QUESTION] and [GUESS] tags prevent invented rules.
- Prompt skill does not replace sitting with QC, RMs, or doctors.
- 
