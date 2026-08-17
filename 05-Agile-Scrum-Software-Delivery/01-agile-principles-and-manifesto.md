# Agile Principles and the Manifesto

## Definition

**Agile** is a way of delivering change in small, inspectable increments with continuous collaboration, rather than a single big-bang handover.

The **Agile Manifesto** (2001) states four value preferences and twelve principles. For a BA, it is a guide for *how* requirements are discovered and refined — not a license to skip clarity.

## Why it matters

Teams quote Agile to avoid artifacts. UAT then collapses because nobody agreed what "done" meant. A BA must translate manifesto values into behaviors: conversations, working increments, and **enough** documentation (AC, rules, diagrams) to test and audit.

## Concepts

### Four values in BA language

| Manifesto value | BA translation | Does not mean |
|---|---|---|
| Individuals and interactions over processes and tools | Sit with users; do not hide behind a BRD template | No process, no Jira |
| Working software over comprehensive documentation | Prefer a demoable slice with AC over a 80-page unread spec | No AC, no rules, no audit trail |
| Customer collaboration over contract negotiation | Discover with PO and users throughout | Ignore contracts, SLAs, or regulators |
| Responding to change over following a plan | Re-order the backlog when evidence changes | No roadmap, no sprint goal, chaos |

The manifesto says "while there is value in the items on the right, we value the items on the left more." Right-side items still exist.

### Twelve principles — BA language

1. **Early and continuous value:** ship a thin checkout, not a perfect program increment on paper.
2. **Welcome changing requirements:** change the backlog with impact analysis; do not pretend the sprint is infinitely elastic.
3. **Deliver working software frequently:** BA prepares slices that can actually be demoed.
4. **Business and developers daily:** BA facilitates; does not throw stories over the wall weekly.
5. **Build around motivated people:** clear goals and unblocked questions, not 40-page status.
6. **Face-to-face (or real-time) conversation:** refinement is a meeting, not only tickets.
7. **Working software is the primary measure:** AC passing on an environment beats slide progress.
8. **Sustainable pace:** do not dump twenty unready stories into a sprint.
9. **Technical excellence:** BA still captures NFRs (security, audit) in AC.
10. **Simplicity:** smallest story that tests the assumption.
11. **Self-organizing teams:** BA does not assign tasks; team pulls ready work.
12. **Reflect and adjust:** retro includes requirement quality, not only velocity.

### What "working software over comprehensive documentation" does NOT mean for a BA

It does **not** mean:

- Skip acceptance criteria or business rules.
- Skip audit, consent, or regulator evidence in banking/health/insurance.
- Replace UAT scenarios with "we'll see in production."
- Let developers infer policy from a mock.
- Delete As-Is/To-Be when the process is the product.

It **does** mean: write the smallest document that prevents the wrong product — AC, examples, and living Confluence — and keep it current.

## Real-world examples

1. **NovaBank:** Agile delivery of a card-freeze story still needs an audit event (documentation of a rule), or compliance blocks release.
2. **QuickBite:** Frequent releases of tracking slices beat a 60-page tracking BRD that nobody updates.

## Scenario / Use case: team stopped writing AC "because Agile"

### Context

ShopEase catalog team drops AC. Stories are titles: "Improve filters." Developers ship. UAT with merchandising: filters ignore out-of-stock rules, brand facets wrong, and "done" items fail every script. Leadership says Agile failed.

### Stakeholders

PO, BA, developers, QA, merchandising, UAT users.

### BA actions

1. Re-teach manifesto: left-side value does not delete AC.
2. Restore DoR: no AC, no sprint entry.
3. Rewrite top stories with GWT and one merchandising example dataset.
4. Retro: "working software" measured by UAT on AC, not by deploy count.

### Sample artifact

One-pager: four values in BA language + "AC is not comprehensive documentation; it is the testable conversation." Example story with three GWT lines vs the old title-only card.

### Failure if ignored

UAT becomes a discovery workshop after build. Rework looks like "scope change." Trust in the BA and in Agile both drop.

## Weak vs strong

| Weak | Strong |
|---|---|
| "We are Agile so no docs" | Thin, current AC and rules |
| Principles as a wall poster | Principle 7 used in sprint review |
| BA writes a mini-waterfall spec every sprint | Just-in-time detail for Ready items |
| Welcome change = mid-sprint pile-on | Change the backlog; protect sprint goal unless PO replans |

## Notes

- Manifesto preferences are relative, not deletions.
- In regulated companies, "enough documentation" is higher; Agile still applies to *when* you write it.
- Principle 2 is not "no impact analysis."
- If UAT collapses, look at AC and collaboration before blaming Scrum.
- Working software includes the rules the business thought it bought.
