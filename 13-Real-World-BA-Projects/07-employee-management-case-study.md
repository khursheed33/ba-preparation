# EmployeeHub — Messy Leave and Attendance

**Domain:** Employee management / HR. **Company:** EmployeeHub (illustrative HR product used by mid-size employers). **Role:** BA, HRIS Leave & Time.

## Business problem

Leave and attendance are split: biometric punches in a vendor clock, leave in Excel + email, comp-off in WhatsApp. Payroll disputes **~9% of employees/month** (illustrative). Managers approve late. Night-shift plants interpret “optional holiday” differently. Audit cannot reconstruct who was in the building.

## Business objective

In 10 weeks: (1) **100%** leave requests in system (zero Excel for regular leave); (2) payroll leave-discrepancy tickets **≤ 2%**; (3) punch + leave single view for managers; (4) policy interpretation consistent across shifts.

## Stakeholders and analysis

| Stakeholder | Inf | Int | Attitude | Move |
|---|---|---|---|---|
| CHRO / Sponsor | H | H | Compliance | Policy workshop |
| Payroll lead | H | H | Cut-off fear | Calendar rules |
| Plant HR | M | H | Night shift | Shadow |
| Managers | M | H | Email habit | Mobile approve |
| Employees | L | H | Unfair balances | UAT |
| Bio-clock vendor | M | M | API | Punch feed |
| Legal / labour | H | M | Shops & est. | BR |
| IT security | M | M | PII | Access |

## Scope

**In:** leave types, apply/approve/reject, balance, attendance punches ingest, exception (missed punch), comp-off, manager dashboard, payroll export.  
**Out:** recruitment, performance, payroll calculation engine, biometric hardware swap, union rostering AI.

## Assumptions and constraints

**Assumptions:** Clock vendor provides daily punch API; policy can be written in one handbook; employees have mobile or kiosk.  
**Constraints:** 10-week MVP; labour-law style constraints (illustrative); cannot stop clocks; payroll cut-off T-3.

## As-Is process (diagram described)

1. Employee emails manager “casual leave tomorrow.”  
2. Manager replies; HR pastes Excel.  
3. Punches live in clock software; HR VLOOKUPs.  
4. Comp-off WhatsApp to plant HR.  
5. Payroll week: mismatches; tickets; manual overrides.

**Problem analysis:** Three systems of record. Unfairness is a data problem, not a “culture” problem only.

**Root cause (Pareto):** 60% payroll tickets = wrong leave type or missing punch + leave same day. 5 Whys: no single ledger; no overlapping-leave decision table; night HR not a stakeholder.

## To-Be process (diagram described)

1. Employee applies leave (type + dates) in EmployeeHub.  
2. Manager approves in app ≤ 24h (escalation).  
3. Punches ingest nightly; dashboard shows present / leave / absent / exception.  
4. Missed punch request with evidence; HR/manager rule.  
5. Comp-off earned from published extra-day events only.  
6. Payroll file export T-3 with balances frozen.

## Gap analysis

| Type | Gap | Action |
|---|---|---|
| Process | Email leave | In-app workflow |
| Tech | No punch ingest | Vendor API |
| Data | Excel balances | Ledger |
| Policy | Optional holiday tribal | Decision table |
| People | Night HR excluded | RACI 24x7 plant |

## Requirements

| ID | Type | Statement |
|---|---|---|
| FR-LV-01 | F | Employee can apply leave against available balance. |
| FR-LV-02 | F | Manager approve/reject; auto-escalate 24h. |
| FR-LV-03 | F | System ingests punches daily; shows status per employee-day. |
| FR-LV-04 | F | Missed-punch request with reason; dual status. |
| FR-LV-05 | F | Comp-off only from approved extra-day events. |
| FR-LV-06 | F | Payroll export of balances and unpaid days at T-3. |
| NFR-LV-01 | NF | Role-based access; employees see only self + reportees for managers. |
| NFR-LV-02 | NF | Punch ingest complete by 06:00 next day. |

