# QuickBite — Late Deliveries and Compensation Chaos

**Domain:** Food ordering. **Company:** QuickBite (illustrative). **Role:** BA, Delivery Promise & CX.

## Business problem

Late deliveries (beyond promised ETA) are **19%** of completed orders (illustrative). Compensation is ad hoc: agents issue free food or refunds with no rule. Cost ₹1.8 Cr/quarter on post-accept cancellations plus ₹90 lakh goodwill. Restaurants are fined when riders are late. Customers still churn.

## Business objective

In 12 weeks: (1) late rate **≤ 10%**; (2) compensation **rule-based**, leakage ≤ 40% of current goodwill; (3) cancel-after-accept **≤ 5%**; (4) restaurant fines only when kitchen misses `food_ready` SLA.

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| CPO | H | H | Speed vs cost | Decision paper |
| Dispatch lead | H | H | Utilisation vs ETA | Shadow shift |
| Restaurant ops | M | H | Angry at fines | P&L workshop |
| CX / agents | M | H | No rules | Decision table |
| Riders | L | H | Batching pain | Interviews |
| Finance | M | H | Leakage | CBA |
| Customer | L | H | Late + hungry | Journey |
| Legal | M | M | Fair terms | BR review |

## Scope

**In:** `food_ready` event; ETA display rules; cancel-after-accept reasons; compensation engine; restaurant vs rider attribution; agent override with reason.  
**Out:** scheduled orders 24x7 expansion; new rider app from scratch; kitchen IoT; insurance of food.

## Assumptions and constraints

**Assumptions:** Restaurant tablet can add one button; dispatch can consume `food_ready`; 8 metros Phase 1.  
**Constraints:** Must not break current assignment engine in week 1; 12-week window; existing payments refund API.

## As-Is process (diagram described)

1. Customer orders; ETA 25 min shown at restaurant **Accept**.  
2. Dispatch **holds** for batching; rider assigned late.  
3. ETA jumps to 55 min → customer cancels or waits.  
4. If late, chat: agent types compensation (inconsistent).  
5. Restaurant fined on “order late” regardless of kitchen vs rider.

**Problem analysis:** Promise is made before a rider exists. Compensation is a symptom. Fines hit the wrong party.

**Root cause (5 Whys + Pareto):** 61% cancels = “ETA too long.” Chain: no `food_ready` → dispatch hold after Accept → tight ETA too early. Pareto: three delay causes (rider wait, kitchen late, address) — compensation must branch.

## To-Be process (diagram described)

1. Restaurant Accept = kitchen SLA clock starts.  
2. Tight customer ETA **only after rider assigned** (or show band: “30–45 min”).  
3. Restaurant taps Food ready; dispatch already moving.  
4. If late: engine attributes kitchen vs rider vs address; compensation per table.  
5. Agent may override with code + cap.

## Gap analysis

| Type | Gap | Action |
|---|---|---|
| Process | Accept ≠ food ready | New event + SLA |
| Tech | No attribution, no engine | FRs |
| Policy | Goodwill unlimited | Decision table |
| Data | Cancel reason free text | Codes |
| People | Agents invent refunds | SOP + cap |

## Requirements

| ID | Type | Statement |
|---|---|---|
| FR-DLV-01 | F | Restaurant must send `food_ready`; clock from Accept. |
| FR-DLV-02 | F | Customer sees precise ETA only after rider assigned; else time band. |
| FR-DLV-03 | F | Cancel-after-accept requires a reason code. |
| FR-DLV-04 | F | Compensation engine applies BR-DLV table; logs amount. |
| FR-DLV-05 | F | Restaurant penalty only if `food_ready` exceeds kitchen SLA. |
| FR-DLV-06 | F | Agent override ≤ ₹300 with reason; above needs lead. |
| NFR-DLV-01 | NF | Event ingest ≤ 2s; 99.9% during peak. |
| NFR-DLV-02 | NF | Audit 180 days. |

## Business rules

