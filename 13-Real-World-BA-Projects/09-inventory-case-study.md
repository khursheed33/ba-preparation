# StockFlow — Inventory Mismatch

**Domain:** Inventory management. **Company:** StockFlow (illustrative WMS/inventory for D2C + retail). **Role:** BA, Inventory Accuracy.

## Business problem

System stock vs physical **varies 11% of SKUs** weekly (illustrative). ShopEase-style sellers using StockFlow oversell; dark-store pickers hit “ghost stock.” Cycle counts are weekend heroics. Finance cannot trust COGS. Customer: paid order then cancel for no stock.

**Related examples:** QuickBite restaurant “item available” vs packed reality; ShieldSure spare-parts stock at cashless garages. Same failure: stock number without a movement ledger.

## Business objective

12 weeks: (1) inventory accuracy **≥ 97%** SKUs (cycle-count sample); (2) oversell incidents **≤ 0.5%** of orders; (3) every stock movement has a reason code; (4) available-to-promise (ATP) used at order accept.

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| Head of Ops | H | H | Sponsor | Accuracy KPI |
| Warehouse lead | H | H | Count fatigue | Process |
| Pickers | L | H | Ghost bins | Floor |
| Finance | M | H | COGS | Ledger |
| Channel (ShopEase API) | M | H | Oversell | ATP |
| IT | M | M | Events | Integration |

## Scope

**In:** inbound, outbound, adjustment, cycle count, ATP, channel publish, reason codes, bin-level.  
**Out:** robot warehouse, full ERP finance, multi-country tax.

## Assumptions and constraints

**Assumptions:** Barcode on all Phase-1 SKUs; Wi-Fi in warehouse.  
**Constraints:** 12 weeks; existing StockFlow core; cannot stop inbound.

## As-Is / To-Be

**As-Is:** GRN on paper → Excel; picks decrement “when remembered”; adjustments with no reason; website stock = last night file.  
**To-Be:** Scan inbound → bin; pick scan mandatory; ATP = on-hand − reserved − QC hold; near-real-time channel; cycle count ABC.

**Problem analysis:** Mismatch is missing movements, not a “wrong dashboard.”

**Root cause (Fishbone):** People skip scans; process allows negative; tech nightly file; data no bin; policy free adjustments.

## Gap analysis

| Type | Gap | Action |
|---|---|---|
| Process | Optional scan | Mandatory scan |
| Tech | Nightly stock file | Event publish |
| Data | No reservation | ATP entity |
| Policy | Free adjust | Dual auth |
| People | Count as blame | ABC cycle |

## Requirements, rules

| ID | Type | Statement |
|---|---|---|
| FR-INV-01 | F | Inbound completes only with SKU+qty+bin scan. |
| FR-INV-02 | F | Pick completes only with bin+SKU scan matching allocation. |
| FR-INV-03 | F | ATP = on-hand − reserved − hold; order consume reserve. |
| FR-INV-04 | F | Adjustment requires reason + dual auth if \|qty\| > threshold. |
| FR-INV-05 | F | Channel stock update ≤ 2 min after movement. |
| NFR-INV-01 | NF | Scan offline queue ≤ 15 min; no silent drop. |

**BR-INV-01:** Negative on-hand blocked. **BR-INV-02:** ABC count: A weekly, B monthly, C quarterly.

## User stories (AC)

1. **As a receiver, I must scan to bin** to finish GRN. **AC:** Unscanned line cannot close.  
2. **As a picker, I want allocation to bin** so I do not hunt. **AC:** Wrong SKU scan blocked.  
3. **As channel, I want ATP** not on-hand. **AC:** Reserved qty not sellable.  
4. **As finance, I want adjustment reasons.** **AC:** Report by reason.  
5. **As ops, I want cycle-count tasks** by ABC. **AC:** A SKUs appear weekly.

## Use case (fully dressed): UC-INV-01 Reserve on order

- **Actor:** Order service. **Pre:** ATP ≥ qty. **Trigger:** Order accept.  
- **Main:** Reserve → decrement ATP → ack.  
- **Exception:** ATP short → reject oversell.  
- **Post:** Reservation row until pick or cancel-release.

## Wireframes

1. GRN scan. 2. Putaway bin. 3. Pick list + scan. 4. Adjustment + reason. 5. Cycle count. 6. ATP vs on-hand dashboard.

## Data, reports, KPIs

**Data:** Sku, Bin, OnHand, Reservation, Movement, Adjustment, CycleCount.  
**Reports:** accuracy; oversell; adjustments; scan compliance.  
**KPIs:** 97% accuracy; oversell ≤ 0.5%; 100% movements coded.

## UAT, RTM, CR, risks

**UAT:** inbound without scan blocked; oversell reject; dual auth; channel 2 min; cancel releases reserve.  
**RTM:** FR-INV-03→US3→UC-INV-01; FR-INV-01→US1; FR-INV-04→US4.  
**CR-INV-01:** Allow negative for “in-transit.” Impact: BR-INV-01. **Reject**; use In-Transit location instead.  
**Risks:** pickers bypass (H/H — device enforced); Wi-Fi (M/M — queue).  
**Dependencies:** channel API, device MDM, barcode quality.

## Final business solution

**Scan-mandatory ledger + ATP + reason-coded adjustments + ABC counts.** Publish ATP, not last night’s Excel. Success = accuracy and oversell, not a prettier stock number.

## Weak vs strong

| Weak | Strong |
|---|---|
| “Fix inventory bug.” | 11% mismatch → ATP + mandatory scan. |

## Notes

- Inventory portfolio: ATP vs on-hand, movements, cycle count.
- Negative stock is a policy failure.
- Illustrative accuracy only.
