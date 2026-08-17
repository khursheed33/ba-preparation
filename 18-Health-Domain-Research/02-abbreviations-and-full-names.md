# Abbreviations, Short Names, and Full Names (Health Domain)

> **Sequence: Phase 1, file 02 of 06.** After `01-ba-in-service-organization.md`.  
> **Next:** `03-health-domain-landscape.md`. Return here 10 minutes every study day. Do not skip to problems (`08`) until drill L is passable.

This file is **healthcare / hospital / payer language**. It is **not** the BA dictionary.

**BA and delivery shorts** (Business Requirements Document (BRD), Functional Requirements Document (FRD), Software Requirements Specification (SRS), Statement of Work (SOW), Requirements Traceability Matrix (RTM), User Acceptance Testing (UAT), Responsible-Accountable-Consulted-Informed (RACI), Change Request (CR) as *scope change*) live in [01-BA-Role-Business-Fundamentals/00-ba-and-business-abbreviations.md](../01-BA-Role-Business-Fundamentals/00-ba-and-business-abbreviations.md). Learn that file **first**.

Memorise **short → full name → one-line meaning**. In a client call, say the full name once, then the short name.

This file is the **clinical/systems study dictionary**. KPIs and regulations stay in `04-glossary-kpis-regulations.md`.

**How to study:** cover the Short column, say the full name aloud, then the meaning. Do one section per day.

---

## How to read a row

| Column | Use |
|---|---|
| Short | What you will hear on a call / in Jira |
| Full name | What you write in a BRD the first time |
| Meaning | Enough to ask a sharp question |

First mention in a document: `Hospital Information System (HIS)`. After that: HIS.

---

## A. Hospital and clinical

| Short | Full name | Meaning |
|---|---|---|
| OPD | Out-Patient Department | Visit without overnight stay |
| IPD | In-Patient Department | Admitted; occupies a bed |
| ER / ED | Emergency Room / Emergency Department | Unscheduled acute care |
| ICU | Intensive Care Unit | High-acuity monitored beds |
| NICU | Neonatal Intensive Care Unit | Newborn intensive care |
| PICU | Paediatric Intensive Care Unit | Child intensive care |
| OT / OR | Operation Theatre / Operating Room | Surgery room (India usually OT) |
| CSSD | Central Sterile Supply Department | Sterilises instruments and trays |
| BMW | Bio-Medical Waste | Segregation and disposal of clinical waste |
| HOD | Head of Department | Clinical owner of a specialty |
| MS | Medical Superintendent | Senior clinical admin of the hospital |
| CMO | Chief Medical Officer | Clinical leadership (title varies) |
| CNO | Chief Nursing Officer | Nursing leadership |
| GP | General Practitioner | Primary-care doctor |
| MBBS | Bachelor of Medicine, Bachelor of Surgery | Basic medical degree (India) |
| MD / MS (degree) | Doctor of Medicine / Master of Surgery | Postgraduate clinical degrees — not Medical Superintendent |
| SOAP | Subjective, Objective, Assessment, Plan | Note structure in EMR |
| Hx / PMH | History / Past Medical History | What happened before this visit |
| Dx | Diagnosis | Named condition (coded when billed) |
| Rx / e-Rx | Prescription / Electronic prescription | Medicine order |
| CPOE | Computerized Physician (or Provider) Order Entry | Orders in the system, not on paper |
| MAR | Medication Administration Record | Nurse records that the dose was given |
| IV | Intravenous | Into the vein |
| NPO | Nil Per Os (nothing by mouth) | Fasting instruction |
| A&E | Accident and Emergency | UK-style name for ER |
| IP / OP | In-patient / Out-patient | Same as IPD / OPD |
| Day-care | Day-care / ambulatory surgery | Procedure, go home same day |
| UHID | Unique Health Identifier (hospital) | That hospital’s patient number |
| MRN | Medical Record Number | Same idea as UHID in many countries |
| MPI | Master Patient Index | Rules that keep one person = one ID |
| EMR | Electronic Medical Record | Chart for this facility |
| EHR | Electronic Health Record | Chart intended to follow the person |
| PHR | Personal Health Record | Record the patient controls (ABDM PHR apps) |
| CDSS | Clinical Decision Support System | Alerts/suggestions in the chart (not automatic treatment) |
| ICD | International Classification of Diseases | Diagnosis codes (ICD-10 / ICD-11) |
| CPT | Current Procedural Terminology | US procedure codes (you will hear it on US accounts) |
| SNOMED CT | Systematized Nomenclature of Medicine — Clinical Terms | Rich clinical vocabulary |
| LOINC | Logical Observation Identifiers Names and Codes | Lab/observation codes |
| ATC | Anatomical Therapeutic Chemical | Drug classification |
| NDC | National Drug Code | US drug identifier |
| Generic vs brand | Generic name vs brand name | Chemical vs marketed name of a drug |
| Allergy / ADR | Allergy / Adverse Drug Reaction | Must-capture clinical risk |
| Vitals | Vital signs | BP, pulse, temp, SpO2, etc. |
| BP | Blood Pressure | mmHg |
| SpO2 | Peripheral oxygen saturation | Pulse oximeter reading |
| BMI | Body Mass Index | Weight/height index |
| ALOS | Average Length of Stay | How many days a typical admission lasts |
| DAMA / LAMA | Discharged / Left Against Medical Advice | Patient leaves against advice |
| MLC | Medico-Legal Case | Police/legal documentation path |
| Death summary | Death summary | Legal clinical document after death |
| DS | Discharge Summary | Clinical + instructions at discharge |
| OT freeze | Operation Theatre freeze | List locked; changes need exception |
| Privilege | Clinical privilege | What this doctor is allowed to do |

