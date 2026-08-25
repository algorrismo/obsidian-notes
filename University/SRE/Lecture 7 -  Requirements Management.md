---
tags:
source: Wiegers & Beatty (2013), Software Requirements — Ch. 27 & 28
created: 2026-08-24
exam_format: MCQ and case study
---
---

# Ch. 07 — Requirements Management: Complete Study Guide

> [!info] How to use this Read it top to bottom once like a lecture. Then jump to **Section 13 (Case Study Exam Prep)** the night before — that's your cheat-sheet for the case study part of the quiz. Section 14 is a self-test with hidden answers (click to expand) so you can actually test recall, not just re-read.


## 1. What _Is_ Requirements Management? (The Big Picture)

Think of it this way: **writing** requirements is a one-time creative act. **Managing** requirements is what keeps those requirements alive, correct, and trustworthy for the entire life of the project — because requirements never stay still. Clients change their minds, markets shift, developers discover things were missed.

> **Definition:** Requirements management is the process of **documenting, analyzing, tracing, prioritizing, and agreeing** on requirements, and then **controlling change** and **communicating** to stakeholders. It is **continuous** — it doesn't stop once the SRS (Software Requirements Specification) is "done."

**Why this matters for the exam:** almost every other topic in this chapter (baselines, change control, CCB, impact analysis) is just a _mechanism_ for doing this one job well.

---

## 2. Requirements Baseline

A **baseline** is a fixed, agreed-upon snapshot of requirements — like a save-point in a video game, or a `git commit` tag. Once you baseline something, you can always come back to "what did we agree to on this date?"

> **Definition:** A **Requirements Baseline** is a set of requirements that stakeholders have **agreed to**, often defining the contents of a specific release or iteration.

**How a baseline is formed:**

1. Requirements are documented and reviewed.
2. Errors found during review are corrected.
3. Once every part is reviewed, corrected, and approved → **it becomes a baseline**.

> [!tip] Key idea A baseline doesn't mean "requirements can never change again." It means **change is now controlled** — any future change must go through a formal process (Change Control) rather than happening silently. This is a _software configuration management_ concept.

---

## 3. The Requirements Management Process — 4 Pillars (Figure 27-1)

Requirements Management branches into **four major activities**. Memorize these four — they're a classic MCQ target.

|Pillar|What it covers|
|---|---|
|**Version Control**|Defining a version ID scheme; tracking versions of individual requirements; tracking versions of whole requirement _sets_|
|**Change Control**|Proposing changes → analyzing impact → deciding → updating requirements/plans → measuring requirements volatility|
|**Requirements Status Tracking**|Defining possible statuses; recording each requirement's status; tracking the status _distribution_ across all requirements|
|**Requirements Tracing**|Linking requirements to other requirements; linking requirements to other system elements (design, code, tests)|

> [!tip] Memory hook **V-C-S-T**: **V**ersion, **C**hange, **S**tatus, **T**race. All four feed into one root node: "Requirements Management."

---

## 4. Accommodating New or Changed Requirements — 4 Levers

