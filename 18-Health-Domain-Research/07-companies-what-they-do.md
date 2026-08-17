# Companies: What They Do, What Breaks, What a BA Would Own

> **Sequence: Phase 2, file 07.** After foundation files `01`–`06`.  
> **Next:** sit the **gate** in `00-how-to-use-this-pack.md`, then `08-industry-problems.md`.  
> This file is an industry map. It is not a BRD. Do not start ApexCare (`10`) from here.

Public facts below are for **research**. Operational pain is the pattern hospitals and health-tech firms talk about in earnings calls, help centres, NABH findings, and news — not a leak of anyone’s internal BRD. Volumes inside solution files remain **illustrative**.

Do not write “I implemented this at Apollo.” Write “I researched Apollo’s public patient journey and built an ApexCare-style cashless case.”

---

## How to read a healthcare company (BA method)

For any firm, fill this card in 20 minutes from annual report + app + help centre:

| Field | Question |
|---|---|
| Customer | Patient, doctor, hospital, insurer, government? |
| Unit of value | Bed-day, consult, test, Rx, premium, lead? |
| System of record | HIS, LIS, app, policy admin? |
| Constraint | NABH, NABL, IRDAI, ABDM, DPDP, price cap? |
| Public KPI | Occupancy, ARPOB, test volume, combined ratio, GMV? |
| Recurring fight | Cashless, TAT, discount, talent, integration? |

---

## A. Hospital chains

### Apollo Hospitals Enterprise

**What they do.** India’s largest listed private hospital platform: tertiary hospitals, clinics, diagnostics, Apollo Pharmacy, and the **Apollo 24/7** digital layer (consult, delivery, records). Growth in FY26 was still hospital-led (EY: ~16% revenue growth cited for Apollo and Max). They add beds while trying to hold occupancy (public commentary around high-60s%).

**What they actually run.** A **group HIS/EMR** plus pharmacy retail plus a consumer app that is *not* the ward system of record. International patients, oncology/cardiac mix, and insurance mix all hit the same TPA desk.

**Problems a BA would hear (pattern, not insider data).**

- App and hospital slot calendars drift (leave, OT list, walk-ins).
- Cashless discharge wait vs patient NPS.
- New hospital ramp-up: occupancy vs pre-opening cost (EY: new units dilute margin).
- Pharmacy vs hospital billing of the same drug.
- ABHA / record share vs existing UHID.

**BA-shaped work.** Slot contract between 24/7 and HIS; cashless pack from EMR; MPI across hospitals; downtime SOP; consent for results.

### Fortis Healthcare

**What they do.** Multi-city tertiary chain (also historically linked to **SRL** diagnostics). Growth via existing hospitals plus acquisitions / O&M (public: People Tree, Gleneagles-style deals). Occupancy in the high-60s% in FY26 commentary.

**Problems.** Integration after acquisition: two HIS, two UHID schemes, two TPA codes. Diagnostic–hospital order loop. Medical tourism mix shifting (Bangladesh vs Africa/CIS in public medical-travel reporting).

**BA-shaped work.** Master-data merge, empanelment codes, “one patient across sites,” claim identity.

### Max Healthcare

**What they do.** North/west India cluster strategy, high occupancy (public ~76% in FY26 commentary — among the tightest of the large chains). Expansion into new cities (Lucknow, Pune, Dwarka, etc.).

**Problems.** High occupancy means **bed turnaround** and OT start-time become the constraint, not “marketing.” Insurance mix still drives AR days. New units need the same playbook (roster, TPA, MPI) on day one.

**BA-shaped work.** Discharge-before-noon process, bed board, OT utilisation, not another brochure app.

### Narayana Health (Narayana Hrudayalaya)

**What they do.** High-volume cardiac and multi-specialty, known for **cost-efficient clinical pathways**. Public: UK acquisition (Practice Plus Group) — overseas ops is a different regulatory grain.

**Problems.** Volume pathways vs local HIS; package pricing vs extras; international vs India consent/privacy.

**BA-shaped work.** Package billing rules, clinical pathway checklists as *orders*, not as a BA-invented protocol.

### Medanta (Global Health), Manipal, Aster / Quality Care, KIMS, HCG, Rainbow, Shalby, Cloudnine

