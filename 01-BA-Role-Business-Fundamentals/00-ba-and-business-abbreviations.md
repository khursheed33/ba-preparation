# BA and Business Abbreviations

Read this **before** the use-case files in this folder. Learn the short form, the full name, and one-line meaning. Then the ShopEase / NovaBank / MediCare+ stories will make sense.

This list is **Business Analyst (BA) and delivery language** — documents, contracts, requirements, Agile, testing, money. It is **not** hospital language (Out-Patient Department (OPD), Hospital Information System (HIS)). Those wait until [11-Domain-Business-Knowledge](../11-Domain-Business-Knowledge/01-how-to-learn-a-domain.md) and [18-Health-Domain-Research/02-abbreviations-and-full-names.md](../18-Health-Domain-Research/02-abbreviations-and-full-names.md).

**Job seat this repo prepares for:** you work in a **technology / IT services company**. Most **clients** will be **healthcare**. You still need this BA vocabulary on day 1; you add clinical words on the account.

## How to use this file

| Rule | Practice |
|---|---|
| First mention in a document | Full name, then short: `Statement of Work (SOW)` |
| After that | SOW |
| Study | Cover the Short column, say the full name aloud, then the meaning |
| Do not | Jump to a 40-page scenario before you can expand BRD, FRD, SRS, SOW, RTM, UAT |

---

## A. People and roles

| Short | Full name | Meaning |
|---|---|---|
| BA | Business Analyst | Elicits, analyses, documents, and validates what should change |
| BSA | Business Systems Analyst | BA with a stronger systems / integration tilt |
| SME | Subject Matter Expert | Person who knows the process (ops lead, clinician on a health account) |
| PO | Product Owner | Owns backlog priority and business value |
| PM | Project Manager | Time, cost, plan; not the same as BA |
| SM | Scrum Master | Facilitates Scrum; does not own requirements |
| DM | Delivery Manager | Services-firm owner of dates, margin, staffing |
| EM | Engagement Manager | Client relationship and contract health |
| PMO | Project Management Office | Governance, status, templates |
| QA / QC | Quality Assurance / Quality Control | Testing function (software) |
| SA | Solution Architect (or System Architect) | Technical design owner |
| TL | Tech Lead | Day-to-day engineering lead |
| Dev | Development / developer | Builds the solution |
| UX / UI | User Experience / User Interface | Journeys and screens |
| Stakeholder | Stakeholder | Anyone affected by or able to influence the change |

## B. Contracts and commercial (tech company → client)

You will hear these in sales and delivery **before** anyone asks for a screen.

| Short | Full name | Meaning |
|---|---|---|
| NDA | Non-Disclosure Agreement | You must not leak client information |
| MSA | Master Service Agreement | Umbrella contract between your firm and the client |
| SOW | Statement of Work | What this engagement is **paid** to do (scope, money, dates) |
| T&M | Time and Materials | Billed by effort |
| FP / FFP | Fixed Price / Firm Fixed Price | Billed to a boxed scope |
| RFP | Request for Proposal | Client asks vendors to bid |
| RFI | Request for Information | Client explores the market |
| RFQ | Request for Quotation | Client wants a price |
| SLA | Service Level Agreement | Contracted performance (time, uptime, TAT) |
| KPI | Key Performance Indicator | Named metric the business cares about |
| OKR | Objectives and Key Results | Goal + measurable results (some product orgs) |
| BAU | Business As Usual | Run the process after the project |
| CR | Change Request | Scope change **after** the baseline (not “computed radiography”) |
| CCB | Change Control Board | Who approves CRs |
| POC / PoC | Proof of Concept | Small trial: can this work? |
| POV | Proof of Value | Trial that must show a business result |
| KT | Knowledge Transfer | Handover of know-how |
| Hypercare | Hypercare | Intense support just after go-live |
| Onsite / offshore | Onsite / offshore | At the client vs at your delivery centre |

## C. Documents the BA writes or lives in

