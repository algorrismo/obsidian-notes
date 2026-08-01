---
tags:
  - SRE
  - midterm
title: SRE - Ch 05 - Finalizing Requirements Development
---

# SRE — Ch. 5: Finalizing Requirements Development

## Full Exam Prep Guide (Lecture 1 of 5)

> [!info] Exam format
> - **MCQ + True/False:** 50 × 1 = 50 marks
> - **Descriptive:** choose 3 of 6 → 3 × 10 = 30 marks
> 
> **Flagged high-probability short-question topics** (from your professor’s hints):
> 1. Types of prototypes and their comparison
> 2. MoSCoW technique with example
> 3. Calculating priority (value% / cost% / risk%) from a benefit-penalty-cost-risk table
> 4. Comparison of informal review techniques
> 5. Formal review technique — Inspection

> [!tip] How to use this file
> ⭐ = importance rating (⭐⭐⭐ = near-certain exam material)  
> 🚩 = common mistake students make  
> 🎯 = how the question is usually asked

# PART A — PROTOTYPES

## A1. Purpose of Prototypes ⭐⭐

Three reasons prototypes exist in requirements work:

1. **Clarify, complete, and validate requirements**
2. **Explore design alternatives**
3. **Create a subset that will grow into the ultimate product**

🎯 MCQ pattern: "Which of the following is NOT a purpose of prototyping?" — distractors usually insert something from _design/architecture phase_ (e.g., "finalize the database schema") to test if you know prototyping is a **requirements-phase** activity, not a construction activity.

---

## A2. Paper Prototypes ⭐

- Cheapest, fastest, lowest-tech way to explore how part of a system might look.
- Tools: paper, index cards, sticky notes, whiteboards — nothing sophisticated.
- Tests whether **users and developers share the same understanding** of requirements.
- Enables **rapid iteration** (iteration = key success factor in RD).
- Good **before** detailed UI design, evolutionary prototyping, or construction.
- Helps manage **customer expectations**.

🚩 Mistake: Students confuse "paper prototype" with "wireframe." Paper prototype = the _medium_ (physical, hand-drawn). Wireframe = a _specific technique_ using low-fidelity boxes/lines, which can be done on paper OR electronically.

---

## A3. Mock-ups (Horizontal Prototype) ⭐⭐

- Also called **horizontal prototype**.
- Focuses on **a portion of the UI** — does NOT go into all architectural layers or detailed functionality (this is the "horizontal" idea: wide UI coverage, shallow depth).
- Lets you explore specific behaviours to refine requirements.
- Helps users judge if the system will let them do their job reasonably.
- **Implies behaviour without implementing it.**
- Can demonstrate: functional options, look & feel (colors, layout, graphics, controls), navigation structure.
- When it's a _throwaway_ mock-up: user should focus on **broad requirements/workflow**, not obsess over pixel-perfect appearance.

🚩 Mistake: "Mock-up implements the backend" — **FALSE**. Mock-ups have **no working code/backend** (see comparison table below). This is a favorite True/False trap.

---

## A4. Wireframe ⭐⭐

- A specific approach to **throwaway prototyping**, common in UI/website design.
- Gives understanding of **three aspects**:
    1. **Conceptual requirements** — understand subject matter / what activities users want to perform on-screen
    2. **Information architecture / navigation design**
    3. **High-resolution, detailed page design**

🎯 MCQ pattern: match "wireframe" to "low fidelity, boxes & lines, no color" vs mock-up's "high fidelity, colors & fonts."

---

## A5. Proof of Concept (Vertical Prototype) ⭐⭐

- Also called **vertical prototype**.
- Implements **a slice of functionality from UI through ALL technical/service layers**.
- Works like the real system because it touches every implementation level.
- Tests **technical feasibility**, not look-and-feel.

🚩 Mistake: Students swap "horizontal" and "vertical." Memory trick:

- **Mock-up = Horizontal** → wide across the _surface_ (UI), shallow depth
- **Proof of Concept = Vertical** → drills _down_ through every layer, narrow slice

---

## A6. Comparison Table — ⭐⭐⭐ HIGH YIELD (on your short-Q list)