| Company | Do | Typical BA problem |
|---|---|---|
| Medanta | Super-tertiary, new city expansion | New-site HIS clone vs local TPA list |
| Manipal | Large private university-hospital network | Multi-HIS heritage; student vs patient identity |
| Aster + Quality Care | Merger scale (beds second only to Apollo-class) | Post-merger process and code-set alignment |
| KIMS | South India expansion | New-hospital margin dilution; standard operating HIS |
| HCG | Oncology network | Chemo chair scheduling, protocol orders, high-value claims |
| Rainbow | Women & children | Paediatric consent, vaccination, high OPD grain |
| Shalby | Ortho / joints | Implant billing, package vs consumable leakage |
| Cloudnine | Maternity | Delivery package, newborn UHID, PCPNDT constraints on USG |

---

## B. Diagnostics chains

### Dr Lal PathLabs

**What they do.** National B2C + B2B diagnostics: labs, collection centres, home collection, specialty tests. Scale is the moat; **hub-and-spoke** is the operating model.

**Problems (public + industry pattern).** Employee cost and new-centre ramp hit margins; aggregator discounts on routine tests (CBC, thyroid, lipid); quality incident is existential; home-collection no-show; sample logistics.

**BA-shaped work.** Accession barcode, TAT clock definition, recollection workflow, aggregator order SLA vs quality.

### Metropolis Healthcare

**What they do.** Premium positioning, large test menu (including specialty/genomics), India + Africa footprint, service centres + labs. FY26 commentary: volume + mix + utilisation, not list-price hikes.

**Problems.** Acquisition integration of small labs; pathologist sign-out queue; B2B hospital LIS vs own LIS.

**BA-shaped work.** Result delivery to referring doctor, critical-value call, NABL evidence in LIS.

### Thyrocare

**What they do.** High-volume **wellness / preventive** and B2B (aggregators, camps). Cost leadership via centralised processing.

**Problems.** Commodity test price war; logistics of overnight samples; brand vs aggregator white-label.

**BA-shaped work.** Camp vs individual order, barcode at camp, B2B invoice vs patient report branding.

### Vijaya, Neuberg, Krsnaa, SRL

| Company | Do | BA angle |
|---|---|---|
| Vijaya Diagnostic | South retail + imaging | RIS/PACS + LIS in one visit |
| Neuberg | Specialty + PE-backed consolidation | Multi-brand LIS merge |
| Krsnaa | PPP / government contracts | Tender SLA, government payment delay, volume reporting |
| SRL | Hospital-attached + retail | Order from Fortis-like HIS into LIS |

**Industry pressure (CareEdge / trade press):** routine tests commoditised; aggregators discount heavily; reagents imported; NABL cost is real. BA work is **operational efficiency and quality**, not a prettier report PDF.

---

## C. Payers (insurance, TPA, schemes)

### Star Health, Niva Bupa, Care Health, bank-attached GI (HDFC Ergo, ICICI Lombard)

**What they do.** Underwrite health policies; run cashless networks; adjudicate claims (in-house or TPA). Combined ratio and claim TAT are the business.

**Problems.** Hospital says “delay”; insurer says “incomplete pack / medical necessity.” Pre-existing, waiting period, room-rent capping, non-payables at discharge. Fraud vs genuine enhancement. NHCX is the industry direction: structured FHIR claims instead of PDF + portal.

**BA-shaped work.** Pre-auth data contract (what the hospital must send); query codes; customer status; not “AI that denies claims.”

### TPAs (medi-assist-style, in-house TPA desks)

**What they do.** Sit between hospital and insurer for cashless. Hospital TPA desk is a **hospital team** using **payer portals**.

**Problems.** Eight logins; eligibility not checked at admission; discharge summary not coded; patient waits in lobby.

**BA-shaped work.** After the gate: `10-solution-apexcare-cashless-rcm.md`.

### PM-JAY / state schemes / NHA

**What they do.** Public packages, empanelment, claim portals, audits.

**Problems.** Photo/ID, package mapping, query, rejection, delayed payment. Empanelment is a master-data project.

---

## D. Digital health and pharmacy

### Practo

**What they do.** Doctor marketplace + clinic SaaS + **Insta** HIS/HMS for hospitals/clinics (OPD, IPD, EMR, lab, pharmacy, billing). Two products: consumer marketplace and provider system of record.

**Problems.** Marketplace supply (doctor slots that are real); clinic HIS adoption; ABDM; competing with entrenched on-prem HIS.

**BA-shaped work.** Slot truth; cancellation policy; clinic vs hospital module scope.

