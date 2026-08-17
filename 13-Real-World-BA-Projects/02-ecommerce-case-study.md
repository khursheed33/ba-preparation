# ShopEase — Returns Cost and Painful Returns Experience

**Domain:** E-commerce. **Company:** ShopEase (illustrative). **Your role:** Business Analyst, Returns & Reverse Logistics.

## Business problem

ShopEase reverse-logistics cost is ₹18 per delivered order (illustrative). Buyers wait 12–14 days for refunds. CSAT on returns is 28. Three reasons (size/fit, transit damage, item-different) drive 82% of return volume. The current “print label and drop at courier” journey creates tickets, not loyalty.

## Business objective

Within two quarters of go-live: (1) reverse cost ≤ ₹12 per delivered order; (2) refund P50 ≤ 3 days after QC pass; (3) returns CSAT ≥ 55; (4) size/fit returns down 25% via listing QA (linked initiative).

## Stakeholders and analysis

| Stakeholder | Influence | Interest | Attitude | Engagement |
|---|---|---|---|---|
| CPO / Sponsor | H | H | Supportive | Weekly decisions |
| Returns Ops Lead | H | H | Cautious (3PL) | Process owner |
| CX / Support | M | H | Frustrated | Journey + UAT |
| Finance | M | H | Cost-focused | CBA, refund timing |
| 3PL Partner | M | M | Neutral | Pickup SLA |
| Seller Ops | M | H | Resistant | Size-chart rules |
| Buyer (persona Priya) | L | H | Angry | Interviews |
| Legal | M | M | Policy | Return window BR |
| Engineering / QA | M | H | Delivery | Specs + UAT |

## Scope

**In:** app/web return request, reason codes, pickup slot, OTP handover, QC status, refund tracker, agent desktop view, seller listing-photo flag for “item different.”  
**Out:** instant refund on all categories; international returns; try-and-buy for jewellery; new 3PL contract (reuse current).

## Assumptions and constraints

**Assumptions:** 3PL API can book pickup slots in 8 metros; prepaid and COD both in scope; QC hubs exist in those metros.  
**Constraints:** 16-week delivery; must reuse ShopEase Wallet/UPI refund rails; 7-day fashion window unchanged this phase; PCI: no card data in returns service.

## As-Is process (diagram described)

1. Buyer opens order → Help → “Return” article.  
2. Fills Google-form style page; prints A4 label (wait: printer).  
3. Drops at courier (wait: 0–3 days).  
4. 3PL to QC hub (wait: 2–4 days).  
5. QC in spreadsheet; email to finance (wait: 2 days).  
6. Refund 5–7 days; buyer chats “where is money?”  

**Problem analysis:** Cost sits in tickets (₹4.2/order support allocation) + 3PL + lost repeat purchase. Pain peaks at no handover proof and no refund status.

**Root cause (Pareto + 5 Whys):** 82% volume = three reasons. Refund delay Why-chain: no QC status in system → finance waits for email → batch refunds twice a week. Pickup pain: no slot because returns never integrated to 3PL pickup API.

## To-Be process (diagram described)

1. Buyer taps Return on order; sees window and reason list.  
2. Selects reason + photos (damage / item-different).  
3. Picks pickup slot (next 48 hours).  
4. Rider OTP-handover; scan in system.  
5. QC hub updates PASS/FAIL; buyer sees status.  
6. PASS → refund to original mode within 24 hours of QC (P50). FAIL → comment + relist path.

## Gap analysis

| Type | Gap | Action |
|---|---|---|
| Process | No pickup, no OTP | New reverse process |
| Tech | No 3PL pickup API, no tracker | FRs below |
| Data | Free-text reasons | Reason code master |
| Policy | Open-box undefined | BR for damage photos |
| People | Agents cannot see 3PL | Agent screen + training |

## Requirements

| ID | Type | Statement |
|---|---|---|
| FR-RET-01 | F | Logged-in buyer can start return on eligible delivered order within policy window. |
| FR-RET-02 | F | Buyer must select a reason code; damage/item-different require 1–5 photos. |
| FR-RET-03 | F | Buyer can book a 2-hour pickup slot in next 48 hours (serviceable PIN). |
| FR-RET-04 | F | Handover completes only after buyer OTP + rider scan. |
| FR-RET-05 | F | Buyer and agent see status: REQUESTED, PICKUP_BOOKED, IN_TRANSIT, QC, REFUNDED, REJECTED. |
| FR-RET-06 | F | On QC PASS, refund instruction to original payment within 24 hours. |
| NFR-RET-01 | NF | Status API p95 ≤ 2s; 99.5% monthly availability. |
| NFR-RET-02 | NF | Photos stored 180 days; PII minimised. |
| NFR-RET-03 | NF | 20k return requests/day peak. |

