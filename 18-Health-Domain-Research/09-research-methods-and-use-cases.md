# Research Methods and Use Cases — How Companies Work, How You Study Them

> **Sequence: Phase 3, file 09.** After `08-industry-problems.md`.  
> **Next:** one solution only — start with `10-solution-apexcare-cashless-rcm.md`.  
> Do not skip the mystery-shop (UC-R01) and jump to a full BRD.

This file is **research practice**: how real operating models work, and how a BA learns them from **public** sources without a hospital ID card. Each use case has a method, what you will observe, and the artifact you produce.

Ethics: mystery-shop as a customer. Do not scrape, do not photograph other patients’ faces or tokens, do not ask staff to export HIS data.

---

## How companies actually run (operating models)

### R-OP-01 — Chain hospital: two fronts, one record

**How it works.** Consumer app (Apollo 24/7-style) and on-site HIS. Marketing owns the app; HIM owns UHID. Slots are only true if the **roster in HIS** is published. TPA desk is a physical counter with browser bookmarks to insurer portals. NABH quality team keeps indicators in Excel if HIS reports do not match definitions.

**What to research.** Book (or start to book) a slot on a public site. Note: doctor, unit, prepaid or not, cancellation rule, ABHA prompt. Call the published helpline and ask “cashless planned surgery — what documents?” Compare to an insurer’s cashless FAQ.

**BA artifact.** Context diagram: App / Call centre / HIS / TPA portal / SMS.

### R-OP-02 — Cashless at the TPA desk (every private IPD hospital)

**How it works (As-Is you will hear everywhere).**

1. Admission: file opened; eligibility sometimes *after* OT.  
2. Pre-auth: coordinator uploads discharge-ish documents into **Portal A**.  
3. Query: missing implant invoice / room type / past history.  
4. Enhancement: bill exceeds approved sum.  
5. Discharge: patient sits while “final approval” is awaited.  
6. Settlement: 30–60 days; denials discovered later.

**How leading teams improve (To-Be pattern).** Eligibility at **admission**; planned pack **T–24h**; implant/OT notes in HIS not WhatsApp; patient sees status (SUBMITTED / QUERY / APPROVED / REJECTED); denial reason coded; NHCX when payer is ready.

**Research method.** Insurer help pages (cashless vs reimbursement). Hospital “TPA / insurance desk” page. IRDAI-style claim TAT *as constraint type*. News on claim disputes — for problem statements, not gossip.

**Artifact.** Swimlane: Patient, Ward, TPA desk, Insurer, Billing. Clock: what starts TAT.

### R-OP-03 — Diagnostics hub-and-spoke

**How it works.** Collection centre or home phlebotomy → logistics → hub lab → pathologist sign-out → PDF/app/HIS. Thyrocare-style: extreme centralisation. Dr Lal / Metropolis: many labs + spokes. Aggregator (1mg/PharmEasy) is a **channel**: they take the order, a partner collects.

**TAT fight.** Marketing clock starts at **payment**. Lab clock starts at **sample in lab**. Those two clocks are why “we met TAT” and “you were late” are both true.

**Research method.** Order a (or browse) wellness package: note promised hours, home-slot, cancellation. Read NABL “what accreditation means” at public level. Trade press on aggregator discounts.

**Artifact.** State machine: ORDERED → COLLECTED → IN_TRANSIT → IN_LAB → RESULTED → REPORTED. Define start/stop per state.

### R-OP-04 — ABHA at a high-volume OPD (public evidence)

**How it works.** MoHFW/NHA want ABHA linked. Floor reality (AIIMS Kalyani OPD study, 2024, published): of recorded *hurdles*, **network**, **no smartphone**, and **refusal** dominated. Tokens generated >> linkages completed. Care still happens.

**How serious programmes behave.** Offer ABHA; do not deny care on refusal; capture reason; offline/poor-signal path; don’t add 4 minutes to a 5-minute consult without a clerk role.

**Research method.** Read the published study abstract. Walk an OPD (as visitor): is ABHA a kiosk, a clerk, or a poster?

**Artifact.** BR: care not conditional on ABHA. FR: refusal reason. NFR: kiosk timeout / offline queue.

### R-OP-05 — EMR adoption vs consult time

**How it works.** US literature and Indian HODs agree: unstructured EMR kills throughput. Workarounds: paper then scan, WhatsApp to secretary, notes after 20:00. Claims then lack diagnosis. RCM suffers.

**How companies that get it right behave.** Specialty templates; Must fields only (allergy, diagnosis, orders); voice/scribe; privilege so a junior cannot skip allergy; mobile vitals at bedside.

**Research method.** Watch a public clinic (your own appointment): does the doctor type, dictate, or write? Time it. That is elicitation by observation.

**Artifact.** Must-field list with clinical owner, not 80 optional boxes.

### R-OP-06 — M&A / new hospital copy

**How it works (EY/ICRA context).** Chains add beds and buy hospitals. Day 1 problems: two UHID, two TPA hospital codes, two pharmacy item masters, staff passwords on a WhatsApp list.

**How PMO/BA programmes run.** Playbook: MPI, code-set, tariff, TPA empanelment, NABH document control, cutover weekend, hypercare. Not a new brand app.

**Research method.** Exchange filings: “we acquired X beds.” Assume dual-HIS for 12–24 months unless they say migration complete.

**Artifact.** Cutover checklist + out-of-scope: clinical protocol unification (HOD).

### R-OP-07 — Marketplace vs provider (Practo vs hospital)

