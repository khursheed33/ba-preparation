# E-commerce and Retail Domain Primer

## Definition

**E-commerce** sells goods (or services) through digital channels: catalog, cart, pay, fulfil, return. **Retail** includes **stores** (POS, shelf, store inventory) plus often the same catalog online (**omnichannel**). ShopEase in these notes is marketplace + some own inventory, app and a few stores.

## Why it matters

“Add to cart” is not the business. The business is **promise** (stock, SLA), **money** (offers, COD, refunds), and **reverse logistics**. Stores vs online disagree on price and stock unless the BA names the master. Returns are a profit leak if policy is vague.

## Business model

| Model | Who holds stock | Money |
|---|---|---|
| 1P (own inventory) | ShopEase | Margin = sell − cost − fulfilment |
| Marketplace 3P | Seller | Commission / take rate |
| Retail store | Store / DC | Margin + footfall |
| Omnichannel | Shared or split | Ship-from-store, BOPIS |

Costs: discounts, COD, returns, last-mile, customer care.

## Key processes (As-Is)

**Catalog:** create SKU → content → price → tax → visibility.

**Cart / checkout:** add → address → pay (UPI/card/COD) → order.

**Fulfilment (1P)**

1. Order allocate to warehouse / store
2. Pick → pack → handover to courier
3. Track → deliver / NDR (not delivered)
4. COD remittance if applicable

**Returns:** request → RMA → pickup → QC → refund/replace (see testing notes).

**Store vs online:** price sync, inventory sync, click-and-collect: reserve shelf stock.

## Stakeholders and systems

| Stakeholders | Interest |
|---|---|
| Buyer | Price, promise, easy return |
| Seller (3P) | Listing, payout, penalties |
| Category / merch | Margin, availability |
| Warehouse / store ops | Pick accuracy, SLA |
| CX | Tickets, refunds |
| Finance | GMV vs contribution, GST |
| 3PL | Pickup windows |

| System | Role |
|---|---|
| Catalog / PIM | Product master |
| OMS | Order lifecycle |
| Inventory / WMS | Stock, pick |
| POS | Store sale |
| Payments / wallet | Capture, refund |
| Pricing / promo | Offers |
| CX / ticketing | After-sales |

## Regulations lite

- Consumer protection, fair returns advertising
- GST invoices, e-invoicing where applicable
- Payments / RBI-ish constraints on stored instruments
- Legal metrology / product claims (don’t oversell)
- Seller KYC on marketplaces

## KPIs and common BA projects

| KPI | Use |
|---|---|
| GMV, AOV | Growth |
| Conversion | Funnel |
| Contribution / order | Profit |
| Fill rate / OOS | Availability |
| On-time dispatch / delivery | Promise |
| Return % by reason | Quality / fit |
| NDR % | Address / COD |
| NPS / ticket rate | Service |

**Projects:** guest checkout, OMS statuses, ship-from-store, returns QC, seller payout, promo engine, store inventory accuracy.

### Weak vs strong

| Weak | Strong |
|---|---|
| One stock number | Channel + warehouse + reserved vs available |
| “Return anything” | Window, SKU flags, QC, refund rail |
| GMV-only success | Contribution and return rate |
| Store and app as two companies | Shared SKU, conflict rules for price |

## Real-world examples

**ShopEase** flash sale: inventory reservation vs oversell.

**Fashion retail:** size fit drives returns — catalog attribute is a requirement.

**Grocery:** perishable SLA and cold chain — NFR + process.

**QuickBite** is not retail SKU catalog in the same way (menu + availability windows) but cart/pay/dispatch rhymes.

## Scenario / Use case: ShopEase store vs online price fight

**Context.** Store POS shows ₹999; app ₹899 on the same SKU during a weekend offer. Customers demand store match. Store P&L takes the hit. Category says “app-only campaign.” POS was never in the promo system’s audience.

**BA work.** Business rule: which channel can deviate, who is master, in-store scan of app price. FR: promo eligibility = channel list; POS reads same engine or explicit “store excluded.” UAT in a real store. KPI: price mismatch tickets.

**If ignored.** Brand damage and silent margin leak at stores.

## Notes

- Catalog, cart, fulfilment, returns are the spine; stores add POS and local stock.
- Promise date is a requirement, not a courier hope.
- COD and returns change cash and fraud — first-class rules.
- Marketplace: seller and buyer are both customers of the platform.
- Inventory grain: available vs reserved vs in-transit.
- Omnichannel needs conflict rules (price, stock, returns to store).
- Contribution beats GMV as a steering KPI.
- NDR and address quality are ops requirements, not “CX later.”