| Short | Full name | Meaning |
|---|---|---|
| BRD | Business Requirements Document | Why, outcomes, scope, high-level needs — not field-level design |
| FRD | Functional Requirements Document | What the system must **do** (behaviour, rules, screens at a useful grain) |
| SRS | Software Requirements Specification | Combined spec (often Waterfall / IEEE-style) |
| FSD | Functional Specification Document | Same family as FRD (name varies by account) |
| PRD | Product Requirements Document | Product-org cousin of BRD/FRD |
| HLD / LLD | High-Level Design / Low-Level Design | Architecture vs detailed technical design (architect owns; BA reads) |
| RTM | Requirements Traceability Matrix | Requirement → story/spec → test → status |
| MOM | Minutes of Meeting | Decisions, owners, dates |
| RAID | Risks, Assumptions, Issues, Dependencies | Steering log |
| RACI | Responsible, Accountable, Consulted, Informed | Who does the work vs who owns the outcome |
| SOP | Standard Operating Procedure | How ops run the process today (or after go-live) |
| WBS | Work Breakdown Structure | PM’s task tree — not a BRD |

**Do not confuse:** BRD (why / business) vs FRD (system behaviour) vs SRS (often one book that mixes both). SOW (what the **vendor is paid for**) vs BRD (what the **business needs**). A need can sit outside the SOW — that is a CR, not a silent story.

## D. Requirements language

| Short | Full name | Meaning |
|---|---|---|
| BR (need) | Business Requirement | Outcome the enterprise wants |
| BR (rule) | Business Rule | Decision logic (“if amount > X then checker”) — say “business rule” in speech if ambiguous |
| ST | Stakeholder Requirement | What a role needs |
| FR | Functional Requirement | What the solution does |
| NFR | Non-Functional Requirement | How well: performance, security, availability, usability |
| TR | Transition Requirement | Training, cutover, dual-run, data migration |
| AC | Acceptance Criteria | Testable “done” for a story or FR |
| DoR | Definition of Ready | Story is fit to start |
| DoD | Definition of Done | Increment is fit to ship |
| MoSCoW | Must, Should, Could, Won’t | Prioritisation for a release window |
| MVP | Minimum Viable Product | Smallest slice that still delivers the outcome |
| Scope | Scope | In vs out |
| Baseline | Baseline | Signed version you change only via CR |
| Sign-off | Sign-off | Named approval of a baseline |

## E. Process and models

| Short | Full name | Meaning |
|---|---|---|
| As-Is | As-Is | How work happens today |
| To-Be | To-Be | How work should happen after the change |
| Gap | Gap analysis | As-Is vs To-Be: what must change |
| BPMN | Business Process Model and Notation | Standard process diagram |
| SIPOC | Suppliers, Inputs, Process, Outputs, Customers | One-page process fence |
| DFD | Data Flow Diagram | How data moves |
| ERD | Entity Relationship Diagram | What we store and how it relates |
| UML | Unified Modeling Language | Use case, activity, sequence, state diagrams |
| UC | Use Case | Actor + main / alternate / exception flows |
| US | User Story | Agile slice: As a / I want / so that |
| Epic | Epic | Big slice that splits into stories |

## F. Delivery, Agile, and testing

| Short | Full name | Meaning |
|---|---|---|
| SDLC | Software Development Life Cycle | How software is conceived, built, released |
| STLC | Software Testing Life Cycle | How testing is planned and closed |
| Waterfall | Waterfall | Sequential phases; spec before build |
| Agile | Agile | Iterative delivery with frequent feedback |
| Scrum | Scrum | Time-boxed sprints, PO, SM, Dev team |
| Kanban | Kanban | Flow board, Work In Progress (WIP) limits |
| WIP | Work In Progress | How much is started but not finished |
| Sprint | Sprint | Time-box (often two weeks) |
| Backlog | Product / sprint backlog | Ordered work |
| SIT | System Integration Testing | Systems talk to each other |
| UAT | User Acceptance Testing | **Client / business** proves it works for the process |
| Regression | Regression testing | Old paths still work |
| Sev / P | Severity / Priority | How bad the defect is vs what we fix first |
| Prod | Production | Live environment |
| UAT env | UAT environment | Where business tests |