**Do not confuse:** MS (Medical Superintendent) vs MS (Master of Surgery). EMR (chart) vs HIS (hospital operations + often billing). UHID (hospital) vs ABHA (national).

---

## B. Diagnostics, imaging, pharmacy

| Short | Full name | Meaning |
|---|---|---|
| Dx (lab sense) | Diagnostics | Tests that produce results |
| LIS | Laboratory Information System | Sample, accession, result master |
| Accession | Accession number | Lab ID for that sample/order |
| TAT | Turnaround Time | Time between two defined events |
| QC | Quality Control | Checks that the analyser/process is valid |
| QA | Quality Assurance | Broader quality system (also software QA) |
| NABL | National Accreditation Board for Testing and Calibration Laboratories | Lab accreditation (India) |
| CAP | College of American Pathologists | Global lab proficiency/accreditation you will hear |
| CBC | Complete Blood Count | Common blood test |
| LFT | Liver Function Test | Panel of liver-related tests |
| RFT / KFT | Renal / Kidney Function Test | Kidney panel |
| TFT | Thyroid Function Test | TSH and related |
| HbA1c | Glycated haemoglobin | Diabetes control test |
| RT-PCR | Reverse Transcription Polymerase Chain Reaction | Molecular test method |
| POCT | Point of Care Testing | Test at bedside/clinic, not hub lab |
| RIS | Radiology Information System | Imaging orders, slots, report status |
| PACS | Picture Archiving and Communication System | Stores and shows images |
| DICOM | Digital Imaging and Communications in Medicine | Image file/network standard |
| Modality | Imaging modality | X-ray, USG, CT, MRI, etc. |
| USG / US | Ultrasonography / Ultrasound | Sound-wave imaging |
| CT | Computed Tomography | Cross-sectional X-ray imaging |
| MRI | Magnetic Resonance Imaging | Magnetic imaging, no ionizing X-ray |
| PET | Positron Emission Tomography | Nuclear imaging, often oncology |
| CR / DR | Computed / Digital Radiography | Digital X-ray capture |
| HL7 ORU | Observation Result (HL7 message) | Result message from analyser/LIS |
| ASTM | American Society for Testing and Materials | Older analyser interface style |
| Critical value | Critical / panic value | Result that must be called immediately |
| Recollection | Recollection | Draw the sample again |
| Hub-and-spoke | Hub-and-spoke | Centres collect; hub processes |
| B2B / B2C | Business-to-Business / Business-to-Consumer | Hospital contracts vs walk-in patients |
| IMS | Inventory Management System | Stock (pharmacy/stores) |
| SKU | Stock Keeping Unit | One sellable item identity |
| NDPS | Narcotic Drugs and Psychotropic Substances (Act) | Controlled drugs — dual control |
| Schedule H / H1 / X | Drug schedules (India) | Who may sell/prescribe which drugs |
| Batch / expiry | Batch number / expiry date | Traceability for recall |
| Indent | Indent | Ward request for stock |
| Formulary | Drug formulary | Approved drug list for the hospital |

