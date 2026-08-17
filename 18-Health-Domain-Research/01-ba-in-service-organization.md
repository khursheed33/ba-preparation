# BA in a Service-Based Organization (Healthcare Accounts)

> **Sequence: Phase 1, file 01 of 06.** Start here after `00-how-to-use-this-pack.md`.  
> **Next:** `02-abbreviations-and-full-names.md`. Do not open solution files `10`–`13` yet.

She will not be employed by the hospital. She will be employed by an **IT services / consulting firm** that is paid (Statement of Work) to analyse, design, and deliver software for a healthcare **client**. The company also sells **Generative AI** work. That changes who she reports to, what “done” means, and what she is allowed to paste into a model.

Teaching firm in this pack: **Nimbus Digital** (illustrative). Teaching client: ApexCare / HelixLab / CityWell.

## Definition

A **vendor BA** (services BA) elicits and baselines requirements **for a client**, then feeds an **onsite–offshore** delivery team, inside a **contracted scope**. She is measured on clarity, change control, and UAT — not on occupancy of the hospital.

A **client BA** (hospital HIM/IT) lives in the process forever. She will sit *with* them. She is not them.

## Why it matters

Product-company stories (“ship the app”) fail in services interviews. Nimbus is paid for a **SOW slice**: cashless file in HIS, or a Gen AI note-draft copilot with HITL — not “transform healthcare.” If she writes out-of-SOW FRs, the Delivery Manager (DM) will cut them, or the firm will deliver unpaid work.

## How a healthcare services engagement actually runs

```
Sales (RFP/orals) → SOW signed
    → Discovery (2–6 weeks, BA heavy)
        → Baseline BRD/FRD or backlog
            → Build in sprints (offshore Dev/QA + onsite BA)
                → SIT → UAT (client SMEs)
                    → Go-live + hypercare
                        → BAU / next CR / next SOW
```

| Phase | What she does | What she does not do |
|---|---|---|
| Pursuit / orals | Domain questions, use-case sanity, estimation inputs | Promise AI diagnosis to win the deal |
| Discovery | As-Is on the floor, stakeholders, gaps, SOW mapping | Unlimited scope “while we are here” |
| Delivery | Stories, AC, RTM, CR impact, vendor API contracts | Invent ICD codes or clinical protocols |
| UAT | Scenarios, defect triage (business vs technical) | Sign clinical safety alone |
| Hypercare | Issue → BR vs bug vs training | Live in the TPA desk forever |

## Stakeholders (two organigrams)

**Client (ApexCare)**  
COO, Medical Superintendent, TPA lead, HIM, DPO, HIS vendor, doctors.

**Nimbus (her company)**  
Engagement Manager, Delivery Manager, Architect, Tech Lead, Dev, QA, Gen AI CoE, her BA lead. Sales may still sit in steering until go-live.

| She optimises | They optimise |
|---|---|
| Testable scope, traceability | EM: renewal; DM: margin and dates; CoE: reusable accelerator |

**Conflict she will feel:** CoE wants to demo a chatbot; TPA desk needs a checklist in HIS. The BA’s job is to **map the demo to a signed use case** or park it as a CR.

## Product BA vs services BA

| | Product BA | Services BA (her) |
|---|---|---|
| Backlog owner | Product org | Client PO + SOW; she facilitates |
| Success | Adoption, revenue of *our* product | Accepted UAT, no leakage of unpaid scope |
| Domain | One product | Many clients; she must learn *this* HIS |
| Gen AI | Feature on our roadmap | Sold as a **use case** under a SOW, data on *client* terms |
| Brand | ShopEase | She does not put ApexCare confidential metrics on LinkedIn |

## Contract words that become requirements

| Term | Full name | BA effect |
|---|---|---|
| SOW | Statement of Work | In-scope / out-of-scope is a **commercial** document |
| MSA | Master Service Agreement | Privacy, subcontractors, AI tools may already be forbidden |
| T&M | Time and Materials | Extra discovery is billable if EM agrees |
| FP | Fixed Price | Every new FR is a **Change Request** |
| SLA | Service Level Agreement | NFR numbers come from here, not from ChatGPT |
| Rate card | Rate card | Her time is a cost; workshops need a purpose |
| Onsite | Onsite | Floor observation, UAT, workshops |
| Offshore | Offshore | Stories must be understandable **without** hallway context |
| KT | Knowledge Transfer | She writes so the next BA can continue |
| Hypercare | Hypercare | Defect vs training vs new BR |