## Business rules

- **BR-RET-01:** Fashion window = 7 days from delivery; electronics 10 days; innerwear no return unless item-different/damage.  
- **BR-RET-02:** Coupon + bank offer stacking unchanged; refund = amount actually paid.  
- **BR-RET-03:** QC FAIL if photos do not match delivered SKU serial/EAN when required.

## User stories (with AC)

1. **As a buyer, I want to start a return from My Orders** so I do not hunt Help. **AC:** Given delivered eligible order, When I tap Return, Then FR-RET-01 flow opens; ineligible shows reason.  
2. **As a buyer, I want a pickup slot** so I need not print a label. **AC:** Given serviceable PIN, When I select slot, Then FR-RET-03 confirms and SMS sent.  
3. **As a buyer, I want OTP handover** so I have proof. **AC:** Given rider at door, When OTP matches, Then status IN_TRANSIT.  
4. **As a buyer, I want refund status** so I do not chat. **AC:** Given QC PASS, Then status REFUNDED within 24h and amount shown.  
5. **As an agent, I want 3PL scan on the ticket** so I can close chats. **AC:** Given ticket on order, Then latest scan and ETA visible.  
6. **As QC, I want reason-coded photos** so I can PASS/FAIL in 2 minutes. **AC:** Given IN_TRANSIT arrival, Then photos + EAN on QC screen.

## Use case (fully dressed): UC-RET-01 Book return pickup

- **Actor:** Buyer. **Pre:** Logged in; order DELIVERED; within window.  
- **Trigger:** Taps Return.  
- **Main:** Select items → reason (+ photos if needed) → slot → confirm → SMS.  
- **Alt:** PIN not serviceable → drop-off list (Should, not Must).  
- **Exception:** Window expired → message + Help.  
- **Post:** ReturnId created; status PICKUP_BOOKED; 3PL job created.

## Wireframes (screen-by-screen)

1. **My Orders:** Return CTA on eligible rows.  
2. **Item + reason:** codes, photo upload, policy snippet.  
3. **Slot picker:** calendar + 2-hour bands.  
4. **Confirm:** address, slot, “OTP at handover.”  
5. **Tracker:** timeline of statuses.  
6. **Agent desktop:** order, scans, QC, refund id.  
7. **QC console:** photos, EAN, PASS/FAIL.

## Data, reports, KPIs

**Data:** Return (id, order_id, reason_code, status, slot); Photo; ScanEvent; QcResult; RefundInstruction.  
**Reports:** daily returns by reason; refund TAT P50/P90; pickup SLA misses; ticket volume on returns.  
**KPIs:** reverse cost/order; refund P50; CSAT; % OTP handover; % top-3 reasons.

## UAT scenarios

- Happy prepaid fashion return, OTP, QC PASS, refund 24h.  
- Damage without photos blocked.  
- Window expired.  
- QC FAIL path.  
- Agent sees scan.  
- COD refund to bank account captured at request.

## RTM

| Req | Story | UC | UAT |
|---|---|---|---|
| FR-RET-01 | US1 | UC-RET-01 | Eligible / ineligible |
| FR-RET-03 | US2 | UC-RET-01 | Slot book |
| FR-RET-04 | US3 | — | OTP |
| FR-RET-05 | US4, US5 | — | Tracker + agent |
| FR-RET-06 | US4 | — | Refund 24h |
| BR-RET-01 | US1 | UC-RET-01 | Window |

## Change request (sample)

**CR-RET-01:** Seller asks “try-and-buy 14 days for fashion.” **Impact:** BR-RET-01, finance float, 3PL volume. **Decision:** Won’t this phase; log as Could next.

## Risks and dependencies

| Risk | P/I | Mitigation | Owner |
|---|---|---|---|
| 3PL slot API late | M/H | Drop-off fallback | PM + 3PL |
| Photo storage cost | L/M | 180-day purge | Architect |
| Seller revolt on item-different | M/M | Evidence pack | Seller Ops |

**Dependencies:** 3PL pickup API; payments refund API; notification service.

## Final business solution

Phased reverse-logistics: **Must** digital return + slot + OTP + tracker + 24h refund after QC. Attack 82% reason Pareto via listing QA as a parallel Should. Do not promise instant refund. Success = cost, TAT, CSAT — not a prettier Help page.

## Weak vs strong (this pack)

| Weak | Strong |
|---|---|
| “Amazon-like returns.” | Cost ₹18→₹12, refund P50 3 days, Pareto 82%. |

## Notes

- Portfolio: e-commerce returns is a complete BA case — cost, journey, 3PL, rules.
- Keep numbers labelled illustrative.
- Trace every FR to UAT; include one CR to show change control.
