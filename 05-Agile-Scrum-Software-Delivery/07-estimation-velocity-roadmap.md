# Estimation, Velocity, and Roadmap

## Definition

**Estimation** is the team's forecast of effort/complexity for a backlog item. **Story points** are a relative unit (often Fibonacci). **Velocity** is completed points per sprint — a **capacity signal**, not a target to game.

A **product roadmap** shows outcomes over time (Now / Next / Later), not a fake Gantt of every story.

**DoR, DoD, and AC** (see also Phase 4 notes) bind estimation to quality: you estimate Ready work, you finish to Done, you prove behavior with AC.

## Why it matters

BAs who force hours create false precision and hide uncertainty. Leaders who treat velocity as a KPI get inflated points and still miss dates. Roadmaps that list 40 features in "Q3" without Now/Next/Later hide trade-offs. Tying DoR/DoD/AC to one story shows how the three gates work together.

## Concepts

### Fibonacci, t-shirt, and hours

| Method | Typical scale | Use |
|---|---|---|
| Fibonacci points | 1, 2, 3, 5, 8, 13 (20+ = split) | Relative complexity + uncertainty |
| T-shirt | XS, S, M, L, XL | Early epics; convert before sprint |
| Hours | Tasks only | Dev breakdown inside a Ready story |

**Why BAs should not force hours:** hours pretend analysis is complete; they compare seniors and juniors unfairly; they push the BA into project-controller mode. The team estimates. The BA clarifies scope so the estimate is about the same story everyone heard.

If finance needs a budget, use range forecasts from velocity, not BA-invented hour sheets per story.

### Velocity as capacity signal, not target

- Use last 3–5 sprints to forecast how much Ready work fits.
- Do not "raise velocity" as a goal — quality and splits will fake it.
- Compare like-for-like: after a team change, reset the signal.
- A drop in velocity after adding AC is often honesty, not failure.

### Roadmap: Now / Next / Later (MediCare+ patient app)

| Horizon | Outcomes (not a task list) | Example slices |
|---|---|---|
| **Now** | Book and manage a visit without calling the clinic | Book slot, cancel with 2h window, SMS confirm |
| **Next** | Reduce no-shows and waiting | Reminders, waitlist, no-show state |
| **Later** | Deeper clinical convenience | Video visit, prescriptions, lab results |

Now is committed enough to staff. Next is likely. Later is directional. Dates are windows, not fake day-level plans.

### Tie DoR / DoD / AC — one story example

**Story:** As a MediCare+ patient, I want to cancel an appointment so that the slot can be reused and I am not marked no-show.

**DoR (ready to estimate and pull):**

- AC written (below).
- Policy confirmed: 2-hour window; late cancel behavior.
- SMS vendor available this sprint or explicitly mocked.
- UI sketch; no open legal issue.

**AC (testable behavior):**

```
Given a confirmed appointment more than 2 hours away
When I cancel
Then status = Cancelled, slot released, I am not a no-show, SMS sent.

Given a confirmed appointment less than 2 hours away
When I cancel
Then I see late-cancel policy and status = Late cancellation.
```

**Estimate:** team points it (e.g. 5) only after DoR. BA does not assign "16 hours."

**DoD:** AC tested on UAT env, SMS or agreed mock, states match the state model, no Sev-1, PO accepts.

Points complete only if DoD is met — not if "code is on a branch."

## Real-world examples

1. **ShopEase:** Velocity used to say "guest checkout + decline handling fit this sprint"; not "we must hit 50 points."
2. **ShieldSure:** T-shirt L on "claims portal" until split; then Fibonacci on verification SLA story.

## Scenario / Use case

### Context

MediCare+ leadership wants a dated Gantt. BA is asked to hour-estimate every story. Velocity is on a dashboard as a target. Cancel story is "Done" without the 2h window (DoD gamed).

### Stakeholders

PO, BA, SM, developers, clinic ops, leadership.

### BA actions

1. Refuse hour-forcing; offer Fibonacci + velocity range for Now.
2. Publish Now/Next/Later roadmap in outcome language.
3. Bind the cancel story to DoR/DoD/AC as above.
4. Explain velocity drop if the team stops counting unfinished work.

### Sample artifact

Roadmap table + the cancel story's DoR/AC/DoD block + forecast: "Now fits ~2 sprints at current velocity 20–24."

### Failure if ignored

Hour estimates become commitments. Velocity inflation. Roadmap promises Later items in Now. Cancel ships; no-shows still rise; UAT fails.

## Weak vs strong

| Weak | Strong |
|---|---|
| BA assigns hours | Team points Ready stories |
| Velocity target | Velocity as forecast band |
| Roadmap = 50 Jira keys | Now / Next / Later outcomes |
| Done = coded | Done = DoD + AC |

## Notes

- Split 13s; do not "average" a 13 into a sprint by optimism.
- T-shirts are for shaping, not sprint commitment.
- Roadmaps change when discovery changes — say so on the page.
- AC without DoR produces surprise estimates in planning.
- DoD without AC produces "technically done" products.
