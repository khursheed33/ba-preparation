# Other Domains: HR, Travel, Government, Real Estate

## Definition

These domains show up often in BA work even if you picked banking or e-commerce first. Each has its own **terminology, processes, systems, and a typical scenario**. Learn them at conversation depth: you can map As-Is and not invent illegal or unsafe shortcuts.

## Why it matters

HR payroll errors are Sev1 for employees. Travel inventory is perishable (the seat vanishes). Government work is audit-first. Real estate is slow money plus legal title. Using ShopEase “checkout” language here produces unusable BRDs.

### Weak vs strong (all four)

| Weak | Strong |
|---|---|
| HR = leave form UI | Hire-to-retire + statutory + maker-checker |
| Travel = pretty search | Inventory, fare rules, PNR, cancel policy |
| Government = portal screens | Citizen identity, SLA Act-style, audit trail |
| Real estate = listing photos | Lead → site visit → booking → agreement → registration |

---

## HR

**Terminology:** employee vs contractor, CTC vs in-hand, attendance, leave types, payroll cut-off, PF/ESI/TDS (names vary), appraisal cycle, org hierarchy, joining/exit (full and final).

**Business model (internal):** HR is a cost/service function; “customers” are employees and managers. HR-tech SaaS sells to companies per employee per month.

**Key process (hire to retire, lite):** requisition → offer → join → attend/leave → payroll → change (transfer) → exit & F&F.

**Systems:** HRMS/HRIS, ATS (recruiting), payroll, biometric/attendance, SSO, helpdesk.

**Regs lite:** labour, privacy of employee data, statutory filings — specialist in the room.

**KPIs:** time-to-hire, offer accept %, payroll error rate, time-to-F&F, attrition.

**Scenario / Use case.** Payroll cut-off is the 20th. A new join on the 22nd is missing from the file. BA writes: cut-off calendar, mid-month joiner proration, exception path with finance maker-checker — not “HR will Excel it.” UAT by payroll ops, not the BA.

---

## Travel

**Terminology:** PNR, sector/leg, fare class, inventory, GDS, ancillaries, no-show, TTL (ticket time limit), refund vs void, hotel room-night, occupancy.

**Business model:** airline/hotel sell perishable inventory; OTAs take commission; QuickBite-like logistics only for airport transfers.

**Key process (air, As-Is):** search → fare rules → hold/PNR → pay → ticket → change/cancel → disruption (delay/cancel) re-accommodation.

**Systems:** GDS/PSS, OTA, payment, loyalty, ops control (irregular ops).

**Regs lite:** passenger rights on delay/cancel, KYC on some payments, GST on tickets.

**KPIs:** conversion, cancellation %, ancillary attach, on-time departure, occupancy (hotels), refund TAT.

**Scenario / Use case.** OTA shows “refundable.” Airline fare is non-refundable minus a small tax. Customer hates the OTA. BA: fare-rule display as AC, not marketing copy; UAT with a real non-refundable PNR; exception: disruption involuntary refund.

---

## Government

**Terminology:** citizen, department, scheme, beneficiary, grievance, file/noting, SLA, certificate, DBT, CSC (assisted), audit, RTI-minded transparency.

**Business model:** not profit; legitimacy, inclusion, leakage control, SLA. Vendors are paid for delivery.

**Key process (certificate/service):** apply → pay fee (if any) → verify (docs, field) → approve/reject → issue → grievance.

**Systems:** national/state ID, department workflow, payment gateway, DMS, grievance portal.

**Regs lite:** Aadhaar/identity usage constraints, data minimization, accessibility, retention, procurement.

**KPIs:** median TAT vs notified SLA, first-time-right %, leakage/fraud flags, grievance reopen %, uptime.

**Scenario / Use case.** Birth certificate portal: duplicate applications because name spelling variants. BA: identity match rules, assisted CSC flow, status SMS without extra PII, audit who approved. UAT with clerks *and* a citizen on mobile data.

---

## Real estate

**Terminology:** listing, inventory (unit), site visit, booking amount, agreement for sale, registration, RERA-style disclosures (where applicable), channel partner, possession, CAM (maintenance).

**Business model:** developer sells units (or leases); brokers take commission; portals take leads. Slow cycle, high ticket, legal-heavy.

**Key process:** lead → qualify → site visit → booking → KYC/funds → agreement → milestones / demand notices → registration → possession → snag list.

**Systems:** CRM, inventory (unit status), channel partner portal, document, ERP collections.

**Regs lite:** RERA-like advertising and escrow (jurisdiction-specific), KYC of buyer, tax on property.

**KPIs:** lead-to-visit, visit-to-booking, booking cancellation, collection vs demand, time-to-registration.

**Scenario / Use case.** Portal shows unit “available.” CRM still “available” after booking because inventory master is a spreadsheet. Two bookings on the same flat. BA: unit status state machine (available → blocked → booked → sold), timeout on block, channel-partner visibility. UAT with sales and a broker.

---

## How these connect to the five companies

ShopEase hires (HR), NovaBank mortgages (real estate + banking), MediCare+ staff roster (HR), QuickBite courier travel time (travel-ish logistics), ShieldSure property insurance (real estate risk). You will cross domains; keep **one home domain** and use this file as a map.

## Notes

- HR: cut-offs, statutory, F&F, employee privacy — payroll errors are Sev1.
- Travel: inventory is perishable; fare rules are the product; PNR is the case ID.
- Government: audit trail and SLA beat “delight”; leakage and inclusion are the problems.
- Real estate: unit inventory status is the OMS equivalent; legal is not a phase-2 extra.
- Terminology first, then one As-Is, then systems, then one scenario — same method as Day 1–30.
- Do not copy e-commerce checkout into these domains.
- Assisted channels (CSC, broker, HRBP) are users, not afterthoughts.
- When domains collide (bank + property + insurance), name the **process owner** per step.
