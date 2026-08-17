# HelixLab Diagnostics — Missed TAT, Barcode Errors, Home-Collection No-Shows

> **Sequence: Phase 4, file 11.** After file `10` (or after `09` if she chose diagnostics first — still after the gate).  
> Grain is **sample**, not bed-day. Terms: file `02` section B.

**Domain:** Diagnostics. **Company:** HelixLab Diagnostics (illustrative regional chain). **Role:** BA, LIS / Operations. **Grain:** Sample / accession (not bed-day).

HelixLab: 1 hub (Pune), 4 satellite labs, 85 collection centres, 40 home phlebotomists. Mix: walk-in, B2B hospital, aggregator (1mg-style) at steep discount on routine tests. LIS is 7 years old; home app is a vendor; Excel is the TAT “dashboard.” NABL on hub; satellites uneven.

## Business problem

**22%** of accessions miss the **committed TAT** the patient/aggregator was promised (illustrative). Marketing clock starts at **payment**; lab clock starts at **sample in hub**. Arguments every evening. **Barcode mismatch / reprint chaos 3.4%**. Recollection 2.1%. Home-collection **no-show 18%** (phlebotomist travel wasted). Critical values sometimes called on personal mobile with no LIS ack. Aggregator penalties eat thin margin. Doctors say “report not received” while PDF sits in a failed SMS.

Management asked for “live GPS tracking and AI to predict delayed samples.”

## Business objective

14 weeks + 4-week adopt, hub + 20 centres first:

1. **TAT met ≥ 92%** against a **single published clock** (see dictionary).  
2. Barcode mismatch **≤ 0.5%**; every reprint **voids** old ID.  
3. Home no-show **≤ 10%** (reminder + slot + fee rule).  
4. **100%** critical values: LIS task + recorded outcome (reached / not reached).  
5. Report delivery failure **visible** (SMS/email/HIS ACK) — no silent PDF.

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| COO / lab director | H | H | Sponsor | Clock workshop (must decide) |
| Pathologists | H | M | Sign-out queue fear | Queue KPI separate from logistics TAT |
| Hub accession / technicians | M | H | Reprint habit | Floor SOP + system block |
| Collection centre leads | M | H | Blamed for hub delay | Spoke TAT vs hub TAT split |
| Home-collection lead | M | H | Overbook to cope | Slot capacity |
| Aggregator manager | M | H | Penalty SLA | Contract clock = our clock |
| Referring doctors / hospitals | L | H | Missing reports | Delivery ACK |
| Patients | L | H | Wait + wrong report fear | Two identifiers |
| LIS vendor | M | M | Analyser middleware | Worklist contract |
| Quality / NABL | H | H | Evidence | Indicators = system fields |
| DPO | H | M | Results on SMS | OTP / app for reports |

## Scope

**In:** TAT clock definition in LIS, barcode lifecycle (print, void, reprint), sample states, home slot + reminder + no-show, critical-value workflow, delivery ACK (SMS/app/HIS), centre vs hub split reports, two-identifier collection.

**Out:** New LIS rip-and-replace, genomics platform, aggregator app rewrite, pricing engine, AI delay prediction (Phase 2 after clocks), radiology RIS (different grain), home-collection for paediatric neonates (later).

## Assumptions and constraints

**Assumptions:** Analysers already send some HL7; DLT SMS exists; home app can consume slot API or we replace Excel roster.  
**Constraints:** NABL quality control not weakened; 14-week MVP; DPDP — no diagnosis/result values in SMS body; two patient identifiers at collection (NABH-style).

## As-Is process (diagram described)

1. Order: centre / app / aggregator; barcode sticker printed, often **reprinted** if wrinkled.  
2. Collect: name-only if barcode fails; **wait**.  
3. Logistics: bag to hub; no scan at pickup sometimes.  
4. Hub receive: clock starts *here* internally; patient thinks clock started at pay.  
5. Analyser: some results typed; mismatch when reprint IDs collide.  
6. Sign-out: queue at 21:00.  
7. PDF WhatsApp to centre; SMS “report ready” with **link**.  
8. Home: verbal slot; 18% door locked.

**Problem analysis:** Three problems glued: **undefined clock**, **ID discipline**, **home access**. GPS on a sample with two barcodes makes it worse.

**Root cause (clock):** Missed TAT because two clocks. Two clocks because marketing sold “6 hours from booking” while ops needed “6 hours from in-lab.” Never written as a BR.

