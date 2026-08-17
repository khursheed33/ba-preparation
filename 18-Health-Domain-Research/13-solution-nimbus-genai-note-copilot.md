# Solution: Nimbus Digital — Gen AI Catalog + ApexCare Note Copilot

> **Sequence: Phase 4, file 13 of 13.**  
> **Do not start** unless the gate in `00-how-to-use-this-pack.md` is passed and files `08`–`12` (or at least `08`, `09`, and `10`) are done.  
> Foundations for this file: `06-gen-ai-foundations-for-healthcare-ba.md`. Cashless grain: `10-solution-apexcare-cashless-rcm.md`. Identity: `12-solution-citywell-abha-emr.md`.

This is the **apply** file: how Nimbus sells Gen AI use cases, then a full Statement of Work (SOW) pack for a clinical note copilot. Rules (HITL, refuse list, tenant) were file `06`. Do not treat this as day-1 reading.

---

## Use-case catalog (what Nimbus can sell)

Score every idea with the **gate in file 06**. If any box is “no,” it is a demo, not an MVP.

### UC-G01 — Clinical note copilot (scribe)

**How companies do it.** Doctor dictates or the consult is transcribed. LLM drafts SOAP. Doctor **edits and signs**. EMR is the record; the model is not.

**BA FRs (shape).** Draft never auto-final. Show diffs. Allergy field cannot be invented — pull from EMR or mark [MISSING]. Audit: prompt version, model version, user, UHID.

**Out of scope.** Diagnosis the doctor did not confirm. Prescription from the model.

**KPI (illustrative).** Median note time −30%; pre-edit fabricated-med count on golden set is a release blocker.

**Worked BRD:** rest of this file.

### UC-G02 — Cashless pack extraction (IDP + LLM)

**How companies do it.** Intelligent Document Processing (IDP): OCR + extraction from estimates, ID, implant invoices into the HIS checklist (`10-solution-apexcare-cashless-rcm.md`). Coordinator confirms low-confidence fields.

**BA FRs.** Field-level confidence. Human confirm below threshold. Never submit to TPA portal without desk accept. Source PDF stored; extracted JSON stored; both auditable.

**KPI.** Pack assemble time; % fields accepted first time; query rate for “missing implant invoice.”

**Sequence note.** Do not sell this SOW until the cashless **file** exists in HIS. AI on WhatsApp PDFs is wasted.

### UC-G03 — Coding assist (not auto-code)

**How companies do it.** After the **signed** discharge summary, model suggests ICD codes. Clinical coder accepts. RCM submits.

**BA FRs.** Suggestions tied to spans in the note (grounding). No code without coder HITL. Do not optimise for higher ARPOB.

### UC-G04 — RAG on approved SOPs

**How companies do it.** Nursing/quality ask “what is the downtime SOP?” Bot answers with **document title + version + clause**. If retrieval is empty: “I don’t know — ask quality.”

**BA FRs.** Corpus = approved Confluence/SharePoint only. No internet. Citation mandatory. Clinical protocol documents owned by HOD.

### UC-G05 — Patient/attendant chatbot (non-clinical)

**How companies do it.** “Where is TPA desk?” “What is my **financial** status label?” Prep instructions from a **template**, not generated advice.

**Hard stop.** Symptoms, “what does this report mean,” medication changes → scripted redirect to care / emergency number.

### UC-G06 — Internal Nimbus BA copilot

**How the firm does it.** Enterprise Microsoft 365 Copilot / Azure OpenAI tenant. Redacted workshop notes → draft user stories. Label “AI draft.” No production extracts.

---

# Solution pack: ApexCare Clinical Note Copilot (MVP)

**Domain:** Healthcare + Gen AI. **Vendor:** Nimbus Digital (services). **Client:** ApexCare Pune OPD + discharge. **Role:** Vendor BA. **SOW type:** Fixed-price MVP, 12 weeks. **Grain:** Encounter note (not claim, not sample).

Process first, model second.

## Business problem

