# Glossary, KPIs, and Regulations Lite

> **Sequence: Phase 1, file 04 of 06.** After `03-health-domain-landscape.md`.  
> **Next:** `05-tools-and-software.md`.

Conversation depth: you can use these in a workshop. You cannot replace a medical superintendent, DPO, or actuary.

**Full study list of short names and expansions:** `02-abbreviations-and-full-names.md`. Use this file for KPIs and constraint types. Use file `02` to memorise HIS = Hospital Information System, HITL = Human-in-the-Loop, and the rest.

---

## Glossary (use in sentences)

| Term | Meaning |
|---|---|
| **Encounter** | One care event (OPD visit, admission day, teleconsult) |
| **UHID / MPI** | Unique hospital ID / master patient index — the person key |
| **ABHA** | Ayushman Bharat Health Account — national health ID (voluntary for care in our BRs) |
| **HPR / HFR** | Registries for professionals and facilities |
| **EMR / EHR** | Clinical record (encounter notes, orders). EHR often means longitudinal / shareable |
| **HIS / HMIS / HMS** | Hospital system: registration, IPD, billing, often EMR modules |
| **CPOE** | Computerised order entry (lab, Rx, radiology) |
| **MAR** | Medication administration record |
| **LIS** | Lab system — sample and result master |
| **Accession** | Lab ID for a sample/order set |
| **RIS / PACS** | Radiology workflow / image archive (DICOM) |
| **ADT / ORM / ORU** | HL7 events: admit-discharge-transfer, order, result |
| **FHIR** | Modern health API standard (ABDM / NHCX) |
| **RCM** | Revenue cycle: eligibility → code → claim → pay |
| **Cashless** | Payer pays hospital; patient pays gap / non-payables |
| **Pre-auth / enhancement** | Approval before / extra amount during stay |
| **TPA** | Third-party administrator (or hospital desk talking to them) |
| **NHCX** | National Health Claims Exchange |
| **PM-JAY** | Public insurance scheme (packages, empanelment) |
| **ARPOB** | Average revenue per occupied bed |
| **Occupancy** | Occupied beds / available beds |
| **ALOS** | Average length of stay |
| **AR days** | How long invoices sit uncollected |
| **Denial / query** | Claim rejected or more docs asked |
| **Package vs item** | Fixed price vs à-la-carte billing |
| **NABH / NABL** | Hospital / lab accreditation |
| **Critical value** | Result that must be called now |
| **TAT** | Turnaround — **useless without clock events** |
| **No-show** | Booked, not arrived (define minutes) |
| **Consent artifact** | Stored permission for a **purpose** |
| **Break-glass** | Emergency access with alarm |
| **Empanelment** | Hospital accepted on a payer network |
| **Non-payables** | Bill lines insurer will not pay (patient gap) |
| **OT freeze** | Theatre list locked |
| **Hub-and-spoke** | Collection centres feed a central lab |
| **DLT SMS** | Registered templates for Indian SMS |
| **PHI / health data** | High-sensitivity personal data |
| **DPDP** | Digital Personal Data Protection Act (India) |
| **Sev1 (health)** | Wrong patient, mix-up, privacy leak, missed critical value |

---

## KPI dictionary (steal the format, not the numbers)

| KPI | Formula idea | Good direction | Trap |
|---|---|---|---|
| Occupancy | Occupied / available | Stable 60–75% typical listed chains | Ignores payer mix |
| ARPOB | IPD revenue / occupied bed-days | Up with acuity mix | Up because of denial write-offs later |
| ALOS | Bed-days / discharges | Specialty-specific | Short ALOS with bounce-back |
| No-show % | No-shows / booked | Down | Without 15-min definition |
| Wait P50 | Check-in → consult start | Down | Walk-in vs booked mixed |
| Duplicate UHID % | Duplicate persons / active | Down | Under-count if never merged |
| Pre-auth TAT | Eligible admit → SUBMITTED | Down | Clock starts too late |
| Discharge financial wait | Clinically fit → financially clear | Down | Fit not timestamped |
| Denial % | Denied / submitted | Down | Uncoded denials |
| AR days insured | Receivables / daily billed | Down | Finance definition |
| Lab TAT met % | Met / accessions | Up | Two clocks |
| Barcode mismatch % | Mismatch / accessions | Down | Reprints hidden |
| Recollection % | Recollect / collections | Down | Some are clinically required |
| Critical ack % | Acked / flagged | 100% | Call not in LIS |
| ABHA offered % | Offered / OPD | 100% | Forced linkage |
| ABHA linked % | Linked / eligible | Honest funnel | Vanity 100% |
| EMR completeness | Encounters with Must fields / total | Up | 40 fields gamed |
| Privacy incidents | Count | 0 | Hidden in IT tickets |