**Do not confuse:** NABL (lab) vs NABH (hospital). RIS (workflow) vs PACS (images). TAT without clock events is not a KPI.

---

## C. India digital health, public schemes, identity

| Short | Full name | Meaning |
|---|---|---|
| ABDM | Ayushman Bharat Digital Mission | India’s national digital health stack |
| ABHA | Ayushman Bharat Health Account | 14-digit citizen health ID |
| NHA | National Health Authority | Runs PM-JAY and much of ABDM |
| MoHFW | Ministry of Health and Family Welfare | Union health ministry |
| HPR | Healthcare Professionals Registry | Doctor/nurse registry in ABDM |
| HFR | Health Facility Registry | Hospital/clinic registry in ABDM |
| HIE-CM | Health Information Exchange — Consent Manager | Consent-based record share |
| UHI | Unified Health Interface | Open protocol for digital health services (booking etc.) |
| PHR (ABDM) | Personal Health Record | Patient-controlled record apps |
| NRCeS | National Resource Centre for EHR Standards | India FHIR/EHR profiles |
| FHIR | Fast Healthcare Interoperability Resources | Modern health API standard |
| Sandbox | ABDM sandbox | Test environment before production |
| PM-JAY | Pradhan Mantri Jan Arogya Yojana | Public hospital insurance scheme |
| AB-PMJAY | Ayushman Bharat PM-JAY | Same scheme, full branding |
| SECC | Socio-Economic Caste Census | Often used in eligibility context (public) |
| CHC / PHC | Community / Primary Health Centre | Public facility types |
| DH | District Hospital | Public secondary hospital |
| eHospital | eHospital (NIC) | Government HMIS |
| eSushrut | eSushrut (CDAC) | Government HMIS product |
| NIC | National Informatics Centre | Builds many government systems |
| CDAC | Centre for Development of Advanced Computing | Builds eSushrut and others |
| Aadhaar | Aadhaar | National ID — **not** a hospital UHID; do not design “Aadhaar = patient chart” |
| OTP | One-Time Password | Second factor |
| KYC | Know Your Customer | Identity proofing (more banking; hospitals still verify ID) |
| DLT | Distributed Ledger Template (SMS DLT) | Registered SMS templates in India |
| TRAI | Telecom Regulatory Authority of India | SMS/WhatsApp compliance context |

**Do not confuse:** ABHA (national) vs UHID (one hospital). PM-JAY (scheme that pays) vs ABDM (digital rails). Sandbox ≠ production.

---

## D. Insurance, billing, revenue cycle

| Short | Full name | Meaning |
|---|---|---|
| RCM | Revenue Cycle Management | Eligibility → code → claim → cash |
| TPA | Third Party Administrator | Processes cashless/claims for an insurer |
| GI | General Insurance | Non-life, including health |
| IRDAI | Insurance Regulatory and Development Authority of India | Insurer regulator |
| Pre-auth | Pre-authorisation | Payer approval before (or early in) treatment |
| Enhancement | Enhancement | Extra amount requested mid-stay |
| Cashless | Cashless treatment | Hospital bills payer; patient pays gap |
| Reimbursement | Reimbursement | Patient pays, then claims |
| Copay / co-pay | Co-payment | Patient share defined by policy |
| Deductible | Deductible | Amount patient pays before cover |
| SI | Sum Insured | Maximum cover |
| GIPSA | General Insurance Public Sector Association | PSU insurer grouping; you may hear “GIPSA rates” |
| PSU | Public Sector Undertaking | Government-owned company |
| NHCX | National Health Claims Exchange | Standard digital claims rail |
| FNOL | First Notice of Loss | Insurance claim intake (more motor; health uses intimation) |
| Adjudication | Claim adjudication | Decide pay / deny / query |
| Denial | Claim denial | Payer will not pay (needs a reason code) |
| Query | Payer query | More documents or clarification |
| AR | Accounts Receivable | Money billed, not yet collected |
| AR days | Accounts Receivable days | How long cash is stuck |
| GL | General Ledger | Finance books (SAP/Tally) |
| GST | Goods and Services Tax | Tax on invoices where applicable |
| PAN | Permanent Account Number | Tax ID — not a clinical ID |
| Package | Treatment package | Fixed price for a procedure bundle |
| Itemized | Itemized billing | Line-by-line charges |
| BOM | Bill of Materials | What is inside a package |
| Non-payables | Non-payable items | Lines the insurer will not pay |
| Empanelment | Network empanelment | Hospital accepted by a payer |
| Tariff | Tariff master | Price list |
| DRG | Diagnosis-Related Group | Bundled payment group (more US/some schemes) |
| HCC | Hierarchical Condition Category | US risk-adjustment coding |
| EDI | Electronic Data Interchange | Older claims file exchange |
| EOB | Explanation of Benefits | What the payer paid (US-style) |
| Combined ratio | Combined ratio | (Claims + expenses) / premium — insurer health |
| STP | Straight-Through Processing | Auto-processed without human (rare for complex health claims) |