When a new requirement shows up mid-project, you have exactly **four knobs** to turn (you can't just "add work for free" — something else has to give):

1. **Defer or cut** lower-priority requirements to a later iteration.
2. **Add staff or outsource** part of the work.
3. **Extend the schedule** / add iterations (in Agile).
4. **Sacrifice quality** to still hit the original date. _(Listed as an option in the book — but it's the worst one; it just moves the pain to post-release bugs.)_

> [!warning] Exam trap If a question asks "what are the _only_ two options when scope grows without changing the deadline," don't overthink — the book frames these four levers as the trade-off menu, not a strict either/or. The classic project-management triangle (scope–schedule–cost–quality) is exactly what's being illustrated here.

---

## 5. Requirement Attributes

Every requirement should carry metadata — not just the requirement text itself. This metadata is what lets you _manage_ it later.

- Date created
- Current **version number**
- **Author**
- **Priority**
- **Origin/source** (who asked for it)
- **Rationale** (why it exists)
- **Release/iteration** it's allocated to
- **Stakeholder to contact** with questions
- **Validation method** / acceptance criteria

> [!tip] Why it matters Without these attributes, you can't answer basic management questions like "who do I ask about this?" or "is this even in scope for the current release?" This is the data that powers **Requirements Status Tracking**.

---

## 6. Tracking Requirements Status (Table 27-1)

Every requirement moves through a **lifecycle** of statuses. This is one of the most quiz-friendly tables in the chapter — statuses are often confused with each other (especially _Implemented_ vs. _Verified_, and _Deferred_ vs. _Deleted_ vs. _Rejected_).

|Status|Meaning|
|---|---|
|**Proposed**|Requested by an authorized source — nothing done yet|
|**In Progress**|A business analyst is actively writing/crafting it|
|**Drafted**|The initial version has been written|
|**Approved**|Impact estimated, stakeholders agreed, allocated to a baseline, dev team **committed**|
|**Implemented**|Code written + unit tested + traced to design/code — ready for further testing|
|**Verified**|Acceptance criteria satisfied, traced to tests — **considered complete**|
|**Deferred**|An _approved_ requirement pushed to a later release|
|**Deleted**|An _approved_ requirement removed from the baseline (with a documented reason/decision-maker)|
|**Rejected**|Was proposed but **never approved**, not planned for any upcoming release (with documented reason/decision-maker)|

**The natural "happy path" flow:**

```
Proposed → In Progress → Drafted → Approved → Implemented → Verified
                                        │
                     ┌──────────────────┼──────────────────┐
                     ▼                  ▼                  ▼
                 Deferred            Deleted           (Rejected happens
             (later release)    (removed from          BEFORE Approved)
                                    baseline)
```

> [!warning] Exam trap **Deferred and Deleted can only happen to a requirement that was already _Approved_.** **Rejected** happens _before_ approval — it was proposed but never got the green light. If a question describes a requirement being "removed after approval, with a documented reason," that's **Deleted**, not Rejected.

---

## 7. Resolving Requirements Issues

### Why use an issue-tracking tool?

- Issues from multiple reviews are collected — nothing gets lost.
- PM can see the current status of all issues at a glance.
- A **single owner** is assigned to each issue.
- **History of discussion** is retained.
- Development can **start earlier** with a known list of open issues, instead of waiting for a "perfect," fully-resolved SRS.

### Table 27-2 — Common Issue Types

|Issue type|Description|
|---|---|
|**Requirement question**|Something isn't understood/decided yet|
|**Missing requirement**|Developers found a gap during design/implementation|
|**Incorrect requirement**|A requirement was wrong — fix or remove it|
|**Implementation question**|Devs have questions about _how_ something should work|
|**Duplicate requirement**|Two+ equivalent requirements found — delete all but one|
|**Unneeded requirement**|It simply isn't needed anymore|

> [!tip] Distinguish these two closely-related pairs
> 
> - _Requirement question_ = confusion about the **requirement itself** (analysis stage).
> - _Implementation question_ = confusion about **how to build it** (coding stage).
> - _Incorrect requirement_ = it's **wrong**. _Unneeded requirement_ = it's **right but no longer relevant**.

---

## 8. Why Manage Changes? (The Organizational Goals)

A serious organization ensures:

1. Proposed changes are **thoughtfully evaluated** before commitment.
2. **Appropriate individuals** make informed business decisions.
3. Change activity is **visible** to affected stakeholders.
4. Approved changes are **communicated** to all affected participants.

This is essentially the "mission statement" behind everything that follows (Change Control Policy, CCB, Impact Analysis).

---

## 9. Managing Scope Creep

- The **single most effective technique** for controlling scope creep: **the ability to say "no."**
- Teams face intense pressure to always say "yes" — philosophies like _"the customer is always right"_ sound nice but **change is not free**; ignoring that cost doesn't make it disappear.
- A softer alternative used in practice: saying **"not now"** instead of a flat rejection — it holds open the possibility of a future release, which is more palatable to stakeholders than an outright "no."

> [!tip] Exam angle If a question asks for the _single best technique_ against scope creep, the answer is **saying no** (or its softer form, "not now") — not "hiring more staff" or "extending the deadline." Those are _coping_ mechanisms; saying no is _prevention_.

---

# ⭐ CHANGE CONTROL — Core Case-Study Territory Starts Here

Everything from here through Section 12 is exactly what your case study will test: **Policy → Board → Impact Analysis → Decision Options → Agile**. Slow down through these sections.

## 10. Change Control Policy

A formal, written policy that governs how _any_ change request is handled. **Seven rules:**

1. **All changes must follow the process.** A change not submitted per this process is not even considered.
2. **No design/implementation work** (other than feasibility exploration) is done on **unapproved** changes.
3. Requesting a change **doesn't guarantee** it happens — the **Change Control Board (CCB)** decides.
4. The **change database is visible** to all project stakeholders.
5. **Impact analysis must be performed** for every change.
6. Every incorporated change must be **traceable to an approved change request**.
7. The **rationale** behind every approval/rejection must be **recorded**.

> [!tip] Memory hook Think of this as **"No shortcuts, no secrets, no memory loss":**
> 
> - _No shortcuts_ → rules 1, 2 (follow process, don't jump ahead)
> - _No secrets_ → rule 4 (visibility)
> - _No memory loss_ → rules 5, 6, 7 (analyze it, trace it, record why)

### A Change Control Process Description (Figure 28-1 template)

A well-documented process itself typically contains:

1. Purpose and scope
2. Roles and responsibilities
3. Change request states
4. Entry criteria
5. Tasks — **5.1 Evaluate** → **5.2 Decide** → **5.3 Implement** → **5.4 Verify**
6. Exit criteria
7. Change control status reporting

- Appendix: attributes stored for each request

> [!warning] Exam trap Note the **task sequence** in step 5: **Evaluate → Decide → Implement → Verify.** A question might scramble this order and ask you to pick the correct sequence.

---

## 11. The Change Control Board (CCB)

The CCB is the **decision-making authority** for changes — it's the "who" behind rule #3 of the policy above.

### CCB Composition — who sits on it

Representatives from:

- Project or program management
- Business analysis / product management
- Development
- Testing / QA
- Marketing, the business unit, or customer representatives
- Technical support / help desk

> [!tip] Why so many roles? Because a change ripples everywhere — dev needs to know feasibility, QA needs to know testability, marketing needs to know customer impact, support needs to know what they'll have to explain later. The CCB is deliberately **cross-functional**, not just "the developers deciding."

### CCB — Making Decisions

Each CCB must define, in advance:

- The **quorum** — minimum number of members (or key roles) needed to make a decision
- The **decision rules** (e.g., majority vote, consensus)
- Whether the **CCB Chair can overrule** the group's collective decision
- Whether a **higher-level CCB or management must ratify** (approve) the decision

### Change Control Tools — what a good tool should do

- Let you define the **attributes** of a change request
- Implement a **change request life cycle** with multiple statuses
- **Enforce the state-transition model** (only authorized users can change specific statuses)
- **Record date + identity** of each status change
- Send **automatic email notifications** on submission/status update
- Produce **standard and custom reports/charts**

---

## 12. Change Impact Analysis

This is the **technical/analytical heart** of change control — the CCB can't decide wisely without it.

### The core procedure (in order):

1. **Understand the possible implications** of the change — a change can ripple into other requirements, architecture, design, code, and tests, and can even **conflict** with other requirements or **compromise quality attributes** (performance, security).
2. **Identify** all requirements, files, models, documents that might need modification.
3. **Identify tasks** needed to implement the change and **estimate effort**.

### Then, more concretely, a working procedure:

1. Work through the **"implications" checklist** (Figure 28-5) — see below.
2. Work through the **"affected work products" checklist** (Figure 28-6) — see below. (Some tools auto-generate this via traceability links.)
3. Use the **effort estimation worksheet** (Figure 28-7).
4. **Sum** the effort estimates.
5. Identify the **sequence/interleaving** with currently planned tasks.
6. Estimate the impact on **schedule and cost**.
7. Evaluate the change's **priority** vs. other pending requirements.
8. **Report results to the CCB.**

### Figure 28-5 — Questions about implications (sample, not exhaustive)

- Will the change enhance or impair satisfying **business requirements**?
- Do existing/pending requirements **conflict** with it?
- What are the consequences of **not** making the change?
- What are the **adverse side effects or risks**?
- Will it hurt **performance or quality attributes**?
- Is it **feasible** given technical constraints/staff skills?
- Will it demand too much of dev/test/operating **resources**?
- Must new **tools** be acquired?
- How does it affect **sequence, dependencies, effort, duration** of planned tasks?
- Will it need **prototyping** or user validation?
- How much **sunk effort** is lost if accepted?
- Will it raise **unit cost** (e.g., third-party licensing)?
- Will it affect **marketing, manufacturing, training, or support** plans?

### Figure 28-6 — Checklist of affected work products

- UI changes/additions/deletions
- Reports, databases, files
- Design components to create/modify/delete
- Source code files to create/modify/delete
- Build files/procedures
- Existing tests to modify/delete + **new** tests needed
- Help screens, training, or support materials
- Other applications/libraries/hardware affected
- Third-party software to acquire/modify
- Impact on **project management, QA, or configuration management plans**

### Figure 28-7 — Effort Estimation Worksheet (categories of hours to estimate)

Update SRS → prototype → new/modified design components → new/modified UI → new/modified documentation → new/modified source code → third-party licensing/integration → build files → new/modified unit & integration tests → perform testing → new/modified system/acceptance tests → automated test suites → **regression testing** → reports/database/data files → project plans → traceability matrix → review → rework → **Total Estimated Effort**.

> [!tip] Big picture You don't need to memorize every line of 28-7 — just recognize the **pattern**: for every artifact type (design, code, tests, docs, plans), ask "does this need to be created or modified, and how long will that take?" That pattern _is_ the exam-testable idea.

### Figure 28-8 — Impact Analysis Template (the "form" that gets filled out)

Change Request ID · Title · Description · Evaluator · Date prepared · **Estimated total effort (hours)** · **Estimated schedule impact (days)** · **Additional cost impact ($)** · Quality impact · Other components affected · Other tasks affected · Life-cycle cost issues.

---

## 13. Measuring Change Activity

Track over time:

- Total change requests received / currently open / closed
- Number of requirements **added, deleted, modified**
- Number of requests **by origin** (customer, marketing, management, dev, hardware, testing, etc.)
- Number of changes against **each requirement** since baselining (= that requirement's "volatility")
- **Total effort** devoted to processing/implementing changes

> [!tip] Why measure this? It's how a PM spots a requirement (or a _stakeholder_) that's an outlier — e.g., "Marketing alone generated 30 of our change requests" (this exact example appears in Figure 28-4's bar chart) — which is a red flag for scope discipline or unclear early requirements.

---

# ⭐ Decision Options — What the CCB Can Actually Decide

When the CCB reviews a change + its impact analysis, there are exactly **three official outcomes**:

|Decision|Meaning|
|---|---|
|**Approved**|Update the baseline, execute immediately (can include _conditions_, e.g., extra budget/time)|
|**Rejected**|Project continues as originally planned — change does not happen|
|**Deferred**|Move the request to a later phase (e.g., "Phase 2" / post-launch)|

> [!tip] Nuance worth remembering A decision can be **"Approved with conditions"** — e.g., approved, but the budget and deadline both shift. This is _not_ a fourth category; it's still "Approved," just with negotiated trade-offs attached (see the CampBites case study below — this is exactly what happened there).

---

## 14. Worked Case Study: The "Mid-Project Feature Request" (CampBites)

This worked example is your **template** for how a change-control case study should be answered. Study its structure, not just its facts.

**Setup:** CampBites is a mobile food-ordering app for a campus. It's **Week 4 of a 6-week timeline**, core features nearly done. Campus Dining Services (the client) asks: _"We want students to pay using Bkash and Nagad, not just credit cards."_

**The 6-Step Change Control Workflow:** `Request → Impact Analysis → CCB Review → Decision → Implementation → Re-baselining`

### Step 1 — Submission of Change Request (CR)

- The requester fills out a **formal Change Request Form** (not an informal email/call).
- **Goal:** prevent scope creep by forcing the stakeholder to clearly state _what_ and _why_.

### Step 2 — Impact Analysis

The Systems Analyst + Tech Lead evaluate across **four dimensions**:

- **Scope:** integrate two external payment SDKs (Apple Pay & Google Pay) + redesign checkout UI
- **Schedule:** +5 days dev, +2 days security/QA testing
- **Cost:** $1,500 (dev hours + third-party API fees)
- **Risk:** delaying launch by 1 week risks missing the start of the semester

### Step 3 — CCB Review

CCB = **Project Sponsor + Project Manager + Tech Lead**. Sample discussion:

> Sponsor: _"Will missing the first week of school hurt us?"_ PM: _"Yes, but 70% of students use Apple Pay. Launching without it might hurt adoption more."_

_(Notice: this is exactly the cross-functional weighing of trade-offs the CCB exists for — business risk vs. technical/market risk.)_

### Step 4 — Decision & Sign-Off

Decision = **Approved with Conditions**: CCB approves, adds **$1,500** to budget, extends deadline by **4 days**.

### Step 5 — Implementation & Verification

- PM updates the **Work Breakdown Structure (WBS)**, assigns new tasks.
- Devs write/test the payment SDK code.
- QA tests transactions on iOS and Android.

### Step 6 — Closure & Re-baselining

- Requirements Document, Schedule Baseline, and Budget Baseline officially updated → **Version 1.1**.
- Change logged as **"Closed/Implemented."**
- Team and stakeholders notified of the new launch date.

### The actual Change Request Form (CR-014) — memorize this shape, it's the exam's "fill in the blank" pattern

|Field|Value|
|---|---|
|CR ID|CR-014|
|Project|CampBites Mobile App|
|Date Requested|Oct 12, 2026|
|Requested By|Sarah Jenkins (Campus Dining Director)|
|Priority|Medium|
|Description|Add Apple Pay & Google Pay to checkout|
|Business Justification|70%+ students use mobile wallets → faster checkout, higher completion|
|Impact Summary|Cost +$1,500 · Schedule +4 days · Scope: 2 SDKs + Checkout UI update|
|CCB Decision|✅ **APPROVED**|
|Signatures|Sponsor: S. Jenkins · PM: M. Chen|

---

## 15. Change Management on Agile Projects

Agile handles change **structurally differently** than the CCB-driven waterfall model above — it doesn't fight change, it **absorbs it into the workflow**.

### Figure 28-9 — The Dynamic Product Backlog

- New requirements/tasks enter the **Prioritized Product Backlog** at any time.
- They get slotted based on priority into: **current iteration → next iteration → future iterations**.
- Items already in the backlog can be **reprioritized** (moved forward) or **deleted**.
- A lower-priority item can get bumped from "next iteration" back into "future iterations" to make room.

> [!tip] The core Agile insight There's no separate "change control process" bolted on — the **backlog itself _is_ the change-control mechanism.** Adding, reprioritizing, or deleting backlog items _is_ what a CR/CCB/impact-analysis cycle does in Waterfall, just continuous and lightweight instead of a discrete formal event.

### Agile vs. Traditional (Waterfall) Change Management — high-value comparison table

|Dimension|Traditional (Waterfall)|Agile|
|---|---|---|
|**Mindset**|Change is a **risk/defect** to minimize|Change is a **competitive advantage** to embrace|
|**Decision Authority**|Change Control Board (CCB)|Product Owner (PO)|
|**Primary Tool**|Formal Change Request Form (CR)|Product Backlog & User Stories|
|**Trade-Off Model**|Expands budget, scope, or timeline|**Swaps** features within fixed timeboxes/sprints|
|**Timing**|Ad-hoc or strict milestone phase gates|Integrated into regular sprint planning|

> [!warning] Exam trap The most commonly tested row is **Trade-Off Model**. Waterfall _expands_ something (budget/scope/time) to fit in a change. Agile does **not** expand the sprint — it **swaps** an existing backlog item out for the new one, keeping the timebox fixed. If an answer choice says "Agile extends the sprint to accommodate new features," that's **wrong** — it violates the fixed-timebox principle.

---

# 13. 🎯 Case Study Exam Prep — The 5-Part Framework

Your quiz explicitly names a case study on: **Change Control Policy · Impact Analysis · CCB · Decision Options · Agile.** Here's a reusable checklist — if you get a _new_ mini-scenario tomorrow, run it through these five questions in order:

1. **Policy check** — Was a formal Change Request submitted? (If not: per policy, it "will not be considered" — no design work should happen yet, beyond feasibility exploration.)
2. **Impact Analysis** — What are the **Scope / Schedule / Cost / Risk** implications? (This 4-part lens, taken straight from the CampBites example, is faster to apply under exam pressure than the full Figure 28-5/28-6 checklists.)
3. **CCB** — Who _should_ be in the room (PM, sponsor, dev/tech lead, QA, business/customer rep)? What trade-off are they weighing (e.g., business risk of delay vs. technical/market risk of omission)?
4. **Decision Options** — Is the right call **Approved**, **Approved with Conditions**, **Rejected**, or **Deferred**? Justify using the impact analysis numbers.
5. **Agile lens** — If this were an Agile project instead: no CCB, no CR form — the **Product Owner** decides, and the feature is just **prioritized into the backlog**, likely **swapping out** a lower-priority item rather than extending the sprint.

> [!success] One-line answer template for a case-study paragraph _"Per the Change Control Policy, [stakeholder] must submit a formal CR — no work proceeds otherwise. The impact analysis shows [scope/schedule/cost/risk] effects of [X]. The CCB, composed of [roles], weighs [business risk] against [technical/market risk] and decides to [Approve/Approve-with-conditions/Reject/Defer] because [reason]. In an Agile context, this would instead be resolved by the Product Owner reprioritizing the backlog rather than convening a CCB."_

---

## 16. Self-Test (Active Recall)

Try to answer _before_ expanding each answer.

**Q1 (True/False):** A requirement can move directly from "Approved" to "Rejected."

> [!success]- Answer **False.** Rejected means it was _never_ approved. Once approved, the only "exit" paths are Deferred or Deleted.

**Q2 (MCQ):** Which of the following is **NOT** one of the four major pillars of the Requirements Management process? A) Version Control B) Change Control C) Risk Management D) Requirements Tracing

> [!success]- Answer **C — Risk Management.** The four pillars are Version Control, Change Control, Status Tracking, and Tracing.

**Q3 (True/False):** According to the Change Control Policy, impact analysis is optional for minor changes.

> [!success]- Answer **False.** "Impact analysis must be performed for **every** change" — no exceptions stated in the policy.

**Q4 (MCQ):** In the CampBites case study, what was the CCB's final decision? A) Rejected B) Deferred to Phase 2 C) Approved with Conditions D) Approved with no changes to budget/schedule

> [!success]- Answer **C — Approved with Conditions** (budget +$1,500, deadline +4 days).

**Q5 (True/False):** In Agile, a new requirement is typically handled by extending the sprint length.

> [!success]- Answer **False.** Agile keeps the **timebox fixed** and **swaps** a lower-priority backlog item for the new one.

**Q6 (MCQ):** Who holds primary decision authority for change in a Traditional/Waterfall project vs. an Agile project, respectively? A) PM / Sponsor B) CCB / Product Owner C) Developer / QA D) Customer / Scrum Master

