# Business Communication for Business Analysts

A BA's analysis is useless if it cannot be communicated clearly.

## Business communication

Communication with a business purpose: to understand, clarify, align, and decide.

BA communication includes:

- Meetings
- Interviews
- Emails
- Requirement documents
- Presentations
- Walkthroughs
- Status updates

The audience changes the style. Business users need process and outcomes. Developers need rules, data, and edge cases.

## Professional communication

- Be clear, short, and specific
- Avoid jargon unless the audience uses it
- Confirm understanding; do not assume it
- Stay neutral when stakeholders disagree
- Document decisions after meetings

Weak: "The page should be better."
Strong: "The checkout page should show estimated delivery date before payment."

## Meeting etiquette

Before:

- Know the goal of the meeting
- Share agenda if you are hosting
- Invite only needed people

During:

- Start with purpose
- Keep discussion on scope
- Capture actions, owners, and due dates
- Park off-topic items

After:

- Send notes / decisions / open questions
- Follow up on unanswered items

A BA meeting without notes often has to be repeated.

## Asking effective questions

This is one of the most important BA skills.

### Open questions

Used to explore.

- "Walk me through how a complaint is handled today."
- "What happens if the customer does not receive OTP?"

### Closed questions

Used to confirm.

- "Is email the only way to reset password today? Yes or no?"

### Probing questions

Used to go deeper.

- "You said it takes too long. How long, and in which step?"
- "Who approves this today, and what do they check?"

### Questions that prevent bad requirements

- What is the business problem?
- Who is the user?
- What is in scope / out of scope?
- What is the exception path?
- How will we know this is successful?
- What happens if this fails?

## Workshop and meeting facilitation

**Facilitation** is running the room so the group produces a decision, not so the loudest person wins. You are the process owner of the session; you are not the solution owner.

| Move | Why |
|---|---|
| Purpose line in the invite | “Decide in/out for gold loans; 30 minutes” |
| Timed agenda + parking lot | Protects the thread |
| Round-robin or silent sticky first | Quiet SMEs (psychiatry, night ops) get airtime |
| One question at a time | Open to explore, closed to lock |
| End with owners and dates | Otherwise the workshop was theatre |

Who to invite: 6–8 people who can speak for a role. A 25-person “alignment” meeting is a presentation, not a workshop. Tools and board hygiene: [modeling tools](../06-Jira-Confluence-BA-Tools/05-modeling-tools.md).

## Presentation

A BA presentation is a **decision pack**, not a feature tour.

| Audience | Length | What they need |
|---|---|---|
| Sponsor | 5–8 minutes | Problem, options, recommendation, risk |
| Delivery / three amigos | 12–15 minutes | Rules, exceptions, data, open questions |
| UAT kickoff | 10 minutes | What to try, what “fail” means, RACI |

Structure: context → evidence (one metric) → options → ask. Portfolio talk tracks: [presentations](../15-Portfolio-Building/05-github-website-presentations.md).

## Negotiation (pointer)

You negotiate **options and trade-offs**, not personalities. Techniques and a worked NovaBank example: [stakeholder management for requirements](../02-Requirements-Engineering/11-stakeholder-management-for-requirements.md).

## Communication rule

Listen more than you speak in elicitation meetings. Your job is to understand, not to impress.

## Real-world examples

| Situation | Weak message | Strong message |
|---|---|---|
| ShopEase email to sellers | “We are enhancing returns for a better experience.” | “From 12 Sep, Size returns under ₹2,000 prepaid auto-approve in 4 hours. You will get a dashboard. Opt-out: email seller-ops by 5 Sep.” |
| NovaBank walkthrough with underwriters | Long BRD read-aloud | 12-minute rule table + 4 exception paths + “what we need you to confirm” |
| MediCare+ with doctors | “The system will notify patients.” | “Psychiatry: app only, no specialty name. General medicine: SMS with time + reschedule. Please confirm.” |

### Question types on a live process (NovaBank)

- Open: “Walk me through a salaried file from apply to disbursal.”
- Closed: “Is PAN mandatory before bureau pull — yes or no?”
- Probe: “You said ‘stuck.’ Is that waiting on the customer, KYC, or underwriter?”

### Weak vs strong

| Weak | Strong |
|---|---|
| Meeting with no purpose line | “Decide in/out for gold loans; 30 minutes.” |
| Notes never sent | Decision mail: decisions, owners, dates, open questions |
| Same jargon for COO and developer | Outcomes vs field-level rules |

## Scenario / Use case: MediCare+ workshop that almost produced the wrong SMS

**Context.** 45-minute workshop. Ops wants “SMS everyone.” A psychiatrist says, once, quietly, “Do not put the clinic name in SMS.” The BA is facilitating, excited, filling a whiteboard of features. No parked-question list.

**Stakeholders.** Ops, two doctors (one psychiatry), PO, legal (not invited), BA.

**What the BA should have done.**

1. **Before:** Goal = confirm reminder channels by specialty; agenda shared; legal invited or a follow-up booked.
2. **During:** Open question to each specialty. Closed confirm of consent flag. Probe the quiet comment: “If we cannot name the clinic, what *can* the SMS say?” Capture as a constraint, not a side chat.
3. **After:** Notes within 2 hours: decision table, open question for legal, action: BA to draft rule table by Thursday.

**Sample artifact.** Post-meeting mail (short):

| Type | Item | Owner | Due |
|---|---|---|---|
| Decision | General medicine: SMS 24h + 2h if consent | Ops | Confirmed |
| Decision | Psychiatry: no SMS; in-app generic | Dr. Mehta | Confirmed |
| Open | Legal review of psychiatry app copy | Legal | 21 Aug |
| Action | Draft specialty-suppression table | BA | 20 Aug |

**What goes wrong if ignored.** Transcript or memory drops the one clinical constraint. SMS ships with “Psychiatry follow-up, 9 a.m.” Trust and compliance fail. Communication is not talking more; it is making the quiet requirement loud and written.

## Notes

- Audience first: sponsor = value and risk; user = steps; builder = rules and exceptions.
- Every elicitation meeting ends with decisions, owners, dates, and open questions — or it did not happen.
- Open to explore, closed to confirm, probe to get the number and the exception.
- Facilitation: purpose, timer, parking lot, quiet voices, named owners.
- Presentations ask for a decision; they do not narrate every screen.
- 
