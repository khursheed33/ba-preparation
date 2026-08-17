# BA Fundamentals Interview

## Definition

Interview questions on **BA concepts**, **requirements**, **documentation**, **stakeholders**, **processes**, **Agile**, and **SDLC** — answered in the first person with ShopEase / NovaBank evidence.

## Why it matters

This round checks vocabulary *and* whether you have done the thinking. Model answers below are a starting bar, not a script to memorize word-for-word.

## How to use these answers

Speak in **I** (portfolio work). Say **practice case**, never “when I was BA at ShopEase.” After each model answer, a typical **follow-up**.

### Weak vs strong

| Weak | Strong |
|---|---|
| Textbook definition only | Definition + ShopEase/NovaBank example |
| “I would document everything” | Named artifact and who signed it |

## 20 Q&A (model answers)

**Q1. What is business analysis?**  
**A:** I treat it as enabling change by defining needs and recommending solutions that deliver value — not as typing a BRD. On ShopEase returns I refused a chatbot wish and defined the need as faster visible refunds.  
**Follow-up:** What is BA *not*? — Not PM, not coding, not QA.

**Q2. What does a BA do day to day?**  
**A:** I elicit, analyze, document, align, and support UAT. In a NovaBank week I would interview RMs Monday, freeze gold loans out of scope Wednesday, and walk completeness rules with credit Thursday.  
**Follow-up:** What do you *own*? — Requirement clarity, not the sprint dates.

**Q3. BRD vs FRD vs user story?**  
**A:** BRD is why and what value; FRD is system behaviour; a story is a slice for a sprint. NovaBank KYC rules sat in a baseline FR; SMS notifications were stories.  
**Follow-up:** Which did you write in Agile? — Stories + AC + a thin rules catalog.

**Q4. Functional vs non-functional?**  
**A:** FR = what it does; NFR = how well. ShopEase FR: auto-approve Size < ₹2,000. NFR: seller notify within 15 minutes; I do not invent numbers without an owner.

**Q5. How do you elicit requirements?**  
**A:** Interviews, observation, data, workshops, document review. I sat with ShopEase QC and sampled 50 returns instead of only taking the VP’s chatbot request.  
**Follow-up:** What if stakeholders have no time? — 20-minute process walk, then async decision log.

**Q6. How do you handle conflicting requirements?**  
**A:** I surface the conflict, options, and impact; the named owner decides. ShopEase: CX auto-approve vs seller “confirm every return.” PO chose auto-approve with notice and a kill switch.

**Q7. What is a good requirement?**  
**A:** Clear, testable, owned, in scope. “Make returns easy” is not. “Prepaid Size under ₹2,000 goes AUTO_APPROVED” is.

**Q8. Traceability?**  
**A:** I keep ID → story → test. NovaBank FR-AUTH-style completeness rule maps to a UAT script so a defect is a failed requirement, not a “random bug.”

**Q9. Who are stakeholders?**  
**A:** Anyone affected, influential, or interested — including silent ones. I missed ShopEase sellers in v1 and had to recover with a seller council.  
**Follow-up:** Power/interest grid? — Credit head manage closely; applicant keep informed via research.

**Q10. RACI?**  
**A:** Who responsible/accountable/consulted/informed. For MediCare+ SMS, legal is consulted; PO is accountable for priority; I am responsible for the rule table.

**Q11. As-Is vs To-Be?**  
**A:** As-Is is how it works (with waits). To-Be is the changed path. ShopEase As-Is waited 2.1 days on seller; To-Be skips seller only when the rule matches.

**Q12. How do you find process bottlenecks?**  
**A:** Timestamps and volumes, not opinions. NovaBank 34% of apps sat in DOCUMENTS_PENDING > 48 hours — that is the bottleneck, not “need AI.”

**Q13. Agile vs Waterfall?**  
**A:** Waterfall sequences phases; Agile slices value. I use what the org uses. NovaBank was hybrid: baseline KYC, sprint the SMS.

**Q14. What is a user story + AC?**  
**A:** As a prepaid buyer, I want Size returns auto-approved so refund wait is not seller queue. AC: Given/When/Then plus QC-fail exception.

**Q15. Definition of Ready / Done?**  
**A:** Ready: scoped, AC, dependencies named. Done: built, tested against AC, UAT for the slice. I do not call a story done because Jira moved.

**Q16. SDLC — where is the BA?**  
**A:** Thickest in requirements and UAT; present in design review, build clarifications, and change. I do not vanish after the BRD.

**Q17. Change request?**  
**A:** Impact on scope, rules, tests, date. Warehouse “add photos while you are here” on ShopEase was a CR or phase 2 — not a silent BRD edit.

**Q18. How do you know value was delivered?**  
**A:** Outcome metric. Simulated ShopEase: 9 → 4.2 days. I would instrument cycle timestamps for real.

**Q19. Documentation in Agile — is it dead?**  
**A:** No. I still write rules, AC, and decisions. I just do not wait for a 40-page gate if the org is Scrum.

**Q20. Why you, a fresher?**  
**A:** I can show two complete practice threads — ShopEase and NovaBank — with problem, scope, artifacts, and a data insight. I will not fake employment.

## Real-world examples of follow-up traps

- They ask “give me a requirement you wrote” — recite an ID, not a slogan.
- They ask “Agile ceremonies” — mention refinement and review, not only stand-up.

## Scenario / Use case: 30-minute fundamentals panel

**Context.** Two interviewers. They start at Q1, then jump to Q6 and Q13.

**What you do.** Short definition, then one company example, then stop. If they want depth they will follow up. Bring a one-page RTM excerpt to slide across the table if allowed.

**What goes wrong if ignored.** You lecture SDLC for eight minutes and never reach stakeholders.

## Notes

- First person + practice-case names; no fake jobs.
- Every concept answer should name an artifact or a metric.
- Follow-ups usually ask for conflict, exception, or “what did you own.”
- Hybrid NovaBank is a better Agile answer than “we don’t document.”
- 