**Do not confuse:** TPA (payer processor) vs hospital TPA *desk* (hospital employees). AR (receivables) vs ARPOB (revenue per bed). Denial vs query.

---

## E. Quality, legal, privacy, safety

| Short | Full name | Meaning |
|---|---|---|
| NABH | National Accreditation Board for Hospitals & Healthcare Providers | Hospital accreditation (India) |
| JCI | Joint Commission International | Global hospital accreditation |
| DPDP / DPDPA | Digital Personal Data Protection Act | India personal-data law |
| DPO | Data Protection Officer | Privacy owner |
| PHI | Protected / Personal Health Information | Health data that must be controlled |
| PII | Personally Identifiable Information | Data that identifies a person |
| HIPAA | Health Insurance Portability and Accountability Act | US privacy law — **do not paste into an Indian BRD as if it were DPDP** |
| GDPR | General Data Protection Regulation | EU privacy law (EU/UK accounts) |
| BAA | Business Associate Agreement | US HIPAA vendor contract |
| DPIA | Data Protection Impact Assessment | Privacy risk assessment |
| Consent | Informed / recorded consent | Purpose-wise permission |
| Break-glass | Break-the-glass access | Emergency chart access with alarm |
| RBAC | Role-Based Access Control | Access by job role |
| ABAC | Attribute-Based Access Control | Access by attributes (location, etc.) |
| Audit trail | Audit trail | Who did what, when |
| Sev1 | Severity 1 | Highest incident — wrong patient, mix-up, leak |
| RCA | Root Cause Analysis | Why it happened |
| CAPA | Corrective and Preventive Action | Fix and stop recurrence |
| SOP | Standard Operating Procedure | Written how-to |
| WI | Work Instruction | Step-level SOP |
| NABH indicator | Quality indicator | Defined metric for accreditation |
| Incident | Patient safety incident | Harm or near-miss |
| Near-miss | Near-miss | Harm did not reach the patient |
| PCPNDT | Pre-Conception and Pre-Natal Diagnostic Techniques Act | Controls sex determination / USG |
| IT Act | Information Technology Act, 2000 | Cyber/legal baseline (India) |
| Clinical Establishments Act | Clinical Establishments (Registration and Regulation) Act | Facility registration where adopted |
| IEC | Information, Education, Communication | Patient-facing material (also electrical safety in other contexts — ask) |

**Do not confuse:** NABH vs NABL. HIPAA (US) vs DPDP (India). QA (quality) vs QA (software testing) — say which.

---

## F. Systems, integration, IT

