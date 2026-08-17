# CRMPulse — Sales Team Losing Leads

**Domain:** CRM. **Company:** CRMPulse (illustrative B2B CRM). **Role:** BA, Sales Operations.

## Business problem

Inside-sales lose **34% of inbound leads** before first connect (illustrative). Leads live in email, WhatsApp, and a spreadsheet. Duplicate accounts. No SLA from form-fill to owner. Marketing blames sales; sales blames “bad leads.” Pipeline coverage is fiction.

**Related examples:** ShopEase seller onboarding leads rotting in a sheet; NovaBank RM referrals never entering the LOS. Same failure: no system of record, no SLA.

## Business objective

8 weeks: (1) **100%** inbound leads in CRM within 5 minutes; (2) first-touch SLA **≤ 30 minutes** business hours; (3) duplicate rate **≤ 5%**; (4) lost-reason coded on 100% of closed-lost.

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| VP Sales | H | H | Sponsor | SLA decide |
| SDRs | M | H | Spreadsheet habit | Shadow + UAT |
| Marketing | M | H | Lead quality | Source taxonomy |
| Sales ops | H | H | Data | Duplicate rules |
| Customer (buyer) | L | M | Slow reply | Mystery form |
| IT / CRM admin | M | M | Fields | Schema |

## Scope

**In:** web-form capture, assignment, duplicate match, activity log, SLA clock, lost reasons, manager dashboard.  
**Out:** CPQ, email sequencer AI, marketing automation rewrite, mobile SDK.

## Assumptions and constraints

**Assumptions:** Form can POST to CRM; email/calendar optional Phase 2.  
**Constraints:** 8 weeks; existing CRMPulse tenant; no new CRM licence.

## As-Is / To-Be (diagrams described)

**As-Is:** Form → email alias → whoever is free pastes Excel → WhatsApp the AE → no log.  
**To-Be:** Form → CRM lead ≤ 5 min → round-robin or territory → SLA 30 min → activities mandatory → won/lost with reason.

**Problem analysis:** Not a “CRM adoption” poster. No system of record, no SLA, no duplicate key.

**Root cause:** 5 Whys — lost leads because no owner. No owner because email is the queue. Email because form never integrated.

## Gap analysis

| Type | Gap | Action |
|---|---|---|
| Process | Email queue | Assignment + SLA |
| Tech | Form not integrated | Webhook |
| Data | No match key | Phone+email match |
| Policy | No lost reasons | Picklist |
| People | SDR paste Excel | Training |

## Requirements, rules

| ID | Type | Statement |
|---|---|---|
| FR-CRM-01 | F | Inbound form creates Lead in ≤ 5 min with source. |
| FR-CRM-02 | F | Auto-assign by territory else round-robin. |
| FR-CRM-03 | F | Duplicate suspected if email or mobile match; block silent create. |
| FR-CRM-04 | F | First activity required to stop SLA clock. |
| FR-CRM-05 | F | Closed-lost requires reason code. |
| NFR-CRM-01 | NF | Form webhook 99.5%; PII encrypted. |

**BR-CRM-01:** SLA 30 min 09:00–18:00 IST; else next business morning. **BR-CRM-02:** Duplicate merge only by sales ops.

## User stories (AC)

1. **As marketing, I want form→CRM** so leads are not mailed. **AC:** Test submit appears ≤ 5 min.  
2. **As an SDR, I want my queue** with SLA colour. **AC:** Red if > 30 min.  
3. **As sales ops, I want duplicate flag.** **AC:** Same email cannot create second lead silently.  
4. **As VP, I want lost reasons.** **AC:** Report by reason.  
5. **As an SDR, I want to log a call** to stop SLA. **AC:** Activity types: call, email, meet.

## Use case (fully dressed): UC-CRM-01 Capture inbound lead

- **Actor:** Website visitor / system. **Pre:** Form live. **Trigger:** Submit.  
- **Main:** Validate → create or flag duplicate → assign → notify SDR.  
- **Exception:** API down → retry queue + marketing alert.  
- **Post:** Lead NEW; SLA started.

## Wireframes

1. Public form. 2. SDR inbox (SLA). 3. Lead detail + log activity. 4. Duplicate review. 5. Lost-reason dialog. 6. Manager SLA dashboard.

## Data, reports, KPIs

**Data:** Lead, Assignment, Activity, DuplicateSuspect, LostReason.  
**Reports:** speed-to-lead; SLA miss; duplicate %; lost reasons.  
**KPIs:** 100% in CRM; 30-min first touch; duplicate ≤ 5%.

## UAT, RTM, CR, risks

**UAT:** form create; duplicate email; SLA colour; lost without reason blocked; webhook retry.  
**RTM:** FR-CRM-01→US1→UC-CRM-01; FR-CRM-03→US3; FR-CRM-05→US4.  
**CR-CRM-01:** Add WhatsApp capture. Impact: channel, PII. **Won’t** 8-week MVP.  
**Risks:** SDRs stay on Excel (H/H — cut spreadsheet access); webhook fail (M/H — retry).  
**Dependencies:** website team, CRM admin, identity of territories.

## Final business solution

Make CRM the **only** inbound queue: 5-min capture, 30-min SLA, duplicates, lost reasons. No AI sequencer until the ledger exists.

## Weak vs strong

| Weak | Strong |
|---|---|
| “Sales must use CRM.” | 34% loss → SLA + webhook + duplicate key. |

## Notes

- CRM portfolio: lead lifecycle, SLA, data quality.
- Illustrative conversion only.
- System of record first, features second.
