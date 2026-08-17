# User Stories

## Definition

A user story is a short, user-centered description of a need: **who** wants something, **what** they want, and **why** it matters. It is a reminder to have a conversation, not a complete specification.

Standard format:

**As a** [persona or role], **I want** [capability], **so that** [business or user value].

## Why it matters

Stories keep work tied to a person and an outcome. Without them, teams build screens and APIs that nobody asked for. A BA uses stories to split work, expose missing users, and write acceptance criteria that testers can check.

## Concepts

### Structure and format: As a / I want / So that

| Part | Question it answers | Weak fill | Strong fill |
|---|---|---|---|
| As a | Who is this for? | user | ShopEase buyer with a delivered order |
| I want | What capability? | returns | start a return from Order Details within 14 days |
| So that | Why does it matter? | convenience | I get a refund without calling support |

Rules:

- One actor, one capability, one outcome per story.
- "So that" must be value, not a restatement of the want.
- Stories are placeholders. Detail lives in acceptance criteria, rules, and examples.

### Persona vs role

| | Role | Persona |
|---|---|---|
| Meaning | Job or system actor | Named, realistic user with goals and constraints |
| Example | Seller, Support agent, Buyer | Priya, 28, sells handmade bags; fears return fraud |
| Use in stories | Fine for access and process | Better when behavior differs inside the same role |

Same role, different personas: a ShopEase power seller and a first-time seller both are "sellers," but return policy needs and UI patience differ. Use the persona when the need is not shared by the whole role.

## Real-world examples

1. **NovaBank:** "As a savings customer, I want to freeze my debit card in the app so that I can stop spend immediately if I lose it." Role is enough; the value is safety, not a pretty freeze button.
2. **QuickBite:** "As a rider, I want a one-tap 'arrived at restaurant' so that the customer sees a real status instead of a stale map pin."

## Good vs bad stories (10 rewrites)

| # | Bad | Why it fails | Strong rewrite |
|---|---|---|---|
| 1 | As a user I want a returns module so that I can use returns. | Generic user; circular so-that | As a ShopEase buyer, I want to request a return from Order Details so that I do not call support for a standard refund. |
| 2 | Build the returns API. | Solution, no user | As a seller, I want to approve or reject a return reason so that I am not auto-refunded for used items. |
| 3 | As a buyer I want everything related to returns. | Epic disguised as story | Split: request return, upload photo, track refund (see scenario). |
| 4 | As admin I want a dashboard. | No outcome | As a support lead, I want open returns older than 48 hours highlighted so that I can assign agents before SLA breach. |
| 5 | As a seller I want the system to be fast. | NFR with no test | As a seller, I want the returns inbox to load in under 3 seconds for 50 open cases so that I can clear them during packing. |
| 6 | As a user I want login so that I can login. | Circular | As a returning buyer, I want to stay logged in on this device for 30 days so that checkout is not blocked by password. |
| 7 | The BA wants a BRD section on returns. | Internal artifact | As a compliance officer, I want every refund to store the original payment method so that we can pass audit. |
| 8 | As support I want to handle all tickets. | Too large | As a ShopEase support agent, I want to see the buyer's return photos on the ticket so that I do not ask the customer to resend them. |
| 9 | As a buyer I want a better experience. | Unmeasurable | As a buyer, I want a 3-step return wizard with progress shown so that I know when the request is submitted. |
| 10 | Developers will add RMA-ID. | Task, not story | As a warehouse operator, I want each approved return to show an RMA barcode so that inbound parcels are matched on scan. |

## Scenario / Use case: ShopEase returns — three stories, not one

### Context

Product asks for one story: "As a user I want returns." ShopEase has three different jobs: buyer starts a return, seller accepts or disputes, support resolves deadlock. One story hides three workflows, three SLAs, and three UIs.

### Stakeholders

Buyer (Priya), seller (Omar), support agent, payments (refunds), warehouse, Product Owner.

### BA actions

1. Split by actor, not by screen.
2. Confirm 14-day window, photo rules, and who pays return shipping.
3. Write three stories plus shared rules (refund method = original payment).
4. Walk QA through each actor's happy and exception path.

### Sample artifact — three stories

1. **Buyer:** As a ShopEase buyer, I want to request a return within 14 days of delivery so that I can get a refund without calling support.
2. **Seller:** As a ShopEase seller, I want to accept or dispute a return within 48 hours so that I am not auto-refunded for items I believe were used.
3. **Support:** As a ShopEase support agent, I want to override a disputed return with a reason code so that the buyer and seller are not stuck after SLA.

Shared business rules (not a fourth "mega story"): refund to original method; no return after 14 days without support override; photos required for "item not as described."

### Failure if ignored

A single "returns" story ships a buyer form only. Sellers never see disputes. Support invents a spreadsheet. Refunds fire automatically. Sellers leave the marketplace.

## Weak vs strong

| Weak | Strong |
|---|---|
| As a user I want returns. | Three actor-specific stories plus shared rules |
| So that it is easy. | So that I get a refund without calling support |
| Role = persona always | Persona when behavior inside the role differs |

## Notes

- If you cannot name the actor, you do not have a story yet.
- "So that" that repeats "I want" is a red flag.
- One story per actor-job; shared rules belong in AC or a rule catalog, not in a mega story.
- Tasks (create table, add endpoint) live under the story; they are not the story.
- Rewrite "the system shall" into As a / I want / So that before sprint planning.
- Watch: [Agile user stories](https://www.youtube.com/watch?v=apOvF9NVguA), [Jeff Patton story mapping](https://www.youtube.com/watch?v=5R1z8POfvgQ), [Given/When/Then](https://www.youtube.com/watch?v=rvgMVcxrV4U).