- **BR-DLV-01:** If kitchen on time AND rider late > 10 min past ETA → coupon ₹100 or 20% max ₹150.  
- **BR-DLV-02:** If kitchen late → no rider-fault compensation; apology template only.  
- **BR-DLV-03:** Customer-caused (wrong pin, unreachable) → no compensation.  
- **BR-DLV-04:** Stack with other coupons per ShopEase-style “no double goodwill.”

## User stories (with AC)

1. **As a customer, I want an honest ETA** so I do not cancel. **AC:** Precise ETA hidden until rider assigned.  
2. **As a restaurant, I want Food ready** so I am not fined for riders. **AC:** Penalty only if kitchen SLA miss.  
3. **As a customer, I want auto-compensation when you are at fault.** **AC:** BR-DLV-01 fires without chat.  
4. **As an agent, I want the rule on screen** so I do not invent. **AC:** Suggested amount + override cap.  
5. **As dispatch, I want food_ready** to stop blind holds. **AC:** Hold rule cannot ignore ready event.  
6. **As finance, I want leakage report** by reason. **AC:** Daily compensation by BR id.

## Use case (fully dressed): UC-DLV-01 Compensate late order

- **Actor:** System (auto) / Agent. **Pre:** Order DELIVERED or CANCELLED_AFTER_ACCEPT; timestamps complete.  
- **Trigger:** Delivery complete or cancel.  
- **Main:** Attribute delay → apply BR → notify customer → wallet/coupon.  
- **Alt:** Missing `food_ready` → treat kitchen as unknown; no restaurant fine; CX coupon per BR-unknown.  
- **Exception:** Duplicate compensation blocked.  
- **Post:** Ledger row; agent sees “already paid.”

## Wireframes

1. Restaurant tablet: Accept | Food ready. 2. Customer: time band then live ETA. 3. Cancel reason picker. 4. Auto “sorry + coupon” card. 5. Agent: attribution + cap. 6. Ops dashboard: late %, leakage, kitchen vs rider.

## Data, reports, KPIs

**Data:** OrderEvents (accept, ready, assign, arrive), CancelReason, Compensation, Attribution.  
**Reports:** late %; cancel-after-accept; compensation ₹; fine accuracy; ETA jump events.  
**KPIs:** late ≤ 10%; cancel-after-accept ≤ 5%; goodwill −40%; % fines matching kitchen miss.

## UAT scenarios

- Kitchen on time, rider late → coupon, no restaurant fine.  
- Kitchen late → no coupon, restaurant SLA miss.  
- ETA band before assign.  
- Agent override above cap blocked.  
- Double compensation blocked.  
- Missing food_ready path.

## RTM

| Req | Story | UC | UAT |
|---|---|---|---|
| FR-DLV-02 | US1 | — | ETA band |
| FR-DLV-05 | US2 | — | Fine |
| FR-DLV-04 | US3 | UC-DLV-01 | Auto coupon |
| FR-DLV-06 | US4 | UC-DLV-01 | Cap |
| FR-DLV-01 | US5 | — | Ready event |

## Change request (sample)

**CR-DLV-01:** Marketing wants “always ₹50 coupon if > 20 min.” Impact: BR-DLV-01/02, leakage. **Decision:** Reject; breaks attribution.

## Risks and dependencies

| Risk | P/I | Mitigation | Owner |
|---|---|---|---|
| Restaurants ignore Food ready | H/H | Make Accept incomplete without training + in-app nudge | Rest. ops |
| Dispatch refuses to stop hold | M/H | Product + dispatch SLA | CPO |
| Customers game cancels | M/M | Reason codes + pattern report | Risk |

**Dependencies:** restaurant app release; dispatch rule change; wallet coupon API.

## Final business solution

Fix the **promise** (ETA after assign + `food_ready`) and replace goodwill with a **decision table**. Fines follow kitchen SLA. Agents get a cap, not a blank cheque. Success = late %, cancel %, leakage — not more chat macros.

## Weak vs strong

| Weak | Strong |
|---|---|
| “Better cancellation UI.” | 5 Whys + compensation BRs + attribution. |

## Notes

- Food-ordering portfolio case: SLA, two-sided marketplace, CX cost.
- Do not fine restaurants for rider delay.
- Illustrative money figures only.
