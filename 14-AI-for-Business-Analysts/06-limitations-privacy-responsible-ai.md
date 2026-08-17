# Limitations, Privacy, and Responsible AI

## Definition

**AI limitations** are structural: models guess fluent text, do not know your live systems, and cannot take accountability.

**Hallucinations** are confident false statements (fake SLAs, fake laws, fake screens).

**Responsible AI usage** for a BA means: approved tools, no forbidden data, human validation of every requirement-like sentence, and the stance that **AI augments BA thinking rather than replacing fundamentals**.

## Why it matters

One paste of a client BRD or a patient list can be an incident. One unvalidated story can be a sprint of waste. Corporates will judge you on judgment, not on how fast you generate Markdown.

## What never to paste

| Never paste | Why | Safer alternative |
|---|---|---|
| PII (names, phone, PAN, health) | Law + trust | Aggregates, fake IDs, role names |
| Secrets, tokens, source code credentials | Security | Nothing — ask IT |
| Full client BRDs / contracts | Confidential business information | Redacted facts you elicited |
| Meeting audio of patients/customers | Consent + confidentiality | Approved enterprise tool or handwritten notes |
| Production query results with account numbers | Data privacy | Counts and bins |

**Confidential business information** includes unreleased pricing, seller GMV, NovaBank credit policy, ShieldSure loss ratios — even without names.

## Policy mindset for corporates

- Assume a written AI policy exists; if not, ask Legal/IT before the first paste.
- Default: **company tenant** (enterprise Copilot/ChatGPT) > consumer ChatGPT.
- Logging: many tools train on or store prompts. Treat prompts as email to a vendor.
- Client contracts may forbid subprocessors. MediCare+ and NovaBank often do.
- When in doubt, do not paste. Draft from memory of *non-secret* process steps.

## Hallucinations and other limitations

| Limitation | BA impact |
|---|---|
| Hallucination | Invented RBI/IRDAI clauses in FR text |
| Stale training | Competitor flows from two years ago |
| No process memory | Quiet exception not in the prompt is gone |
| Sycophancy | Agrees with “we need AI” instead of challenging |
| No accountability | It cannot sign UAT |

## Human validation of AI-generated requirements

Checklist before a story is “yours”:

1. Every number traces to a metric, interview, or [QUESTION].
2. In/out scope matches the signed list.
3. Exceptions exist (at least one negative path).
4. Named actor, not “user.”
5. Testable AC; no “easy/seamless.”
6. Conflicts with existing SOPs resolved by a human owner.
7. Compliance/privacy reviewed if data or health/money is involved.
8. SME or PO has walked through it.
9. You can explain it in an interview without the chat log.

### Weak vs strong

| Weak | Strong |
|---|---|
| “ChatGPT said RBI requires X” | Circular number + compliance SME |
| Pasting yesterday’s BRD to “make it nicer” | Rewrite from redacted bullets in an approved tool |
| Skipping elicitation because the draft “looks complete” | Draft is a hypothesis |

## Real-world examples

1. **ShopEase.** Intern pastes seller emails; model writes a fair-sounding policy that legal never approved.
2. **NovaBank.** Model invents a cooling period that is *stricter* than fraud wants — still a hallucination if nobody confirmed it.
3. **MediCare+.** De-identified appointment counts are OK to analyze; a CSV of patient mobiles is never OK.

## Scenario / Use case: “just polish the FRD” on a public chatbot

**Context.** ShieldSure claims FRD, marked Confidential. A BA pastes it into a free ChatGPT to “improve English” before a steering committee. The model also “fills gaps” with cashless rules from public blogs.

**What the BA should have done.**

1. Use enterprise tool or a human editor.
2. Polish only a redacted section.
3. Run the validation checklist; delete invented IRDAI timelines.
4. Tell the committee: wording polish vs content change — separately.

**What goes wrong if ignored.** Confidential document in a consumer log. Steering pack contains unofficial rules. Audit asks “source?” You answer “the model.” That is not BA practice.

## Notes

- Never paste PII, secrets, or client BRDs into public AI.
- Hallucinations are normal; validation is the job.
- Corporate policy: approved tools, contracts, logging — ask before you paste.
- Human validation checklist is mandatory for AI-drafted requirements.
- AI should augment BA thinking, not replace elicitation, analysis, or fundamentals.
- 
