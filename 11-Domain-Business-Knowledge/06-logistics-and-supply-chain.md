# Logistics, Supply Chain, and Manufacturing (Overlap)

## Definition

**Logistics** is the movement and storage of goods: warehouses, carriers, tracking, last mile. **Supply chain** is the broader flow from supplier → plant/DC → customer, including planning and inventory. **Manufacturing** makes goods from inputs using a **BOM (bill of materials)** — the recipe of components and quantities. **Order to cash (O2C)** is the commercial spine: order → fulfil → invoice → collect.

QuickBite last-mile and ShopEase warehouses live here; a factory adding a dispatch module does too.

## Why it matters

BAs write “show tracking” without events (picked, in-transit, exception). Plants cannot ship because BOM and inventory are different systems. A dashboard of GPS is not on-time (see KPI notes). Manufacturing BAs who ignore BOM lite design the wrong allocation.

## Business model

| Player | Makes money by |
|---|---|
| 3PL / courier | Per shipment, weight, SLA tiers |
| Marketplace logistics | Bundled in take-rate or billed to seller |
| Manufacturer | Product margin; logistics is cost-to-serve |
| QuickBite-style | Delivery fee + restaurant commission; density matters |

## Key processes (As-Is)

**Order to cash (lite)**

1. Order captured (B2B PO or B2C cart)
2. Credit / pay check
3. Allocate inventory (ATP)
4. Pick / pack / ship
5. POD (proof of delivery)
6. Invoice; collect; deductions (shortage)

**Warehouse**

1. Inbound ASN → GRN → putaway
2. Storage, cycle count
3. Wave pick → pack → handover
4. Returns GRN

**Tracking:** scan events on a **milestone model** (not raw GPS as the KPI).

**BOM lite (manufacturing)**

1. Finished SKU has components + qty + scrap factor
2. Work order consumes components, produces FG
3. Cannot promise FG if component ATP is short (unless substitute rule)

## Stakeholders and systems

| Stakeholders | Interest |
|---|---|
| Planner | ATP, lead time |
| Warehouse | Accuracy, productivity |
| Carrier / rider | Density, wait time |
| Customer / store | ETA honesty |
| Finance | Freight cost, deductions |
| Plant | BOM, yield |

| System | Role |
|---|---|
| WMS | Warehouse execution |
| TMS | Carrier, routing |
| OMS / ERP | Order, invoice |
| MES / ERP | Work orders, BOM |
| Tracking / visibility | Events |
| Slotting / labour | Optional |

## Regulations lite

- Dangerous goods, food safety, temperature logs
- E-way bill / GST movement where applicable
- Labour and contractor (riders) — process and payments
- Import/export if cross-border (lite awareness)

## KPIs and common BA projects

| KPI | Use |
|---|---|
| On-time (promised window) | Customer |
| Fill rate / OTIF | Perfect order |
| Dock-to-stock time | Inbound |
| Pick accuracy | Quality |
| Cost per shipment | Finance |
| Rider wait / food-ready (QB) | Marketplace delivery |
| Inventory accuracy | WMS vs book |
| Yield / scrap (mfg) | BOM reality |

**Projects:** event-based tracking, ATP promise, ship-from-multi-node, returns inbound, rider assignment, ASN/GRN, simple BOM explosion for promise dates.

### Weak vs strong

| Weak | Strong |
|---|---|
| Map = tracking | Milestone events + exception codes |
| One inventory number | Location + status (available, QC, reserved) |
| Ignore BOM | FG promise uses component ATP |
| GPS pings as KPI | On-time % + wait reasons |

## Real-world examples

**ShopEase:** split shipment (two warehouses) — one order, two tracking IDs; invoice rules.

**QuickBite:** restaurant prep vs rider — two clocks.

**Manufacturing:** promotional combo SKU — BOM of two FGs + sleeve; planning error if treated as one purchased item.

**Telecom:** CPE (router) logistics to home — install appointment is logistics + field workforce.

## Scenario / Use case: factory promise date ignores BOM

**Context.** B2B portal shows “ships in 3 days” from FG stock. FG is assembled to order. Components for a cable + PCB are 12 days out. Sales promised 3 days; plant expedites air freight; margin dies.

**BA work.** Promise engine: MTO vs MTS flag; if MTO, ATP = max(component lead, capacity). FR: show “estimated” vs “confirmed.” Planner stakeholder. UAT with a real BOM. KPI: % orders recut after promise.

**If ignored.** Expedite cost and customer distrust.

## Notes

- O2C, warehouse, tracking, BOM lite are the four pictures to sketch.
- Tracking is a state machine of events, not a map widget.
- Inventory status beats a single on-hand number.
- Manufacturing overlap: you cannot promise FG without BOM/ATP rules.
- OTIF / on-time need a defined promise.
- Returns are a second inbound process.
- Cost-to-serve (weight, attempts, COD) belongs in requirements for fees.
- Field logistics (install, delivery slot) is a capacity problem like clinics.
