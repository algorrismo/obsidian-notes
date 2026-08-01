---
title: "SRE - Lecture 1: The Essential Software Requirement"
tags:
  - SRE
exam-weight: "MCQ/TF: 50×1=50 | Descriptive: 3 of 6 × 10 = 30"
---

# 📘 Lecture 1 — The Essential Software Requirement

### Faculty Notes for Midterm Prep

> [!info] Legend
> ⭐ = **High-yield** (very likely MCQ/TF/short answer)  
> 🎯 = **Likely descriptive** (10-mark) question  
> ⚠️ = Common student mistake

---


## 1. Why Requirements Matter (Intro Section)

### 1.1 The "Tree Swing" Cartoon ⭐

Shows how the same idea gets distorted at each stage: customer explains it → PM understands it → analyst designs it → programmer writes it → business consultant describes it → **what the customer actually needed**.

- **Point of the cartoon:** miscommunication at every handoff between stakeholders is the root of most software failure — not bad coding.
- ⚠️ **Mistake:** Students think this cartoon is "just a joke" and skip it. Examiners _do_ ask TF/MCQ like: _"The tree-swing cartoon illustrates poor communication in the requirements process. (T/F)"_ → **True**.

### 1.2 Current Common Problems ⭐

Memorize these as a _list_ — MCQs love picking one out and asking "which of the following is a common requirements problem?"

- Business objectives/vision/scope never clearly defined
- Lack of communication — customers too busy to work with analysts/devs
- Customers claim _all_ requirements are critical → no prioritization
- Developers guess when they hit ambiguity/missing info
- Requirements never approved by customer
- Requirements approved, then **changed continually**
- Scope increases but schedule/resources don't
- Change requests get lost — no status tracking
- Built functionality that's **never used**
- Spec satisfied, but business objective/customer **not** satisfied

🎯 **Likely descriptive question:** _"List and explain any five common problems in requirements engineering."_ **How to answer:** Pick 5, one line each (cause) + one line each (consequence). Don't just list bullet phrases — examiners want you to explain _why_ it's a problem.

⚠️ **Mistake:** Confusing "customer never approved requirements" with "customer approved then changed them" — these are **two separate, distinct problems**. Don't merge them into one point.

---

## 2. Root Causes of Project Failure/Success ⭐⭐ (High-yield numbers)

|Failure Causes|%|Success Causes|%|
|---|---|---|---|
|Lack of user input|13%|User involvement|16%|
|Incomplete requirements/specs|12%|Executive management support|14%|
|Changing requirements/specs|12%|Clear statement of requirements|12%|

- **Memory trick:** Success % > Failure % across the board (16>13, 14>12, 12>12-tie) — user involvement is the single biggest lever in _both_ directions.

