# AI for Meetings and Research

## Definition

Using AI to **transcribe** meetings, **summarize** them, **extract action items**, and **assist research** — under consent, confidentiality, and a BA who still listens for the sentence that was said once.

## Why it matters

Workshops are where requirements hide. A transcript that drops a clinical constraint is more dangerous than no transcript, because the team trusts the summary.

## Consent and confidentiality

| Rule | Practice |
|---|---|
| Consent | Say at the start: recording/transcription on/off; who will see it |
| Confidentiality | Client names, patients, account numbers do not go to a public model |
| Policy | Use only company-approved meeting AI; doctors and banks often forbid consumer tools |
| Retention | Know where audio lives; delete if policy says so |
| Guests | Vendors and patients may not have agreed to your Copilot |

If one MediCare+ doctor refuses recording, you take typed notes. Do not secretly record.

## Transcript → decision log → open questions

Do not ship “summary bullets” as the artifact. Convert:

```text
Transcript (raw)
  → Decision log (what we agreed, owner)
  → Open questions (unresolved, owner, due)
  → Parking lot (out of scope)
  → Requirement seeds (IDs later)
```

**BA pass on any AI summary:** search the transcript for “don’t,” “except,” “never,” “only if,” “legal,” “compliance.” Those words are where AI summaries fail.

### Action-item extraction

AI is decent at “Rahul to send the API spec.” It is weak at implied actions (“we should probably tell sellers”). You add owners and dates or it is not an action.

## AI-assisted research

Good uses: competitor *public* flows, glossary of domain terms, list of questions to ask ShieldSure claims.

Then **verify**: competitor screens change; IRDAI/RBI text must come from primary sources, not a chatbot paraphrase.

### Weak vs strong

| Weak | Strong |
|---|---|
| Record without saying so | Consent line in the agenda |
| Paste full patient-workshop transcript into ChatGPT | Approved tool or local notes; redact |
| Research = “what is KYC” from the model as FR | Glossary draft + RBI circular + SME |
| Trust action list as complete | BA adds implied actions and the quiet ‘no’ |

## Real-world examples

1. **ShopEase.** AI summary of a returns workshop omits a seller who said “Size is used to dump damaged stock.” That one line becomes a leakage risk.
2. **NovaBank.** Research prompt on “loan TAT benchmarks” invents a competitor number. You label it unverified; you do not put it in the BRD.
3. **QuickBite.** Action extraction lists “build compensation engine” because marketing said it loudly, and drops finance’s “cap leakage at 1.5%.”

## Scenario / Use case: MediCare+ workshop — AI misses a clinical constraint said once

**Context.** 50-minute outpatient reminder workshop. Transcription + auto-summary enabled on an approved tool. Ops talks 70% of the time about SMS templates. Dr. Mehta (psychiatry) says, once, at 00:41:12: “Do not put the specialty or clinic name in SMS for my patients.” Legal is absent. Next day the BA posts the AI summary: “Team agreed SMS 24h and 2h for all confirmed appointments with consent.”

**Stakeholders.** Ops, Dr. Mehta, PO, legal, patients, BA, info-sec.

**What happens.**

1. Stories go to sprint: `SMS body includes clinic name and time`.
2. UAT with a GP clinic looks fine.
3. Psychiatry patients receive “Psychiatry follow-up, Wing B.” Incident. Doctors lose trust in BA.

**What the BA should have done.**

1. **Consent:** announced transcription; offered opt-out.
2. **During:** parked Dr. Mehta’s line on the whiteboard in 10-point font, not only in audio.
3. **After AI summary:** Ctrl+F transcript for “don’t,” “psychiatry,” “SMS.” Restore the constraint.
4. **Decision log:**

| Decision / question | Owner | Notes |
|---|---|---|
| GP clinics: SMS with clinic + time if consent | Ops | Confirmed |
| Psychiatry: no SMS; in-app generic only | Dr. Mehta | Said once; now written |
| Legal review of app copy | Legal | Open — workshop incomplete |

5. **Research:** competitor health apps’ reminder patterns — then verify with legal, not copy.

**What goes wrong if ignored.** The system of record becomes the AI summary. The quiet expert is statistically a footnote. Meeting AI without a BA pass is how missed requirements get a timestamp.

## Notes

- Consent first; approved tools only; no public paste of workshops with PII or client process.
- Pipeline is transcript → decision log → open questions, not “nice bullets.”
- Search for negations and exceptions before you trust a summary.
- Research is a draft glossary and competitor map — verify on primary sources and SMEs.
- Action items need owners and dates or they are decoration.
- 
