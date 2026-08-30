
### Ch.09 Improving Requirements Processes + Ch.10 Requirements & Risk Management

_Think of this as me sitting next to you the night before the quiz, going slide by slide._

---

## PART 1 — CHAPTER 9: Improving Your Requirements Processes

### Slide 2 — Objective of Process Improvement

**Plain meaning:** Why do we even bother "improving" how we gather requirements? Because bad requirements = wasted money and rework. The end goal is always: **cheaper to build, more value delivered.**

Three ways to get there:

1. **Fix past mistakes** — look at what went wrong last project and correct it.
2. **Prevent future mistakes** — anticipate problems before they happen.
3. **Adopt better practices** — replace old/inefficient habits with proven ones.

**Exam tip:** If asked "what is the ultimate goal of requirements process improvement?" → _reduce cost of creating/maintaining software and increase the value delivered._

---

### Slide 3 — How Requirements Relate to Other Project Processes

This is a diagram (Figure 31-1) with "Software Requirements" in the center, connected to 6 other processes:

|Process|Relationship to Requirements|
|---|---|
|Project Planning|Requirements **serve as input to** planning; planning **adjusts scope**|
|Project Tracking & Control|**Status is tracked by** this process; it can **request changes in scope**|
|Change Control Process|Requirements **are the baseline for** it; it **modifies** requirements|
|Acceptance & System Testing|Requirements **are reference for** testing; testing **verifies correct implementation**|
|Construction (coding)|Requirements **are basis for** construction; work products **are traced to** requirements|
|User Documentation|Requirements **are basis for** the user docs|

**Why this matters for the quiz:** Notice the phrase _"work products are traced to"_ Construction — this is literally **requirement tracing** in action. Requirements aren't an isolated document — everything downstream (code, tests, docs) connects back to them.

---

### Slide 4 — Requirements and Various Stakeholder Groups

Another spoke diagram (Figure 31-2). Center = "Software Development Group." Around it:

- **Marketing/Product Mgmt** → specifies business/market requirements, requests changes
- **Technical Support** → feeds back bug reports & enhancement requests
- **Users** → describe user requirements & quality attributes; review requirements
- **Project Sponsor** → provides business requirements
- **Systems Engineering** → allocates system requirements to software; requests changes
- **Procurers** → specify business/quality requirements; join vendor selection
- **Legal Department** → handles licensing of tools/components
- **Management** → sets constraints, resources, commitments

**Exam tip:** Just remember — requirements aren't written by one person. Every stakeholder contributes a different _kind_ of input.

---

### Slide 5 — Gaining Commitment to Change

People resist process improvement. Three forms of resistance:

