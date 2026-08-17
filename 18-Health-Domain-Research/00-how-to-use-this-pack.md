# Health Domain Research Pack — Read in This Order

Sequence matters. She must **finish the foundation** (who she is, language, domain, systems, Gen AI rules) **before** companies-as-problems, research drills, or solution use cases. Opening ApexCare on day 1 produces fluent jargon with no HIS vs EMR.

This pack is for a **vendor Business Analyst (BA)** in a **service-based IT firm** that also sells **Generative AI (Gen AI)**. Teaching firm: **Nimbus Digital** (illustrative). She is not on the hospital payroll.

Craft primers (read later, not instead of this sequence): `11-Domain-Business-Knowledge/04-healthcare.md`, `13-Real-World-BA-Projects/04-healthcare-case-study.md`, `14-AI-for-Business-Analysts`.

---

## The rule

| Phase | Files | She may |
|---|---|---|
| **1 — Foundation** | `01` → `06` | Learn role, words, domain, KPIs, tools, Gen AI rules |
| **2 — Industry map** | `07` | Name real companies and what they sell |
| **Gate** | Checklist below | Only then continue |
| **3 — Problems and research** | `08` → `09` | Problems, how to research |
| **4 — Apply** | `10` → `13` | Full solution use cases |

Do **not** skip to `08`, `09`, or `10`–`13` because they look like interview material. They *are* interview material — after the gate.

---

## Phase 1 — Foundation (files 01–06)

Do these **in number order**. Each file assumes the one before it.

| # | File | She is done when she can |
|---|---|---|
| 01 | `01-ba-in-service-organization.md` | Explain vendor BA vs client BA; Statement of Work (SOW); change request (CR); onsite vs offshore |
| 02 | `02-abbreviations-and-full-names.md` | Expand the 40 shorts in drill L; first mention = full name (SHORT) |
| 03 | `03-health-domain-landscape.md` | Name the four processes: access, chart, money, privacy; say the grain (slot vs sample vs claim vs person) |
| 04 | `04-glossary-kpis-regulations.md` | Define occupancy, ARPOB, TAT *with a clock*; DPDP vs NABH vs NABL |
| 05 | `05-tools-and-software.md` | Say what HIS, EMR, LIS, RIS, PACS, RCM are **master for**; Jira is not the hospital |
| 06 | `06-gen-ai-foundations-for-healthcare-ba.md` | HITL, RAG, hallucination, what to refuse; no public ChatGPT with PHI |

**Daily (10 minutes):** file `02` — cover Short, say full name. Do not postpone this to “after use cases.”

---

## Phase 2 — Industry map (file 07)

| # | File | She is done when she can |
|---|---|---|
| 07 | `07-companies-what-they-do.md` | Separate hospital / diagnostics / payer / marketplace / HIS vendor; one KPI each |

This is still **context**, not a BRD. Do not start rewriting Apollo’s app.

---

## Gate — pass before problems and use cases

Cover the answers. If any line fails, go back. Do not open `08`.

1. I work for a services firm. Scope is the **SOW**. Extra Gen AI is a **CR** unless signed.  
2. Hospital Information System (HIS) runs the hospital. Electronic Medical Record (EMR) is the chart. They are not the same job.  
3. Unique Health Identifier (UHID) is the hospital’s person key. Ayushman Bharat Health Account (ABHA) is national and **not** a condition of care in our rules.  
4. National Accreditation Board for Hospitals (NABH) ≠ National Accreditation Board for Testing and Calibration Laboratories (NABL).  
5. Revenue Cycle Management (RCM) and Third Party Administrator (TPA) are money. Laboratory Information System (LIS) is samples.  
6. Turnaround Time (TAT) without start/stop events is not a KPI.  
7. Digital Personal Data Protection (DPDP) Act is the India privacy constraint. Do not paste HIPAA into an Indian BRD as if it were the law.  
8. Large Language Model (LLM) drafts. Human-in-the-Loop (HITL) signs. The model is not the author of the record.  
9. I will not paste client Personal Health Information (PHI) or a full Business Requirements Document (BRD) into a public chatbot.  
10. I can expand: SOW, UAT, RTM, FHIR, HL7, DICOM, NHCX, MPI, OCR, RAG, HITL.

---

## Phase 3 — Problems and research (files 08–09)

| # | File | She is done when she can |
|---|---|---|
| 08 | `08-industry-problems.md` | Pick **one** problem, name the grain, name people/process/tech/data/policy |
| 09 | `09-research-methods-and-use-cases.md` | Mystery-shop one public journey; write As-Is; no screens first |

---

## Phase 4 — Apply (files 10–13)

Only after Phase 3. One solution file at a time. 15-minute walkthrough: problem → gaps → one use case → RTM.

| # | File | Company | Grain |
|---|---|---|---|
| 10 | `10-solution-apexcare-cashless-rcm.md` | ApexCare Hospitals | Claim / cashless |
| 11 | `11-solution-helixlab-sample-tat.md` | HelixLab Diagnostics | Sample / TAT |
| 12 | `12-solution-citywell-abha-emr.md` | CityWell Clinics | Person / UHID / consent |
| 13 | `13-solution-nimbus-genai-note-copilot.md` | Nimbus (vendor) for ApexCare | Gen AI note copilot + catalog |

Numbers in solution files are **illustrative**. Do not claim employment at a named chain.

Related teaching case (appointments grain): `13-Real-World-BA-Projects/04-healthcare-case-study.md` — after file 10, not before file 03.

---

## Study calendar (matches the sequence)

45–60 minutes on weekdays.

| Days | Phase | Work |
|---|---|---|
| 1 | 1 | File 01 (role) + file 02 sections A–C |
| 2 | 1 | File 02 D–F + file 03 landscape |
| 3 | 1 | File 02 G–H + file 04 KPIs/regs |
| 4 | 1 | File 05 tools + file 02 confusable pairs |
| 5 | 1 | File 06 Gen AI foundations + drill L |
| 6 | 2 | File 07 companies. **Then sit the gate.** |
| 7 | 3 | File 08 — one problem only |
| 8 | 3 | File 09 — one mystery-shop As-Is |
| 9–10 | 4 | File 10 ApexCare walkthrough |
| 11 | 4 | File 11 HelixLab **or** file 12 CityWell (not both in one day) |
| 12 | 4 | File 13 Nimbus Gen AI solution. Mock: 1-page SOW problem as Nimbus BA |

If the gate fails on day 6, **repeat days 1–5**. Do not “make up time” on ApexCare.

---

## Ethics (every phase)

- Public research on real companies is allowed. Fake tenure is fraud.  
- No hospital BRDs, HIS configs, or patient data in a portfolio.  
- She does not invent clinical protocols or ICD codes.  
- Consent, audit, wrong-patient chart are functional.  
- Gen AI: enterprise tenant + redaction only.

## Weak vs strong

| Weak | Strong |
|---|---|
| Open file 10 on day 1 | Gate → one problem → one solution |
| Memorise company slogans | Map each company to a process and a KPI |
| Memorise abbrs after use cases | Full name (SHORT) from day 1 |
| “We’ll add ChatGPT” | HITL, tenant, eval, fallback, SOW line |

## Notes

- Folder order **is** the syllabus.  
- MediCare+ (roadmap folder 13) = appointments. ApexCare = money. HelixLab = samples. CityWell = identity. Nimbus copilot = Gen AI on the chart.  
- A fluent BRD that is out of SOW is still a failure in a services firm.