### Apollo 24/7, Tata 1mg, PharmEasy, MediBuddy, MFine-style telehealth

| Company | Do | Recurring problem |
|---|---|---|
| Apollo 24/7 | Consult + pharmacy + diagnostics on Apollo brand | Sync with hospital HIS; Rx fulfilment |
| Tata 1mg | Pharmacy + diagnostics aggregator + content | Discount vs partner lab quality; order-to-sample |
| PharmEasy | Pharmacy + diagnostics + care | Unit economics; partner TAT; returns of medicines |
| MediBuddy | Corporate health + cashless-ish OPD | Eligibility file, empaneled clinics |
| Telehealth apps | Video consult | Prescription legality, follow-up, emergency redirect |

**BA-shaped work.** Order state machine (placed → collected → resulted); partner SLA; who owns clinical liability; DPDP on reports.

### Apollo Pharmacy / MedPlus

**What they do.** Retail pharmacy at scale. Hospital-adjacent stores share patients with IPD billing.

**Problems.** Substitution, schedule-H/H1/X controls, expiry, bill matching discharge meds.

---

## E. HIS / EMR / imaging vendors (who the BA sits with)

| Vendor / product | Where you see it | BA note |
|---|---|---|
| Practo Insta | Indian hospitals/clinics | Full HMS; HL7/API story |
| Aarogya HMIS and similar long-running Indian HMIS | Mid hospitals | Deep local billing/TPA habits |
| eHospital / eSushrut / CDAC (public) | Government | Procurement + ABDM + volume |
| Oracle Health (Cerner), Epic | Large / international / rare India flagship | Long implementation; not a 12-week app |
| PACS (GE, Philips, Fujifilm, Agfa…) | Radiology | DICOM; RIS is the workflow |
| Analyser middleware (HL7/ASTM) | Labs | Roche, Abbott, Mindray, Sysmex worklists |
| Tally / SAP / Oracle Finance | Finance | HIS bill vs GL — leakage lives here |
| WhatsApp / DLT SMS | Everyone | Consent + template; not the EMR |

Large Indian chains often run a **core HIS** (sometimes aged) plus **best-of-breed** LIS/PACS plus a **consumer app**. The BA’s first diagram is that map.

---

## F. What “problems they are facing” looks like in 2026 (cross-cutting)

From public industry sources (ICRA, EY-Parthenon, ABDM implementation papers, diagnostics trade press):

1. **Capacity vs execution.** Beds are being added; new units dilute margin until occupancy ramps.
2. **Insurance mix.** Occupancy can be healthy while cash is stuck in claims (AR days).
3. **Digital stack friction.** ABHA linkage fails on network, smartphones, and refusal — not only APIs (AIIMS Kalyani OPD study).
4. **Legacy HIS.** Mid-size ABDM integration quoted in research around ₹30–50 lakh plus workflow burden on a 2–5 minute consult.
5. **Diagnostics price war.** Aggregator discounts on routine tests vs NABL cost.
6. **Talent.** Nurses, technicians, coders — not “we need more dashboards.”
7. **Cyber + DPDP.** Health data is high-sensitivity; breach is a board event.
8. **M&A.** Two hospitals, two UHID, two TPA IDs — classic BA master-data programme.

---

## Scenario / Use case: researching Fortis without working there

**Context.** Interview: “Tell me a hospital problem.”

**What you do.** Read the latest annual report (beds, occupancy, payer mix if disclosed). Book a mock OPD slot on the public site. Time the cashless FAQ on the insurer site. Write As-Is: registration → consult → bill. Pick **one** gap (e.g. no eligibility check). Put it in ApexCare clothing.

**If ignored.** You say “they need AI.” The interviewer asks how pre-auth works. You cannot answer.

## Weak vs strong

| Weak | Strong |
|---|---|
| List of logos | Each logo → unit of work → system of record → one KPI |
| “Practo is a hospital” | Practo is marketplace + HIS vendor |
| Mixing Star Health with Apollo | One pays, one delivers care |
| Fake tenure | “Public journey + practice case” |

## Notes

- Hospitals sell care; insurers sell risk transfer; diagnostics sell information; marketplaces sell access. Different BRDs.
- M&A and new-bed ramp are process-copy problems. The BA copies the playbook, then localises TPA and roster.
- Consumer apps are satellites. HIS/LIS remains the record.
- Use this file to pick a firm type before you write FRs. Then open the matching solution file.