| Short | Full name | Meaning |
|---|---|---|
| HIS / HMIS / HMS | Hospital Information System / Hospital Management Information System / Hospital Management System | Registration, IPD, billing, often EMR |
| LIS | Laboratory Information System | Lab master |
| RIS | Radiology Information System | Imaging workflow |
| PACS | Picture Archiving and Communication System | Images |
| HL7 | Health Level Seven | Family of health data standards |
| HL7 v2 | Health Level Seven version 2 | Pipe-delimited messages still common |
| ADT | Admit, Discharge, Transfer | Patient movement messages |
| ORM | Order Message | Order (lab/Rx/rad) |
| ORU | Observation Result | Result |
| ACK | Acknowledgement | “I received your message” |
| FHIR R4 | Fast Healthcare Interoperability Resources, Release 4 | Common FHIR version |
| API | Application Programming Interface | How systems call each other |
| REST | Representational State Transfer | Common web API style |
| JSON | JavaScript Object Notation | API data format |
| XML | Extensible Markup Language | Older/common payload format |
| DICOM | Digital Imaging and Communications in Medicine | Images |
| Interface engine | Integration engine (Mirth, etc.) | Routes HL7/FHIR |
| Middleware | Middleware | Sits between analyser and LIS |
| VPN | Virtual Private Network | Secure network path |
| SSO | Single Sign-On | One login to many apps |
| AD | Active Directory | Enterprise user directory |
| IAM | Identity and Access Management | Who can log in and as whom |
| DR | Disaster Recovery | How you come back after outage |
| RPO | Recovery Point Objective | How much data you may lose |
| RTO | Recovery Time Objective | How fast you must be back |
| SLA | Service Level Agreement | Contracted performance |
| SLO | Service Level Objective | Internal target |
| Uptime | Uptime | % time the system is available |
| On-prem | On-premises | Servers in the hospital/data centre |
| SaaS | Software as a Service | Vendor-hosted software |
| IaaS / PaaS | Infrastructure / Platform as a Service | Cloud layers |
| DC | Data Centre | Where servers live |
| PACS viewer | DICOM viewer | Screen that shows images |
| CRM | Customer Relationship Management | Leads, campaigns — not MPI |
| ERP | Enterprise Resource Planning | Finance/HR/supply (SAP etc.) |
| HRMS / HRIS | Human Resource Management / Information System | Staff master, often roster |
| BI | Business Intelligence | Reports and dashboards |
| MIS | Management Information System | Operational reports |
| ETL | Extract, Transform, Load | Data warehouse pipeline |
| OLAP | Online Analytical Processing | Analytics queries |
| Replica | Read replica | Copy of DB for reporting — still PHI |
| PHI store | Protected health information store | Any database with patient data |

**Do not confuse:** API vs HL7 (HL7 can travel over APIs). CRM vs HIS. Cloud vs “ABDM compliant” (not the same).

---

## G. BA and delivery — recap (already learned in folder 01)

**Do this section last.** The canonical BA dictionary is [00-ba-and-business-abbreviations.md](../01-BA-Role-Business-Fundamentals/00-ba-and-business-abbreviations.md) (BRD, FRD, SRS, SOW, RTM, UAT, RACI, …). This table is a **recap on a health account**, plus a few services-firm extras (orals, bench, utilisation).

Health-only: HIM. Collision: CR = Change Request **or** Computed Radiography — expand once.

| Short | Full name | Meaning |
|---|---|---|
| BA | Business Analyst | Elicits, analyses, documents, validates requirements |
| BSA | Business Systems Analyst | BA with stronger systems tilt |
| SA | Solution / System Architect | Technical design owner |
| PO | Product Owner | Prioritises the backlog (client or vendor) |
| PM | Project Manager | Time, cost, RAID |
| DM | Delivery Manager | Account/delivery outcome in services firms |
| EM | Engagement Manager | Client relationship + SOW |
| SM | Scrum Master | Scrum facilitation |
| QA / QC (software) | Quality Assurance / Quality Control | Testing function |
| Dev | Development | Engineering |
| UI / UX | User Interface / User Experience | Screens and journeys |
| SME | Subject Matter Expert | Client expert (doctor, TPA lead, HIM) |
| HIM | Health Information Management | Medical records / coding / MPI |
| PMO | Project Management Office | Governance, status, templates |
| CoE | Centre of Excellence | Shared practice (e.g. Gen AI CoE) |
| SOW | Statement of Work | What the services firm is paid to do |
| MSA | Master Service Agreement | Umbrella contract |
| T&M | Time and Materials | Billed by effort |
| FP / FFP | Fixed Price / Firm Fixed Price | Billed to a scope box |
| CR | Change Request | Scope change after baseline |
| RAID | Risks, Assumptions, Issues, Dependencies | Steering log |
| RACI | Responsible, Accountable, Consulted, Informed | Who does what |
| BRD | Business Requirements Document | Why + business needs |
| FRD | Functional Requirements Document | What the system must do |
| SRS | Software Requirements Specification | Combined spec (often waterfall) |
| FR / NFR | Functional / Non-Functional Requirement | Behaviour vs quality (SLA, security) |
| BR | Business Rule | Decision logic |
| TR | Transition Requirement | Go-live, training, downtime SOP |
| RTM | Requirements Traceability Matrix | Req → story → test |
| UC | Use Case | Actor + flow + exceptions |
| US | User Story | Agile slice of value |
| AC | Acceptance Criteria | Testable done |
| DoD / DoR | Definition of Done / Ready | Quality gates |
| MVP | Minimum Viable Product | Smallest releasable slice |
| MoSCoW | Must, Should, Could, Won’t | Prioritisation |
| As-Is / To-Be | Current / future process | Process modelling |
| BPMN | Business Process Model and Notation | Process diagram standard |
| UML | Unified Modeling Language | Use case, activity, sequence diagrams |
| DFD | Data Flow Diagram | Data movement |
| UAT | User Acceptance Testing | Client proves it works in business terms |
| SIT | System Integration Testing | Systems talk to each other |
| Regression | Regression testing | Old paths still work |
| P1 / Sev | Priority 1 / Severity | Defect ranking |
| Sprint | Sprint | Time-box (often 2 weeks) |
| PI | Program Increment | SAFe planning cycle (if the account uses SAFe) |
| SAFe | Scaled Agile Framework | Enterprise Agile (some accounts) |
| Jira | Jira | Work tracking (Atlassian) |
| Confluence | Confluence | Wiki/specs |
| ADO | Azure DevOps | Microsoft’s Jira-like tool |
| Onsite / offshore | Onsite / offshore | Client location vs delivery centre |
| KT | Knowledge Transfer | Handover |
| Hypercare | Hypercare | Intense support right after go-live |
| BAU | Business As Usual | After project, run the process |
| RFP / RFI / RFQ | Request for Proposal / Information / Quotation | Sales pursuit |
| Orals | Oral presentation | Sales pitch to client |
| Rate card | Rate card | Price per role per day |
| Bench | Bench | People between projects |
| Utilisation | Utilisation | % of a person’s time billed |
| Timesheet | Timesheet | How T&M is billed |
| Client vs vendor BA | Client BA vs vendor (services) BA | She is usually the **vendor BA** |

