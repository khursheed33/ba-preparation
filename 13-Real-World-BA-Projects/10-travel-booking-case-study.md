# TripNest — Travel Booking Pain (Failed Bookings & Refunds)

**Domain:** Travel booking. **Company:** TripNest (illustrative flights + hotels). **Role:** BA, Booking & Fulfilment.

## Business problem

**8% of paid flight bookings** fail at supplier (illustrative) after customer is charged. Refunds take **11 days**. Agents re-book on WhatsApp. Customers double-pay. NPS booking **18**. Hotel voucher vs supplier mismatch causes airport/hotel fights.

**Related examples:** ShopEase capturing payment before seller confirms stock; MediCare+ sending a “booked” SMS before HIS locks the slot. Same failure: money or promise before inventory.

## Business objective

10 weeks: (1) paid-but-unconfirmed **≤ 1.5%**; (2) auto-refund **≤ 48 hours** when supplier fail; (3) 100% bookings have supplier PNR/voucher in record; (4) agent desktop shows same status as customer.

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| CPO | H | H | Sponsor | Fail % |
| Airline/GDS ops | H | H | Timeouts | Timeout BR |
| Hotels supply | M | H | Allotment | Voucher rules |
| Payments | M | H | Charge vs capture | Auth-capture |
| CX agents | M | H | WhatsApp | Desktop |
| Customer | L | H | Anxiety | Journey |
| Finance | M | H | Refund float | SLA |

## Scope

**In:** search-select-pay-confirm, supplier poll, fail/refund, PNR display, hotel voucher, agent tools.  
**Out:** packages/dynamic packaging, loyalty rewrite, insurance attach (Could).

## Assumptions and constraints

**Assumptions:** GDS/hotel APIs return status; payments support void/refund.  
**Constraints:** 10 weeks; PCI via existing PSP; supplier SLAs not fully in our control.

## As-Is / To-Be

**As-Is:** Pay capture immediately → async supplier → fail silent → customer chats day 3 → manual refund.  
**To-Be:** Auth hold → supplier confirm → capture; if fail, auto-void/refund and notify; PNR/voucher mandatory before “CONFIRMED.”

**Problem analysis:** Money moves before inventory is sure.

**Root cause:** Capture-before-confirm; no poll SLA; hotel voucher generated from cache.

## Gap analysis

| Type | Gap | Action |
|---|---|---|
| Process | Capture first | Auth then capture |
| Tech | Weak poll | Status machine |
| Data | PNR optional | Mandatory |
| Policy | Refund 11 days | 48h BR |
| People | Agent WhatsApp | Same desktop |

## Requirements, rules

| ID | Type | Statement |
|---|---|---|
| FR-TRP-01 | F | Booking CONFIRMED only with supplier PNR (air) or voucher id (hotel). |
| FR-TRP-02 | F | Payment capture only after supplier confirm (or policy BR-TRP-02).  
| FR-TRP-03 | F | Supplier fail → auto refund/void and SMS/email ≤ 48h. |
| FR-TRP-04 | F | Customer and agent see identical status + PNR. |
| FR-TRP-05 | F | Hotel voucher PDF from supplier payload, not cache name only. |
| NFR-TRP-01 | NF | Supplier poll ≤ 30s timeout; retry 3. |

**BR-TRP-01:** Statuses: INIT, AUTH, SUPPLIER_PENDING, CONFIRMED, FAILED, REFUNDED. **BR-TRP-02:** If supplier requires prepay, show “charge now; refund 48h if fail.”

## User stories (AC)

1. **As a traveller, I want CONFIRMED only with PNR.** **AC:** Ticket screen shows PNR.  
2. **As a traveller, I want auto-refund on fail.** **AC:** 48h; status REFUNDED.  
3. **As an agent, I want the same PNR** as the app. **AC:** No WhatsApp lookup.  
4. **As finance, I want auth vs capture report.** **AC:** Daily recon.  
5. **As a traveller, I want hotel voucher that matches the hotel.** **AC:** Supplier id on voucher.

## Use case (fully dressed): UC-TRP-01 Book flight

- **Actor:** Traveller. **Pre:** Fare selected. **Trigger:** Pay.  
- **Main:** Auth → supplier book → PNR → capture → CONFIRMED.  
- **Alt:** Supplier timeout → retry; still fail → void + FAILED.  
- **Post:** Itinerary email with PNR.

## Wireframes

1. Search results. 2. Review fare rules. 3. Pay (auth messaging). 4. Pending spinner with honest wait. 5. Confirmed + PNR. 6. Failed + refund ETA. 7. Agent booking desk.

## Data, reports, KPIs

**Data:** Booking, PaymentAuth, SupplierRef (PNR/voucher), StatusHistory.  
**Reports:** fail after pay; refund TAT; auth-capture mismatch.  
**KPIs:** unconfirmed ≤ 1.5%; refund ≤ 48h; 100% PNR on confirmed.

## UAT, RTM, CR, risks

**UAT:** happy PNR; supplier fail void; agent PNR match; hotel voucher id; timeout retries.  
**RTM:** FR-TRP-01→US1→UC-TRP-01; FR-TRP-03→US2; FR-TRP-04→US3.  
**CR-TRP-01:** Add travel insurance attach. **Could** Phase 2.  
**Risks:** supplier SLA (H/H — messaging + refund); PCI (L/H — PSP only).  
**Dependencies:** GDS, hotel API, PSP, email.

## Final business solution

**Do not sell a ticket you do not hold.** Auth-capture alignment, mandatory supplier refs, 48h fail-refund, one status for customer and agent.

## Weak vs strong

| Weak | Strong |
|---|---|
| “Better booking UX.” | 8% fail-after-pay → confirm-before-capture. |

## Notes

- Travel portfolio: supplier vs merchant of record, PNR, refunds.
- Cache-generated vouchers are a data lie.
- Illustrative fail rates only.