## To-Be process (diagram described)

1. Order creates **accession**; barcode printed once; reprint = void + new ID + reason.  
2. Collection: two identifiers (name+UHID/mobile+DOB as policy); scan on collect.  
3. States: ORDERED → COLLECTED → IN_TRANSIT → RECEIVED_LAB → IN_PROCESS → RESULTED → APPROVED → REPORTED.  
4. **Patient TAT** start/stop published on invoice. **Ops TAT** start RECEIVED_LAB. Both stored.  
5. Home: slot, SMS reminder T–2h, 15-min wait then NO_SHOW, capacity on roster.  
6. Critical: LIS alert; call logged; ACK by pathologist/tech.  
7. Report: app/HIS/OTP; SMS is “ready” only.  
8. Daily: % met by clock type, mismatch, no-show, critical ack.

## Gap analysis

| ID | Type | Gap | Action |
|---|---|---|---|
| G-01 | Policy | Two unspoken clocks | Dictionary + invoice text |
| G-02 | Tech | Reprint duplicates IDs | Void workflow |
| G-03 | Process | No scan at collect | Mandatory scan FR |
| G-04 | Data | Silent SMS fail | Delivery log |
| G-05 | People | Home verbal slots | Roster + no-show BR |
| G-06 | Process | Critical on personal phone | LIS task |
| G-07 | Tech | Analyser not always worklist | HL7 ORU contract |
| G-08 | Policy | Result in SMS link | Consent + OTP |

## Requirements

| ID | Type | Statement |
|---|---|---|
| FR-LAB-01 | F | Every order has one accession ID; labels print from LIS only. |
| FR-LAB-02 | F | Reprint voids previous barcode; both IDs stored; reason mandatory. |
| FR-LAB-03 | F | Collection cannot complete without scan of current barcode + two identifiers. |
| FR-LAB-04 | F | System records state timestamps for the eight states listed in To-Be. |
| FR-LAB-05 | F | Patient-promise TAT and ops TAT calculated from configured events; both reported. |
| FR-LAB-06 | F | Home slot booking; reminder; NO_SHOW after 15 min at geofence or marked arrived. |
| FR-LAB-07 | F | Critical flag creates task; cannot APPROVE without call outcome. |
| FR-LAB-08 | F | Report REPORTED only if at least one delivery channel ACK or explicit fail + retry task. |
| FR-LAB-09 | F | Aggregator orders use the same accession and clock; channel = AGG. |
| NFR-LAB-01 | NF | Scan-to-state ≤ 3s; LIS 99.5% 06:00–23:00. |
| NFR-LAB-02 | NF | Audit barcode void and critical call. |
| NFR-LAB-03 | NF | SMS/WhatsApp body has no numeric results. |
| TR-LAB-01 | T | Downtime: paper accession book with pre-printed range; catch-up scan. |

## Business rules

- **BR-LAB-01:** Two identifiers before needle (or equivalent collection).  
- **BR-LAB-02:** Haemolysed / insufficient: recollection order linked; original TAT clock **stops** with reason; new clock on new accession.  
- **BR-LAB-03:** Patient-promise TAT start = COLLECTED (not payment). Invoice and aggregator contract must say this — commercial change owned by COO.  
- **BR-LAB-04:** Home NO_SHOW after 15 minutes; slot released; fee per published policy.  
- **BR-LAB-05:** Critical values: attempt call within 30 minutes of flag; outcomes controlled list.  
- **BR-LAB-06:** No result values in SMS.  
- **BR-LAB-07:** Capacity: home roster published day-before or slots freeze.

**Decision log:** Marketing wanted start-at-payment. COO chose **COLLECTED** so ops can meet the promise. Aggregator renegotiation is a dependency, not a silent FR.

## User stories (with AC)

1. **As a phlebotomist, I want reprint to void the old barcode** so two IDs do not exist. **AC:** Old scan rejected.  
2. **As hub accession, I want RECEIVED_LAB timestamp** so ops TAT is honest. **AC:** Report splits centre vs hub.  
3. **As a patient, I want a home slot reminder** so I am present. **AC:** T–2h SMS; reschedule link until T–1h.  
4. **As pathologist, I want critical call logged** so NABL evidence is not a register. **AC:** APPROVE blocked without outcome.  
5. **As COO, I want one TAT definition** on the invoice. **AC:** Help text matches BR-LAB-03.  
6. **As quality, I want delivery failures queued** so “doctor didn’t get it” is a ticket. **AC:** Fail → retry task.

