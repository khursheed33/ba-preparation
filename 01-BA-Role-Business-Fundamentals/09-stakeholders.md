# Stakeholders

## Who is a stakeholder?

Anyone who is affected by the project, can influence it, or has an interest in the outcome.

Stakeholders are not only senior managers. They include users, customers, IT, legal, operations, vendors, and sometimes regulators.

## Why this matters for a BA

If you miss a stakeholder, you miss requirements. Missed requirements often appear late as change requests or production issues.

## Stakeholder identification

Find who should be involved.

Ask:

- Who uses the current process?
- Who owns the process?
- Who pays for the project?
- Who builds and supports the system?
- Who can block or approve the change?
- Who is affected after go-live?

Common groups:

- Sponsor / business owner
- End users
- Product Owner
- Project Manager
- Developers and architects
- QA
- Operations / support
- Legal / compliance
- Vendors
- Customers (sometimes)

## Stakeholder analysis

Understand each stakeholder's:

- Role
- Interest (how much they care)
- Influence (how much power they have)
- Expectations
- Attitude (supportive, neutral, resistant)
- Information they need

## Stakeholder mapping

A common map is the **Influence vs Interest** grid:

| | High interest | Low interest |
|---|---|---|
| **High influence** | Manage closely | Keep satisfied |
| **Low influence** | Keep informed | Monitor |

Examples:

- Sponsor: high influence, high interest → manage closely
- End users: high interest, maybe medium influence → keep informed and involved
- A distant department: low interest, low influence → monitor only

## RACI matrix

**RACI** says who does the work vs who owns the outcome.

| Letter | Meaning | Rule |
|---|---|---|
| **R**esponsible | Does the task | Can be several people |
| **A**ccountable | Owns the outcome; one “yes” | **Exactly one A** per task |
| **C**onsulted | Two-way input before the decision | Interviews, workshops |
| **I**nformed | One-way update after | Mail, Confluence, dashboard |

A missing A is how ShopEase auto-approve ships with “everyone thought product signed.” Two As is how NovaBank policy fights IT in UAT.

### ShopEase auto-approve (snippet)

| Task | PO | CX | Seller ops | Warehouse | Legal | BA |
|---|---|---|---|---|---|---|
| Scope of auto-approve | **A** | C | C | C | C | R (facilitate) |
| Size/value rules | A | C | **R** | C | C | R (document) |
| Consumer-protection wording | C | I | I | I | **A/R** | C |
| UAT execution | C | I | **R** | R | I | C |
| Go-live sign-off | **A** | C | C | I | C | R (RTM pack) |

Keep RACI to 8–12 rows. A 40-row RACI nobody maintains is wallpaper.

## Communication planning

A **communication plan** is who needs what, in which channel, how often — derived from the stakeholder map, not a generic “weekly status.”

| Audience | Need | Channel | Cadence | Owner |
|---|---|---|---|---|
| Sponsor / PO | Outcomes, risks, decisions | 1-page, steering | Fortnightly | BA + PM |
| Users / sellers | What changes for them | Notice + job aid | Before UAT and go-live | BA + ops |
| Developers | Rules, data, exceptions | Stories, ERD, walkthrough | Refinement | BA |
| Legal / compliance | Constraints, evidence | Short brief + tracked questions | As decisions arise | BA |
| Silent high-influence (core system owner) | Freeze dates, schema impact | Direct ping + decision log | When scope hits their system | BA |

Match **influence vs interest**: manage-closely people get two-way sessions; monitor people get a changelog, not a workshop invite.

## BA communication rule

Do not treat all stakeholders the same. A CEO needs outcomes and risks. A user needs process and screen-level detail. A developer needs rules, data, and edge cases. The plan makes that difference explicit.

## Real-world examples

**NovaBank personal loan — influence vs interest**

| Stakeholder | Influence | Interest | Strategy |
|---|---|---|---|
| Credit head | High | High | Manage closely — owns policy |
| Branch RM | Medium | High | Involve in As-Is and UAT |
| Salaried applicant | Low | High | Research + UAT sample |
| Core-banking owner | High | Medium | Keep satisfied — schema freeze |
| Marketing | Low | Low–Med | Monitor; no silent scope adds |

**ShopEase vs MediCare+ missed-stakeholder pattern**

| Missed person | Missed requirement | Late pain |
|---|---|---|
| ShopEase seller | Notice before auto-approve | Seller revolt, rollback |
| MediCare+ legal | SMS consent by specialty | Incident after go-live |
| NovaBank fraud | Cooling period after mobile change | SIM-swap losses |

### Weak vs strong

| Weak | Strong |
|---|---|
| Stakeholder list = “business + IT” | Named roles, interest, influence, attitude, info need |
| Only the sponsor is interviewed | Users + blockers + compliance + vendor |
| Same slide deck for all | Outcome pack for sponsor; rule table for dev |

## Scenario / Use case: ShopEase auto-approve — the seller who was not in the room

**Context.** Product and CX love auto-approve for Size returns under ₹2,000. The BA interviewed support and warehouse. Sellers hear about it on a marketplace blog two days before UAT. Top seller “UrbanStitch” threatens to pause listings.

**Stakeholders.** CX, PO, warehouse QC, support, sellers (missed), legal, finance (refund leakage), BA.

**What the BA does now (recovery).**

1. Admit the gap: sellers are stakeholders — they fund QC disputes and own inventory.
2. Run a 90-minute seller council: 5 sellers by GMV tier. Capture interest (false Size claims) and influence (they can leave).
3. Update map: UrbanStitch = high influence, high interest → manage closely.
4. Change the requirement: 14-day notice, seller dashboard of auto-approved SKUs, kill switch per seller tier, QC audit sample.
5. Re-approve with seller ops in the RACI.

**Sample artifact.** Stakeholder register row:

| Name / role | Interest | Influence | Attitude | Need from BA | Risk if ignored |
|---|---|---|---|---|---|
| UrbanStitch (seller) | False Size returns | High (GMV) | Resistant | Notice, metrics, opt-out path | Listing pause |
| Warehouse QC | Leakage vs speed | Med | Neutral | Rule table, audit sample | Silent quality drop |

**What goes wrong if ignored.** You “manage closely” only the VP. Users and partners explode at UAT. Missed stakeholders are missed requirements with a face.

## Notes

- If they can block, use, pay, or be hurt, they are a stakeholder — including silent sellers and doctors.
- Influence ≠ interest. A core-system owner may not care about CX copy but can freeze your schema.
- Revisit the map after every major scope change.
- RACI: one A per task; R does the work; C before, I after.
- Communication plan: audience × message × channel × cadence — not one weekly deck for everyone.
- Watch: [RACI explained](https://www.youtube.com/watch?v=1U2gngDxFkc) and [RACI walk-through](https://www.youtube.com/watch?v=TdQQdIF5z8E).
- 
