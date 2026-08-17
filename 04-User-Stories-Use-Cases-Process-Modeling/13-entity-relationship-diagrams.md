# Entity Relationship Diagrams (ERD) for Business Analysts

An **Entity Relationship Diagram (ERD)** shows **business objects** (entities), their **attributes**, and how they **relate** (cardinality). It is the data cousin of a [DFD](10-bpmn-dfd-context-diagrams.md): a DFD shows data *moving*; an ERD shows data *remembered*.

A BA draws a **conceptual / logical** ERD so stakeholders and developers share one meaning of “order,” “claim,” or “appointment.” A DBA or architect turns it into physical tables, indexes, and keys. You already meet this idea in [database fundamentals](../08-SQL-for-Business-Analysts/01-database-fundamentals.md).

## Why it matters

Requirements like “show last payment on the order” fail when payment is not a child of order, or when returns can exist with no order. Interviews will not surface that. An ERD will. ShopEase finance reconciling returns with nullable `order_id` is an ERD problem that looked like an ops complaint.

## Concepts a BA must own

| Term | Meaning | Example |
|---|---|---|
| **Entity** | A thing the business tracks | Customer, Order, Payment, Return |
| **Attribute** | A fact about the entity | `order_status`, `placed_at` |
| **Primary key** | Unique id of one instance | `order_id` |
| **Foreign key** | Pointer to another entity | `orders.customer_id` |
| **Relationship** | How two entities connect | Customer places many Orders |
| **Cardinality** | 1:1, 1:N, M:N | Order has many Payments; Products on Orders need `order_items` |

### Crow’s foot (read it, do not decorate it)

| Notation idea | Meaning |
|---|---|
| One | Exactly one |
| Many (crow’s foot) | Zero or more, unless you mark mandatory |
| Inner bar / circle | Mandatory vs optional (one order **must** have a customer; a customer **may** have zero orders) |

If you cannot say the sentence “one X has many Y,” do not draw the line.

### Conceptual vs logical vs physical

| Level | BA role | Contains |
|---|---|---|
| **Conceptual** | Own it | Entities and relationships in business words |
| **Logical** | Co-own with architect | Attributes, keys, M:N resolved to a junction |
| **Physical** | Review only | Table names, types, indexes, partitions |

If the diagram needs clustered indexes, hand it over. If it still says “customer name is the key,” you have not finished the logical ERD.

## ShopEase (logical, lite)

```text
CUSTOMER 1──< ORDER 1──< ORDER_ITEM >──N PRODUCT
                 │
                 ├──< PAYMENT
                 └──< RETURN  (FK to ORDER and usually ORDER_ITEM)
```

| Rule the ERD forces | Requirement consequence |
|---|---|
| One order, many payment attempts | “Last successful payment” is a rule + query, not a field on `orders` unless you snapshot it |
| Return needs an order (or a stated exception) | Walk-in POS return is a different entity or a dummy order — decide in the FR |
| Product M:N via `order_items` | Qty and line GMV live on the item, not as a comma list |

## ERD vs DFD vs class diagram

| Model | Question it answers | BA trap |
|---|---|---|
| **ERD** | What do we store, and how do things relate? | Drawing screens as entities (`LoginPage`) |
| **DFD** | What data moves between processes and stores? | Using DFD as a UI flow |
| **UML class** | Software structure | BA inventing design patterns |

Use ERD in data workshops with finance and ops. Use DFD when integrations are the fight. Use class diagrams only if architecture asks you to review theirs.

## Collaborating with architects and developers

1. Bring **grain**: “one row = one return request,” not “returns data.”
2. Walk **exceptions**: guest checkout, split payments, partial return.
3. Agree **business keys** (UHID, CIF, policy number) vs **surrogate ids**.
4. Write FRs that name entities: “system records each payment attempt against the order.”
5. Leave physical design (sharding, ORM) to architecture; stay in the workshop until cardinality is agreed.

**Three amigos on data:** BA + developer + QA. QA will ask “can there be two successful payments?” That is an ERD + business-rule question.

## Weak vs strong

| Weak | Strong |
|---|---|
| Boxes copied from screens | Entities with grain and keys |
| M:N as `sku_list` | Junction entity `order_items` |
| ERD only in the DBA’s head | Logical ERD on Confluence, versioned with the FRD |
| BA “not a data person” | BA owns conceptual meaning; DBA owns physical |

## Scenario / Use case: MediCare+ appointment vs slot vs visit

**Context.** Product says “appointment” for booking, reminder, and completed consult. Ops bills a **visit**. The roster has **slots**. The BA writes stories on one word. After go-live, no-show reports double-count cancelled slots, and billing cannot find visits without a booking.

**Stakeholders.** Reception, billing, doctors, EMR vendor, BA, architect.

**What the BA does.**

1. Split entities: **Slot** (calendar capacity), **Appointment** (booking against a slot), **Visit** (care event that may exist without an online appointment — walk-in).
2. Cardinality: Slot 1──< Appointment (optional); Appointment 0..1──Visit; Visit may have no Appointment.
3. Attributes: `no_show` lives on Appointment, not Slot. `billable` lives on Visit.
4. Architect maps to HIS tables; BA writes FRs and reports against the logical model.

**Sample artifact.**

| Entity | One row means | Key |
|---|---|---|
| Slot | One doctor-time capacity | `slot_id` |
| Appointment | One booked hold on a slot | `appointment_id` → `slot_id` |
| Visit | One encounter | `visit_id` → optional `appointment_id` |

**What goes wrong if ignored.** One table called `appointments` stores three concepts. KPIs lie. The BA is blamed for “wrong reports” that were wrong entities.

## Notes

- ERD is solution-assessment work: you are specifying what the solution must remember.
- Conceptual/logical ERD is BA work; physical ERD is not.
- If two teams disagree on a word (order, appointment, claim), they disagree on an entity — draw it.
- Cross-check DFD stores against ERD entities; a store with no entity is a gap.
- Watch: [Lucidchart ERD Part 1](https://www.youtube.com/watch?v=QpdhBUYk7Kk) (~3.4M views), then [create an ERD in Lucidchart](https://www.youtube.com/watch?v=RBZtPhZkUZM).
- 