## Use case (fully dressed): UC-LAB-01 Collect and accession walk-in

- **Actor:** Centre phlebotomist. **Pre:** Paid/order exists; barcode printed.  
- **Trigger:** Patient at chair.  
- **Main:** Verify two IDs → scan → COLLECTED → bag scan IN_TRANSIT (optional at centre) → hub RECEIVED_LAB.  
- **Alt:** Barcode unreadable → void reprint flow FR-LAB-02.  
- **Exception:** Patient mismatch → do not collect; supervisor.  
- **Post:** Sample in chain of custody; clocks started per BR.

## Wireframes

1. Order + clock text. 2. Collect scan + two IDs. 3. Void/reprint. 4. Hub receive. 5. Critical call form. 6. Home slot calendar. 7. TAT dashboard (two clocks until cutover, then one patient clock). 8. Delivery fail queue.

## Data, reports, KPIs

**Entities:** Order, Accession, BarcodeEvent, SampleState, HomeSlot, CriticalCall, DeliveryAttempt, Channel (WALKIN/HOME/B2B/AGG), QcFlag.

**Reports:** % TAT met (patient clock, ops clock); mismatch; recollection; home no-show; critical 30-min; delivery fail; aggregator vs walk-in.

**KPIs:** Objectives above. Volume illustrative: ~4,000 accessions/day hub.

## UAT scenarios

- Reprint: old barcode rejected.  
- Collect without second identifier blocked.  
- Haemolysis: clock stop + new accession.  
- Home no-show 15 min.  
- Consent false: no SMS; app still REPORTED if opened.  
- Critical APPROVE blocked without call.  
- SMS contains a number like “Hb 6.2” — **fail UAT**.  
- Aggregator order same states.  
- Downtime paper range no collision.

## RTM

| Req | Story | UC | UAT |
|---|---|---|---|
| FR-LAB-02 | US1 | UC-LAB-01 alt | Reprint |
| FR-LAB-03 | — | UC-LAB-01 | Two IDs |
| FR-LAB-05 | US5 | — | Invoice clock |
| FR-LAB-06 | US3 | — | Home no-show |
| FR-LAB-07 | US4 | — | Critical |
| FR-LAB-08 | US6 | — | Delivery fail |
| NFR-LAB-03 | — | — | SMS content |
| BR-LAB-02 | — | — | Haemolysis |

## Change request (sample)

**CR-LAB-01:** GPS live map for every bag. Impact: cost, privacy of staff location. **Decision:** Phase 2; scan events are Must. GPS only for exception after 60 min IN_TRANSIT.

## Risks and dependencies

| Risk | P/I | Mitigation | Owner |
|---|---|---|---|
| Aggregator refuses new clock | H/H | COO commercial; until then dual report | COO |
| Staff reprint off-system | H/H | No blank labels in drawer; audit | Quality |
| Analyser HL7 gaps | M/H | Vendor milestone; manual with flag | IT |
| Home roster not published | M/H | Freeze slots | Home lead |
| Result leak via WhatsApp PDF | H/H | Centre policy + DPO | DPO |

**Dependencies:** LIS barcode, SMS, home app, analyser middleware, aggregator contract, NABL SOP update.

## Final business solution

**Define the TAT clock in writing and in LIS**, enforce **one live barcode**, split logistics vs sign-out, run home collection like OPD slots, and make critical calls and report delivery **auditable**. Do not buy AI delay models on a double clock. Align aggregator SLA with COLLECTED start or stop selling that SLA.

**Phasing.** W1 clock workshop + baseline extract. W2–5 barcode + states. W6–8 home slots. W9–11 critical + delivery. W12–14 UAT and remaining centres.

## Weak vs strong

| Weak | Strong |
|---|---|
| “TAT < 24h” | Start COLLECTED, stop REPORTED, haemolysis rule |
| GPS first | Scan + void |
| Result in SMS | “Ready” + OTP |
| Blame courier only | Split spoke vs hub vs sign-out |

## Notes

- Matches Dr Lal / Metropolis / Thyrocare operating grain; HelixLab is teaching.  
- Two-identifier rule is safety.  
- Commercial clock change is a COO decision recorded in BR-LAB-03.  
- Illustrative volumes only.