1. **"No time for improvement"** — people are too busy firefighting to invest in doing things better. (Counter-argument: if you never invest time, the next project won't improve either.)
2. **Change control process seen as a "barrier"** — people think it slows them down. Reality: it's a **structure**, not a barrier — it lets informed people make good decisions and communicate them.
3. **Requirements documentation seen as a "waste of time"** — developers/managers think writing/reviewing requirements delays "real work" (coding). Reality: skipping this causes constant code rewrites later, which is far more expensive.

**Exam tip:** Key contrast to remember → _"barrier vs. structure"_ and _"administrative waste vs. cost-saving investment."_

---

### Slide 6 — Fundamentals of Software Process Improvement

Four foundational principles:

1. Improvement should be **evolutionary and continuous** (not a one-time event).
2. People/organizations only change when they have an **incentive**.
3. Process changes should be **goal-oriented** (tied to a specific measurable goal).
4. Treat improvement efforts as **mini-projects** (with plans, milestones, etc.)

---

### Slide 7 — Root Cause Analysis (Fishbone / Ishikawa Diagram)

Figure 31-4 — a **cause-and-effect (fishbone) diagram**. The "effect" (the big problem) sits at the head of the fish: **"Don't finish projects on time."** The "bones" are categories of causes:

- **Process** → requirements missed during elicitation → because analyst not trained, user class not represented, no change control process
- **People** → developers fixing problems from late requirement changes on the previous project; developers aren't available
- **Project** → didn't get input from the right people, market poorly defined, legislative changes, requirements change too frequently

**Concept to remember:** Root cause analysis doesn't just treat the _symptom_ (late project) — it digs into the _underlying causes_ across People/Process/Project categories. This is a classic quality-improvement tool (also used in manufacturing, borrowed here for software).

---

### Slide 8 — The Process Improvement Cycle

Figure 31-5 — a 4-step continuous loop:

1. **Assess current practices** → produces findings & recommendations
2. **Plan improvement actions** → produces an action plan
3. **Create, pilot, and roll out processes** → "roll-out" = bringing something to market / making it accessible
4. **Evaluate results** → feeds back into Assess (cycle repeats)

Each arrow has a guiding question: _Did new processes achieve results? How well did planning work? How smoothly did the pilot go?_

**Exam tip:** This is basically a **PDCA-style cycle** (Plan-Do-Check-Act) applied to requirements process improvement.

---

### Slide 9 — The Learning Curve ("Valley of Despair")

Figure 31-7. When you start improving a process, performance **dips before it rises** — because people are learning the new way and are temporarily less efficient.

- X-axis = Time, Y-axis = Performance
- Starts flat (initial state) → dips into a valley (learning curve) → **"don't quit here!"** → rises to a new, higher plateau (improved future state)

**Exam tip:** The key lesson = don't abandon a process improvement just because performance temporarily drops. That dip is _expected_, not a sign of failure.

---

### Slides 10–11 — Types of Process Assets

"Process assets" = reusable resources that help teams follow good practices consistently.

|Asset|Meaning|
|---|---|
|**Checklist**|A memory-jogger list of items/activities to verify — stops busy people from overlooking things|
|**Example**|A real, representative sample of a work product to imitate|
|**Plan**|Outline of how an objective will be accomplished|
|**Policy**|A guiding principle / management expectation|
|**Procedure**|Step-by-step sequence of tasks + who performs them|
|**Template**|A reusable pattern/structure for producing a document (with "slots" to fill in)|

---

### Slide 12 — Requirements Engineering Process Assets (Figure 31-8)

Split into two buckets:

**Requirements _Development_ Process Assets:**

- Requirements development process
- Requirements allocation procedure
- Requirements prioritization procedure
- Vision & scope template
- Use case template
- SRS (Software Requirements Specification) template
- Requirements review checklist

**Requirements _Management_ Process Assets:**

- Requirements management process
- Requirements **status tracking** procedure
- Change control process
- Change control board (CCB) charter template
- Requirements change impact analysis checklist
- **Requirements tracing procedure** ⭐

**⭐ This is your first direct textbook mention of "Requirements Tracing" — it lives under Requirements _Management_, not Development.** It's grouped with change control and impact analysis because tracing is what lets you analyze the _impact_ of a change.

---

### Slide 13 — Performance Indicators (Table 31-2)

How do you _measure_ whether your requirements process improved? Some example goals & their indicators:

|Improvement Goal|Example Indicator|
|---|---|
|Reduce rework from requirements errors|Hours of rework caused by bad requirements; % of requirements with errors found after baselining|
|Reduce negative impact of requirement changes|# of new requirements found after baselining that could've been known earlier; % of requirements modified after baselining|
|Reduce time to clarify requirements|# of requirement questions raised after baselining; average time to resolve each|
|Improve estimation accuracy|Estimated vs. actual labor hours on requirements work|
|Reduce unneeded features built|% of committed features removed before/after implementation|

**Exam tip:** Note the recurring word **"baselining"** — a baseline is the "frozen" approved version of requirements. A lot of indicators measure what happens _after_ that baseline (which is exactly where traceability becomes critical).

---

### Slide 14 — Creating a Requirements Process Improvement Road Map (Figure 31-9)

A road map = a sequence of improvement actions leading to milestones (M1–M5), each tied to a measurable goal:

- Path 1: Train team → train in reviews → review requirements docs → **M1 → Reduce system testing effort by 25% in 6 months**
- Path 2: Adopt SRS template → adopt use case approach → **M2** → adopt prioritization procedure → **M3 → Improve customer satisfaction by 1 rating point**
- Path 3: Set up CCB & charter → document change procedure → **M4** → adopt change impact analysis → track requirements status → **M5 → Reduce requirements volatility by 20%**

---

### Slides 15–17 — Three Worked Roadmap Examples

These are the applied, story versions of Slide 14's diagram. Know the **goal → actions → result** for each:

**Roadmap 1 — Quality & Defect Prevention**

- _Scenario:_ Logistics company; QA wastes 40% of time logging bugs from ambiguous requirements.
- _Actions:_ Train PMs/Analysts on writing testable acceptance criteria → train QA/engineers in formal review techniques (e.g., **Fagan inspections**) → mandatory peer walkthroughs of every requirement doc before design.
- _Result:_ Bug density cut in half; system testing effort reduced **25% in 6 months**.

**Roadmap 2 — Standardization & Usability**

- _Scenario:_ Healthcare SaaS vendor; low customer satisfaction (3.2/5.0) because features miss real clinical workflows.
- _Actions:_ Adopt standardized SRS template (e.g., **ISO/IEC/IEEE 29148**) → model requirements as structured **Use Cases** (Actor, Preconditions, Main Flow, Exception Flows) → apply **MoSCoW** prioritization (Must/Should/Could/Won't) with client steering committees.
- _Result:_ Satisfaction rises from **3.2 → 4.2**.

**Roadmap 3 — Governance & Scope Control**

- _Scenario:_ Mobile banking project suffering "scope creep" from informal stakeholder requests via chat/phone.
- _Actions:_ Form a **Change Control Board (CCB)** with charter → enforce formal **Change Request Form** → track requirement states (Proposed/Approved/Rejected/In-Progress) in Jira, with impact analysis on budget/timeline/architecture.
- _Result:_ Requirement volatility (churn) reduced by **20%**.

**Exam tip:** These three roadmaps map directly onto the three "paths" in slide 14's diagram — testing effort, customer satisfaction, and requirements volatility.

---

## PART 2 — CHAPTER 10: Software Requirements & Risk Management

### Slide 2 — Elements of Risk Management (Figure 32-1)

Risk Management breaks into three branches:

1. **Assessment** → Identification, Analysis, Prioritization
2. **Avoidance**
3. **Control** → Management Planning, Resolution, Monitoring

**Exam tip:** This is the master framework — everything else in this chapter (documenting risks, elicitation risks, etc.) is really just filling in the details of _Assessment_ and _Control_.

---

### Slides 3–4 — Documenting Project Risks (Risk Log Template + Sample)

A risk is logged with these fields:

|Field|Meaning|
|---|---|
|ID|Sequence number|
|Date Opened / Closed|When identified / resolved|
|Description|Written as **"condition → consequence"**|
|Probability|Likelihood (0–1 scale)|
|Impact|Potential damage if it happens (scale, e.g., 1–10)|
|**Exposure**|**Probability × Impact** — this is the key formula!|
|Mitigation Plan|Actions to control/avoid/minimize the risk|
|Owner|Person responsible|
|Date Due|Deadline for mitigation|

**Worked sample (Slide 4):**

- Risk: "Insufficient user involvement in requirements elicitation could lead to extensive UI rework after beta testing."
- Probability = 0.6, Impact = 7 → **Exposure = 0.6 × 7 = 4.2**
- Mitigation: gather usability requirements early, hold workshops, build a throwaway prototype and test it with users.
- Owner: Helen. Due: workshop by 4/16/2003.

**⭐ MEMORIZE THIS FORMULA: Exposure = Probability × Impact.** This is a very common quiz/numeric question.

---

### Slides 5–9 — Requirements-Related Risks: **Elicitation**

Risks that occur while _gathering_ requirements, and their mitigations:

|Risk|Mitigation|
|---|---|
|Vague product vision / scope creep|Nail down vision & scope early|
|Too little time spent on requirements dev|Spend ~**10–15%** of project effort on requirements; track actual time spent|
|Low customer engagement|Identify stakeholders/user classes early; find "voice of the customer," product champions|
|Incomplete/incorrect specs|Write usage scenarios & test cases early; build prototypes|
|Innovative products are hard to gauge|Market research, prototypes, focus groups|
|Neglected non-functional requirements (NFRs)|Explicitly ask about performance, usability, integrity, reliability|
|Customers don't agree with each other|Identify the _real_ decision-makers|
|Unstated (implicit) requirements|Use open-ended questions to surface hidden expectations|
|Using an existing product as the "spec" (reverse engineering)|Inefficient/incomplete — document what you find and have customers confirm it's still relevant|
|Solutions presented as "needs"|Analyst must dig to find the _real intent_ behind a proposed solution|
|Distrust between business & dev team|Build good-faith collaboration — distrust threatens elicitation itself|

---

### Slide 10 — Requirements-Related Risks: **Analysis**

- Requirements prioritization (conflicts over what's most important)
- Technically difficult features
- Unfamiliar technologies/methods/languages/tools/hardware

---

### Slide 11 — Requirements-Related Risks: **Specification**

- **Requirements understanding:** different people interpret requirements differently → mitigate with **formal inspections** (dev+test+customer) and prototypes
- **Time pressure to proceed despite TBDs** ("to be determined" items left unresolved) — risky to build on unresolved items
- **Ambiguous terminology:** define terms with both common & technical meaning; build a **data dictionary**
- **Design embedded in requirements:** don't let the SRS dictate _how_ to build it — that limits developer options; requirements should state the _what_, not the _how_

---

### Slide 12 — Requirements-Related Risks: **Validation**

- **Invalidated requirements:** writing test cases early feels scary, but confirming correctness _before_ construction avoids expensive rework later
- **Inspection proficiency:** if inspectors don't know how to properly review requirement docs, they'll miss serious defects

---

### Slide 13 — Requirements-Related Risks: **Management** ⭐ (Traceability lives here!)

- **Changing requirements:** defer implementing requirements likely to change until they're stable; design for easy modification
- **Requirements change process:** risk if there's no defined process, an ineffective one, or people bypass it — takes time to build a change-management culture
- **Unimplemented requirements:** ⭐ **"The requirements traceability matrix helps to avoid overlooking any requirements during design, construction, or testing."** — this is the textbook's _direct definition-in-context_ of what an RTM is for.
- **Expanding project scope:** vaguely specified areas eat more effort than expected → plan for phased/incremental delivery

---

### Slides 14–15 — Case Study: Healthcare.gov (2013)

This is the deck's featured real-world case study, and it's the strongest link between **risk management failures** and **lack of requirements traceability**. Full breakdown below in Part 3.

---

## PART 3 — DEEP DIVE: Requirement Tracing & Requirement Traceability Matrix (RTM)

_(This is your case-study focus — read this section twice.)_

### 3.1 What is "Requirement Tracing"? (the main theme)

**Requirement tracing** is the practice of creating and maintaining **links** between a requirement and every other artifact connected to it across the project lifecycle — its origin (why it exists), its design elements, the code that implements it, the test cases that verify it, and any related requirements.

Think of it like a **chain of custody** for a requirement:

```
Business Need / Stakeholder Request
        ↓
Requirement (in the SRS)
        ↓
Design Element(s)
        ↓
Code / Implementation
        ↓
Test Case(s)
```

There are two directions of tracing, and this distinction is a favorite quiz question:

- **Forward tracing:** "Where did this requirement go?" — from requirement → design → code → test. Used to make sure **every requirement was actually built and tested** (nothing got dropped).
- **Backward tracing:** "Where did this come from?" — from code/design/test → back to the requirement → back to the business need. Used to catch **unauthorized or unnecessary features** ("gold-plating") — code that exists but traces back to _no requirement at all_.

**Main theme in one sentence:** Tracing exists so that nothing gets **lost** (forward) and nothing gets **added without justification** (backward).

### 3.2 What is a Requirement Traceability Matrix (RTM)? (the main theme)

The **RTM** is simply the _tool_ that records these links in a structured table/grid. Each row is typically one requirement; the columns capture where it came from and everywhere it's been implemented/verified.

A typical simple RTM looks like:

|Req ID|Requirement Description|Source (Business Need)|Design Element|Code Module|Test Case ID|Status|
|---|---|---|---|---|---|---|
|REQ-01|System shall verify user eligibility via IRS DB|Business rule BR-3|DES-14|Module: EligibilityCheck.py|TC-101|Passed|

**Main theme in one sentence:** The RTM turns "did we build everything we promised, and can we verify it?" into a **checkable, auditable document** instead of relying on memory or hope.

### 3.3 Why it matters (the "so what")

- It prevents **unimplemented requirements** from silently falling through the cracks (directly stated on Ch.10 Slide 13).
- It supports **impact analysis**: if a requirement changes, the RTM tells you exactly which design/code/tests need to be revisited — without it, you're guessing.
- It gives auditors/testers/managers **visibility** into coverage: "Is every requirement tested? Is every test case tied to a real requirement?"
- Without it, large or multi-vendor/multi-team projects (like Healthcare.gov) **lose the ability to see downstream impact** when requirements change late.

### 3.4 Key Keywords to Memorize

|Keyword|Meaning in one line|
|---|---|
|**Forward tracing**|Requirement → design → code → test (checking nothing was missed)|
|**Backward tracing**|Code/test → requirement → business need (checking nothing unauthorized was added)|
|**Bidirectional traceability**|Having _both_ forward and backward links maintained|
|**RTM (Requirements Traceability Matrix)**|The table/tool recording all these links|
|**Baseline**|The frozen/approved version of requirements that tracing is measured against|
|**Impact analysis**|Using the RTM to see what's affected when a requirement changes|
|**Orphan requirement**|A requirement with no linked design/code/test — i.e., it was never implemented|
|**Gold-plating**|Code/feature that exists but has no requirement behind it (found via backward tracing)|
|**Coverage**|% of requirements that have at least one linked test case|
|**Volatility / churn**|How often requirements change — high volatility makes tracing harder to keep updated|
|**Sub-contractor / interface tracing**|Tracing across organizational boundaries (this is exactly what failed in Healthcare.gov)|

---

## PART 4 — 5 Practice Case Studies (with Model Answers)

### Case Study 1 — The Basic "Missing Requirement"

**Scenario:** An e-commerce team lists 50 requirements in their SRS. During final User Acceptance Testing (UAT), the client discovers that "the system shall send an order-confirmation email" was written in the SRS but was **never coded and never tested**. Nobody caught it earlier.

**Q: What tool/practice would have prevented this, and how?**

**Model Answer:** An **RTM** would have prevented this. Every requirement — including the email-confirmation one — should have a row in the matrix linking it to a design element, a code module, and a test case. If the "Code Module" and "Test Case ID" columns for that requirement were empty, it would visibly stand out as an **orphan requirement** during a routine RTM review — long before UAT. This is a textbook example of forward tracing (requirement → implementation) failing because tracing wasn't maintained.

---

### Case Study 2 — Backward Tracing / Gold-Plating

**Scenario:** A banking app's code review reveals a "loyalty points" feature in the live app. No one on the current team remembers a requirement for it, and the client insists they never asked for it. It quietly adds complexity and security risk.

**Q: How would traceability have flagged this, and what's this phenomenon called?**

**Model Answer:** This is a case for **backward tracing** — starting from the implemented code and tracing back to see which requirement (and business need) justified it. If no requirement links to the "loyalty points" module, it's flagged as **gold-plating**: functionality built without an authorized requirement behind it. Backward tracing via the RTM (or the absence of a row/link for that module) is exactly how QA or an auditor would catch this — the code exists in a "column" of the matrix with nothing connecting it back to Req ID.

---

### Case Study 3 — Build a Mini RTM

**Scenario:** A small requirements set for a library system:

- REQ-01: System shall allow a member to search the catalog by title.
- REQ-02: System shall allow a librarian to check out a book to a member.
- REQ-03: System shall send an overdue notice after 14 days.

Design docs: DES-A (Search Module), DES-B (Checkout Module), DES-C (Notification Module). Test cases: TC-1 (search returns results), TC-2 (checkout updates book status), TC-3 (overdue email sent after 14 days).

**Q: Construct the RTM.**

**Model Answer:**

|Req ID|Requirement|Design Element|Code Module|Test Case|Status|
|---|---|---|---|---|---|
|REQ-01|Search catalog by title|DES-A|SearchModule|TC-1|Traced ✅|
|REQ-02|Librarian checks out book|DES-B|CheckoutModule|TC-2|Traced ✅|
|REQ-03|Overdue notice after 14 days|DES-C|NotificationModule|TC-3|Traced ✅|

_(In an exam, the "trick" version of this question removes one Test Case or Design link — you're expected to spot the gap and say "REQ-0X is not fully traced / is at risk of being unverified.")_

---

### Case Study 4 — Impact Analysis Using the RTM

**Scenario:** Midway through development, the client changes REQ-02 above: "checkout" must now also check whether the member has unpaid fines before allowing checkout.

**Q: Using the RTM, what should the team do, and why is this safer than making the change directly in code?**

**Model Answer:** Using the RTM, the team looks up REQ-02's row and immediately sees it's linked to **DES-B (Checkout Module)** and **TC-2**. This tells them:

1. The design for Checkout must be revised to add a fine-check step.
2. The CheckoutModule code must be updated.
3. TC-2 must be updated (and possibly a new test case, TC-2b, added for "checkout blocked due to unpaid fine").

Without the RTM, a developer might patch the code directly without realizing the _design doc_ and _existing test case_ are now out of sync with the new behavior — leading to either a design/code mismatch or an outdated test that no longer reflects real requirements. This is the RTM enabling **impact analysis**, directly tying back to Ch.10 Slide 13's point about unimplemented/changing requirements.

---

### Case Study 5 — Healthcare.gov (2013): Applying Traceability Concepts

**Scenario (from your slides):** Healthcare.gov required real-time integration across IRS, Social Security, DHS, and hundreds of private insurers. Federal policy guidance was finalized late, causing **500+ late requirement changes**. A late architectural decision (forcing full account creation before browsing plans) multiplied server load 10x. The prime contractor **had no formal RTM**, so it could not assess how late policy changes impacted the interfaces built by sub-contractors. On launch day: 250,000 concurrent users, 99% error rate, only 6 successful enrollments, $200M+ in emergency remediation.

**Q: Explain specifically how the _absence_ of a Requirements Traceability Matrix contributed to the failure, using the concepts of forward/backward tracing and impact analysis.**

**Model Answer:**

1. **No forward tracing across contractors:** Because there was no RTM linking federal policy requirements to each sub-contractor's specific interface/module, when a policy changed, the prime contractor had no reliable way to identify _which_ downstream integration components (built by different sub-contractors) needed to change. Without forward links (requirement → design → code across organizational boundaries), late changes couldn't be reliably propagated.
2. **No impact analysis capability:** The RTM is precisely the artifact that supports impact analysis (Ch.10 Slide 13). Without it, the team could not answer "if this requirement changes, what else breaks?" — so the architectural decision to require full account creation before browsing wasn't evaluated against its true downstream load impact until it was too late.
3. **Neglected NFR traceability:** Non-functional requirements (performance, scalability) were never properly specified _or_ traced to load-testing test cases — meaning there was no RTM row connecting "must support X concurrent users" to an actual test case, so the system was never realistically benchmarked.
4. **Result:** The system failed catastrophically on launch because gaps that a maintained RTM would have surfaced (unimplemented NFRs, unverified downstream interface impacts) were invisible until real users hit the system.

**One-line exam summary:** _Healthcare.gov shows that traceability isn't just paperwork — without it, an organization loses the ability to see the downstream consequences of a change before it's too late, which is exactly what a Requirements Traceability Matrix exists to prevent._

---

## Quick-Fire Revision Checklist

- [ ] Objective of process improvement = reduce cost, increase value
- [ ] 3 forms of resistance: time, change control seen as barrier, documentation seen as waste
- [ ] Fishbone diagram = Root Cause Analysis (People/Process/Project)
- [ ] Process Improvement Cycle = Assess → Plan → Create/Pilot/Rollout → Evaluate (repeat)
- [ ] "Valley of Despair" = performance dips before it improves; don't quit
- [ ] Process assets: Checklist, Example, Plan, Policy, Procedure, Template
- [ ] Requirements tracing procedure = a Requirements _Management_ process asset
- [ ] Elements of Risk Management = Assessment (Identify/Analyze/Prioritize), Avoidance, Control (Plan/Resolve/Monitor)
- [ ] **Exposure = Probability × Impact**
- [ ] RTM prevents unimplemented requirements + enables impact analysis
- [ ] Forward tracing = requirement → build (catches missing work)
- [ ] Backward tracing = build → requirement (catches gold-plating)
- [ ] Healthcare.gov = the flagship case study connecting risk failure + no RTM