**Rule for fixed-price:** If it is not in the SOW, it is a CR — even if a doctor asked in the lift.

## Day-in-the-life (illustrative)

**Onsite week (client hospital / client office)**  
Stand-up with Nimbus. Shadow TPA desk 45 min. Workshop on eligibility BR. Update Confluence. Confirm DPO on SMS templates. Send offshore a recorded walkthrough of one screen (no patients in frame).

**Offshore week (delivery centre)**  
Groom stories with Dev/QA. Clarify HL7 ACK. Review QA cases against RTM. Flag a CR because the client added PM-JAY portal. Draft UAT script. Use **enterprise** Gen AI to rephrase AC from *her* notes — no PHI.

## How she uses Gen AI as a services BA (internal)

Allowed pattern (company tenant, MSA permits):

1. Redact. No UHID, no real names, no bill PDFs.  
2. Prompt: draft stories / find ambiguity / make a workshop agenda.  
3. She edits. SME confirms. Then Jira.

Forbidden: paste ApexCare FRD into public ChatGPT; paste discharge summaries “to summarise”; let the model invent IRDAI clauses.

See folder `14-AI-for-Business-Analysts` and, after the gate, `13-solution-nimbus-genai-note-copilot.md`. Foundations: `06-gen-ai-foundations-for-healthcare-ba.md`.

## Typical Nimbus-style healthcare + AI SOWs (what she will be staffed on)

| SOW type | Client problem | BA grain |
|---|---|---|
| HIS implementation / rollout | New unit or replacement | MPI, billing, downtime TR |
| Integration | HIS–LIS–PACS–TPA | HL7/FHIR contracts, ACK, retry |
| RCM / cashless | Denials, discharge hold | ApexCare file `10` (Phase 4) |
| ABDM / NHCX | Badge vs real linkage | CityWell file `12` (Phase 4) |
| Patient app | Satellite channel | Consent, not a second UHID |
| Gen AI copilot | Notes, documents, coding assist | HITL, eval, PHI — files `06` then `13` |
| Support / AMS | Tickets after go-live | BR vs bug |

AMS = Application Management Services (full name): run and small changes after the project.

## Elicitation constraints unique to services

- Badge and chaperone: she may not wander wards. Observation is scheduled.  
- No photos of patients or whiteboards with UHIDs.  
- Client HIS training tenant only — not production.  
- Offshore team will never see the floor: **write the exception paths**.  
- Client SMEs are busy; 25-minute slots. Go with a decision, not a tour.

## Weak vs strong (interview and floor)

| Weak | Strong |
|---|---|
| “I will transform their EMR” | “SOW is cashless file in HIS; AI pack-extraction is a CR” |
| Demo-led AI | Use case: owner, data class, HITL, KPI, fallback |
| Stories only happy path | Offshore can build the query-code exception |
| Scope creep to please the MS | Logged CR with impact on date/cost |
| Public LLM + client PDF | Enterprise tenant + redaction |
| “We are like Apollo 24/7” | Vendor BA on a 3-hospital HIS contract |

## Scenario / Use case: first week on Nimbus–ApexCare

**Context.** She joins a T&M discovery. Sales promised “Gen AI claims.” Floor shows eight TPA portals and WhatsApp implants.

**What she does.** Map SOW vs floor. Write: Must = HIS cashless file (Phase 4, file `10`). Gen AI document extraction = later SOW with DPO. EM and client COO sign the split.

**If ignored.** CoE builds a chatbot. UAT fails. Timesheets burn. Client remembers “AI didn’t work.”

## Notes

- She is a **vendor BA**. Scope is the product.  
- Healthcare language (file `02`) + delivery language (SOW, CR, UAT) together.  
- Gen AI is a practice the firm sells; it is not a substitute for eligibility BRs.  
- Confidentiality: client names and metrics stay off the portfolio unless allowed. Teaching companies exist for that.  
- Gen AI rules now: `06-gen-ai-foundations-for-healthcare-ba.md`. Copilot SOW after the gate: `13-solution-nimbus-genai-note-copilot.md`.
