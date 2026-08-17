# Gen AI Foundations for a Healthcare BA (Services Firm)

> **Sequence: Phase 1, file 06 of 06.** Prerequisites: `01`–`05`.  
> **Do not open** `13-solution-nimbus-genai-note-copilot.md` yet. That file is Phase 4 (catalog + full SOW).  
> **Next after this file:** `07-companies-what-they-do.md`, then the **gate** in `00-how-to-use-this-pack.md`.

Nimbus Digital (illustrative IT services company) sells **Generative AI (Gen AI)** alongside Hospital Information System (HIS) / Revenue Cycle Management (RCM) work. Before she writes a use case, she must know the **rules**: Human-in-the-Loop (HITL), what the model must not author, what never goes into a public chatbot.

Internal BA use of Large Language Models (LLMs) is also in `01-ba-in-service-organization.md` and folder `14-AI-for-Business-Analysts`. Expansions: `02-abbreviations-and-full-names.md` section H.

## Definition

**Generative AI (Gen AI)** creates text (and sometimes images/code) from a prompt. In healthcare delivery, the useful pattern is almost always:

**Retrieve or extract from a known source → draft → clinician / coder / coordinator confirms → then it becomes a record.**

Unsupervised “AI doctor” or “AI denies the claim” is not a junior-BA programme. It is a liability event.

| Term | Full name | She must remember |
|---|---|---|
| LLM | Large Language Model | Drafts fluent text; does not know this HIS |
| HITL | Human-in-the-Loop | Named human accepts before it is the record |
| RAG | Retrieval-Augmented Generation | Answers from **approved** documents, with citation |
| Hallucination | Hallucination | Fluent but false (invented drug, fake SLA) |
| PHI | Personal / Protected Health Information | Never in a public ChatGPT prompt |
| OCR / IDP | Optical Character Recognition / Intelligent Document Processing | Turns cashless PDFs into fields |
| ASR | Automatic Speech Recognition | Dictation → text for a scribe |

## Why it matters on her accounts

Clients hear ChatGPT and ask for it on day one. Nimbus wins if she can say: **which job, which system of record, which human, which KPI, which data must never leave the tenant.** That is BA work, not model-tuning.

## Pattern table (conversation depth — not a BRD yet)

| Pattern | What “good” looks like | What fails |
|---|---|---|
| Clinical scribe / note draft | Speech-to-text → SOAP draft → doctor edits → EMR save | Auto-save without review |
| Coding assist | Suggest ICD from the **signed** note → coder accepts | Model invents diagnosis to raise ARPOB |
| Document intelligence | OCR + extract into a HIS checklist → coordinator confirms | PDF chatbot with no fields |
| RAG on SOPs | Answer with **document + version + clause** | Model quotes a blog as NABH |
| Patient FAQ | Appointments, location, financial **labels** — no diagnosis | Symptom checker as advice |
| Internal BA copilot | Draft AC from **redacted** notes | Paste PHI into public ChatGPT |

Indian constraints she must name: **Digital Personal Data Protection (DPDP) Act**, purpose-wise consent, data localisation questions for Legal. **Ayushman Bharat Digital Mission (ABDM)** is identity and rails — not an LLM. **National Health Claims Exchange (NHCX)** wants structured Fast Healthcare Interoperability Resources (FHIR) — not a GPT paragraph.

## The BA gate (every Gen AI idea)

If any box is “no,” it is a demo, not an MVP. She uses this in Phase 4; she must **memorise it now**.

| Gate | Question |
|---|---|
| Job | One actor, one artifact (note, checklist, code, FAQ) |
| Source of truth | HIS / EMR / SOP / PDF pack — named |
| HITL | Named role must accept before it is “real” |
| PHI | Tenant; no training on client data unless Legal signs |
| Harm | What if the model is wrong? Fallback path |
| KPI | Minutes saved, edit rate, field precision — not “wow” |
| SOW | In this contract or a Change Request (CR)? |

## What she should refuse or park (learn now)

| Ask | Why park |
|---|---|
| Symptom checker that “triages like a doctor” | Liability, wrong-patient routing |
| Auto-deny claims | Regulator + fairness |
| WhatsApp bot that opens lab PDFs for families | Privacy incident (CityWell grain — Phase 4) |
| Fine-tune on years of discharge summaries | PHI, DPDP, no evaluation set |
| “ABDM in a chatbot” | ABHA is identity + consent, not an LLM |

## Tools she will hear (conversation depth)

| Short | Full name | BA note |
|---|---|---|
| Azure OpenAI | Azure OpenAI Service | Common enterprise GPT-class APIs |
| Bedrock | Amazon Bedrock | AWS equivalent |
| Copilot | GitHub / Microsoft 365 Copilot | Dev vs office — different PHI |
| RAG | Retrieval-Augmented Generation | Default for SOP bots |
| Vector DB | Vector database | Where SOP chunks live |
| Guardrails | Safety filters | Block diagnosis language on patient bots |
| Eval harness | Evaluation harness | Golden set belongs **in the SOW** |

She does not pick the model. She writes: **P95 latency, no PHI in logs, HITL, citation, fallback.**

HIS/EMR tools: `05-tools-and-software.md`.

## Requirement patterns (copy later into an FRD — learn the shape now)

| ID type | Example statement |
|---|---|
| FR | System displays AI draft and requires ACCEPT / EDIT / REJECT before EMR save. |
| FR | If retrieval returns zero passages, reply with the configured “I don’t know” template. |
| BR | The model shall not be the legal author of the discharge summary; the doctor is. |
| NFR | Prompts and outputs containing PHI stay in the client-approved region. |
| NFR | Model and prompt-template version are logged on every generation. |
| TR | Users trained that REJECT is success, not failure. |
| Out | Autonomous prescribing; internet-grounded medical advice. |

**Evaluation is in-scope.** A BA who cannot write User Acceptance Testing (UAT) for hallucination will lose UAT.

UAT ideas she should be able to name (not run until Phase 4):

- Scribe invents a drug the doctor did not say → extra text for edit; cannot silently merge.  
- Extraction reads the wrong implant amount → low confidence, human confirm.  
- Patient bot: “I have chest pain” → emergency redirect, no slot booking.  
- SOP bot: question not in corpus → “I don’t know.”  
- Architecture: public internet is **not** called.

## How she uses Gen AI internally (Nimbus BA)

Allowed (company tenant, Master Service Agreement permits): redact → draft stories / find ambiguity → she edits → Subject Matter Expert (SME) confirms.

Forbidden: paste a client FRD or discharge summary into public ChatGPT.

## Weak vs strong

| Weak | Strong |
|---|---|
| “We’ll add ChatGPT” | Gate table + HITL + SOW line |
| Demo on a public model | Approved tenant |
| Skip this file, open file 13 | Foundations → gate → then the copilot SOW |

## Notes

- Gen AI is a **layer**. HIS/EMR remains the record.  
- She will write FRs, not train models.  
- **Stop here.** Sit the gate in `00-how-to-use-this-pack.md`. Then file `07`.  
- Detailed catalog (UC-G01…) and the ApexCare copilot BRD are file `13`, Phase 4.
