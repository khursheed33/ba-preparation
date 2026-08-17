# Generative AI and LLM Fundamentals

## Definition

**Generative AI** is software that produces new text, images, or other content from a prompt, instead of only retrieving a stored answer.

A **Large Language Model (LLM)** is the engine behind most BA-relevant tools (ChatGPT, Copilot, Gemini). It predicts likely next tokens from patterns in training data plus your prompt. It does not “know” ShopEase policy and it does not query NovaBank’s core system unless a tool is wired in.

### What gen AI is / is not

| Is | Is not |
|---|---|
| A fast drafter and summarizer | A stakeholder, sign-off, or source of truth |
| Pattern completion on language | Understanding of your live process |
| Useful with a human in the loop | A replacement for elicitation, judgment, or UAT |

## Why it matters

BAs will be asked to use these tools. If you treat the model as an analyst, you ship fluent nonsense. If you treat it as an intern who drafts, you go faster without giving away the job.

## Tokens, prompts, context, hallucination (BA level)

| Term | BA meaning | Practical limit |
|---|---|---|
| Token | Chunk of text the model reads/writes (roughly a short word) | Long BRDs get truncated; the model may “forget” page 40 |
| Prompt | Your instruction + pasted context | Garbage in → confident garbage out |
| Context window | How much of the prompt + chat it can see at once | Paste less; point to the section that matters |
| Hallucination | Fluent content that is not true for *your* business | Invented SLAs, fake RBI clauses, made-up screens |

**Hallucination example.** You ask: “What is ShopEase’s return window for innerwear?” The model answers “30 days, like Amazon.” ShopEase policy is 7 days. The sentence is well written. It is still wrong.

## What it can and cannot replace in BA work

| Can help (draft / accelerate) | Cannot replace |
|---|---|
| First-pass user stories, AC, interview guides | Stakeholder identification and conflict handling |
| Summaries of *your* notes (if policy allows) | Validation that the need is real |
| Rephrasing for a CEO vs a developer | Sign-off, traceability, UAT judgment |
| Listing exception *questions* to ask | Domain exceptions a doctor said once |
| Critique pass: “what is ambiguous here?” | Owning the requirement |

### Weak vs strong use

| Weak | Strong |
|---|---|
| “Write the BRD for ShopEase returns” with no facts | “Using *only* this process and these numbers, draft section 3.2” |
| Pasting the full client BRD into a public chatbot | Redacted snippet + company-approved tool |
| Presenting AI text as analysis | Label as draft; validate with SMEs |

## Real-world examples

1. **NovaBank.** A BA asks the LLM for “KYC requirements in India.” It mixes RBI ideas with generic fintech blogs. Useful as a *reading list*, not as FR text.
2. **MediCare+.** Copilot drafts “SMS all patients 24 hours before.” It never invents the psychiatry suppression rule because that rule is not in the prompt.
3. **QuickBite.** AI lists compensation rules from public apps. Finance’s leakage cap is not in any training set.

## Scenario / Use case: intern pastes the BRD into ChatGPT and presents it as done

**Context.** ShopEase returns phase 1. The lead BA is on leave. An intern is told: “Draft the functional section for auto-approve Size returns under ₹2,000 prepaid.” The intern pastes last year’s 38-page BRD (including seller emails and PAN-masked but still sensitive order dumps) into a public ChatGPT window. The model returns a polished FRD. Next morning the intern presents it in stand-up as the requirements pack.

**Stakeholders.** Intern, lead BA, PO, sellers, legal/info-sec, engineering, QA.

**What breaks (in order).**

1. **Confidentiality.** Client process, volumes, and seller names left the company. Info-sec incident, not a “learning moment.”
2. **Hallucinated rules.** The model adds “14-day fashion window” and “QR drop-off at stores” because those patterns are common in e-commerce text. ShopEase has no store drop-off in this phase.
3. **Lost exceptions.** Last year’s BRD mentioned damaged-vs-used QC. The context window dropped the appendix. QA never sees the rule.
4. **No owner.** Nobody can answer “who confirmed auto-approve with sellers?” The document has no interview evidence.
5. **Traceability.** Stories in Jira do not map to IDs because the AI invented new numbering.
6. **Trust.** Engineering builds store drop-off. Warehouse cannot support it. Rollback. The intern “used AI”; the BA practice failed.

**What the intern should have done.**

1. Use an approved tool or none.
2. Paste only a redacted As-Is paragraph and the in-scope line.
3. Prompt: “List gaps and questions; do not invent SLAs.”
4. Walk sellers and QC through the draft.
5. Say in stand-up: “AI draft, not baselined.”

**Sample prompt (safe pattern).**

> Role: you are a BA intern. Context: prepaid ShopEase returns, reason = Size, amount < ₹2000. Task: list 10 questions I must ask warehouse QC. Do not write policy. Do not assume Amazon-like rules.

**Sample artifact.** Cover sheet on every AI-assisted doc: source of facts | AI used (Y/N) | validated by | date.

## Notes

- An LLM predicts tokens; it does not own ShopEase, NovaBank, or MediCare+ truth.
- Hallucination is not a rare bug — it is the default when facts are missing.
- Gen AI can draft; it cannot replace elicitation, conflict resolution, or sign-off.
- Public paste of a BRD is a privacy failure even if the English is excellent.
- Treat the model as a junior drafter who has never sat in your workshop.
- 
