# What Are Requirements?

A **requirement** is a documented condition, capability, or constraint that a solution must satisfy so the business gets the intended value.

It is not a wish, not a design, and not a slogan. It is a testable statement of what must be true.

## Why it matters for a BA

If you confuse a need with a feature, or a wish with a specification, the team builds the wrong thing. ShopEase, NovaBank, and MediCare+ all fail the same way: someone says “we need a better checkout / faster KYC / smarter booking,” and engineering starts coding before the need is defined.

The BA’s job is to turn vague talk into statements the business can approve and the team can build and test.

## Need, requirement, specification, feature, wish

These words get mixed in meetings. Keep them separate.

| Term | Meaning | Example (ShopEase) |
|---|---|---|
| Need | The business problem or outcome people care about | Reduce checkout drop-off so more carts become orders |
| Requirement | A condition the solution must meet | Guest checkout must complete in 4 steps or fewer |
| Specification | Precise, buildable detail of that requirement | Guest checkout: phone + OTP, address, payment; no account creation |
| Feature | A chunk of product capability | Guest checkout |
| Wish | A preference with no owner, measure, or constraint | “Make checkout delightful” |

**Need** answers *why*. **Requirement** answers *what must be true*. **Specification** answers *how precisely we will define it for build*. **Feature** is a product packaging of capabilities. **Wish** is unowned opinion.

### Weak vs strong

| Weak | Strong |
|---|---|
| We need a better checkout. | Reduce checkout abandonment from 42% to under 28% in 90 days for mobile web. |
| Add wallet. | Registered ShopEase buyers can pay using ShopEase Wallet if balance covers the payable amount. |
| Make it user-friendly. | First-time guest checkout completes in ≤ 4 screens; error messages name the field and the fix. |

## Requirement vs solution

A **requirement** states the needed capability or constraint. A **solution** is one way to satisfy it.

- Requirement: ShopEase buyer must be able to pay without creating an account.
- Solution A: guest checkout with OTP.
- Solution B: “Buy as guest” plus optional account after payment.
- Solution C: social login only (this may *not* meet the requirement if the buyer has no social account).

If you write the solution too early, you lock the team into one design and miss cheaper options.

NovaBank example: the *need* is “customers locked out of net banking can regain access without visiting a branch.” The *requirement* is “retail customers can reset password using registered mobile OTP within 10 minutes.” The *solution* might be SMS OTP, or app-based reset, or video KYC — those are design choices, not the requirement.

## Business language vs system language

| Layer | Language | Who speaks it | Example |
|---|---|---|---|
| Business | Outcomes, policy, risk, money | Product, ops, legal, finance | “We cannot ship innerwear returns after 7 days.” |
| User | Tasks and pain | Customer, agent, seller | “I don’t want to create an account just to buy one item.” |
| System | Data, rules, interfaces, states | Dev, QA, architects | “Order.status = PAID before inventory is reserved.” |

The BA translates **up and down**. You do not dump system language on a product owner, and you do not leave developers with “make it better.”

MediCare+ example:

- Business: reduce no-shows for specialist clinics.
- User: patient should get a reminder they can act on.
- System: send SMS 24 hours before `appointment.start_time` if `status = CONFIRMED` and `consent.sms = true`.

## Scenario / Use case: ShopEase “we need a better checkout”

**Context.** ShopEase mobile web checkout abandonment is 42%. The product owner (PO) tells the BA: “We need a better checkout. Add one-click pay, wallet, and maybe Apple Pay. Make it like Amazon.” Sellers complain that prepaid orders convert better. Finance wants fewer COD orders. UX has a Figma already.

**Stakeholders.** PO, UX, checkout engineering, payments team, finance (COD cost), customer support (failed payments), legal (RBI e-mandate / card storage), and a sample of buyers.

**What the BA does.**

1. Separate wish from need. “Like Amazon” is a wish. The need is lower abandonment and fewer failed payments without increasing fraud.
2. Elicit current pain: extra account-creation screen, address form on a tiny keyboard, COD as default, wallet not offered until the last step.
3. Refuse to treat the Figma as the requirement. The mock-up is a proposed solution.
4. Write requirements in business language first, then specify behaviour.

**Sample requirement / artifact.**

| ID | Statement | Type |
|---|---|---|
| BR-CHK-01 | Reduce mobile-web checkout abandonment from 42% to ≤ 28% within 90 days of release. | Business |
| ST-CHK-01 | Guest buyers can complete purchase without creating a ShopEase account. | Stakeholder |
| FR-CHK-04 | After payment success, the system creates an order and sends SMS + email confirmation within 60 seconds. | Functional |
| NFR-CHK-02 | Checkout payment page p95 load time ≤ 2.5 seconds on 4G. | Non-functional |

Out of scope recorded in the same session: Apple Pay (not a near-term India priority), one-click card-on-file for guests (PCI + consent not ready).

**What goes wrong if ignored.** Engineering builds “one-click pay” for logged-in users only. Abandonment barely moves because 60% of drop-off is guests. Finance is unhappy because COD is still the default. The PO says “that’s not what I meant,” and the sprint is wasted.

## How a BA should respond in the room

Do not say “sure, we’ll make checkout better.” Ask:

- Better for whom — guest, logged-in buyer, or seller?
- Better measured how — conversion, time, error rate, COD mix?
- What must not break — offers, GST invoice, seller payout?
- What is a constraint — payment gateway, RBI, existing cart service?

Then write the **need**, then **requirements**, then evaluate **solutions**.

## Quick map you can reuse

Need → Requirement → Specification → Feature in backlog → Tests.

Wish stays in a parking lot until it has an owner, measure, and constraint.

## Notes

- 