⚠️ **Mistake:** Numbers get swapped in MCQs (e.g., "Lack of user input causes 16% of failures" — **False**, that's actually the _success_ stat for user involvement, not the failure stat).

🎯 Possible short question: _"What are the top three causes of software project failure according to requirements research?"_ — Answer with the table above, briefly explained.

---

## 3. Relative Cost to Repair a Defect (200:1 Rule) ⭐⭐

|Stage|Relative Cost|
|---|---|
|Requirements time|0.1 – 0.2|
|Design|0.5|
|Coding|1|
|Unit test|2|
|Acceptance test|5|
|Maintenance|20|

- **Core idea:** the later a defect is found in the lifecycle, the _exponentially_ more expensive it is to fix — up to **200 times** more expensive at maintenance vs. requirements phase.
- ⭐ **Very likely MCQ:** "At which stage is defect repair cheapest?" → **Requirements time**. "At which stage is it most expensive?" → **Maintenance**.

⚠️ **Mistake:** Students think "1" (coding) is the baseline for the "200:1" ratio. Actually the ratio is comparing **maintenance (20) vs requirements (0.1)** = 200:1. Know this calculation, examiners sometimes ask you to _derive_ the ratio.

🎯 **Descriptive potential:** _"Explain the relative cost to repair a defect across the software lifecycle, with the 200:1 rule."_ Draw the pyramid, explain increasing cost, explain **why** (more artifacts/code/tests depend on it by the time it's caught later).

---

## 4. The Leakage Problem ⭐⭐

Defects found at each phase (in %):

|Phase|% of requirement defects found here|
|---|---|
|Requirements analysis (ideal)|**74%**|
|Preliminary/high-level design|4%|
|Detailed design|7%|
|Maintenance (worst case)|4%|

- ⚠️ **Mistake:** Note the numbers **don't sum to 100%** in the slide (74+4+7+4 = 89%) — the deck doesn't explicitly cover the remaining %, don't panic if an MCQ asks for the "missing" phase (likely testing/coding, not explicitly given in these slides — if asked, answer with what's given and note testing phases account for the rest).
- **Ideal takeaway:** requirements analysis phase is the cheapest/best place to catch requirement errors — 74% _should_ be caught there.

⭐ Likely TF: _"The majority of requirement-related defects are found during requirements analysis. (True)"_

---

## 5. What Is a "Requirement"? 🎯⭐ (Core Definition — MUST KNOW verbatim-ish)

> **A requirement is a property that a product must have to provide value to a stakeholder.**

Key facts to reproduce exactly:

- Requirements = specification of _what_ should be implemented (not _how_)
- Descriptions of system property/attribute/behavior, or a **constraint** on development
- Encompass **two views**:
    - User's view of external system behavior
    - Developer's view of internal characteristics
- **Time dimension** of requirements:
    - **Present tense** — current capability
    - **Near-term (high priority)** or **hypothetical (low priority) future**
    - **Past tense** — needs once specified, later discarded

⚠️ **Mistake:** Students only remember "present and future" and forget the **past tense** dimension (discarded requirements) — this is a favorite trick MCQ option.

🎯 **Very likely descriptive question:** _"Define 'requirement.' Explain the time dimension of requirements with examples."_

---

## 6. The Three Levels of Requirements 🎯⭐⭐⭐ (THE most important topic in this lecture)

```
Business Requirement (business goal)
        ↓
User Requirement (user need)
        ↓
Functional Requirement (system behavior)
```

### 6.1 Business Requirements

- **Why** the organization is building the system — business benefit
- Focus = business objectives of org/customer
- Can **conflict** if gathered from multiple sources
- Example: _Airline wants to cut counter staff cost by 25% → build a check-in kiosk_
- **Sources:** funding sponsor, acquiring customer, manager of users, marketing dept, product visionary

### 6.2 User Requirements

- Goals/tasks users must perform with the product to get value
- Represented via **use cases** and **user stories**
- Example use case: _"Check in for a flight"_
- Example user story: _"As a passenger, I want to check in for a flight so I can board my airplane."_
- ⚠️ **Mistake:** Confusing use case wording ("Check in for a flight") with user story format ("As a [role], I want [goal], so that [benefit]"). **Know both formats — you may be asked to convert one into the other.**

### 6.3 Functional Requirements

- Specify **behaviors** the product exhibits under specific conditions
- What developers must implement so users can accomplish tasks (satisfying business requirements)
- Written in **"shall" statements**:
    
    > "The Passenger **shall** be able to print boarding passes..."
    
- A **constraint** = restriction imposed on developer's design/construction choices (e.g., "must use open-source tools and run on Linux")

⚠️⚠️ **BIGGEST TRAP in this lecture:** Distinguishing a **functional requirement** from a **constraint**. A functional requirement describes _behavior_; a constraint restricts _how_ it's built. Expect an MCQ giving a statement and asking "Is this a functional requirement or a constraint?"

### Full Example Chain (memorize this table — high MCQ/matching potential) ⭐

|BR|UR|FR|
|---|---|---|
|Increase food delivery orders by 30%/year via digital platform|Customers should order food online from nearby restaurants|System shall allow browsing menus, adding to cart, placing orders|
|Improve customer satisfaction via delivery transparency|Customers should track order status/location in real time|System shall display status (Confirmed/Preparing/Out for Delivery/Delivered) + live map|
|Reduce cancellations from payment issues|Customers should pay securely via multiple methods|System shall integrate payment gateways: cards, mobile banking, wallets|

🎯 **Extremely likely descriptive question (this is basically guaranteed given your listed topics):** _"Explain the three levels of requirements with a suitable example."_ **How to answer:**

1. Define all 3 levels (one line each)
2. Draw/state the flow: Business → User → Functional
3. Give ONE clean example chain end-to-end (use the food delivery or airline example above, or invent your own e.g. hospital: "Reduce patient waiting time" → "Patients want to book appointments online" → "System shall allow slot booking and display queue position")
4. Mention that alignment across all 3 levels = key to project success

---

## 7. Working with the Three Levels (Stakeholder Roles) ⭐

|Level|Corporate Role|Commercial Role|
|---|---|---|
|Business Requirements|Manager|Marketing|
|User Requirements|Business Analyst + User Reps|Product Manager|
|Functional Requirements|Business Analyst|Business Analyst/Product Manager|
|(Output goes to)|Developer, Tester|Developer, Tester|

⚠️ **Mistake:** Mixing up which role owns which document — Business Analyst appears at **both** User and Functional levels; don't assume one person = one level only.

---

## 8. System Requirements ⭐

- For products composed of **multiple components/subsystems**
- Can be all-software, or software + hardware (e.g., biometric device)
- **People and processes are part of a system** — some functions may be allocated to humans, not software
- Classic example: **supermarket cashier workstation** — barcode scanner + scale + handheld scanner + keyboard + display + cash drawer
- System requirements → business analyst derives specific functionality → **allocated** to individual subsystems + interfaces between them

⚠️ **Mistake:** Students think "system requirement" = same as "functional requirement." It's actually a **broader concept** — describes the whole system of components, which functional requirements then get allocated into.

---

## 9. Non-Functional Requirements (NFRs) 🎯⭐⭐

- Also called **"quality attributes"** — the "-ity/-ilities" (usability, reliability, scalability, portability, etc.)
- Describe **service or performance characteristics**, not behavior
- Important to users **or** developers/maintainers: performance, safety, availability, portability
- **High chance of conflict** between different NFRs (e.g., security vs. usability, performance vs. portability)
- Other NFR classes:
    - **External interfaces** — connections to other software, hardware, users, communication (→ **interoperability**)
    - **Design/implementation constraints** — restrict developer's options (→ **security**)

⚠️⚠️ **Common trap:** Telling apart a **Functional Requirement** ("shall allow user to...") from a **Non-Functional Requirement** ("shall respond within 2 seconds," "shall be available 99.9% of the time"). NFRs describe **quality/how well**, FRs describe **what** the system does.

🎯 **Very likely descriptive question:** _"What are non-functional requirements? Explain with examples and how they differ from functional requirements."_

---

## 10. Business Rules ⭐

- Corporate policies, government regulations, industry standards, computational algorithms
- **NOT themselves software requirements** — they exist independent of any specific software (⭐ frequently tested distinction)
- They _dictate_ that the system must contain functionality to comply (e.g., online purchase limit)
- A restriction on developer's choices, e.g.: "no red colour in webpage" — called an **Inverse requirement**
- Sometimes the origin of quality attributes → implemented as functionality (e.g., corporate security policy → firewall)
- You can **trace** a functional requirement's origin back to a business rule

⚠️ **Mistake:** Thinking business rules ARE requirements. Exam trick TF: _"Business rules are a type of software requirement. (False — they exist outside the software's boundary, but give rise to requirements)."_

---

## 11. Feature ⭐

- One or more **logically related system capabilities** that provide value to a user
- Described by a **set of functional requirements**
- One feature can encompass **multiple user requirements**
- Example: "Bookmarks" feature in a web browser → user requirements like "Add a Bookmark," "Edit Bookmarks" → each has functional requirements underneath

⚠️ **Mistake:** Confusing "feature" with "functional requirement" — a feature is a **higher-level grouping**; functional requirements are the detailed behaviors _under_ a feature.

---

## 12. Relationships Diagram (Figure 1-1) 🎯

Chain of influence/storage:

```
Business Rules → (origin of) → Business Requirements → Vision & Scope Document
                → (origin of) → Quality Attributes
                → (origin of) → External Interfaces / Constraints influence Functional Requirements

Business Requirements → User Requirements → User Requirements Document
User Requirements → Functional Requirements
System Requirements → Functional Requirements
Functional Requirements + Quality Attributes + External Interfaces + Constraints → Software Requirements Specification (SRS)
```

- **Solid arrows = "are stored in"**
- **Dotted arrows = "are the origin of / influence"**

⚠️ **Mistake:** Mixing up solid vs dotted arrow meaning — this is a classic diagram-based MCQ ("What does a dotted arrow represent in Figure 1-1?").

---

## 13. Product vs. Project Requirements 🎯⭐

- **Product requirements** = properties of the software system to be built → go in the **SRS**
- **Project requirements** = other deliverables/expectations necessary for project success, but **not part of the software itself** (e.g., maintaining a schedule deadline)
- **SRS should NOT include:** design/implementation details (except known constraints), project plans, or test plans — keep requirements development focused on _what_ to build

### Examples of Project Requirements (list to memorize, ⭐ MCQ-friendly):

- Physical resources (workstations, hardware, test labs/tools, team rooms, videoconferencing)
- Staff training / user documentation (tutorials, manuals, release notes)
- Infrastructure changes in operating environment
- Release/install/configuration/installation-testing procedures
- Beta testing, manufacturing, packaging, marketing, distribution
- Customer service-level agreements (SLAs)
- Legal protection (patents, trademarks, copyrights)

⚠️⚠️ **High-value trap:** Given a list of items, identify which are **product** vs **project** requirements. E.g., "The system shall support 10,000 concurrent users" = product. "The team needs a dedicated test lab by March" = project.

🎯 **Descriptive potential:** _"Differentiate between product and project requirements with examples."_

---

## 14. Requirements Engineering: Development & Management 🎯🎯⭐⭐⭐ (Explicitly on your short-question list)

```
Requirements Engineering
        ├── Requirements Development
        │        ├── Elicitation
        │        ├── Analysis
        │        ├── Specification
        │        └── Validation
        └── Requirements Management
```

### 14.1 Elicitation

- Identify expected **user classes** and other stakeholders
- Understand user tasks/goals + business objectives they align to
- Learn about the **environment** the product will be used in
- Work with representatives of each user class → functionality needs + quality expectations

### 14.2 Analysis

- Model the application environment
- Distinguish user info into: functional requirements, quality expectations, business rules, suggested solutions
- **Decompose** high-level requirements into detail
- **Allocate** requirements to software components (system architecture)
- **Negotiate** priority and implementation order

### 14.3 Specification

- Business analyst documents requirements in the **SRS**
- Transcribe user needs → written requirements + diagrams for review/comprehension
- SRS describes expected behavior fully; used in dev, testing, QA, PM
- Adopt requirement **templates** (standardized writing)
- Identify **requirement origins**
- **Uniquely label** each requirement (for cross-referencing/cross-cutting requirements)

### 14.4 Validation

- Review the SRS before dev team accepts it — check: **feasible, consistent, complete**
    - **Consistency** = no contradictory requirements
    - **Completeness** = no missing needed services/constraints
    - Also: discard unnecessary requirements
- Develop **acceptance tests/criteria** to confirm requirements meet customer needs & business objectives
- **Simulate** requirements (e.g., wireframing) to catch errors early

⚠️⚠️⚠️ **MOST COMMON CONFUSION IN THE WHOLE LECTURE:** Students mix up which activity belongs to **Development** vs **Management**, and within Development, which of the 4 sub-phases a given activity belongs to. Practice matching:

- "Talking to stakeholders to understand needs" → **Elicitation**
- "Writing 'shall' statements in a document" → **Specification**
- "Checking requirements are consistent and complete" → **Validation**
- "Deciding which component a requirement belongs to" → **Analysis**
- "Tracking change requests" → **Management** (not Development!)

🎯 **This is explicitly one of your listed likely short questions** — practice writing a clean 4-sub-phase answer with 2-3 bullet points each, in order: Elicitation → Analysis → Specification → Validation.

---

## 15. The Requirements Development Process Framework (Iterative) 🎯⭐

Figure 3-1 shows it's **iterative**, not linear:

```
Elicitation → Analysis → Specification → Validation
   ↑ clarify     ↑ close gaps  ↑ rewrite
   ←────────────── re-evaluate ─────────────
   ←──────────────── confirm and correct ────
```

### The 17-Step Framework (Figure 3-2) — know the ORDER, this is very testable ⭐⭐

**Phase A (once per project):**

1. Define business requirements
2. Identify user classes
3. Identify user representatives
4. Identify requirements decision makers
5. Plan elicitation
6. Identify user requirements
7. Prioritize user requirements

**Phase B (repeats per iteration):** 8. Flesh out user requirements _(expand)_ 9. Derive functional requirements 10. Model the requirements 11. Specify nonfunctional requirements 12. Review requirements 13. Develop prototypes 14. Develop or evolve architecture 15. Allocate requirements to components 16. Develop tests from requirements 17. Validate user/functional/nonfunctional requirements, analysis models, prototypes

→ **Repeat steps 8–17 for iteration 2, 3, ... N**

⚠️ **Mistake:** Thinking ALL 17 steps repeat each iteration — only **steps 8–17 repeat**; steps 1–7 happen once at the start.

🎯 Possible question: _"Explain the requirements development process framework and why it is iterative."_

### Effort Distribution Over Time (Figure 3-3) ⭐

- **Waterfall/Sequential** — huge spike of effort early, then drops off
- **Iterative/Phased** — smaller repeated bumps
- **Agile/Incremental** — frequent small bumps, **timeboxed (e.g., 1 month)**

⭐ Likely MCQ: _"Which lifecycle model shows one large upfront spike in requirements effort?"_ → **Waterfall**

---

## 16. Requirements Management 🎯🎯⭐⭐⭐ (Explicitly on your short-question list)

Core activities:

- Establish a **requirements change control process**
- Perform **impact analysis** on changes
- **Track status** of each requirement + track requirements issues
- Maintain a **history** of requirement changes
- Maintain a **requirements traceability matrix**:
    - Relationships/dependencies **between** requirements
    - Trace individual requirements → design, source code, **and tests**

⚠️ **Mistake:** Forgetting traceability goes in **both directions** — requirement-to-requirement AND requirement-to-(design/code/test). Exams like to test "traceability matrix" definition precisely.

### The Development ↔ Management Boundary (Figure 1-5) 🎯⭐⭐ — **Explicitly on your list!**

```
Marketing, Customers, Management → requirements
        ↓
   Analyze, Document, Review, Negotiate     [Requirements DEVELOPMENT]
        ↓
   ══════ BASELINED REQUIREMENTS ══════     ← THE BOUNDARY LINE
        ↓                        ↑
Requirements Change Process ←──────────    [Requirements MANAGEMENT]
   ↑ (current baseline)      ↑ (revised baseline)
Marketing/Customers/Mgmt → requirement changes
Project Environment → project changes
```

- **Baselined Requirements** = the reviewed, agreed-upon, "frozen for now" set of requirements that marks the handoff point between **Development** (creating/analyzing requirements) and **Management** (controlling changes to them going forward).
- Everything **above** the baseline = Requirements Development.
- Everything **below/around** the baseline (the change process) = Requirements Management.
- Once baselined, any modification must go through the **Requirements Change Process**, which produces a **revised baseline** — this is a cycle, not a one-time event.

⚠️⚠️ **This diagram is explicitly flagged as a likely short question — expect to redraw or explain it.** The single most important sentence to memorize:

> _"Baselined requirements represent the boundary between requirements development and requirements management — once requirements are baselined, changes to them are handled through the requirements change control process rather than through further development activity."_

🎯 **Guaranteed-style question:** _"What is a baselined requirement? Explain the boundary between requirements development and requirements management."_ **How to answer:** Define baseline → draw/describe the diagram → explain the change process loop (current baseline → change process → revised baseline) → mention inputs from Marketing/Customers/Management and Project Environment.

---

## 17. Role of Requirements (The Quote) ⭐

> _"The hardest single part of building a software system is deciding precisely what to build... No other part of the work so cripples the resulting system if done wrong. No other part is more difficult to rectify later."_

- This is a well-known quote (commonly attributed to Fred Brooks, _The Mythical Man-Month_ — the slide doesn't attribute it, but know the **content**, not necessarily the author, since it's not named in your deck).
- Core message: getting requirements right is the **hardest and most consequential** part of software engineering.

⭐ Likely TF/MCQ paraphrase: _"According to the lecture, requirements are the easiest part of building software. (False)"_

---

## 18. Reasons Behind Bad Requirements ⭐⭐

- **Insufficient user involvement**
- **Inaccurate planning**
- **Creeping user requirements** — gradually increasing/changing scope
- **Ambiguous requirements** — e.g., "respond as soon as possible" (no measurable definition)
- **Gold plating** — extra functionality beyond what was specified
- **Overlooked stakeholders**

⚠️⚠️ **Common trap:** Confusing **"Gold plating"** with **"Creeping requirements."**

- **Gold plating** = developer/team adds unrequested extra features on their own initiative
- **Creeping requirements** = customer keeps adding/changing requirements over time These are DIFFERENT causes and DIFFERENT sources (dev-driven vs customer-driven) — a favorite MCQ distinction.

🎯 Possible short question: _"List and explain reasons behind bad requirements, giving an example for ambiguous requirements."_

---

## 19. Benefits of a High-Quality Requirements Process ⭐

Memorize as a list (great MCQ "which is NOT a benefit" material):

- Fewer defects (requirements + delivered product)
- Reduced development rework
- Faster development and delivery
- Fewer unnecessary/unused features
- Lower enhancement costs
- Fewer miscommunications
- Reduced scope creep
- Reduced project chaos
- Higher customer/team satisfaction
- Products that do what they're supposed to do

---

## 20. In-Class Practice Tasks (from the slides — solve these yourself before the exam!)

### Task 1: Classify as Business / User / Functional

|Statement|Type|
|---|---|
|Increase online sales by 25% within one year|**Business**|
|Customers should be able to search products by category|**User**|
|The system shall allow users to filter products by price range|**Functional**|
|Reduce customer service calls by 30%|**Business**|
|Customers should be able to track order status|**User**|
|The system shall send an email when an order is shipped|**Functional**|

### Task 2: Requirement Levels — "Reduce waiting time in a hospital"

|Level|Requirement|
|---|---|
|Business|Reduce patient waiting time|
|User|Patients should be able to book appointments in advance / check queue status online|
|Functional|The system shall allow patients to book a time slot online|
|Functional|The system shall display the current queue number/position to patients|
|Functional|The system shall send a notification when it's nearly the patient's turn|

⚠️ **These exact fill-in-the-blank style tasks are HIGH RISK to reappear on the exam with different scenarios (e.g., banking, e-commerce, school). Practice creating your own Business→User→Functional chain for 2-3 random domains as final prep.**

---

## 🎯 Predicted Descriptive Question Bank (pick 3 of 6 in real exam)

Based on your listed topics + slide emphasis, prepare full 10-mark answers for:

1. **Requirement and its levels with examples** → Section 6 (use the food-delivery or hospital example)
2. **Non-functional requirements** → Section 9 (define + give 3-4 examples + contrast with functional)
3. **Requirement engineering, Requirement Development and Management** → Sections 14 & 16 (full diagram: RE splits into Development [4 sub-phases] + Management)
4. **Different phases of requirement development** → Section 14 (Elicitation, Analysis, Specification, Validation — explain each with 2-3 points)
5. **Requirement Development and Management boundary** → Section 16, Figure 1-5 (baseline concept — draw the diagram!)
6. **Baselined Requirements** → Section 16 (definition + role as the boundary + change process loop)

**Strategy:** Since these overlap heavily (14, 16, and "boundary," "baseline" are basically one connected topic), master Sections 14 and 16 deeply — that alone likely covers 3 of your 6 probable questions.

---

## ⚡ Quick-Fire Revision Checklist (night before exam)

- [ ] Can you state the 3 levels of requirements + example chain from memory?
- [ ] Can you list all 4 requirement development sub-phases in order?
- [ ] Can you draw the baseline boundary diagram (Fig 1-5) from memory?
- [ ] Do you know the difference: Functional Req vs Non-Functional Req vs Constraint vs Business Rule?
- [ ] Do you know Gold Plating vs Creeping Requirements?
- [ ] Do you know the 200:1 defect cost rule and which stage is cheapest/most expensive?
- [ ] Do you know Product Requirements vs Project Requirements (with examples)?
- [ ] Can you list at least 5 "common problems" and 3 "reasons behind bad requirements"?

Good luck — this lecture is very definition-heavy, so precision in wording (not just general idea) will win you MCQ and TF marks.