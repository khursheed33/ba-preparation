# As-Is, To-Be, Gap, and Root Cause

## Definition

**As-Is** is the current process as it actually runs. **To-Be** is the designed future process. **Gap analysis** lists what must change (people, process, tech, data, policy) to move from As-Is to To-Be. **Root cause analysis (RCA)** finds why a problem exists, not only where it shows up. **5 Whys** drills a chain of causes. **Fishbone (Ishikawa)** groups causes by category. **Business process improvement** is the change program that closes gaps after causes are known.

## Why it matters

Jumping to To-Be screens without As-Is misses workarounds. Listing gaps as "need a portal" without RCA rebuilds the same delay. 5 Whys without evidence becomes storytelling. A BA pairs narrative, step tables, and cause tools so solutions match the real constraint.

## Concepts

### Gap list dimensions

| Dimension | Question | ShopEase returns example |
|---|---|---|
| People | Skills, roles, capacity | Sellers have no returns owner after 6 p.m. |
| Process | Steps, SLAs, handoffs | Buyer emails support; no RMA |
| Tech | Systems, integrations | No seller dispute screen |
| Data | Fields, quality, history | Reason codes free text; cannot report |
| Policy | Rules, eligibility | 14-day window not enforced; goodwill chaos |

### 5 Whys

Ask "why" until a **actionable** cause appears (usually process/policy/system), not a person to blame. Stop when a change would prevent recurrence. Record evidence at each why.

### Fishbone / Ishikawa

Draw the problem at the head. Bones are categories (classic: People, Process, Systems, Data, Policy, Environment — adapt to the domain). Use for messy problems with multiple contributing causes (no-shows, not a single broken field).

## Real-world examples

1. **NovaBank:** As-Is branch KYC vs To-Be digital KYC; gap in policy (video KYC allowed?) before any app story.
2. **QuickBite:** 5 Whys on "cold food" may land on restaurant ready-time, not rider speed.

## As-Is vs To-Be: ShopEase returns (narrative + steps)

**As-Is narrative:** Buyer messages support. Agent asks for photos in chat. Ticket waits for a seller who replies on email. Refund is a manual wallet credit. No RMA. Warehouse sometimes receives parcels with no case id.

**To-Be narrative:** Buyer starts return in Order Details. System creates RMA. Seller accepts or disputes in 48 hours. Support only handles disputes. Refund follows original payment on warehouse scan (or policy-defined point).

| Step | As-Is | To-Be |
|---|---|---|
| 1 | Buyer contacts support | Buyer submits return in app (14-day check) |
| 2 | Agent requests photos ad hoc | Photos required by reason code |
| 3 | Seller emailed informally | Seller inbox with 48h SLA |
| 4 | Agent decides refund | Auto-accept or support override |
| 5 | Manual wallet credit | Refund to original method + RMA |

### Gap list (returns)

- People: train sellers on 48h SLA; support becomes exception-only.
- Process: introduce RMA and dispute clock.
- Tech: buyer wizard, seller inbox, warehouse scan.
- Data: structured reason codes; photo store linked to RMA.
- Policy: 14-day rule; used-item dispute standard.

## 5 Whys worked example: "refunds delayed"

**Problem:** ShopEase buyers wait 12 days for refunds (target 5).

1. **Why?** Refund is triggered only after a manual finance batch on Fridays.  
2. **Why?** Finance does not trust item-received flags.  
3. **Why?** Warehouse scan does not update the case; agents type "received" in comments.  
4. **Why?** Returns have no RMA barcode on the packet.  
5. **Why?** The return request never created a structured case id — only a support ticket.

**Root cause to act on:** No structured RMA linking request → parcel → refund (process + tech + data).  
**Not the root:** "Finance is slow" (symptom of distrust in data).

## Fishbone categories: MediCare+ appointment no-shows

**Head:** High no-show rate for first visits.

| Bone | Example causes |
|---|---|
| People | Reminder not in patient's language; elderly patients without app |
| Process | No confirm-24h call; booking too far out with no reconfirm |
| Systems | SMS fails silently; calendar not updated after clinic cancel |
| Data | Wrong phone number; duplicate patients |
| Policy | No fee for late cancel; easy overbooking |
| Environment | Traffic / clinic hard to find (address not in SMS) |

Do not pick one bone and ignore others. A reminder SMS (systems) fails if the number is wrong (data).

## Scenario / Use case

### Context

ShopEase wants a "returns portal" because refunds are delayed. Leadership assumes a UI gap only.

### Stakeholders

Buyer, seller, support, warehouse, finance, PO, BA.

### BA actions

1. Document As-Is with a step table and wait times.
2. Run 5 Whys on delayed refunds with finance + warehouse evidence.
3. Build gap list across five dimensions; draft To-Be steps.
4. Sequence stories: RMA + scan before pretty portal chrome.

### Sample artifact

One-pager: As-Is table, To-Be table, gap list, 5 Whys chain, proposed first slice (RMA barcode).

### Failure if ignored

A portal that still emails finance a spreadsheet. Refunds stay weekly. No-shows at MediCare+ get an app redesign while phone numbers stay wrong.

## Weak vs strong

| Weak | Strong |
|---|---|
| To-Be = more screens | To-Be = new handoffs, rules, and data |
| Gap = "need IT" | Gap by people/process/tech/data/policy |
| 5 Whys blaming a team | 5 Whys to a preventable system cause |
| Fishbone as art | Fishbone with evidence on each bone |

## Notes

- As-Is must be validated; SOPs lie.
- Close one critical gap first (RMA link) rather than boiling the ocean.
- 5 Whys needs a single problem statement and metrics.
- Fishbone is for multiple causes; 5 Whys for a linear chain — you can use both.
- Improvement is not complete until the gap owner and measure are named.
