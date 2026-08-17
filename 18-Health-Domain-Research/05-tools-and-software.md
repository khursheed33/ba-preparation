# Tools and Software in Healthcare (and What the BA Uses)

> **Sequence: Phase 1, file 05 of 06.** After `04-glossary-kpis-regulations.md`.  
> **Next:** `06-gen-ai-foundations-for-healthcare-ba.md`. Expansions: file `02`.

A hospital does not run on Jira. It runs on **HIS + LIS + RIS/PACS + billing/RCM**, with SMS, TPA portals, and Excel around the edges. Your job is to know **what each system is master for**, not to implement Oracle Health.

---

## 1. Clinical and hospital systems (floor)

| System | Master for | Typical modules | BA failure if ignored |
|---|---|---|---|
| **HIS / HMIS / HMS** | Registration, UHID, appointments, IPD, billing header | OPD, IPD, OT, stores, billing | You design an app that creates a second patient ID |
| **EMR / EHR** | Encounter notes, orders, allergies, discharge summary | SOAP, CPOE, MAR, e-Rx | Notes in Word; claims have no diagnosis |
| **LIS** | Sample, accession, result, TAT | Phlebotomy, analyser, QC, sign-out | HIS order never becomes a worklist |
| **RIS** | Imaging order, slot, report status | Modality worklist | Patient waits; film is not the report |
| **PACS** | Images (DICOM) | Viewer, archive | Report without image; image without order |
| **OT / anaesthesia** | Theatre list, implant, notes | Checklist, implant log | Cashless missing implant invoice |
| **ICU / device** | Vitals streams | Device interface | Alert fatigue; not a BA “AI” project in week one |
| **Pharmacy / IMS** | Drug stock, batch, expiry | Indent, issue, NDPS | Bill without issue; issue without bill |
| **Blood bank** | Unit, crossmatch | Traceability | Separate regulated system |
| **CSSD / BMW** | Sterile tray, waste | NABH evidence | Audit finding, not a patient app |

**India products you will hear:** Practo Insta, Aarogya and other long-running HMIS, Rely-style HIS, chain-specific builds, government **eHospital / eSushrut**. Global: **Oracle Health (Cerner)**, **Epic** (uncommon as default in mid-size India).

**Rule.** Ask on day one: “What is the UHID system of record?” If two answers, that is the first project.

---

## 2. Revenue, payer, identity, patient channel

| System | Master for | BA notes |
|---|---|---|
| **Billing / RCM inside HIS** | Charge, package, receipt | Package BOM, copay, GST as applicable |
| **TPA / insurer portals** (many) | Pre-auth, query, approval | As-Is is eight logins; To-Be is one desk workflow |
| **NHCX gateway** (direction of industry) | Structured claim exchange | FHIR bundles; eligibility; not a PDF email |
| **PM-JAY / state portals** | Scheme claims | Empanelment IDs, package codes, photos |
| **Finance (SAP, Oracle, Tally)** | GL, AR | HIS billed ≠ cash posted |
| **ABDM** (ABHA, HPR, HFR, PHR, UHI) | National IDs and consent exchange | Optional for care; mandatory if you claim “ABDM live” |
| **CRM / patient app / call centre** | Leads, reminders, tickets | Satellite. Cannot be MPI. |
| **DLT SMS / WhatsApp Business** | Notifications | Consent + template; no diagnosis in SMS |
| **IVR / queue / kiosk** | Token, check-in | Must write back to HIS appointment status |
| **HR / roster / biometric** | Who is on duty | Roster unpublished = fake slots |

---

## 3. Integration standards (conversation depth)

| Standard | Use | What you write in FRs |
|---|---|---|
| **HL7 v2** | ADT, ORM, ORU (admit, order, result) | Event, fields, ACK, retry |
| **FHIR (R4)** | ABDM / NHCX / modern APIs | Resource, consent artifact, not “REST somehow” |
| **DICOM** | Images | Accession links RIS ↔ PACS |
| **ASTM** | Older analysers | Middleware still exists |
| **SNOMED / LOINC / ICD** | Coded clinical / lab / diagnosis | Who codes; when; not BA as coder |
| **NDHM / NRCeS profiles** | India FHIR profiles | Vendor must name version |

You do not design the interface engine. You **contract**: “When HIS order status = COLLECTED, LIS accession exists within 2 minutes or incident.”

---

## 4. Analytics and reporting (what ops actually opens)

| Tool | Who | Typical pack |
|---|---|---|
| HIS MIS / Crystal-style reports | Billing, MS | Occupancy, collection, doctor-wise |
| **Excel** | Everyone | TPA tracker, OT list, duty roster — this *is* the As-Is system |
| **Power BI / Tableau / Metabase** | COO | Occupancy, ARPOB, denial, TAT — after a warehouse exists |
| SQL on replica | Analyst / BA | Validation, duplicate UHID, TAT clock |
| NABH / NABL dashboards | Quality | Indicator definitions must match policy |

BA work: **define the metric** (clock start/stop, inclusion) before the dashboard. A pretty Power BI on a wrong TAT clock is worse than Excel.

---

## 5. What **you** use as a BA (same as other domains, healthcare flavour)