## G. Money, analysis, and strategy (business acumen)

| Short | Full name | Meaning |
|---|---|---|
| CBA | Cost-Benefit Analysis | Costs vs benefits with assumptions |
| ROI | Return on Investment | Benefit relative to cost (simple story, not CFA-level) |
| TCO | Total Cost of Ownership | Build + run, not only licence |
| NPV | Net Present Value | Finance’s discounted model — hand to Finance |
| Capex | Capital Expenditure | One-time / capitalised spend |
| Opex | Operating Expenditure | Run cost |
| FY | Financial Year | Accounting year |
| YoY / QoQ / MoM | Year on Year / Quarter / Month | How a metric moved |
| SWOT | Strengths, Weaknesses, Opportunities, Threats | Internal + external scan |
| PESTLE | Political, Economic, Social, Technological, Legal, Environmental | External-only scan |
| RCA | Root Cause Analysis | Why it really happens (5 Whys, fishbone) |

## H. Profession and standards

| Short | Full name | Meaning |
|---|---|---|
| IIBA | International Institute of Business Analysis | Professional body |
| BABOK | Business Analysis Body of Knowledge | IIBA guide to BA work |
| ECBA / CCBA / CBAP | Entry / Capability / Certified Business Analysis Professional | IIBA certifications (optional) |
| PMI | Project Management Institute | PM profession (PMBOK is their guide) |
| IEEE | Institute of Electrical and Electronics Engineers | SRS-style standards you may see cited |

## I. Everyday tech words a BA must expand once

| Short | Full name | Meaning |
|---|---|---|
| API | Application Programming Interface | How two systems exchange data |
| DB | Database | Organised store of data |
| UI | User Interface | What the user sees |
| PII | Personally Identifiable Information | Data that can identify a person (never in public AI tools) |
| KPI vs metric | Key Performance Indicator vs metric | A KPI is a metric **someone owns** for a decision |
| MIS / BI | Management Information System / Business Intelligence | Reports and dashboards |

Health-account extras (HIS, EMR, Protected Health Information (PHI), OPD) — **not here.** Learn them in folder `18` after this file.

---

## Drill (cover Short, say Full)

Do this until it is automatic. Then open `01-what-is-business-analysis.md`.

BA, SME, PO, PM, SOW, MSA, NDA, SLA, RFP, BRD, FRD, SRS, RTM, MOM, RACI, RAID, CR, FR, NFR, AC, DoR, DoD, MoSCoW, MVP, As-Is, To-Be, BPMN, ERD, DFD, UML, SDLC, UAT, SIT, KPI, ROI, CBA, BAU, KT, WIP, US, UC.

---

## After the words: one call (tech firm, health client)

**Context.** You work at **Nimbus Digital** (illustrative IT services firm). Client is a hospital group. Sales signed an **MSA**; this slice is a **SOW**: cashless admission file in the hospital system. A doctor says “also add an AI chatbot.”

**What you say (now that the shorts mean something).**

1. “That chatbot is outside this **SOW**. Log a **CR**; **EM** and the client **PO** decide.”
2. “We baseline a **BRD** for why cashless is slow, then **FR**s / stories with **AC**, traced in the **RTM**.”
3. “**UAT** is signed by the client **SME** (TPA / admissions), not by the BA.”
4. First mention in the Confluence page: `Statement of Work (SOW)`, `Business Requirements Document (BRD)`, `User Acceptance Testing (UAT)`.

**What goes wrong if you skip this file.** You hear “send me the SRS and the SLA for UAT” on week 1 and freeze, or you write a BRD for work the SOW never bought.

## Notes

- Expand the short form the **first** time in every artifact; then use the short form.
- SOW = paid scope. BRD = business need. FRD/SRS = system behaviour. RTM = thread. UAT = client proof.
- CR after baseline; do not hide extra work in a “small story.”
- Domain dictionaries (healthcare, banking) come **after** this BA dictionary.
- 
