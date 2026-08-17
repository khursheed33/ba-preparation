# What is Business Analysis?

## Definition

Business Analysis is the practice of enabling change in an organization by defining needs and recommending solutions that deliver value to stakeholders.

It is not only about writing documents. It is about understanding a business problem, finding what should change, and making sure the solution actually solves that problem.

## Core idea

A Business Analyst (BA) sits between **business people** (who know the problem) and **technical people** (who build the solution). The BA translates business needs into clear, usable requirements.

## What Business Analysis covers

- Identifying business problems and opportunities
- Understanding stakeholder needs
- Defining scope
- Eliciting and analyzing requirements
- Recommending solutions
- Supporting delivery, testing, and change

## What Business Analysis is not

- It is not project management (the PM owns timeline, budget, and delivery)
- It is not coding (developers build the solution)
- It is not QA (testers verify quality)
- It is not pure data analysis (data analysts focus on data insights)

## Why it matters

Projects fail when:

- The problem is unclear
- The wrong solution is built
- Stakeholders disagree
- Requirements are incomplete or changing without control

Business Analysis reduces these risks.

## Real-world examples

| Company | Vague request | What Business Analysis actually does |
|---|---|---|
| ShopEase | “Fix returns. Customers are angry.” | Define the need (returns take 9 days, NPS drops), map As-Is, write rules for pickup vs drop-off, recommend a solution that ops can run. |
| NovaBank | “Make loan approval faster.” | Separate policy delay from system delay, measure cycle time by step, write requirements for document completeness checks — not “add AI.” |
| MediCare+ | “We need a patient app.” | Ask which problem: no-shows, lab results, or billing? Recommend reminders first if no-shows are the value leak. |

### Weak vs strong understanding of BA

| Weak | Strong |
|---|---|
| BA = person who writes BRDs | BA = person who makes the change valuable and buildable |
| BA copies what the VP said | BA tests whether the VP named a symptom, a cause, or a solution |
| BA is “junior PM” | BA owns problem clarity; PM owns delivery |

## Scenario / Use case: ShopEase “just add a returns chatbot”

**Context.** ShopEase marketplace. Return cycle time is 9 days (target 4). Support tickets about “where is my refund?” are 18% of volume. A VP of CX tells the intern BA: “Business analysis is documenting what I said. Write a BRD for a returns chatbot and we will be done.”

**Stakeholders.** VP CX, returns ops, warehouse, payments (refunds), sellers, customer support, legal (consumer protection), the intern BA, engineering.

**What the BA does.**

1. Reframe: a chatbot is a *solution*. The *need* is faster, visible refunds.
2. Map As-Is: buyer raises return → seller approves (avg 2.1 days) → pickup slot → QC → refund. Chatbot cannot shrink seller approval.
3. Quantify: 62% of “where is my refund?” tickets are status, not policy questions. A tracking SMS may beat a chatbot.
4. Recommend options: (A) status notifications, (B) auto-approve low-value returns, (C) chatbot for policy FAQs. Recommend A+B first.

**Sample artifact.**

| ID | Statement |
|---|---|
| BR-RET-01 | Reduce average return-to-refund time from 9 days to ≤ 4 days for prepaid orders under ₹2,000. |
| ST-RET-02 | Buyers can see return status without calling support. |

**What goes wrong if ignored.** Engineering builds a chatbot that answers “7–10 business days.” Tickets fall 3%. Cycle time stays 9 days. Leadership says “BA work doesn’t add value,” because analysis never happened — only documentation of a wish.

## Notes

- Business Analysis is change + needs + value, not a document factory.
- Always separate problem, requirement, and solution before you write a BRD.
- ShopEase, NovaBank, and MediCare+ fail the same way: they start with a tool (chatbot, AI, app) instead of a need.
- Your first question as a BA is “what changes for whom, and how will we know it worked?”
- Industry reference map: [BABOK and the BA lifecycle](13-babok-and-ba-lifecycle.md).
- 