**Do not confuse:** UAT (business) vs SIT (technical). CR (change request) vs CR (computed radiography). QA (testing) vs NABH QA.

---

## H. Gen AI, data, and analytics (you will hear this daily)

| Short | Full name | Meaning |
|---|---|---|
| AI | Artificial Intelligence | Umbrella term — always ask which technique |
| Gen AI | Generative AI | Models that *create* text/images/code |
| LLM | Large Language Model | Text generator (GPT-class) |
| ML | Machine Learning | Models that learn patterns from data |
| NLP | Natural Language Processing | Language tasks (older + newer) |
| GPT | Generative Pre-trained Transformer | A family of LLMs |
| Transformer | Transformer architecture | Neural net design behind LLMs |
| Prompt | Prompt | Instructions + context you send the model |
| Context window | Context window | How much text the model can see at once |
| Token | Token | Chunk of text the model counts |
| Hallucination | Hallucination | Fluent but false output |
| RAG | Retrieval-Augmented Generation | Model answers using *retrieved* approved documents |
| Embedding | Embedding | Numeric vector for a piece of text |
| Vector DB | Vector database | Stores embeddings for search |
| Fine-tune | Fine-tuning | Extra training on a model (expensive, PHI risk) |
| Grounding | Grounding | Forcing answers to cite sources |
| HITL | Human-in-the-Loop | A person must confirm before it counts |
| Copilot | Copilot | Assistant in a product (Microsoft, GitHub, etc.) |
| Chatbot | Chatbot | Conversational UI — not automatically clinical |
| Agent | AI agent | Model that can call tools/steps (needs tight BRs) |
| OCR | Optical Character Recognition | PDF/image → text |
| IDP | Intelligent Document Processing | OCR + extraction (cashless packs, bills) |
| Speech-to-text | Speech-to-text / ASR | Dictation → text (clinical scribe) |
| ASR | Automatic Speech Recognition | Same as speech-to-text |
| Evaluation / eval | Model evaluation | Measured quality, not a demo vibe |
| Golden set | Golden dataset | Hand-checked examples for eval |
| Precision / recall | Precision / recall | How many extracted fields are right / found |
| Latency | Latency | How long the model takes |
| Guardrail | Guardrail | Blocks unsafe outputs (diagnosis, PHI leak) |
| Red-teaming | Red-teaming | Attack the model on purpose to find harm |
| PII scrubbing | PII / PHI de-identification | Strip identifiers before a model |
| Tenant | Cloud tenant | Your company’s isolated AI environment |
| Azure OpenAI | Azure OpenAI Service | Enterprise GPT-style APIs on Azure |
| Bedrock | Amazon Bedrock | AWS managed foundation models |
| Vertex | Google Vertex AI | Google Cloud model platform |
| On-prem LLM | On-premises LLM | Model inside the client data centre (rare, costly) |
| CoE (Gen AI) | Generative AI Centre of Excellence | Internal practice that builds accelerators |
| Accelerator | Accelerator | Reusable demo/asset the firm sells |
| Use case | Use case (sales + BA) | A bounded AI job with owner, data, HITL, KPI |
| Shadow AI | Shadow AI | Staff pasting client data into public ChatGPT |
| Responsible AI | Responsible AI | Privacy, fairness, accountability, human control |

