# Lean and Six Sigma Basics for Business Analysts

**Lean** improves flow by removing **waste** (work that does not add value for the customer). **Six Sigma** reduces **variation and defects** using a structured problem method, commonly **DMAIC** (Define, Measure, Analyse, Improve, Control). A BA uses both as **lenses on process**, not as a Black Belt certification.

This sits on top of [process analysis](07-process-analysis.md) and [As-Is / To-Be / gap](08-as-is-to-be-gap-root-cause.md). Lean/Six Sigma names the *kind* of pain; those files show how you map and change it.

## Why it matters

ShopEase “add a returns dashboard” can hide seven wasted handoffs. ShieldSure “hire more adjusters” can hide a measurement problem (cycle time includes weekend, or does not). Lean stops you automating waste. Six Sigma stops you changing a process you never measured.

## Lean: value vs waste

**Value** is what the customer (or next process) would pay for or wait for. Everything else is a candidate for remove, reduce, or control.

### Eight wastes (TIMWOODS) — BA translation

| Waste | Meaning | BA example |
|---|---|---|
| **T**ransport | Moving things with no value | ShopEase return parcel visits seller, then warehouse, then seller again |
| **I**nventory | Piles of work-in-progress | NovaBank “documents pending” queue of 400 files |
| **M**otion | People hunting for information | MediCare+ receptionist flipping three screens for one slot |
| **W**aiting | Idle time | ShieldSure 4-day wait in document verification |
| **O**ver-processing | Extra steps “because we always did” | Dual data entry: Excel + HIS |
| **O**ver-production | Doing more than demanded | Generating 12 reports nobody opens |
| **D**efects | Rework, wrong outcome | Wrong UHID merge; claim paid twice |
| **S**kills (underuse) | Experts doing clerical work | Credit officer retyping PAN from PDF |

You do not need to label every box. You need one or two wastes that explain the metric.

### Flow and pull (lite)

- **Flow:** work moves without batching and re-queues (verify the pack when it arrives, not every Friday).
- **Pull:** start the next step when the next station can take it (do not assign a QuickBite rider before food is actually ready).

To-Be stories should remove a named waste, not add a screen that still waits.

## Six Sigma: variation and DMAIC

**Defect** here is a business failure (late claim, incomplete KYC), not only a software bug.

| DMAIC step | BA work | Output |
|---|---|---|
| **Define** | Problem statement, scope, stakeholders | One metric, one process boundary |
| **Measure** | Baseline: volume, time, % defective | Sample, operational definition of the KPI |
| **Analyse** | Root cause (5 Whys, fishbone, Pareto) | Causes you can act on |
| **Improve** | To-Be, rules, system slice | Requirements + process change |
| **Control** | How we keep the gain | Report, SLA, audit sample, alert |

If you jump from Define to Improve, you are guessing. That is how “AI chatbot” appears in a BRD with no Measure.

**Sigma** language (defects per million) is optional. Sponsors care that you **defined the defect**, **measured it**, and **will re-measure** after change.

## Lean vs Six Sigma vs “process improvement”

| | Lean | Six Sigma | Generic improvement |
|---|---|---|---|
| Primary question | Where is waste / wait? | Where is variation / defect? | What should we change? |
| Typical tool | Value stream, wastes, flow | DMAIC, operational definition, control | As-Is / To-Be, gap |
| BA trap | Relabelling delays as “waste” with no time on arrows | Fake precision (3.4 sigma) with no data | New fields, same queue |

Use Lean when the map is full of waits and rework. Use DMAIC when leadership argues about the number. Use both on ShieldSure claims: Lean for the 4-day wait; Six Sigma for “what counts as a complete pack.”

## Weak vs strong

| Weak | Strong |
|---|---|
| “We will apply Lean Six Sigma” on a slide | Named waste: waiting in verification; DMAIC Measure: 30-case sample |
| Automate the As-Is | Remove dual intake, then automate |
| Control = “people should be careful” | Control = completeness checklist + 1-day SLA + weekly % first-time-complete |
| TIMWOODS poster in Confluence | Two wastes tied to the KPI in the BRD |

## Scenario / Use case: ShieldSure claims — waste then DMAIC

**Context.** Average time to first decision is 9 days. Ops wants a new claims portal. Sampling (Measure) shows **document verification wait is 4 days**. WhatsApp photos never reach the case file (defect + over-processing).

**Stakeholders.** Policyholder, doc-verification team, adjuster, PO, BA, compliance.

**What the BA does.**

1. **Lean.** Label wastes: waiting (queue), defects (incomplete pack), over-processing (WhatsApp + email ZIP).
2. **Define.** Defect = pack not complete at first verification; metric = % first-time-complete and verification cycle time.
3. **Measure.** 30-case sample; operational definition: “complete” = FNOL + photos + bill, in the case file, not in a personal chat.
4. **Analyse.** Fishbone: intake channel, unclear checklist, batching on Fridays.
5. **Improve.** Customer upload with required-doc list; verification SLA 1 business day (see process analysis file).
6. **Control.** Weekly dashboard: % complete packs; alert if wait > 1 day.

**Sample artifact.**

| Lens | Finding | Requirement / rule |
|---|---|---|
| Waste | Waiting 4 days | To-Be: verify within 1 business day of complete pack |
| Defect | Photo not in file | FR: upload attaches to claim ID; WhatsApp is not a source of truth |
| Control | Gain must stick | Report: first-time-complete %; owner: claims ops lead |

**What goes wrong if ignored.** A portal emails the same ZIP to the same queue. Lean was a buzzword. DMAIC never left Define.

## Notes

- Lean/Six Sigma for BAs is vocabulary + discipline, not a belt exam.
- Name the waste; put time on arrows; define the defect before you write stories.
- DMAIC Control is how you avoid “we went live and stopped looking.”
- Software is one Improve lever; checklist, SLA, and intake channel are others.
- Watch: [fishbone / Ishikawa](https://www.youtube.com/watch?v=itpF2Yknjwk). More lectures: [roadmap.md](../roadmap.md#youtube-lectures-curated).
- 