|Prototype Type|What it Tests|Look & Feel|Backend Code?|
|---|---|---|---|
|**Wireframe**|Structure & Navigation|Low fidelity (boxes & lines)|No|
|**Mock-up**|Aesthetics & Visual UI|High fidelity (colors & fonts)|No|
|**Proof of Concept**|Technical Feasibility|No fidelity (raw/ugly)|**Yes** (functional core)|

🎯 **Likely short question phrasing:** _"Compare wireframe, mock-up, and proof of concept in terms of purpose, fidelity, and backend implementation."_ **Answer skeleton:** State each prototype's definition (1 line) → fill this exact table → add one sentence per row explaining _why_ (e.g., "PoC has backend because it must prove technical feasibility, which requires real code touching all layers").

🚩 Mistake: Saying wireframe has "some code" — it has **none**, same as mock-up. Only PoC has functional code.

---

## A7. Throwaway vs. Evolutionary — Table 15-1 ⭐⭐

||Throwaway|Evolutionary|
|---|---|---|
|**Mock-up**|Clarify/refine requirements; identify missing functionality; explore UI approaches|Implement core + priority-based user requirements; implement/refine websites; adapt to changing business needs|
|**Proof of concept**|Demonstrate technical feasibility; evaluate performance; improve construction estimates|Implement/grow core multi-tier functionality & communication layers; optimize algorithms; test/tune performance|

**Key distinction (Future Use attribute, see A8):**

- **Throwaway** = discarded after generating feedback
- **Evolutionary** = grows into the final product through iterations

🎯 T/F trap: "An evolutionary prototype is always discarded." → **False**.

---

## A8. Classes of Prototype Attributes ⭐⭐

Three lenses to classify any prototype:

|Attribute|Meaning|
|---|---|
|**Scope**|Mock-up → focuses on user experience. Proof-of-concept → explores technical soundness (e.g., an ATM system)|
|**Future use**|Throwaway (discarded after feedback) vs. Evolutionary (grows into final product)|
|**Form**|Paper prototype (sketch on paper/whiteboard/drawing tool) vs. Electronic prototype (working software for part of the solution)|

🚩 Mistake: Confusing "Form" with "Future use" — Form is about the **medium** (paper vs. electronic); Future use is about the **fate** (throwaway vs. evolutionary). These are independent — you can have a throwaway _electronic_ prototype, or an evolutionary _paper_ one (rare but conceptually possible).

---

## A9. Incorporating Prototypes into the SDLC (Figure 15-1) ⭐

Cycle: **Elicit user requirements** → branches two ways:

- Left path: **Develop throwaway mock-up** → **Design user interface** → feeds into **Construct evolutionary prototype**
- Right path: **Develop/refine architecture** → **Construct proof of concept** → **Design software architecture** → feeds into **Construct evolutionary prototype**

Both converge → **Construct evolutionary prototype** → **Verify and deliver product incrementally** → also loops back to refine architecture (**begin next iteration**) and back to elicit requirements (**refine user requirements**) → Eventually: **Construct and verify product** → **Deliver product**

🎯 Likely MCQ: "Which prototype feeds into UI design?" → mock-up. "Which feeds into software architecture design?" → proof of concept.

---

## A10. Working with Prototypes / Dialog Map (Figure 15-2) ⭐

Flow: **Use Case → Dialog Map → Throwaway Prototype/Wireframe → Detailed UI Design**, with **feedback loops** flowing backward at every stage.

- **Dialog Map** = a UI modeled as a **state-transition diagram** representing interaction/navigation.

🚩 Mistake: Calling the Dialog Map a "data flow diagram" — it's specifically a **state-transition** model of navigation, not a data flow model.

---

## A11. Risks of Prototyping ⭐⭐

1. Pressure to release the prototype (as if it were the final product)
2. Distraction by details (user obsesses over visuals, misses functional gaps)
3. Unrealistic performance expectations
4. Investing excessive effort in prototypes

🎯 MCQ pattern: gives a scenario ("A client insists the prototype be shipped as-is because it 'looks done'") → identify the risk (**pressure to release**).