**Do not confuse:** RAG (documents as source of truth) vs fine-tune (changing the model). Chatbot vs CDSS. Copilot for *doctors* vs Copilot for *BAs* (different PHI rules).

---

## I. Hospital money and ops metrics (short names)

| Short | Full name | Meaning |
|---|---|---|
| ARPOB | Average Revenue Per Occupied Bed | Core hospital revenue metric |
| Occupancy | Bed occupancy rate | Occupied ÷ available beds |
| ALOS | Average Length of Stay | Days per admission |
| ARPOB vs occupancy | — | High occupancy + slow insurance cash can still hurt |
| EBITDA | Earnings Before Interest, Tax, Depreciation, Amortisation | Profitability (investor decks) |
| NPS | Net Promoter Score | Loyalty survey — weak alone in healthcare |
| CSAT | Customer Satisfaction | Survey score |
| No-show | No-show rate | Booked, did not arrive |
| Utilisation (OT) | Theatre utilisation | Used OT minutes ÷ available |
| FTE | Full-Time Equivalent | Staffing unit |

---

## J. Confusable pairs (exam these)

| You hear | People mix it with | Difference |
|---|---|---|
| HIS | EMR | HIS runs the hospital; EMR is the chart |
| EMR | EHR | EMR = this facility; EHR = shareable/longitudinal idea |
| UHID | ABHA | Local vs national |
| NABH | NABL | Hospital vs lab |
| TPA | Insurer | TPA processes; insurer carries risk (sometimes in-house) |
| RIS | PACS | Workflow vs images |
| TAT | SLA | TAT is a process clock; SLA is a contract |
| BA | DA / DS | Business Analyst vs Data Analyst vs Data Scientist |
| UAT | SIT | Business sign-off vs integration test |
| CR | Change request vs computed radiography | Context |
| QA | Quality vs testing | Say “NABH quality” or “software QA” |
| Agent | AI agent vs insurance agent vs patient attendant | Always disambiguate |
| Token | LLM token vs OPD token vs SMS token | Three different things |
| Copilot | GitHub Copilot vs Microsoft 365 Copilot vs “clinical copilot” | Different products, different data |

---

## K. First-mention examples (copy this habit)

- Hospital Information System (HIS)
- Electronic Medical Record (EMR)
- Laboratory Information System (LIS)
- Picture Archiving and Communication System (PACS)
- Revenue Cycle Management (RCM)
- Third Party Administrator (TPA)
- Ayushman Bharat Health Account (ABHA)
- Ayushman Bharat Digital Mission (ABDM)
- National Health Claims Exchange (NHCX)
- Digital Personal Data Protection Act (DPDP Act)
- Large Language Model (LLM)
- Retrieval-Augmented Generation (RAG)
- Human-in-the-Loop (HITL)
- Statement of Work (SOW)
- User Acceptance Testing (UAT)
- Requirements Traceability Matrix (RTM)

---

## L. 10-minute drill (say full names)

1. HIS, EMR, LIS, RIS, PACS  
2. UHID, MPI, ABHA, HPR, HFR  
3. RCM, TPA, NHCX, AR, ARPOB  
4. HL7, FHIR, DICOM, ICD, SNOMED  
5. NABH, NABL, DPDP, DPO, PHI  
6. BRD, FRD, RTM, UAT, SOW *(recap from folder `01` file `00` — fail this line if you skipped the BA glossary)*  
7. LLM, RAG, HITL, OCR, IDP  
8. OPD, IPD, OT, ICU, ALOS  

If you cannot expand these 40 without looking, you are not interview-ready.

## Notes

- Learn by writing one sentence that uses the term, not by highlighting this table.  
- US accounts add HIPAA, CPT, DRG, HCC. Indian hospital accounts add ABHA, NABH, TPA, DPDP.  
- Services-firm calls add SOW, T&M, onsite, utilisation, CoE.  
- Never invent an expansion. If you are unsure, ask: “When you say MS, do you mean Medical Superintendent?”
