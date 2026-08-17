# Insurance Domain Primer

## Definition

**Insurance** is a risk-transfer contract: the customer pays **premium**; the insurer promises to pay on a covered **event** under a **policy**. **Underwriting** decides whether to accept the risk and at what price. A **claim** is the request to pay. **Cashless** means the insurer (or TPA) settles the hospital/garage directly within a network, rather than the customer paying first and seeking reimbursement.

ShieldSure in these notes is a general + health insurer with agency and digital channels.

## Why it matters

BAs mix up quote, bind, policy, endorsement, and claim. Then cashless fails at the hospital desk. Leakage (paying what was not covered) and delay (not paying what was) are both failures. Requirements must follow **policy wording + process + network**.

## Business model

| Stream | Idea |
|---|---|
| Premium | Price × exposure; collected up front or instalments |
| Investment income | Float until claims paid |
| Cost | Claims + commission + ops + reinsurance |
| Health cashless | Network hospitals + TPA; control via pre-auth |

Combined ratio (claims + expense / premium) is the health of underwriting — a BA should know the term, not run the actuarial model.

## Key processes (As-Is)

**Policy (new business)**

1. Quote (product, sum insured, medical/vehicle details)
2. Underwrite (STP rules or refer)
3. Payment of premium
4. Bind / issue policy pack
5. Renewal / lapse / reinstatement

**Endorsement:** change mid-term (address, add member) → extra premium or refund.

**Cashless health claim**

1. Hospital raises pre-auth (planned) or intimation (emergency)
2. TPA/insurer checks coverage, waiting period, network, sum insured
3. Approval / query / denial
4. Discharge: final bill vs approved; copay / non-payables
5. Settlement to hospital; customer pays gap

**Reimbursement:** customer pays → submits bills → adjudicate → pay customer.

## Stakeholders and systems

| Stakeholders | Interest |
|---|---|
| Policyholder / patient | Speed, cashless honour |
| Agent / broker | Commission, issuance |
| Underwriter | Risk selection |
| Claims adjudicator / TPA | Leakage vs service |
| Hospital / garage (network) | Approval TAT, payment |
| Actuarial / finance | Reserves, combined ratio |
| Compliance | IRDAI-style conduct, disclosures |

| System | Role |
|---|---|
| Policy admin | Quote, bind, endorse, renew |
| Claims | FNOL, reserve, pay |
| TPA portal | Cashless pre-auth |
| CRM / agency | Partners |
| Document / OCR | Bills, discharge summary |
| Finance | Premium, commission, claim pay |

## Regulations lite

- Product wording and disclosures; cooling-off on some products
- Claim TAT expectations and grievance
- Health: waiting periods, pre-existing, network rules
- Data privacy of medical information
- Intermediary licensing (agents)

BA: do not invent coverage; **trace every FR to a rule in wording or a filed product**.

## KPIs and common BA projects

| KPI | Use |
|---|---|
| Quote-to-bind % | Funnel |
| Underwriting STP % | Speed |
| Issuance TAT | Ops |
| Pre-auth TAT | Cashless experience |
| Claim settlement TAT | Conduct |
| Claim repudiation % | Quality vs harshness |
| Leakage / audit fail | Adjudication |
| Renewal persistency | Book |

**Projects:** digital issuance, cashless pre-auth portal, FNOL app, agency portal, renewal journey, fraud rules, customer claim tracker.

### Weak vs strong

| Weak | Strong |
|---|---|
| “Approve all cashless fast” | States: in-network, waiting period, sum remaining |
| One status: pending | Query vs approved vs denied vs documents |
| Dashboard counts claims × coverages | Distinct claim_id (see BI notes) |
| Ignore TPA | TPA is in the process, not “integration later” |

## Real-world examples

**ShieldSure motor:** cashless garage vs reimbursement; surveyor step in As-Is.

**Health vs term life:** health is high-frequency claims; life is underwriting-heavy, claims rare.

**Travel insurance:** trip dates, geographical scope — different endorsements.

## Scenario / Use case: ShieldSure cashless denied at discharge

**Context.** Pre-auth approved ₹1.8 lakh. At discharge, bill ₹2.4 lakh. Hospital demands full cash. Customer tweets. Ops says “non-payables and copay.” App showed only “Approved.”

**BA work.** FR: show approved amount, exclusions, estimated gap; hospital and customer see the same numbers; query state before discharge. Process: final bill submission SLA. UAT with hospital desk, not only ShieldSure employees. KPI: % cashless with gap surprise.

**If ignored.** Cashless brand promise breaks; grievance spike.

## Notes

- Policy ≠ claim ≠ cashless; learn the three processes separately.
- Underwriting is risk acceptance, not “form fill.”
- Cashless = network + pre-auth + final bill; reimbursement is another journey.
- Trace coverage rules to product wording.
- TPA, hospital, agent are first-class stakeholders.
- KPIs: bind %, pre-auth TAT, settlement TAT, persistency.
- Status models must include query, not only yes/no.
- Medical data is sensitive — access and audit are requirements.