On a real job: 2-week baseline extract, then targets. Label portfolio numbers **illustrative**.

---

## Regulations and standards lite (constraint types)

| Source | What it constrains | BA behaviour |
|---|---|---|
| **DPDP Act** | Purpose, consent, access, retention, breach | Purpose-wise consent; DPO in room |
| **Clinical ethics / council** | Who may see the chart; minors | Not a footer NFR |
| **NABH** | Identification, consent, infection, document control, indicators | Two identifiers; evidence in system |
| **NABL** | Lab quality, TAT, critical values, QC | Clock + call log |
| **Clinical Establishments** (where applicable) | Registration, records | Record retention |
| **Pharmacy / NDPS / schedule H,H1,X** | Who dispenses what | Dual control FRs |
| **PCPNDT** | Sex determination / USG | Hard stops; legal specialist |
| **IRDAI-style health claims** | Conduct, TAT, cashless behaviour | Do not invent coverage |
| **PM-JAY / NHA** | Packages, empanelment, portals | Master data |
| **ABDM** | IDs, FHIR, consent exchange | Voluntary care path |
| **IT Act / cyber** | Security, logs | Audit NFRs |
| **GST** (as applicable) | Invoice | Billing rules with finance |

**BA rule:** Trace FRs to a named constraint or a signed internal BR. Do not quote this file as legal advice.

---

## Tools cheat-sheet (one line each)

See `05-tools-and-software.md` for depth.

- **HIS** — person, visit, bill  
- **EMR** — notes, orders  
- **LIS** — sample  
- **RIS/PACS** — image  
- **RCM/portals/NHCX** — claim  
- **Jira/Confluence/Figma/SQL/Excel** — your artifacts  

---

## Interview answers (30 seconds)

**“How is healthcare different?”**  
Four processes: access, chart, money, privacy. Failure can harm. Identity is safety.

**“HIS vs EMR?”**  
HIS runs the hospital. EMR is the clinical chart. Often modules of one product; still two jobs.

**“What would you do week one at ApexCare?”**  
Measure eligibility timing, discharge hold, top denial reasons from 50 files. No dashboard until clocks exist.

**“ABHA mandatory?”**  
Offer it. Do not deny care. Capture REFUSED/FAILED. Public OPD studies show network and smartphones dominate hurdles.

**“You are a vendor BA — how is that different?”**  
The hospital owns the process. Nimbus is paid for a SOW slice. Extra Gen AI is a change request unless it is signed. HITL and DPDP are in MVP.

**“How would you use Gen AI here?”**  
Draft SOAP with doctor sign-off, or extract cashless fields with coordinator confirm. Not a symptom checker. Not auto-deny. Not public ChatGPT with discharge summaries.

---

## Weak vs strong

| Weak | Strong |
|---|---|
| 200-term unread glossary | 30 terms used in ApexCare/HelixLab/CityWell |
| “HIPAA” in an Indian BRD | DPDP + NABH + named BR |
| KPI without formula | Clock start/stop in the dictionary |
| BA as doctor | HOD owns protocol; BA owns process/data |

## Notes

- Learn terms by writing one FR that uses them.  
- Occupancy and ARPOB are hospital; TAT is diagnostics; combined ratio is insurer — do not mix.  
- Expand every short name from `02-abbreviations-and-full-names.md`. First mention in a BRD: full name (SHORT).  
- Update this file when you mystery-shop (UC-R01–R07 in file `09`).  
- Never put live UHIDs or reports in a portfolio.