## Business rules

- **BR-LV-01:** Casual and sick cannot overlap same calendar day.  
- **BR-LV-02:** Optional holiday: if plant works, attendance=present or leave; if plant closed, holiday (no leave debit).  
- **BR-LV-03:** Leave + present punch same day → exception queue (not silent).  
- **BR-LV-04:** Negative balance blocked unless CHRO override.

## User stories (with AC)

1. **As an employee, I want to apply leave in the app** so I stop emailing. **AC:** Balance check; confirmation.  
2. **As a manager, I want one queue** of leave + exceptions. **AC:** Approve on mobile.  
3. **As payroll, I want a frozen export T-3.** **AC:** File schema agreed; no Excel paste.  
4. **As plant HR, I want optional-holiday by plant calendar.** **AC:** BR-LV-02.  
5. **As an employee, I want missed-punch request** instead of WhatsApp. **AC:** Status visible.  
6. **As audit, I want who approved what.** **AC:** Immutable log.

## Use case (fully dressed): UC-LV-01 Apply leave

- **Actor:** Employee. **Pre:** Active employee; balance > 0 for type.  
- **Trigger:** Apply leave.  
- **Main:** Type → dates → reason optional → submit → manager pending.  
- **Alt:** Half-day AM/PM.  
- **Exception:** Overlap with existing leave → block with message.  
- **Post:** RequestId; calendar blocked; notification.

## Wireframes

1. My balance. 2. Apply (type, dates, half-day). 3. Manager queue. 4. Day-strip: punch in/out + leave flag. 5. Missed punch form. 6. Comp-off events. 7. Payroll export job. 8. Plant calendar admin.

## Data, reports, KPIs

**Data:** Employee, LeaveType, LeaveRequest, BalanceLedger, Punch, Exception, CompOffEvent, PlantCalendar.  
**Reports:** pending approvals age; exception volume; payroll ticket %; unpaid days.  
**KPIs:** 100% system leave; tickets ≤ 2%; ingest SLA; % exceptions closed before T-3.

## UAT scenarios

- Apply + approve + balance debit.  
- Overlap blocked.  
- Leave + punch same day → exception.  
- Optional holiday plant closed vs working.  
- Escalation 24h.  
- Payroll export freeze.  
- Employee cannot see peer balances.

## RTM

| Req | Story | UC | UAT |
|---|---|---|---|
| FR-LV-01 | US1 | UC-LV-01 | Apply |
| FR-LV-02 | US2 | — | Queue / escalate |
| FR-LV-03 | US2 | — | Day-strip |
| FR-LV-04 | US5 | — | Missed punch |
| FR-LV-06 | US3 | — | Export |
| BR-LV-02 | US4 | — | Optional holiday |

## Change request (sample)

**CR-LV-01:** Union asks shift-swap marketplace. Impact: roster, labour rules. **Decision:** Out of scope; new epic.

## Risks and dependencies

| Risk | P/I | Mitigation | Owner |
|---|---|---|---|
| Clock API incomplete | H/H | File drop fallback | IT |
| Managers ignore app | H/M | Escalation + CHRO | HR |
| Policy fights at plants | M/H | Written calendar owner | CHRO |

**Dependencies:** biometric vendor, payroll file spec, SSO.

## Final business solution

One **ledger** for leave + punches + exceptions; plant calendar as master; decision table for overlaps; payroll consumes export not Excel. Night plants are in RACI. Success = dispute rate and audit trail — not a prettier calendar widget.

## Weak vs strong

| Weak | Strong |
|---|---|
| “Implement HRMS leave module.” | 9% → 2% tickets; BR overlap; punch ingest SLA. |

## Notes

- Employee-management portfolio: policy + time data + payroll boundary.
- Capability gap: night HR must be a stakeholder.
- Illustrative dispute rates only.