> [!success]- Answer **B — CCB / Product Owner.**

**Q7 (MCQ):** A requirement status of "Implemented" means: A) It's fully tested and considered complete B) Code is written, unit-tested, and traced to design/code but not yet formally verified C) It has only been drafted D) It was rejected by the CCB

> [!success]- Answer **B.** "Verified" (not Implemented) is the status that means fully complete/acceptance-tested.

**Q8 (True/False):** The single most effective technique for controlling scope creep is hiring additional staff.

> [!success]- Answer **False.** The book states it's **the ability to say "no"** (or "not now").

**Q9 (MCQ):** Which is the correct order of tasks in a Change Control Process description (Figure 28-1)? A) Decide → Evaluate → Implement → Verify B) Evaluate → Decide → Implement → Verify C) Implement → Evaluate → Decide → Verify D) Evaluate → Implement → Decide → Verify

> [!success]- Answer **B.**

**Q10 (MCQ):** A requirement that was approved, then later removed from the baseline with a documented explanation, should be marked: A) Rejected B) Deferred C) Deleted D) In Progress

> [!success]- Answer **C — Deleted.**

---

## References

- Wiegers, K., & Beatty, J. (2013). _Software Requirements._ Pearson Education. (Ch. 27 – Requirements Management; Ch. 28 – Change Control)

> [!info] Double-check note This guide is built directly from your uploaded slide deck (Ch.07). No outside facts were added except the transitional explanations and analogies for teaching clarity — if any definition here seems to diverge from what your instructor emphasized in lecture, trust the lecture.