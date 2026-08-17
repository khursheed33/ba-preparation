# Business Model, Customer Journey, and Value Stream

**Business model analysis** explains how the organisation creates, delivers, and captures value (who pays, for what, via which channels). **Customer journey mapping / journey analysis** follows a person’s experience across stages (awareness → use → support), including emotion and pain. **Value stream analysis** follows the work that delivers a customer request, splitting **wait time** from **work time**, to see where delay and waste sit.

## Why it matters

Requirements pulled only from a feature backlog miss *why* Subly exists, *where* ShopEase buyers rage during returns, and *which* NovaBank loan step is waiting, not working. These techniques generate requirements from value, pain, and waste — not from whoever shouted in stand-up.

## Business model canvas (lite) — Subly

Subly is a subscription platform (SaaS for creators and small businesses to sell memberships).

| Block | Subly (lite) |
|---|---|
| Customer segments | Creators, coaching businesses, fans/members |
| Value proposition | Recurring billing, access control, dunning, simple member portal |
| Channels | Web app, payment links, email dunning |
| Customer relationships | Self-serve + success for > ₹50k MRR |
| Revenue streams | % of GMV + monthly platform fee |
| Key activities | Billing, failed-payment recovery, access provisioning |
| Key resources | Payment gateway, tax engine, support playbooks |
| Key partners | Stripe/Razorpay, GST tools, email/SMS |
| Cost structure | Gateway fees, cloud, support, chargebacks |

**BA use:** if Subly’s model is “% of GMV,” a requirement that waives retries on failed cards attacks revenue. If key activity is dunning, “one email and stop” is a business-model defect, not a UX preference.

## Journey map: ShopEase returns (awareness → use → support)

Persona: Priya, repeat buyer, prepaid order, item damaged.

| Stage | What she does | Touchpoint | Emotion | Pain | Opportunity / requirement seed |
|---|---|---|---|---|---|
| Awareness | Notices damage; searches “ShopEase return” | Help article, app | Anxious | Policy buried; 7-day clock unclear | FR: return window visible on order |
| Use | Starts return, picks reason, waits for pickup | App, 3PL | Frustrated | Must print label; no slot | FR: in-app pickup slot |
| Use | Handover to rider; no receipt | Doorstep | Distrust | “Will I get refund?” | FR: OTP handover + status |
| Support | Chases refund day 10 | Chat, email | Angry | 14-day refund; no tracker | FR: refund SLA + status bar |
| Support | Repeat ticket | Agent desktop | Exhausted | Agent cannot see 3PL scan | FR: agent view of reverse scan |

Journey analysis adds **moments of truth** (handover, refund credit) and **channel breaks** (app vs chat vs 3PL SMS). Emotion is data when paired with volume (CSAT, ticket tags), not decoration.

## Value stream: NovaBank personal loan (wait vs work)

Customer request: salaried personal loan, ₹5 lakh.

| Step | Work time | Wait time | Waste type |
|---|---|---|---|
| App fill + OTP | 12 min | 0 | — |
| Document upload | 8 min | 0 | Rework if blurry |
| Branch KYC appointment | 20 min | **2–4 days** | Waiting |
| Credit officer re-key bureau | 25 min | **1 day** in queue | Extra processing |
| Physical Form 16 | 5 min | **2 days** courier | Waiting + over-processing |
| Offer + e-sign | 10 min | 0 | — |
| Disbursal ops | 15 min | **1 day** cut-off | Batch waiting |

Typical elapsed: **~9 days**. Value-added work: **~1.5 hours**. Most delay is wait and re-key. Requirements should attack waits (video KYC, bureau API, e-Form 16), not add a prettier application form.

## How these generate requirements

| Technique | Generates | Example |
|---|---|---|
| Business model | Constraints on monetisation, partners, segments | Subly: retry failed payments 4 times in 14 days (FR + BR) |
| Journey | Channel, status, emotion-driven SLAs | ShopEase: OTP handover, refund tracker |
| Value stream | Remove wait, rework, batch delays | NovaBank: no re-key; same-day disbursal cut-off twice daily |

Trace: journey pain “no refund tracker” → FR-RET-11; value-stream wait “Form 16 courier” → FR-LOS-04 e-document; model “% GMV” → BR-SUB-02 dunning must run before access cut.

## Weak vs strong

| Weak | Strong |
|---|---|
| Canvas: we are customer-centric. | Subly revenue = take-rate; dunning is a key activity — therefore retry rules are Must. |
| Journey: user is sad. | Stage Use, doorstep, distrust; 38% of return tickets tagged “where is refund.” |
| Value stream: loan is slow. | 9 days elapsed vs 1.5 hours work; 2–4 days wait on KYC. |
| Requirements from a workshop wishlist. | Each FR cites a canvas block, a journey step, or a wait step. |

## Real-world examples

**QuickBite:** journey from “I’m hungry” to “food at door” — pain at assignment wait; value stream shows kitchen work vs rider wait.

**ShieldSure:** motor claim journey (FNOL → survey → repair → pay); value stream wait on surveyor appointment.

**TripNest:** business model (commission vs merchant of record) changes refund requirements.

## Scenario / Use case: ShopEase returns journey to BRD

**Context.** CX wants “delightful returns.” Engineering wants a new returns microservice. Finance wants lower return cost.

**What the BA does.**

1. Lite canvas reminder: ShopEase makes money on delivered GMV minus returns and logistics — returns UX cannot ignore cost.
2. Journey map with 8 buyers and 4 agents; quantify pains with ticket tags.
3. Value stream of a return: buyer request (5 min work) → label print wait → 3PL pickup **3 days** → QC **2 days** → refund **5 days**.
4. Requirements: pickup slot, OTP handover, QC SLA, refund tracker; out of scope: instant refund on all categories (economic model).

**If ignored.** A beautiful returns homepage, same 14-day refund, same print-label pain.

## Notes

- Business model canvas lite: who pays, key activities, partners — use it to kill requirements that attack the model.
- Journey: stages + emotion + pain + requirement seed; awareness → use → support is the default spine.
- Value stream: elapsed vs work; wait time is usually the requirement goldmine.
- Generate FRs from a named canvas block, journey step, or wait step — then trace them.
- Do not decorate journeys with emoji instead of volumes.
