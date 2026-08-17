# Meeting Minutes, Workshop Notes, and Decision Logs

If it is not written the **same day**, it did not happen. Memory is a conflict generator.

This file covers **meeting minutes**, **requirement workshop notes**, and **decision logs** — three artifacts with different jobs.

## Why it matters for a BA

QuickBite’s delivery SLA workshop will produce three versions of “late” by Wednesday if you wait until Friday to type notes. Finance will swear they never agreed to restaurant-caused delay. The BA is the memory of the program.

## Meeting minutes

Minutes record **a meeting**: attendance, agenda, facts shared, decisions, actions. They are not a transcript and not a requirements catalog.

### Template

- Title, date, time, location/tool
- Attendees / absentees
- Purpose (one sentence)
- Agenda items
- Discussion summary (short; facts vs opinions labelled if needed)
- Decisions (or “none — see parking”)
- Action items: owner, date, ID
- Next meeting
- Author and distribution list
- Link to recordings / slides / requirement IDs touched

### Filled example — QuickBite delivery SLA workshop

**Title:** Delivery SLA and compensation — workshop 1  
**Date:** 14 Jul 2026, 10:00–12:00 IST, Meet  
**Author:** BA (Delivery Experience) — minutes issued 14 Jul 17:40  
**Attendees:** Ops lead (R. Nair), Logistics (S. Banerjee), Restaurant partnerships (A. Kapoor), Finance (P. Desai), Support lead (N. Joseph), Product (M. Shah), Data (K. Menon), BA  
**Absent:** Legal (sent comments on SOP v1.4 by mail)  
**Purpose:** Agree how “late” is defined and who bears compensation cost.

**Agenda**

1. Current SOP v1.4
2. Data: 500 compensated orders
3. Proposed cause rules
4. Customer-facing vs cost-allocation

**Discussion (summary)**

- SOP uses promised customer time only; reason code defaults to RIDER_DELAY (fact: support form).
- Data: 61% of compensated orders had restaurant accept > 8 min (fact: K. Menon pack).
- Partnerships: restaurants will reject a tablet SLA that auto-cancels (opinion → to be tested).
- Finance: customer goodwill and partner cost must be separate ledgers (position).

**Decisions** (full text also in decision log DL-DLV-04)

- D1: Customer compensation still based on promised time (unchanged for this release).
- D2: Cost allocation uses delay cause from timestamps, not agent dropdown.

**Actions**

| ID | Action | Owner | Due |
|---|---|---|---|
| A-12 | Draft BRULE-DLV-12 (8-min accept) | BA | 16 Jul |
| A-13 | Mock support form without RIDER default | Product | 21 Jul |
| A-14 | Legal review of restaurant communication | Partnerships | 23 Jul |

**Reqs touched:** BR-DLV-04, FR-DLV-22, FR-DLV-23 (draft).

**Weak minutes:** “Discussed SLA. Team aligned. Follow up later.”
**Strong minutes:** the table above, issued the same day.

## Requirement workshop notes

Workshop notes are **working papers** for elicitation: richer than minutes, not yet the FRD.

Include:

| Zone | What goes there |
|---|---|
| Process / model | As-is steps, times, systems |
| Candidate requirements | Raw statements, later typed |
| Business rules heard | With source if given |
| Parking lot | Off-topic but valuable |
| Open questions | Who will answer |
| Parking decisions | “Not deciding today” with why |
| Conflicts | Two quotes, not smoothed |

### Parking lot vs open questions vs parking decisions

| | Parking lot | Open question | Parking decision |
|---|---|---|---|
| Meaning | Topic we will not solve in this room | Missing fact | We *choose* not to decide yet |
| Example | New Year’s Eve surge pricing | What is current tablet accept p95? | Whether to auto-unassign restaurant after 8 min — wait for legal |
| Follow-up | Backlog or later workshop | Named owner + date | Date when we must decide |

If you dump everything in parking, nothing moves. If you force a decision with no data, you fake alignment.

**QuickBite snippet**

- Parking lot: rider tips feature (out of SLA scope).
- Open question: Q-19 — is 8 minutes measured from placed_at or from restaurant online_at? Owner: Data. Due: 16 Jul.
- Parking decision: PD-03 — auto-reject of late restaurant accept deferred until partnerships legal review (A-14).

## Decision log

A **decision log** is the durable record of **choices that bind requirements**. Minutes can be forgotten; the log is cited in the FRD.

### Template fields

| Field | Purpose |
|---|---|
| Decision ID | DL-DLV-04 |
| Decision (one sentence) | What we will do |
| Date | When |
| Owner / approvers | Names |
| Context | Why it came up |
| Alternatives considered | A/B/C |
| Impact | Reqs, cost, risk, people |
| Revisit date | If time-boxed |

### Filled example — QuickBite

| Field | Content |
|---|---|
| ID | DL-DLV-04 |
| Decision | Compensation **cost** is allocated by delay cause from order events. If `restaurant_accepted_at − placed_at` > 8 minutes, cause = RESTAURANT (no rider penalty). Customer-facing compensation remains based on promised delivery time for this release. |
| Date | 14 Jul 2026 |
| Owner | Product M. Shah; Finance P. Desai; Ops R. Nair |
| Alternatives | (A) All late = rider (status quo) (B) All late = restaurant (C) Split by timestamps — adopted |
| Impact | New BRULE-DLV-12; support form FR-DLV-22; finance ledger split; restaurant comms A-14. Does *not* change customer voucher rule this release. |

NovaBank analogue: DL-UPI-07 hybrid maker-checker above ₹25,000 (see stakeholder file). Same fields.

MediCare+: DL-APT-02 — reminder SMS shall not include diagnosis (NFR-REM-S01). Alternatives: include department vs include doctor only — doctor + clinic name adopted.

## Why the same day

- Stakeholders forget and rewrite history.
- Action dates slip if not mailed.
- You will mix two meetings in your head.
- Developers start coding from hallway talk before your FR exists.
- Legal asked for “what was agreed” — yesterday’s minutes are evidence; next week’s essay is not.

Target: draft in 2 hours; send within 8 hours; corrections via reply within 24 hours, then freeze.

If a decision is reversed, do not edit history silently. Add DL-xx v2 or a new ID that supersedes, with a pointer.

## Weak vs strong set

| Weak | Strong |
|---|---|
| No minutes, Slack “thanks everyone” | Minutes + workshop pack + DL IDs |
| Transcript dump | Structured zones + actions |
| Decisions only in BA’s notebook | Log everyone can read |

## Notes

- 