Doctors finish OPD notes in Word after 20:00 (illustrative). Discharge summaries miss implant lines that TPA later queries (file `10`). CoE demoed a chatbot. Floor need is **draft notes in EMR with HITL**, not a public ChatGPT.

**Baseline (illustrative):** 40% of OPD encounters have no structured diagnosis in HIS same day; median note completion **11 hours** after consult; 3 privacy near-misses last quarter (notes on personal Drive).

## Business objective

12 weeks, 2 specialties (General Medicine, Orthopaedics):

1. **≥ 70%** of in-scope encounters: note **signed in EMR same calendar day**.  
2. Median doctor **edit time on AI draft ≤ 4 minutes**.  
3. **0** auto-saves of unsigned AI text into the legal record.  
4. Pre-edit golden-set: **0** fabricated medications (blocker).  
5. PHI: **0** calls to public LLM endpoints (architecture test).

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| ApexCare COO | H | H | Wants “AI” headline | KPI = same-day notes |
| Medical Superintendent | H | H | Liability fear | HITL BR in writing |
| Doctors (2 specialties) | H | H | Click fatigue | Template + scribe |
| HIM | M | H | Record integrity | Author = doctor |
| DPO | H | H | DPDP | Tenant + consent |
| Nimbus DM | H | H | Date/margin | Freeze out-of-scope chatbot |
| Gen AI CoE | M | H | Accelerator reuse | Eval harness Must |
| HIS vendor | M | M | API | Save-draft vs save-final |
| Patients | L | M | Not in the loop of the note | No patient-facing bot in MVP |

## Scope

**In:** Speech-to-text + LLM draft SOAP for 2 specialties; pull allergies from EMR (do not invent); doctor edit/sign; version/audit; golden-set eval; training; DPO DPIA support.  
**Out:** Patient chatbot, auto ICD submit, auto TPA portal, other specialties, fine-tune on historical notes, open internet RAG, prescribing, image interpretation.

## Assumptions and constraints

**Assumptions:** HIS has encounter draft API or Nimbus stores draft sidecar until sign; doctors have mics; Azure OpenAI (or client-approved equivalent) in allowed region.  
**Constraints:** DPDP; MSA no public LLM; 12-week FP; clinical author is the doctor; NABH record control.

## As-Is / To-Be

**As-Is:** Consult → paper/Word → secretary types next day → diagnosis missing for RCM.  
**To-Be:** Consult → optional dictation → AI draft in EMR → doctor edits → SIGNED → legal record. REJECT returns to blank template.

**Root cause:** Not “lack of AI.” Lack of **same-day structured note** with a tolerable click cost.

## Gap analysis

| Type | Gap | Action |
|---|---|---|
| Process | Note after hours | Same-day sign BR |
| Tech | No draft object | HIS API / sidecar |
| Policy | Unclear authorship | Doctor is author |
| Data | Word on personal Drive | Block; EMR only |
| People | Fear of extra clicks | 8 Must fields (CityWell, file `12`) + draft |
| Eval | Demo only | Golden set in SOW |

## Requirements (excerpt)

| ID | Type | Statement |
|---|---|---|
| FR-AI-01 | F | For an open encounter, user can generate a draft from dictation or typed bullets. |
| FR-AI-02 | F | Draft displays as DRAFT; HIS legal note remains unchanged until SIGN. |
| FR-AI-03 | F | Allergies and known meds are inserted from EMR; if missing, field shows [NOT IN EMR] — model shall not fill them. |
| FR-AI-04 | F | User must ACCEPT (after edit) or REJECT; REJECT discards draft. |
| FR-AI-05 | F | Audit stores: user, UHID, encounter, model id, prompt-template id, timestamps. |
| FR-AI-06 | F | Generation is disabled if the approved AI endpoint is unreachable; user documents manually (fallback). |
| NFR-AI-01 | NF | P95 generate ≤ 8s for ≤ 3 min audio equivalent. |
| NFR-AI-02 | NF | PHI only on approved endpoint; no training on client prompts. |
| NFR-AI-03 | NF | 99.5% availability of fallback (manual note) even if AI is down. |
| BR-AI-01 | BR | Unsigned AI text is not a medical record. |
| BR-AI-02 | BR | Model must not add diagnoses, exams, or meds absent from dictation/EMR. |
| TR-AI-01 | TR | Super-users trained; “REJECT is OK” message in UI. |

