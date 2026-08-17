# SWOT and PESTLE

**SWOT** is an internal-plus-external scan: Strengths, Weaknesses, Opportunities, Threats. **PESTLE** is an external-only scan: Political, Economic, Social, Technological, Legal, Environmental. A BA uses both to explain *why* a change is needed before writing requirements.

## Why it matters

Teams jump to features. SWOT and PESTLE force a structured look at context. ShopEase expanding into grocery is not “add a category.” NovaBank digital lending is not “build an app.” These techniques turn strategy talk into factors the BRD can cite and a strategy deck can defend.

## SWOT vs PESTLE

| Lens | Focus | Typical question | Output a BA can use |
|---|---|---|---|
| Strengths | Internal, helpful | What do we already do well? | Capabilities to reuse |
| Weaknesses | Internal, harmful | Where do we fail today? | Gaps and constraints |
| Opportunities | External, helpful | What market or regulation opens a door? | Business objectives |
| Threats | External, harmful | What could hurt us if we do nothing? | Risks and NFRs |
| PESTLE | External only | What forces sit outside the org? | Assumptions, legal constraints, market facts |

SWOT mixes inside and outside. PESTLE never lists “our ops team is slow” — that is a Weakness.

## Weak vs strong

| Weak | Strong |
|---|---|
| Strength: good brand. | Strength: ShopEase already has 12M logged-in buyers and last-mile in 40 cities — grocery can ride existing delivery slots. |
| Threat: competition. | Threat: QuickBite and kirana aggregators already promise 15-minute grocery; ShopEase average non-grocery SLA is 2 days. |
| Political: government. | Political: NovaBank digital lending must track RBI digital lending guidelines and state stamp-duty on loan agreements. |
| SWOT that fits any company. | Every bullet names ShopEase grocery or NovaBank lending with a fact, metric, or named competitor. |

## Real-world examples

**ShopEase (e-commerce) — SWOT for grocery expansion**

| | Helpful | Harmful |
|---|---|---|
| **Internal** | S: existing buyer accounts, warehouse network, payment rails, seller onboarding playbook. | W: dry-grocery packaging only; no cold chain; 2-day SLA; returns team not trained for perishables. |
| **External** | O: urban demand for 30–60 min staples; dark-store partners available in 8 metros. | T: QuickBite grocery, kirana apps, and thin margins if spoilage is high. |

**NovaBank (banking) — PESTLE for digital lending**

| Factor | What it means for digital personal loans |
|---|---|
| Political | Priority-sector and financial-inclusion pressure; state vs central rules on recovery practices. |
| Economic | Rate cycles change EMI affordability; unemployment spikes raise NPA risk. |
| Social | Younger customers expect in-app loans; older customers still trust branch RM. |
| Technological | Video KYC, bureau APIs, account aggregator, device fingerprinting are available — and so is fraud. |
| Legal | RBI digital lending, KYC/AML, fair-practice code, data localisation, IT Act consent. |
| Environmental | Paperless journeys reduce branch paper; e-waste and data-centre energy become ESG talking points, not core loan rules. |

**ShieldSure** uses PESTLE before a motor-claim portal: Legal (IRDAI TAT), Social (cashless expectation), Tech (garage network APIs). **MediCare+** uses SWOT before online appointments: Strength = doctor roster; Weakness = walk-in token culture.

## How a BA uses these in a BRD vs a strategy deck

| Artifact | Role of SWOT / PESTLE | Depth | Audience |
|---|---|---|---|
| Strategy deck | Decide *whether* and *where* to play. One slide SWOT, one slide PESTLE, then recommendation. | High-level factors, 4–6 bullets each. | Sponsor, CXO, product. |
| BRD / business requirements | Justify *why this problem* and seed constraints, assumptions, risks. Do not paste the full matrix as requirements. | Factors become numbered assumptions, legal constraints, and risks. | Delivery, compliance, QA. |

**BRD translation examples**

- SWOT Weakness “no cold chain” → constraint: Phase-1 grocery is ambient SKUs only; cold chain is out of scope.
- PESTLE Legal “RBI digital lending” → NFR: loan offer display must show APR, cooling-off, and grievance URL.
- SWOT Opportunity “30-minute grocery demand” → business objective: 60-minute SLA in 8 metros within 6 months.
- PESTLE Tech “bureau APIs exist” → assumption: bureau uptime ≥ 99% or fallback to branch.

A strategy deck *recommends*. A BRD *specifies*. Never copy “Opportunity: grow grocery” as a functional requirement.

## Pitfall: generic SWOT that could apply to any company

If you can paste the same SWOT onto EmployeeHub, TripNest, and NovaBank, it is useless.

| Generic (reject) | Company-specific (keep) |
|---|---|
| Strength: talented people | ShopEase last-mile already does 180k deliveries/day in 40 cities |
| Weakness: legacy systems | NovaBank LOS still requires a branch officer to print Form 16 for every unsecured loan |
| Opportunity: digital growth | Urban ShopEase buyers already search “atta” and “milk” 2.1M times/month with no listing |
| Threat: new competitors | QuickBite grocery live in same 8 metros with 15-minute promise |

**Test:** delete the company name. If the sentence still works, rewrite it.

## Scenario / Use case: ShopEase grocery go / no-go

**Context.** ShopEase CPO wants grocery in Q3. Marketing drafted a SWOT: “strong brand, weak ops, huge market, Amazon.” Legal has not spoken. Delivery ops says 2-day SLA. The BA is asked to “put SWOT in the BRD.”

**What the BA does.**

1. Rebuild SWOT with facts from ops, finance, and seller team — not slogans.
2. Run a light PESTLE: FSSAI labelling, GST on food, cold-chain regulation, urban waste rules for packaging.
3. Strategy deck (6 slides): SWOT, PESTLE, recommendation = **ambient grocery in 8 metros, 60-min SLA via dark-store partners; perishables out of scope.**
4. BRD: in-scope SKU types, SLA, partner integration; out-of-scope cold chain; assumptions on partner capacity; risks on spoilage and QuickBite response.

**Sample BRD traces from SWOT/PESTLE**

| Source | Becomes in BRD |
|---|---|
| W: no cold chain | Constraint CON-GR-01: chilled/frozen SKUs out of scope |
| T: 15-min competitors | Objective: 60-min delivery, not 2-day |
| Legal: FSSAI | NFR: seller must upload FSSAI licence before listing |
| S: existing payments | Reuse ShopEase Wallet and UPI; no new PSP in Phase 1 |

**If ignored.** Engineering builds “Grocery” as another category. Milk is listed, spoils in transit, return cost explodes, FSSAI notice arrives, and the SWOT in the appendix still says “strong brand.”

## Notes

- SWOT = internal + external. PESTLE = external forces only.
- Strategy deck uses SWOT/PESTLE to recommend. BRD uses them to seed constraints, assumptions, and risks — not as requirements.
- Every SWOT bullet must fail the “any company” test.
- Name the company, the metric, the regulator, or the competitor in every cell.
- Translate each factor to one BRD object (objective, constraint, assumption, risk, NFR).
- Grocery SWOT without cold chain and SLA is incomplete. Digital lending PESTLE without RBI is incomplete.
