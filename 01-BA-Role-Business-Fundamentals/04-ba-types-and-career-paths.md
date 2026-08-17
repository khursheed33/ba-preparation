# Types of Business Analysts and Career Paths

## Types of Business Analysts

### Technical BA

Works closely with IT. Understands systems, APIs, data, integrations, and technical constraints. Writes more detailed technical/functional specs.

### Functional BA

Focuses on how the system should behave for users. Documents features, business rules, screens, and workflows. Less technical than a Technical BA.

### Business / Process BA

Focuses on business processes rather than software screens. Maps As-Is and To-Be processes, finds bottlenecks, and recommends process improvements.

### Product Analyst

Works with product teams. Looks at user behavior, metrics, experiments, and feature impact. Mix of BA and data/product thinking.

### Systems Analyst

Focuses on how systems interact. Studies existing applications, data flows, interfaces, and system requirements.

### IT BA

The title most vendor and in-house IT job ads use. Overlaps Technical + Functional: elicitation, FRD/stories, interfaces, UAT. You sit with delivery, not in a business-only process team. NovaBank “IT BA – digital lending” is this seat.

### Product BA

Sits with a product squad. Backlog, discovery, metrics, and stories more than an 80-page BRD. Close to Product Analyst, but still owns requirement quality and stakeholder alignment. ShopEase “Product BA – returns” reports to the PO, not to a PMO.

### Data BA

Requirements for reports, KPIs, quality rules, and pipelines. SQL, grain, and metric definitions matter more than screen flows. ShieldSure “Data BA – claims MIS” specifies *what* a paid-claim means, not the dashboard colours.

### Agile BA

Same core BA skill, Scrum/Kanban cadence: refinement, AC, three amigos, slice-sized discovery. Not a different profession. If the org is Waterfall, you still do analysis — you just do not call it sprint grooming.

## Other titles you may see

- Salesforce / ERP / Domain BA (Banking BA, Healthcare BA, etc.)
- Business / Process BA (already above) vs “Transformation BA”

Job ads mix these labels. Demonstrate **one** type with a case study; do not claim every title on the list.

## Career paths

A BA can grow in several directions:

1. **Senior BA → Lead BA → BA Manager / Principal BA**
2. **Product Owner / Product Manager**
3. **Project Manager / Delivery Manager**
4. **Consultant**
5. **Domain specialist** (e.g., Banking, Insurance, Healthcare)
6. **Process / Transformation consultant**

## How to choose a path

Early on, focus on core BA skills. Later, choose based on interest:

- Like systems and data → Technical BA / Systems Analyst / Data BA
- Like users and features → Functional BA / Product BA
- Like operations and workflows → Process BA
- Like Scrum delivery → Agile BA (usually the same person as Functional/IT BA)
- Like strategy and market → Product Manager

## Real-world examples of each type

| Type | Where you would sit | Typical artifact |
|---|---|---|
| Technical BA | NovaBank integrations: core banking ↔ bureau ↔ SMS | Sequence of APIs, field mappings, error codes |
| Functional BA | ShopEase returns screens and rules | User stories, AC, field-level behaviour |
| Process BA | MediCare+ clinic check-in | As-Is / To-Be BPMN, bottleneck times |
| Product Analyst | QuickBite “late order compensation” experiment | Metric spec, funnel, recommendation to PO |
| Systems Analyst | ShieldSure policy admin vs claims vs garage network | Interface catalog, data-flow diagram |
| IT BA | Vendor squad on NovaBank digital lending | FRD + stories + UAT pack |
| Product BA | ShopEase returns squad | Discovery notes + ranked backlog |
| Data BA | ShieldSure claims MIS | Metric dictionary + grain rules |
| Agile BA | Same squad, Scrum cadence | Ready stories, three-amigo notes |

**Same company, different BA jobs (ShopEase):** a Functional BA writes the return-status SMS stories; a Technical BA specifies the event `return.qc_passed` on the Kafka topic; a Process BA redesigns seller approval SLA; a Product Analyst checks whether auto-approve hurt repeat-purchase rate.

### Weak vs strong career thinking

| Weak | Strong |
|---|---|
| Applying to every title that says “analyst” | Naming the type you can demonstrate with a case study |
| “I will become PM in six months” with no delivery evidence | Senior BA path first, then PO/PM if you like prioritization or planning |
| Collecting certifications only | One domain + one strong project + core BA method |

## Scenario / Use case: choosing a path after the NovaBank loan case

**Context.** You finished a portfolio case: NovaBank salaried personal loans, cycle time 10 → 4 days (simulated). A recruiter calls with three roles: Technical BA (integrations), Functional BA (digital journeys), Process BA (credit operations). You have SQL and Excel, no Java.

**Stakeholders.** You, the recruiter, hiring managers, your future team.

**What you do.**

1. Map the case to types: you elicited from RMs (functional + process), you wrote a document-checklist FR (functional), you noted bureau API SLA as an NFR (light technical). You did not design the ISO message.
2. Do not fake “Technical BA with API design.” Say: “I specified the *business* behaviour of the bureau pull and the error the user sees. A Technical BA / systems analyst would own the ISO/field map.”
3. Choose Functional BA as the honest first role; keep learning APIs so you can grow into Technical BA.
4. In the interview, show process maps *and* stories so you are not boxed as “only docs” or “only workshops.”

**Sample artifact.** Career one-pager in your portfolio:

| Strength shown in case | Role it supports | Gap to close |
|---|---|---|
| As-Is loan process + SLA | Process / Functional BA | BPMN notation polish |
| FR + AC for document checklist | Functional / Agile BA | Jira hygiene |
| NFR for bureau latency | Technical BA (junior) | Sequence diagrams, error catalogs |

**What goes wrong if ignored.** You accept a Systems Analyst seat, freeze in the first interface workshop, and the team concludes “freshers cannot do BA.” The issue was type mismatch, not intelligence.

## Notes

- Core BA skill is reusable; type is a lens (process, function, system, product, data, agile cadence).
- Early career: pick one type to *demonstrate*, not five titles to *claim*.
- IT BA / Agile BA are usually the same core job on a delivery team; Data BA and Process BA are different seats.
- Domain BA (banking, healthcare, insurance) is a later overlay on these types.
- 