## User stories (with AC)

1. **As a doctor, I want a draft from my dictation** so I do not type SOAP from scratch. **AC:** Draft labelled DRAFT; meds not in dictation or EMR appear highlighted as extra.  
2. **As a doctor, I want to sign only after edit.** **AC:** Sign disabled until explicit Accept.  
3. **As HIM, I want the signed author to be the doctor.** **AC:** Record author ≠ “Nimbus AI.”  
4. **As DPO, I want no public LLM.** **AC:** SIT proves traffic only to approved endpoint.  
5. **As DM, I want eval in the sprint.** **AC:** Golden set of 30 de-identified notes; fabricated-med count reported.

## Use case: UC-AI-01 Generate and sign OPD note

- **Actor:** Doctor. **Pre:** Encounter open; consent for recording if required by policy.  
- **Trigger:** Generate draft.  
- **Main:** Dictation → draft → edit → accept → sign.  
- **Alt:** Typed bullets instead of audio.  
- **Exception:** Endpoint down → manual note; AI outage incident. Hallucinated med → doctor deletes; optional feedback flag for CoE.  
- **Post:** Signed EMR note; audit row; draft discarded or archived per policy.

## UAT scenarios

- Happy path sign same day.  
- Invented drug highlighted / removed.  
- Allergy [NOT IN EMR] not auto-filled with “NKDA” unless doctor enters.  
- REJECT: no legal note.  
- AI down: manual path works.  
- Network trace: no public GPT.  
- Patient-in-background audio: policy — pause/consent (DPO).  
- Ortho vs GM template fields.

## RTM (slice)

| Req | Story | UC | UAT |
|---|---|---|---|
| FR-AI-02 | US2 | UC-AI-01 | Sign blocked |
| FR-AI-03 | US1 | — | Allergy |
| BR-AI-01 | US3 | — | Author |
| NFR-AI-02 | US4 | — | Endpoint |
| BR-AI-02 | US5 | — | Fabricated med |

## Change request (sample)

**CR-AI-01:** Patient-facing “explain my report” bot. **Decision:** Out of SOW. New discovery; CityWell privacy rules (file `12`) apply. Do not sneak into MVP.

## Risks

| Risk | P/I | Mitigation | Owner |
|---|---|---|---|
| Doctors ignore drafts | H/H | 2 specialties, MS mandate, measure same-day % | MS |
| Hallucinated findings | H/H | Highlight extras; golden set gate | CoE + BA |
| PHI leak | M/H | Tenant, DPO, SIT | Architect |
| HIS API delay | M/H | Sidecar draft | PM |
| Scope to chatbot | H/M | SOW freeze | DM |

## Final business solution

Nimbus delivers a **HITL note copilot** into ApexCare EMR for two specialties, with audit, fallback, and an evaluation gate. The hospital still owns clinical authorship. Cashless extraction (UC-G02) is the logical **next SOW**, after file `10`’s checklist exists.

**Phasing.** W1–2: DPIA, golden set, HIS contract. W3–8: build. W9–10: silent shadow (drafts not shown as default) + eval. W11–12: UAT, training, go-live hypercare.

## Weak vs strong

| Weak | Strong |
|---|---|
| “ChatGPT for doctors” | DRAFT vs SIGNED, author = doctor |
| Demo on a public model | Approved tenant + SIT on egress |
| No eval | Fabricated-med = release blocker |
| Bot that diagnoses | Redirect; out of SOW |
| This file on day 1 | File `06` + gate + file `10` first |

## Notes

- Gen AI is a **layer**. HIS/EMR remains the record.  
- She will be staffed to write these FRs, not to train models.  
- Expansions: `02-abbreviations-and-full-names.md` section H.  
- Never put real ApexCare notes in a portfolio.