**How it works.** Marketplace sells **discovery + booking**. Hospital sells **care**. If the marketplace slot is not the HIS slot, no-show and double-book follow. Cancellation fees and doctor leave are the business rules.

**Research method.** Book and cancel (if free) on a marketplace. Screenshot the rule. Compare to the clinic’s own phone instruction.

**Artifact.** BR table: who may cancel, until when, refund, which system is master.

---

## Research use cases (you perform these)

### UC-R01 — Mystery-shop OPD access (90 minutes)

**Objective.** Write As-Is for appointments without internal access.

**Steps.**

1. Pick a public hospital/clinic site or app.  
2. Attempt book: specialty → doctor → slot. Note errors, prepaid, ABHA, OTP.  
3. Read cancellation/no-show text.  
4. Time: first screen to confirm (or to fail).  
5. If you visit: token vs appointment, wait, billing sequence. No photos of other patients.

**Output.** 8–12 step As-Is; 3 exceptions; 1 KPI you *could* measure (wait, clicks to fail).

**Pass.** You did not propose screens before the process.

### UC-R02 — Reverse-engineer cashless from public docs (2 hours)

**Objective.** Understand payer–provider contract enough to write ApexCare-style FRs.

**Steps.**

1. Open one insurer cashless FAQ (planned vs emergency).  
2. Open one hospital “insurance desk” page.  
3. List documents: ID, policy, pre-auth form, estimates, implant invoices.  
4. Mark which exist only *after* OT (that is the discharge delay).  
5. Draft completeness checklist (planned vs emergency).

**Output.** Checklist + query reasons (missing doc types). Label illustrative.

### UC-R03 — Annual report KPI card (45 minutes)

**Objective.** Talk occupancy and expansion like a BA, not a stock tip.

**Steps.**

1. Download latest investor presentation of one listed chain (Apollo, Fortis, Max, Narayana, Metropolis, Dr Lal).  
2. Extract: beds or centres, occupancy or volume, ARPOB or realisation if given, expansion.  
3. Write 5 questions you would ask ops (payer mix, denial, ALOS, new-unit ramp).

**Output.** One-page card. No financial advice. No fake “I worked on their HIS.”

### UC-R04 — Diagnostics TAT clock debate (60 minutes)

**Objective.** Never write “TAT < 24h” without events.

**Steps.**

1. Browse a lab’s promised TAT on a package.  
2. List candidate events: paid, slot, collected, received-at-hub, analyser, signed, SMS.  
3. Pick start and stop for *patient promise* vs *lab ops*.  
4. Write 3 UAT cases: haemolysed sample, delay in transit, critical value.

**Output.** Clock definition table (HelixLab style).

### UC-R05 — Privacy / family phone (45 minutes)

**Objective.** Turn DPDP + ethics into FRs (CityWell / MediCare+).

**Steps.**

1. Note what SMS/email a health app sends (you as customer).  
2. Classify: reminder (low) vs result (high) vs marketing.  
3. Write consent purposes and a rule: no diagnosis in SMS.  
4. Exception: shared family number — OTP to UHID, not deep link.

**Output.** Consent matrix + 2 UAT scenarios.

### UC-R06 — NABH/NABL as requirement source (45 minutes)

**Objective.** Quality manuals are elicitation, not wallpaper.

**Steps.**

1. Read public NABH/NABL summaries: identification, consent, infection, document control, TAT, critical values.  
2. Convert 5 standards into BRs (“two identifiers before sample”).  
3. Mark which need a system field vs a floor SOP.

**Output.** 5 BRs with “system vs SOP” tag.

### UC-R07 — Stakeholder map from a job description (30 minutes)

**Objective.** Healthcare JDs name systems; use them.

**Steps.**

1. Search BA + HIS / RCM / EMR jobs.  
2. List systems named (HIS brand, SAP, Salesforce, etc.).  
3. Infer stakeholders: HIM, RCM, nursing, TPA.

**Output.** Power/interest grid for a fictional programme using those titles.

---

## How a real BA elicits on the floor (when you do have access)

| Technique | Healthcare version |
|---|---|
| Interview | 25 min with TPA lead: last 10 denials |
| Observation | Stand behind front desk (permission); count duplicate search |
| Document analysis | Package master, TPA SOP, downtime circular |
| Data analysis | Masked HIS: duplicate rate, TAT, no-show |
| Workshop | Roster or pre-auth pack — one decision |
| Prototype | Training tenant, not production PHI |

**Never:** photograph charts, take home a discharge summary, use a live UHID in Figma.

---

## Scenario / Use case: “Research AI for hospitals”

**Context.** You want a trendy case.

**What you do instead.** Research **denial reason codes** or **TAT clocks**. If you still want AI: the real use is coding assistance or slot no-show *prediction* **after** the process exists. UAT must include harm: wrong triage.

**If ignored.** Interviewer hears vapour. Floor staff need eligibility check, not a chatbot.

## Weak vs strong

| Weak | Strong |
|---|---|
| Blog “top 10 HIS” | One mystery-shop + one clock table |
| Copying a hospital logo case | Teaching company + public method |
| Research = ChatGPT glossary | Annual report + observation + FAQ |
| Ignore consent | Family-phone UAT in every patient-channel project |

## Notes

- Companies run **HIS + Excel + portals**. Your research must include the Excel.
- Two clocks (marketing vs ops) explain most TAT fights.
- ABHA refusal is a valid path. Design it.
- Public sources: investor decks, help centres, NHA/ABDM pages, NABH summaries, published operational studies.
- Produce artifacts (As-Is, BR, clock, consent matrix). Notes without IDs are not BA work.
