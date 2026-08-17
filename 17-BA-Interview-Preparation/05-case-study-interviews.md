# Case-Study Interviews

## Definition

A live **case** (often 20–30 minutes, whiteboard or shared doc) on **requirements**, **process improvement**, **product**, **data analysis**, **business problem solving**, or **root-cause analysis**.

They want a **method**, not a hidden “right app.”

## Why it matters

Cases mimic the job: ambiguous prompt, time box, no full data. A structured BA beats a candidate who jumps to screens.

## How to run a 20–30 minute case (whiteboard)

| Min | What you do |
|---|---|
| 0–3 | Restate the problem; ask 5 clarifying questions; write in/out as *hypotheses* |
| 3–8 | Stakeholders + As-Is (boxes and waits) even if guessed — label assumptions |
| 8–15 | Root cause options; pick one to test; metrics |
| 15–22 | To-Be, 5–8 requirements or stories, 1 NFR, 1 risk |
| 22–28 | Recommendation, rollout slice, UAT idea |
| 28–30 | “What I would verify Monday” |

Say **assumption** out loud. Draw. Talk. Leave a decision log on the board.

### Weak vs strong

| Weak | Strong |
|---|---|
| Instant solution (“build an app”) | Problem, process, evidence, options |
| Silent drawing | Narrated trade-offs |
| 40 features | One slice + out of scope |

---

## Practice case 1 — Requirements (ShopEase checkout drop-off)

**Prompt.** “Mobile checkout abandonment is 42%. What requirements do you write?”

**Approach (not the only answer).**  
Clarify guest vs logged-in, COD vs prepaid, India constraints. Stakeholders: buyer, payments, finance, legal. Do not start with Apple Pay. Sample FRs: guest checkout ≤ 4 steps; payment errors named; COD not default if that is the finding. NFR: p95 load. Out: Apple Pay this quarter. UAT: first-time guest on 4G.

## Practice case 2 — Process (NovaBank branch password reset)

**Prompt.** “Customers visit branch to reset password. Calls are high. Improve the process.”

**Approach.** Map As-Is (2-day token). Waits: branch slot, print, CIF mobile missing. Options: SMS OTP vs video KYC vs keep branch for exceptions. Recommend OTP if mobile on CIF ≥ 72 hours; branch remains for no-mobile. Risks: SIM-swap. Requirements: attempts, expiry, lock. Do not skip info-sec.

## Practice case 3 — Product (QuickBite late orders)

**Prompt.** “Should we launch a compensation engine this quarter?”

**Approach.** Product case = value vs cost vs scope. Split kitchen vs rider delay (ask for data). If 70% kitchen, a generic engine leaks money. Recommendation: rider-after-ready only, leakage cap 1.5% GMV, one-city pilot. Success metric: tickets and repeat rate, not “engine launched.”

## Practice case 4 — Data (MediCare+ no-shows)

**Prompt.** Here is a pivot: no-shows by clinic and weekday. What do you recommend?

**Approach.** Check filters (cancelled vs no-show). Find the hotspot (e.g. Monday 9 a.m. specialists). Do not SMS psychiatry without a rule. Next query: consent rate. Recommendation: 24h+2h reminder pilot on the hotspot clinic, then expand. Insight card: question, evidence, action, caveat.

## Root-cause mini case (ShieldSure claims TAT 14 days)

**Prompt.** “Why are claims slow? We think the portal is old.”

**Approach.** Treat “old portal” as a hypothesis. Sample 50 claims. Count delay hours by cause (incomplete FNOL, garage network, surveyor, downtime). Five Whys on the biggest bucket. Problem statement with evidence, **no portal inside it**. Requirements may be photo guidance and a longer upload link — cheaper than a new portal.

## Business problem solving (generic wrapper)

Always: problem vs solution; goal/objective; value; options; recommend; communicate; document. Same spine as scenario interviews.

## Real-world examples of case failure

- Building a MediCare+ “super app” in 20 minutes with no consent.
- Using fake industry numbers as facts (“RBI says 3 days”) — say *assumption*.

## Scenario / Use case: they give you a blank board and “QuickBite is losing users”

**Context.** 25 minutes, two observers, no data file.

**What you do.** Clarify: losing new vs repeat, city, channel. Assume (stated) Friday-night late delivery. Sketch process. Ask *what data you would pull* (kitchen-ready vs delivered). Offer a pilot, not a platform. Write 5 FRs for the pilot. End with open questions.

**What goes wrong if ignored.** You design a loyalty program because “users” sounded like product marketing. Cases reward the BA who narrows.

## Notes

- 20–30 min: clarify, As-Is, causes, slice, requirements, UAT, verify-next.
- Four practice types: requirements, process, product, data — plus ShieldSure root-cause mini.
- Label guesses; ask for data; keep out-of-scope visible.
- The “right” answer is a defensible approach, not a brand-name feature list.
- 