| Work | Tool (typical) | Healthcare twist |
|---|---|---|
| Stories, sprint | **Jira** / Azure DevOps | Clinical Must vs Could; safety bugs Sev1 |
| Specs, decisions | **Confluence** / SharePoint / Word | Versioned BR; DPO sign-off on consent |
| Process | **BPMN** in Draw.io / Visio / Miro | Swimlanes: patient, desk, nurse, TPA, HIS |
| UML / use case | Draw.io, PlantUML | UC must include exception: emergency, refusal, downtime |
| Wireframes | **Figma** / Balsamiq / paper | Front-desk 800 patients/day: three clicks, not a design award |
| Traceability | Excel RTM or Jira links | FR → story → UAT; include BRs |
| Data | Excel, SQL | Never production PHI on a laptop; masked extract |
| Meetings | Teams/Zoom + recording policy | Clinical areas: no camera on patients |
| Prototyping | HIS training tenant | Prefer configure over custom |

---

## 6. Software map for a 400-bed Indian hospital (as-is you will find)

```
[Patient app / Practo / 24/7]     [Call centre]
              \                    /
               → [HIS: UHID, appt, IPD, bill] ← [Roster Excel]
                         |     |
              HL7 ORM    |     | ADT
                         v     v
                   [LIS]     [RIS] → [PACS]
                         |
                    [Pharmacy]
                         |
              [TPA portals × 8] [PM-JAY] [Tally]
                         |
                    [SMS DLT]
```

**To-Be** is rarely “rip HIS.” It is: one MPI, one order ID, one cashless file, SMS consent, NHCX later.

---

## 7. Selecting / changing HIS (BA role)

| Question | Why |
|---|---|
| On-prem vs cloud vs India data centre | DPDP localisation questions for legal |
| ABDM sandbox / NHCX readiness | Strategy, not a checkbox in week 12 |
| TPA/package billing maturity | Indian hospitals live here |
| Analyser and PACS history | Switching LIS is a clinical risk |
| Downtime behaviour | Paper? Read-only? |
| Audit log granularity | Who opened which chart |
| Cost | Licence vs implementation vs interfaces — interfaces win |

BA writes **requirements and cutover**, not the RFP legal terms alone. Bring HIM, nursing, billing, and a doctor who still sees 60 OPD/day.

---

## 8. Security and privacy tools (functional, not optional)

| Control | System behaviour you specify |
|---|---|
| RBAC | Role sees only assigned location + privilege |
| Break-glass | Emergency access with reason + alert |
| Audit | User, UHID, timestamp, action; retained per policy |
| Masking | Results not in SMS body |
| Consent | Purpose-wise: reminder vs report vs research |
| Backup / DR | RPO/RTO named; tested |
| Vendor access | Privileged, time-bound, logged |

Wrong-patient and leaked reports are **Sev1**. Treat like payments in banking.

---

## 9. Services-firm and Gen AI tools (her daily stack)

She will spend more hours in **Jira + Confluence + Teams** than in HIS. HIS is the client’s system of record. Nimbus tools are how the SOW is delivered.

| Tool | Full name / product | What she uses it for |
|---|---|---|
| Jira / ADO | Jira / Azure DevOps | Stories, AC, defects, sprint |
| Confluence / SharePoint | Wiki / document library | BRD, decisions, RTM |
| Figma / Balsamiq | Design / wireframe | Desk screens — three clicks |
| Visio / Draw.io / Miro | Diagramming | As-Is swimlanes for offshore |
| Excel / SQL | Spreadsheet / Structured Query Language | Masked extracts, clocks |
| Teams / Zoom | Meetings | Record only if MSA/DPO allow |
| Azure OpenAI / Bedrock | Enterprise LLM APIs | Client copilots **if SOW**; never public GPT with PHI |
| M365 Copilot | Microsoft 365 Copilot | Internal drafts from **redacted** notes |
| OCR / IDP platform | Optical Character Recognition / Intelligent Document Processing | Cashless pack fields |
| DLP | Data Loss Prevention | Blocks paste of PHI to public AI |

**Architecture sentence she should be able to say:** “The Large Language Model (LLM) drafts; Retrieval-Augmented Generation (RAG) grounds SOP bots; Human-in-the-Loop (HITL) is mandatory; Hospital Information System (HIS) remains the record.”

Detail: `06-gen-ai-foundations-for-healthcare-ba.md` now; full SOW in `13-solution-nimbus-genai-note-copilot.md` after the gate. Expansions: `02-abbreviations-and-full-names.md` section H.

---

## Scenario / Use case: vendor demo day

**Context.** Three HIS vendors demo “AI EMR.”

**What you do.** Script 8 tasks from *this hospital’s* As-Is: register duplicate mobile, package billing with implant exception, cashless query, downtime, ABHA refusal, barcode reprint, doctor leave mid-session, user from Hospital B must not open Hospital A chart. Score the script. Ignore the heat map animation.

**If ignored.** You buy a demo. Floor staff keep Excel.

## Weak vs strong

| Weak | Strong |
|---|---|
| “We need Epic” | Contract the HIS you have; name the API |
| Dashboard first | Clock definition first |
| WhatsApp as LIS | Accession in LIS; WhatsApp is a channel |
| BA learns only Jira | BA can read an HL7 event name and a TAT formula |
| Public ChatGPT + discharge PDF | Approved tenant, HITL, eval, fallback |

## Notes

- Draw the system map before FRs. Master data lives in one box.
- Excel and WhatsApp are in-scope As-Is systems. Write them down.
- HL7/FHIR/DICOM: know the job of each; specialists map fields.
- Your tools (Jira, Confluence, Figma, SQL) produce artifacts. HIS/LIS produce care and cash.
- Gen AI is a layer. It does not replace HIS, LIS, or the doctor’s signature.
- Never put real patient extracts in a portfolio.