---

## A12. Prototyping Success Factors ⭐⭐

1. Include prototyping tasks in the **project plan** (schedule time/resources)
2. **State the purpose** before building — and what happens after (discard/archive vs. build upon)
3. **Plan multiple prototypes** — rarely right on first try (that's the point)
4. Build throwaway prototypes **fast and cheap** — minimum effort to answer the question
5. **Don't prototype what you already understand** (except to explore design alternatives)
6. **Don't expect a prototype to replace written requirements**

🚩 Mistake: Believing a good prototype eliminates the need for a requirements document — **False**, per point 6.

---

# PART B — PRIORITIZATION

## B1. Why Prioritize Requirements? ⭐

- High customer expectations + short timelines → must deliver the most critical/valuable functionality first.
- Prioritization = managing **competing demands for limited resources**.

## B2. Prioritization Pragmatics — 6 issues to understand ⭐⭐

1. Needs of the customers
2. Relative importance of requirements to customers
3. Timing of delivery
4. Requirements that are **predecessors** for others (dependencies)
5. Requirements that must be implemented **as a group**
6. **Cost** to satisfy each requirement (hard/soft cost)

🎯 T/F trap: "Prioritization only depends on customer importance." → False — cost, dependencies, and timing all matter too.

---

## B3. Prioritization Techniques Overview ⭐⭐

**In or Out** — simplest method. Stakeholders go down the requirement list, binary decision: in or out.

**Pairwise Comparison / Rank Ordering** — compare every requirement against every other requirement in pairs to judge relative priority, rather than guessing a number directly.

---

## B4. Worked Example: Paired Comparison Analysis ⭐⭐

**Scenario:** entrepreneur choosing between: (A) Overseas Market, (B) Home Market, (C) Customer Service, (D) Quality.

**How it works:** for every pair, mark which option wins and by how much (a small score, e.g. 1 or 2), then total each letter's wins.

**Result from the slide:** A = 3 (37.5%), B = 1 (12.5%), **C = 4 (50%)**, D = 0

**So Customer Service (C) is the top priority**, because it accumulated the most "wins" across all pairwise comparisons.

🎯 **How this could be examined:** They may give you a _smaller_ pairwise grid (e.g., 3 options instead of 4) and ask you to total the scores and rank them. **Method to practice:**

1. List every unique pair once (no repeats, no comparing an item to itself)
2. For each pair, note the winner
3. Tally total wins per item
4. Convert to % of total wins
5. Highest % = highest priority

🚩 Mistake: Comparing an item to itself, or double-counting a pair (A vs B is the same comparison as B vs A — don't count both).

---

## B5. Worked Example: Weighted Grid Analysis ⭐⭐

**Scenario:** choosing a car considering Cost, Board (storage for windsurfing board), Storage, Comfort, Fun, Look — each criterion has a **weight** reflecting its importance, and each option gets a raw score per criterion.

**Method:**

1. Assign a **weight** to each factor (how important is this factor overall?)
2. Score each option (car) against each factor
3. Multiply score × weight for each cell (or the slide's version pre-multiplies and just sums)
4. **Total = sum across all weighted factors**
5. Highest total = best option

From the slide: **Station Wagon scored highest (36)**, beating 4-Wheel Drive (28), Sports Car (27), and Family Car (25) — despite the person "always loving open-topped sports cars," the data-driven weighted analysis pointed elsewhere. This is the pedagogical point: **weighted grid analysis removes personal bias by forcing quantification.**

🎯 Likely descriptive/short question: _"Explain weighted grid analysis with an example and explain why it's more objective than gut-feeling prioritization."_

🚩 Mistake: Forgetting to multiply by weight — a factor with weight 5 (Storage) contributes more to the total than one with weight 1 (Storage-typo... careful, re-check which is 1 vs 5 in your specific table if given a new one on the exam). **Always show the weight × score step explicitly in your answer**, don't just write final totals.

---

## B6. MoSCoW Technique — ⭐⭐⭐ HIGH YIELD (on your short-Q list)

|Letter|Meaning|Consequence if omitted|
|---|---|---|
|**Must**|Requirement MUST be satisfied for the solution to succeed|Project fails / is illegal / cancelled|
|**Should**|Important, should be included if possible — NOT mandatory|Slightly poor UX, but system still works|
|**Could**|Desirable, could be deferred/eliminated — implement only if time/resources permit|Zero negative impact on core workflow|
|**Won't**|Will NOT be implemented now — may be included in a future release|Protects budget/deadline; deferred to next phase|

🎯 **How this is examined (guaranteed-style question):** _"Explain the MoSCoW technique with an example."_

**Model answer structure:**

1. Define MoSCoW and expand the acronym (1-2 lines)
2. One line per category — definition + consequence of omission (use table above)
3. **Give an original example** (don't just copy ZestyBites verbatim — adapt it or use a new app, e.g., a library management system, a hospital appointment app). Example:
    - Must: user login (app can't function without it)
    - Should: push notifications (nice, but SMS is a workaround)
    - Could: dark mode (cosmetic, zero core impact)
    - Won't: AI recommendations this cycle (deferred to Phase 2)

🚩 Mistake #1: Saying "Won't" means the requirement is bad/rejected forever — **False**. It just means "not now," it can return in a future release. 🚩 Mistake #2: Confusing "Should" and "Could" — the test is: _"can we survive with a temporary manual fix?"_ (Should) vs. _"is this a low-cost luxury with zero harm if skipped?"_ (Could).

---

## B7. Worked Example: ZestyBites Food Delivery App ⭐⭐

(3-month deadline scenario)

- **Must Have:** User Registration & Login, Restaurant Browsing (menus) — app cannot launch without these
- **Should Have:** Real-time GPS map tracking (workaround: SMS alerts like "driver picked up food")
- **Could Have:** Group Ordering, Advanced Scheduling (3 days ahead), Dark Mode
- **Won't Have:** AI meal recommendations, Cryptocurrency payments, Drone delivery — explicitly banned from current timeline to avoid scope creep

🎯 MCQ pattern: they'll give a NEW feature (e.g., "Push notification when order is confirmed") and ask you to classify it Must/Should/Could/Won't based on the "checklist question" logic — practice applying the **test question**, not memorizing the ZestyBites list itself, since the exam will likely use a different scenario.

---

## B8. MoSCoW Summary / Checklist Table ⭐⭐⭐

|Category|Checklist Question|Impact of Omission|
|---|---|---|
|Must Have|Can the system function legally, safely, fundamentally without this?|Project is cancelled or illegal|
|Should Have|Is this highly important, but can we survive day one with a manual fix?|Slightly poor UX, but fully operational|
|Could Have|Is this a low-cost luxury that doesn't hurt anyone if left out?|Zero negative impact on core workflow|
|Won't Have|Is this a cool idea we agree to ignore until next year?|Protects budget and strict deadlines|

**Memorize this table verbatim — it's the most "quotable" content in the whole prioritization section and is very likely to appear as an MCQ answer key or fill-in-the-blank.**

---

## B9. Three-Level Scale (Importance × Urgency) ⭐⭐

- **High priority** = important AND urgent (needed next release)
- **Medium priority** = important but NOT urgent (can wait for later release)
- **Low priority** = neither important nor urgent (can wait, perhaps forever)

Matrix (Importance columns × Urgency rows):

|Urgency ↓ / Importance →|Low|Medium|High|
|---|---|---|---|
|**Low**|Low & Low|Low & Medium|Low & High|
|**Medium**|Medium & Low|Medium & Medium|Medium & High|
|**High**|High & Low|High & Medium|**High & High**|

🚩 Mistake: Treating "Importance" and "Urgency" as the same thing — they're independent axes. A requirement can be important but not urgent (Medium priority).

---

## B10. Multipass Prioritization ⭐

- When using the three-level scale, you must watch for **requirement dependencies**.
- Problem case: a high-priority requirement depends on a lower-priority one that's scheduled later → conflict. You must re-pass through the prioritization to fix ordering issues caused by dependencies.

---

## B11. The $100 Test ⭐⭐

- Give the prioritization team **100 imaginary dollars**.
- They "buy" the requirements they want implemented — allocate more $ to higher-priority items (e.g., 9x vs 3x if one requirement is 3x as important).
- Once the $100 is spent, nothing else gets implemented in that release.
- Multiple stakeholders can each allocate their own $100; **sum the dollars per requirement** to find overall priority.

🎯 T/F trap: "The $100 method uses real money." → False, it's imaginary/symbolic dollars used purely to force relative weighting.

---

## B12. Prioritization Based on Value, Cost, and Risk — Participants ⭐⭐

- **Project manager / business analyst** — leads process, arbitrates conflicts, adjusts data
- **Customer representatives** (product champion/manager/owner) — supply **benefit and penalty** ratings
- **Development representatives** — supply **cost and risk** ratings

🚩 Mistake: Mixing up who provides which ratings. Memory trick: **Customers care about Consequences (Benefit/Penalty). Developers estimate Difficulty (Cost/Risk).**

---

## B13. Steps to Use the Prioritization Model — ⭐⭐⭐ HIGHEST YIELD (guaranteed calculation-style question)

**Step-by-step method:**

1. List all features/requirements in a spreadsheet
2. Customers rate **Benefit** (1–9): how useful is it? (1 = no one cares, 9 = extremely valuable)
3. Customers rate **Penalty** (1–9): how upset would people be if it's missing? (1 = no one minds, 9 = serious downside)
4. **Total Value = Benefit + Penalty**
5. Developers rate **Cost** (1–9): 1 = quick/easy, 9 = time-consuming/expensive
6. Developers rate **Risk** (1–9): probability of NOT getting it right first try (1 = trivial, 9 = serious feasibility concern)
7. Convert each column to a **percentage of column total**: Value%, Cost%, Risk%
8. Compute **Priority**:

> **Priority = Value% ÷ (Cost% + Risk%)**

**Higher priority number = implement first** (high value relative to how expensive/risky it is).

### Worked example from your slide (chemical stockroom system):

|#|Feature|Benefit|Penalty|Total Value|Value%|Cost|Cost%|Risk|Risk%|Priority|
|---|---|---|---|---|---|---|---|---|---|---|
|1|Print MSDS|2|4|8|5.2|1|2.7|1|3.0|1.22|
|2|Query vendor order status|5|3|13|8.4|2|5.4|1|3.0|1.21|
|3|Generate stockroom inventory report|9|7|25|16.1|5|13.5|3|9.1|0.89|
|5|Search vendor catalogs|9|8|26|16.8|3|8.1|8|24.2|0.83|
|10|Import chemical structures|7|4|18|11.6|9|24.3|7|21.2|**0.33 (lowest)**|

Note: **Feature 1 has the LOWEST total value (8) but the HIGHEST priority (1.22)** — because its cost and risk are also very low. This is the core insight: **priority isn't about raw value, it's about value relative to effort/risk.**

🎯 **How you'll be tested:** They will likely give you a small table (3–5 features) with Benefit/Penalty/Cost/Risk numbers and ask you to:

1. Compute Total Value for each
2. Compute Value%, Cost%, Risk% (each = row value ÷ column sum × 100)
3. Compute Priority = Value% / (Cost% + Risk%)
4. **State which feature should be built first**

**Practice this arithmetic tonight** — it's the single most "calculable" and therefore most fair/likely question type on the exam, since it has one objectively correct numeric answer.

🚩 Mistakes to avoid:

- Forgetting Priority uses **percentages**, not raw totals
- Dividing by Cost% × Risk% instead of Cost% **+** Risk%
- Forgetting Total Value = Benefit **+** Penalty (not multiplied)
- Rounding too early and compounding errors — carry decimals through

---

# PART C — VALIDATION, VERIFICATION & REVIEWS

## C1. Verification vs. Validation ⭐⭐⭐ (classic exam trap)

|Term|Question it answers|Focus|
|---|---|---|
|**Verification**|"Are we building the product **right**?"|Does the product meet its stated requirements?|
|**Validation**|"Are we building the **right** product?"|Does it satisfy actual customer needs?|

Requirements validation attempts to ensure:

- Requirements accurately describe intended capabilities/properties satisfying stakeholders
- Requirements are correctly derived from business requirements, system requirements, business rules
- Requirements are complete, feasible, verifiable
- All requirements are necessary; the full set is sufficient for business objectives
- All requirement representations are consistent (no conflicts)
- Requirements provide an adequate basis for design/construction

🎯 Guaranteed MCQ/TF format: a scenario is given ("Team checks whether the delivered app matches the written spec" = **Verification**; "Team checks with users whether the app actually solves their problem" = **Validation**). Practice flipping between these — this is one of THE most commonly mis-swapped pairs in all of software engineering exams.

---

## C2. Reviewing Requirements — Informal Techniques ⭐⭐⭐ HIGH YIELD (on your short-Q list)

|Feature|Peer Desk Check|Pass Around|Walkthrough|
|---|---|---|---|
|**Core concept**|Author asks ONE trusted colleague to review|Author distributes to MULTIPLE reviewers concurrently (email/shared drive)|Author leads a LIVE meeting, steps through line by line|
|**Interaction**|Async or brief 1-on-1|Strictly asynchronous, independent work|Synchronous, real-time group discussion|
|**# Reviewers**|Exactly one|Multiple (typically 2–5)|Group of diverse stakeholders (Dev, QA, BA, Client)|
|**Advantages**|Low overhead, fast, good for raw drafts|Diverse perspectives at once, saves meeting time, no scheduling needed|Resolves ambiguity instantly, ensures cross-functional alignment, finds logical gaps|
|**Disadvantages**|High risk of missing errors (single biased/tired reviewer), limited viewpoint|No synergy/debate, easy to ignore the request|Can devolve into design/brainstorm meeting, time-consuming for groups|
|**Best used when**|Fresh draft, want a sanity check|Need input from busy experts who can't coordinate a meeting|Complex/novel requirements involving conflicting business areas|

🎯 **Likely short question:** _"Compare peer desk check, pass around, and walkthrough."_ **Model answer structure:** Define each in 1 sentence → present the table above (or a condensed version) → give 1 example scenario where each is the best choice (use the "Best used when" row).

🚩 Mistake: Calling Pass Around "synchronous" — it's **strictly asynchronous** (this is its defining, most-tested feature). Also, don't confuse "Walkthrough" (author-led, live) with "Inspection" (formal, structured, has defined roles — see below).

---

## C3. Reviewing Requirements — Formal (Inspection) ⭐⭐⭐ HIGH YIELD (on your short-Q list)

- Formal peer reviews follow a **well-defined process** and produce a **report** identifying: material examined, reviewers, and the team's judgment on acceptability.
- The best-established formal review type = **Inspection** — one of the **highest-leverage software quality techniques available**.

### Inspection Participants

- **Author** of the work product (and peers of similar competence — Analyst)
- **Sources** of information feeding into the item (Customer)
- People who will **do work based on** the item (Developer)
- People **responsible for interfacing systems** affected by the item

### Inspection Roles

- **Author**
- **Moderator**
- **Reader**
- **Recorder**

🚩 Mistake: Confusing "Participants" (who's in the room / why they're relevant — customer, developer, etc.) with "Roles" (the job each person does during the session — moderator, reader, recorder, author). These are two DIFFERENT lists in the slide, and the exam may test this distinction directly.

### Entry Criteria (before inspection can begin)

- Document conforms to standard template; no obvious spelling/grammar/formatting issues
- Line numbers/unique identifiers present (for referencing specific locations)
- All open issues marked **TBD** or tracked in an issue-tracking tool
- Moderator found **≤3 major defects** in a 10-minute sample check

### Inspection Stages (Figure 17-2) ⭐⭐

**Initial Work Product → Planning → Preparation → Inspection Meeting → Rework → Follow-Up → Baselined Work Product**

- Dotted lines: rework may loop back to Preparation if extensive re-inspection is needed.

🎯 MCQ: order these stages correctly, or identify "which stage comes right after the Inspection Meeting?" → **Rework**.

### Exit Criteria (before inspection is considered done)

- All issues raised have been addressed
- Any changes made were made **correctly**
- All open issues resolved, OR each has a documented resolution process, target date, and owner

🎯 **Likely short question:** _"Explain the formal Inspection review technique, including its roles, entry criteria, and exit criteria."_ **Model answer structure:** 1 line defining Inspection → list the 4 roles → list entry criteria (bullet, 3-4 points) → describe the stage flow briefly → list exit criteria (bullet, 3 points). This lets you hit almost every sub-fact for full marks on a 10-mark question.

---

## C4. Defect Checklist ⭐⭐

**Completeness:**

- Do requirements address all known needs?
- Missing info marked TBD?
- Algorithms specified where needed?
- All external hardware/software/comm interfaces defined?
- Expected behaviour documented for error conditions?
- Adequate basis for design and test?
- Implementation priority included?
- In scope for this release/iteration?
- Actually necessary for the product?

**Correctness:**

- Any conflicting/duplicate requirements?
- Clear, concise, unambiguous, grammatically correct?
- Error messages clear/meaningful?
- Technically feasible within constraints?

**Quality Attributes:**

- Quality objectives properly specified, quantified, with trade-offs stated?
- Quality requirements measurable and verifiable?

🚩 Mistake: Mixing up "Completeness" items (is everything _there_?) with "Correctness" items (is what's there _right_?). If a question gives you a checklist item and asks which category it belongs to, ask: _"missing info vs wrong/conflicting info?"_

---

## C5. Requirements Review Tips ⭐

- Plan the examination (focus on sections, don't read the whole thing blind)
- Start early (catch major defects sooner)
- Allocate sufficient dedicated time
- Provide context to reviewers unfamiliar with the project
- Set review scope (what to examine, what to look for)
- Limit re-reviews (max ~3 times on the same material)
- Prioritize high-risk / frequently-used functionality for review

## C6. Requirements Review Challenges ⭐

- Large requirements documents
- Large inspection teams
- Geographically separated reviewers
- Unprepared reviewers

---

# PART D — TESTING & USE OF REQUIREMENTS

## D1. Prototyping in Requirements Validation ⭐

- Prototypes are validation tools that make requirements real
- Help find missing requirements **before** expensive dev/test activities
- Confirm shared stakeholder understanding
- **Proof-of-concept prototypes demonstrate feasibility**

## D2. Testing the Requirements (Figure 17-5) ⭐⭐

Two parallel derivations from **User Requirements**:

- **Analyst** path → Functional Requirements & Analysis Models
- **Tester** path → Test Cases & Scenarios
- These two are **compared** against each other (consistency check)
- Similarly, **Technical/UI Designs** (from Functional Requirements) are **compared** against **Test Procedures & Scripts** (from Test Cases)

**Key idea:** development and testing artifacts are derived from a **common source** (the requirements) — enabling traceability and cross-checking.

## D3. V-Model of Software Development ⭐⭐

Left side (definition) mirrors right side (testing), connected across:

- User requirements ↔ Acceptance testing
- Functional requirements ↔ System testing
- Architecture ↔ Integration testing
- Design ↔ Unit testing
- Bottom point: **Coding**

🎯 MCQ: "Which testing phase corresponds to Architecture?" → **Integration testing**.

## D4. Acceptance Criteria & Tests ⭐⭐

**Acceptance criteria** — conditions that must hold before a product is accepted:

- High-priority functionality present and working
- Essential non-functional criteria/quality metrics satisfied
- Remaining major open issues/defects resolved
- Legal/regulatory/contractual conditions satisfied
- Supporting materials (training, infrastructure) available

**Acceptance tests** — focus on **normal flows** of use cases and their exceptions; **less** attention to rarely-used alternative flows.

🚩 Mistake: Assuming acceptance tests must cover every alternative flow exhaustively — the slide explicitly says **less attention** to those.

## D5. Use of (Baselined) Requirements — Figure 19-1 ⭐

Baselined Requirements drive three things:

|Drives →|Actions|
|---|---|
|**Project Plans**|Size the project/iteration; base estimates on product size; update plans as requirements change; use priorities to drive iterations|
|**Designs & Code**|Developers review requirements; quality attributes drive architecture; allocate requirements to components; trace requirements to designs/code|
|**Tests**|Start test design early; users create acceptance tests; base system testing on requirements; trace requirements to tests|

---

# PART E — RAPID-FIRE TRAP BANK (practice yourself, not real exam Qs)

Use these to self-test — cover the right column and try to answer True/False or fill-in first.

|Statement|T/F|Why|
|---|---|---|
|A mock-up has working backend code.|**False**|Only Proof of Concept has functional backend code.|
|Wireframe is high-fidelity with color and fonts.|**False**|Wireframe = low fidelity, boxes & lines. Mock-up = high fidelity.|
|An evolutionary prototype is always thrown away.|**False**|Throwaway is discarded; evolutionary grows into the product.|
|"Won't Have" in MoSCoW means permanently rejected.|**False**|It's deferred, may return in a future release.|
|Pass Around reviews happen in real time as a group.|**False**|Pass Around is strictly asynchronous.|
|Verification asks "did we build the right product?"|**False**|That's Validation. Verification = "did we build it right (per spec)?"|
|Inspection's exit criteria require zero open issues at all times.|**False**|Open issues may remain if each has a documented resolution plan, date, and owner.|
|Priority = Value% ÷ (Cost% + Risk%).|**True**|Core formula — memorize exactly.|
|The $100 test uses actual currency allocations by finance.|**False**|Imaginary dollars, used purely for relative weighting.|
|Acceptance tests must cover every alternative flow in depth.|**False**|Focus is on normal flows + their exceptions; less attention to rare alternative flows.|

---

# PART F — Descriptive Question Prep (pick-3-of-6 strategy)

Given your professor's hints, these 5 areas are near-certain descriptive candidates — prepare all 5 deeply so that whichever 3 appear, you're ready:

1. **Types of prototypes and comparison** → use Section A6 table + A3/A4/A5 definitions. Structure: define each type (2 lines) → comparison table → 1 example use-case per type.
2. **MoSCoW with example** → use Section B6 + B8 tables + an original worked example (not copy-pasted ZestyBites — adapt names).
3. **Priority calculation (value%/cost%/risk%)** → use Section B13. Practice the arithmetic with a fresh small table so you're fast under time pressure. Always show your working (Value = Benefit+Penalty, then %, then formula) — partial marks are usually awarded per step.
4. **Comparison of informal review techniques** → use Section C2 table, emphasize the "Interaction mode" and "Best used when" rows as they're the most distinguishing/testable facts.
5. **Formal review (Inspection)** → use Section C3: roles → entry criteria → stages → exit criteria, in that order, for a complete structured answer.

**General descriptive-answer strategy for a 10-mark question:**

- Spend the first 1–2 lines on a crisp definition
- Use bullet points or a small table — examiners scan for keywords/structure, not prose
- Include at least one concrete example
- If the topic has a "compare X vs Y" shape, always end with a direct one-line contrast statement

---

# Quick Cram Sheet (night-before, 5-minute reread)

- Mock-up = horizontal, UI only, no code. PoC = vertical, all layers, has code.
- Wireframe = low-fi structure. Mock-up = high-fi look. PoC = no fidelity, raw.
- Throwaway = discarded. Evolutionary = grows into product.
- MoSCoW: Must=can't function without it. Should=temporary fix ok. Could=zero-harm luxury. Won't=deferred, not dead.
- Priority = Value% ÷ (Cost% + Risk%). Value = Benefit + Penalty.
- Verification = built it right (per spec). Validation = built the right thing (per user need).
- Peer Desk Check = 1 reviewer. Pass Around = many, async. Walkthrough = live meeting, author-led.
- Inspection roles: Author, Moderator, Reader, Recorder.
- Inspection stages: Planning → Preparation → Inspection Meeting → Rework → Follow-Up → Baselined.
- V-Model pairs: User req↔Acceptance test; Functional req↔System test; Architecture↔Integration test; Design↔Unit test.