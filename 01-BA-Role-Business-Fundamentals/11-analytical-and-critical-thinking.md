# Analytical Thinking, Critical Thinking, and Structured Problem Solving

These are core BA skills. Tools like Jira or Excel are secondary. Thinking is primary.

## Analytical thinking

Breaking a large problem into smaller parts.

Example: "Sales dropped" is too big. Split it:

- Which product?
- Which region?
- Which customer segment?
- Since when?
- Online or offline?
- Conversion issue or traffic issue?

A BA uses analysis to move from a vague complaint to a specific, solvable problem.

## Critical thinking

Questioning what you hear instead of accepting it as fact.

Ask:

- Is this a fact or an opinion?
- Who says this, and what is their interest?
- What evidence exists?
- What else could explain this?
- Are we solving the symptom or the cause?

Example: A manager says "We need AI." Critical thinking asks: What decision is slow or poor today? Would AI actually help, or is a simpler process change enough?

## Structured problem solving

A repeatable way to move from problem to recommendation.

Simple BA structure:

1. Understand the current situation (As-Is)
2. Define the problem clearly
3. Identify root causes
4. Define the desired situation (To-Be)
5. Find gaps
6. Recommend options
7. Define requirements for the chosen option

Do not jump from complaint → solution. That is how wrong software gets built.

## Habits to practice

- Write the problem before writing features
- Ask "why" more than once
- Separate facts, assumptions, and opinions
- Use numbers when possible
- Compare options instead of falling in love with one idea

## Real-world examples

**Analytical split (ShopEase “sales dropped”)**

| Cut | Finding |
|---|---|
| Product | Returns-heavy fashion SKUs, not electronics |
| Region | West warehouses slower QC |
| Segment | Prepaid vs COD — prepaid refunds drive the NPS hit |
| Time | After festival sale, seller approval SLA broke |
| Channel | App vs web — same process, app shows no status |

**Critical thinking (NovaBank “we need AI”)**

- Fact vs opinion: “AI will cut TAT” is opinion until you know where hours go.
- Interest: vendor wants a model; ops wants fewer incomplete files.
- Alternative: a completeness checklist might move TAT more than a model this quarter.

**Structured path (MediCare+)**

As-Is (no reminder) → problem (22% no-show) → root (no prompt + painful reschedule) → To-Be (remind + one-tap reschedule) → gaps (consent, specialty suppress) → options (SMS vs app vs call centre) → requirements for the chosen mix.

### Weak vs strong

| Weak | Strong |
|---|---|
| Accepts “AI” as the problem | Asks which decision is slow and what a simple rule would do |
| One cause, one feature | Cuts the metric; lists competing causes; tests with data |
| Jumps to Figma | Writes problem and options first |

## Scenario / Use case: QuickBite Friday-night “the app is slow”

**Context.** CX says the app is slow on Friday nights so orders are late. Engineering wants a performance sprint. A restaurant partner says kitchens are slammed. Rider ops says rain. You have a pivot of 4 weeks of orders.

**Stakeholders.** CX, engineering, restaurants, rider ops, BA, PO.

**What the BA does.**

1. **Analyze:** split late orders by cause code if it exists; if not, proxy: restaurant accept time, “ready” timestamp, rider assigned, delivered.
2. **Critical:** “app is slow” is a diagnosis from CX, not a fact. Check p95 checkout time vs kitchen-ready delay.
3. **Structure:** As-Is timestamps → problem statement with the biggest delay bucket → options (kitchen throttling, rider buffer, app perf) → recommend based on evidence.
4. Finding (example): 70% of Friday-late had kitchen-ready > promised prep; app p95 was fine. Performance sprint would not fix the business problem.

**Sample artifact.** Cause table (illustrative):

| Delay bucket | % of late orders | Thinking |
|---|---|---|
| Kitchen past promised prep | 70% | Process / restaurant SLA |
| Rider after ready | 18% | Logistics |
| Checkout / payment errors | 7% | App — real but smaller |
| Address / customer | 5% | UX |

**What goes wrong if ignored.** The team ships app caching. Restaurants still go late. CX still shouts. Critical thinking was skipped because a senior person named a technical cause.

## Notes

- Split before you solve. Question before you agree. Structure before you recommend.
- Facts, opinions, and assumptions get different columns — never one paragraph of mush.
- Tools (Jira, Excel) do not replace this; they record it.
- 
