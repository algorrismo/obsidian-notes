---
tags:
  - SRE
  - software-requirements
source: SRE - Ch 01 - The Essential Software Requirement
exam_format: 50 MCQ/TF (1 mark each) + 3 of 6 Descriptive (10 marks each)
---

# 📘 SRE — Chapter 1: The Essential Software Requirement

## Midterm Study Guide

> [!info] How to use this note
> 
> - 🔴 = **High-yield** (very likely MCQ/TF material, or an exam-confirmed short-question topic)
> - 🟡 = Medium priority (good for context, occasional MCQ)
> - ⚠️ = **Common mistake zone** — this is where students lose easy marks
> - 🧠 = How the question is likely to be _phrased_ + how to answer it


## 🎯 Priority Radar: Your 6 Confirmed Short-Question Topics

Your professor told you these _will_ appear as short/descriptive questions. I've built dedicated prep outlines for each — jump straight there if you're short on time:

1. [[#5. Levels of Requirements (Business → User → Functional)|Requirement and its levels, with examples]]
2. [[#9. Non-Functional Requirements|Non-functional requirements]]
3. [[#14. Requirements Engineering = Development + Management|Requirement engineering, Development and Management]]
4. [[#15. Requirements Development — The Four Phases|Different phases of requirement development]]
5. [[#18. The Development ↔ Management Boundary|Requirement Development and Management boundary]]
6. [[#19. Baselined Requirements|Baselined Requirements]]

Full descriptive-answer outlines for all six are in the [[#📝 Descriptive Question Bank (Your 6 Flagged Topics)|Descriptive Question Bank]] at the bottom.

---

## 1. Why This Chapter Exists — "Humor, But Fact" 🟡

The opening cartoon (swing set drawn 8 different ways by 8 stakeholders) is **not just a joke** — it's the thesis of the whole chapter: **everyone interprets requirements differently**, and the gap between "what the customer needed" and "what was built" is the core problem Requirements Engineering exists to solve.

> [!question] 🧠 How it's tested A TF/MCQ might ask: _"The main lesson of the swing-cartoon example is that developers are bad at coding."_ → **False**. The lesson is **miscommunication across stakeholders**, not coding skill.

---

## 2. Common Problems in Requirements Projects 🔴

Two slides list recurring failure patterns. Group them mentally into **3 buckets** — that's how exam questions test them:

| Bucket                             | Examples from slide                                                                                                                   |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Definition failures**            | Business objectives/vision/scope never clearly defined                                                                                |
| **Communication/process failures** | Customers too busy to engage; requirements never formally approved; changes get lost with no tracking                                 |
| **Change-control failures**        | Customers change approved requirements continually; scope grows but schedule/resources don't adjust; unused features get built anyway |

> [!warning] ⚠️ Common mistake Students confuse **"customers claimed all requirements were critical"** with a _technical_ problem. It's a **prioritization/communication** problem — customers didn't rank requirements, so everything looked equally urgent.

> [!question] 🧠 How it's tested TF: _"Scope increasing without additional resources or removed functionality causes schedule slippage."_ → **True** (directly from slide).

---

## 3. Root Causes of Success/Failure 🔴

**Failure causes (with %):**

- Lack of user input — 13%
- Incomplete requirements/specifications — 12%
- Changing requirements/specifications — 12%

**Success causes (with %):**

- User involvement — 16%
- Executive management support — 14%
- Clear statement of requirements — 12%

> [!warning] ⚠️ Common mistake These numbers are **easy MCQ bait**. Students mix up which % belongs to _failure_ vs _success_, or swap "lack of user input" (13%) with "user involvement" (16%) — these are the **same theme from two different surveys** (a failure study and a success study), not opposites of one number.

> [!question] 🧠 How it's tested MCQ: _"According to the success-factor survey, the single highest-ranked success factor is:"_ → **User involvement (16%)** — the #1 answer in BOTH failure avoidance and success studies, which is the point the professor wants you to notice: **user involvement is the single biggest lever** in requirements engineering.

---

## 4. Relative Cost to Repair a Defect (200:1 Rule) 🔴

The cost pyramid, from cheapest to most expensive stage to fix a defect:

|Stage|Relative Cost|
|---|---|
|Requirements time|0.1 – 0.2|
|Design|0.5|
|Coding|1|
|Unit test|2|
|Acceptance test|5|
|Maintenance|20|

> [!important] 🔴 Memorize this pyramid shape, not just numbers The core idea: **the earlier you catch a defect, the cheaper it is to fix.** A defect caught in maintenance can cost **up to 200x more** than one caught during requirements (20 ÷ 0.1 = 200).

> [!warning] ⚠️ Common mistake Students think "1" (coding) is the baseline for the "200:1" ratio. It's actually **maintenance (20) vs requirements time (0.1)** → 20/0.1 = **200**. Don't anchor the ratio to coding.

**The Leakage Problem** (directly connected concept):

- 74% of requirements defects are found **during requirements analysis** (the cheapest, best place)
- 4% leak into preliminary/high-level design
- 7% leak into detailed design
- 4% aren't found until **maintenance** (after release, most expensive)

> [!question] 🧠 How it's tested MCQ: _"What percentage of requirements defects are ideally caught during requirements analysis?"_ → **74%**. This is the single most memorized number in this chapter — expect it verbatim in MCQ/TF.

---

## 5. Levels of Requirements (Business → User → Functional) 🔴🎯

### What is a "Requirement"?

> A requirement is **a property that a product must have to provide value to a stakeholder.**

Key nuances (frequently turned into TF questions):

- Requirements = specification of **what** should be implemented (not _how_ — that's design)
- Requirements include **both**: the user's view of external behavior AND the developer's view of internal characteristics
- Requirements have a **time dimension**: present tense (current capability), near-term/high-priority future, hypothetical/low-priority future, or even **past tense** (needs once specified, later discarded)

> [!warning] ⚠️ Common mistake Students forget the **"past tense"** category exists — they assume requirements are only present/future. TF questions exploit this directly: _"Requirements can never be written in the past tense."_ → **False.**

### The Three Levels — THE most important model in this chapter

```
Business Requirement (business goal)
        ↓
User Requirement (user need)
        ↓
Functional Requirement (system behavior)
```

|Level|Definition|Who provides it|Example (airline)|
|---|---|---|---|
|**Business Requirement**|_Why_ the org is building the system — the business benefit|Funding sponsor, customer, marketing, product visionary|Reduce airport counter staff costs by 25%|
|**User Requirement**|Goals/tasks the user must accomplish; written as **use cases** or **user stories**|User representatives|"As a passenger, I want to check in for a flight so I can board my airplane."|
|**Functional Requirement**|_What developers must implement_, usually a **"shall" statement**|Business analyst (derived from user reqs)|"The system shall assign a seat if no seating preference is set."|

> [!important] 🔴 Memorize the exact chain Business goal → User need → System behavior. This exact phrase ("Business Requirement (business goal) → User Requirement (user need) → Functional Requirement (system behavior)") is **lifted straight from the slide** — expect it as a fill-in-the-blank or matching MCQ.

**Worked example from the slide (food delivery app):**

|BR|UR|FR|
|---|---|---|
|Increase food delivery orders by 30% in one year via digital platform|Customers should order food online from nearby restaurants|System shall allow browsing menus, adding to cart, placing orders|
|Improve satisfaction via delivery transparency|Customers should track order status/location in real time|System shall show order status + live map location|
|Reduce cancellations from payment issues|Customers should pay securely via multiple methods|System shall integrate payment gateways (cards, mobile banking, wallets)|

> [!warning] ⚠️ Common mistake — THE #1 exam trap in this whole chapter Given a requirement statement, students confuse **User Requirement** vs **Functional Requirement** because both can start with "Customer/User should be able to..." **The test:** does it use **"shall"** language describing precise system behavior (→ Functional), or does it describe a **goal/task in the user's own words without implementation detail** (→ User)?
> 
> - "Customers should be able to search products by category" → **User** (goal, no system mechanics)
> - "The system shall allow users to filter products by price range" → **Functional** ("shall" + specific mechanic)

> [!question] 🧠 How it's tested (this is literally Task 1 on your slide) You WILL get a table of requirement statements and be asked to classify Business/User/Functional. Practice the trigger words:
> 
> - Business → % increase, cost reduction, revenue, market goals, "reduce/increase X by Y%"
> - User → "Customer/user should be able to..." (goal only, no system mechanics)
> - Functional → "The system shall..." (specific behavior)

### Also note: Levels ≠ just 3 — System Requirements is a related-but-different concept (see §8 below). Don't conflate the two.

---

## 6. Constraints (hides inside Functional Requirements section) 🟡

A **constraint** = a restriction imposed on the developer's choices for design/construction.

> Example: _"The system shall be developed using open-source tools and run on Linux OS."_

> [!warning] ⚠️ Common mistake Students think constraints are a **4th level** of requirements. They're **not** — they're a **cross-cutting restriction** that can apply at any level (and they overlap heavily with Business Rules — see §11).

---

## 7. Working with the Three Levels — Roles Diagram 🟡

Two parallel paths shown in the slide (Figure 1-3):

**Corporate path:** Business Need → _Manager_ → Business Requirements → _Business Analyst & User Reps_ → User Requirements → _Business Analyst_ → Functional Requirements → Developer/Tester

**Commercial path:** Market Need/Product Concept → _Marketing_ → Business Requirements → _Product Manager_ → User Requirements → _Business Analyst/Product Manager_ → Functional Requirements → Developer/Tester

> [!question] 🧠 How it's tested MCQ might ask _who typically derives Functional Requirements_ → **Business Analyst** (in both paths) — not the developer. The developer/tester **receives** functional requirements; they don't originate them.

---

## 8. System Requirements 🔴

- Describes requirements for a product composed of **multiple components/subsystems**
- Can be **all-software** or **software + hardware** (e.g., biometric device)
- **People and processes are part of a system too** — some functions can be allocated to humans, not just machines
- Classic example: **supermarket cashier workstation** (bar code scanner + scale + hand-held scanner + keyboard + display + cash drawer)

> [!warning] ⚠️ Common mistake Students assume "System Requirements" = "Functional Requirements" (same thing, different name). **They're not.** System requirements sit **above** functional requirements — the BA derives specific functional requirements _from_ system requirements and allocates them to specific subsystems. Look at Figure 1-1: `System Requirements → Functional Requirements` (an arrow, meaning system reqs feed into functional reqs, not replace them).

---

## 9. Non-Functional Requirements 🔴🎯

Also called: **quality attributes** ("-ity, -ilities").

> Definition: describes a **service or performance characteristic** of the product — not _what_ it does, but **how well** it does it.

Dimensions mentioned explicitly in the slide:

- Performance, safety, availability, portability
- Usefulness, flexibility, reliability
- **Interoperability** (connections to other software/hardware/communication interfaces)
- **Security** (comes from design/implementation constraints)

> [!important] 🔴 Key exam-relevant facts to memorize
> 
> 1. Non-functional requirements have a **fairly high chance of conflicting with each other** (e.g., high security vs. high usability/speed) — explicitly stated on the slide.
> 2. They cover **external interfaces** between system and outside world (other software, hardware, users, communication).
> 3. **Design/implementation constraints** are a _type_ of non-functional requirement.

> [!warning] ⚠️ Common mistake Students think Non-Functional Requirements are a **4th level** stacked under Functional in the same chain (Business→User→Functional→Non-Functional). **They are NOT part of that linear chain.** Look at Figure 1-1 carefully: Non-Functional (labeled "Quality Attributes") sits **parallel to** Functional Requirements, both flowing into the Software Requirements Specification (SRS) — it's a **separate branch**, not a downstream step.

> [!question] 🧠 How it's tested — likely descriptive phrasing _"Explain non-functional requirements with examples and explain why they might conflict."_ **Answer skeleton:** Define (quality attribute, "-ilities") → give 3–4 examples (performance, security, usability, reliability) → explain conflict (e.g., stronger security often reduces usability/performance) → mention they still trace back to business rules/quality attributes in Figure 1-1.

---

## 10. Business Rules 🔴

> Definition: corporate policies, government regulations, industry standards, computational algorithms.

Critical distinctions:

- **Business rules are NOT themselves software requirements** — they exist independently of any specific software application
- They **dictate** that the system must contain functionality to comply with them
- Example (inverse requirement): _"no red colour in webpage"_ — a restriction on developer's design choices
- Sometimes business rules are the **origin of quality attributes** (non-functional requirements) — e.g., corporate security policy → firewall functionality
- You can **trace the origin** of certain functional requirements back to a specific business rule

> [!warning] ⚠️ Common mistake — high-value trap TF: _"Business rules are a type of software requirement."_ → **FALSE.** This is one of the most exploitable TF questions in the chapter because it feels counter-intuitive (business rules obviously _affect_ software) — but the slide is explicit that they exist **beyond the boundary** of any specific application.

> [!question] 🧠 How it's tested Given the online-purchase-limit example or "no red colour" example, you'll be asked to identify it as a **business rule**, not a functional requirement — even though it _produces_ functional requirements.

---

## 11. Feature 🟡

> A feature = one or more **logically related system capabilities** that provide value to a user, described by a **set of functional requirements**.

- A feature can encompass **multiple user requirements**
- Each user requirement implies certain functional requirements must exist to let the user perform that task

Example (Figure 1-2, web browser): "Bookmarks" is a feature → contains user requirements like "Add a Bookmark," "Edit Bookmarks" → each implies functional requirements ("shall display bookmarks as collapsible/expandable tree," "user shall be able to resequence bookmarks," etc.)

> [!question] 🧠 How it's tested Ordering question: _"Arrange from broadest to narrowest: Functional Requirement, Feature, User Requirement"_ → **Feature → User Requirement → Functional Requirement** (a feature contains user requirements, which imply functional requirements).

---

## 12. The Master Relationships Diagram (Figure 1-1) 🔴

This is the single most information-dense diagram in the chapter — treat it as a **map connecting everything above**.

```
Business Rules ⇄ Business Requirements → [Vision and Scope Document]
Business Rules → Quality Attributes, External Interfaces, Constraints (all → Functional Requirements)
Business Requirements → User Requirements → [User Requirements Document]
User Requirements → Functional Requirements
System Requirements → Functional Requirements
Functional Requirements + Quality Attributes + External Interfaces + Constraints → [Software Requirements Specification]
```

> [!important] 🔴 Arrow meaning (will absolutely be tested)
> 
> - **Solid arrows** = "are stored in" (e.g., Business Requirements are stored in the Vision and Scope Document)
> - **Dotted arrows** = "are the origin of" / "influence" (e.g., Business Rules influence/originate Business Requirements, Quality Attributes, and Functional Requirements)

> [!warning] ⚠️ Common mistake Students assume ALL arrows mean the same thing. Exam questions will directly test: _"What does a dotted arrow represent in Figure 1-1?"_ → **origin/influence**, NOT storage.

---

## 13. Product vs. Project Requirements 🔴

||Product Requirements|Project Requirements|
|---|---|---|
|Definition|Properties of the software system to be built|Other deliverables/expectations necessary for project success, but **not part of the software itself**|
|Housed in|SRS (Software Requirements Specification)|Separate documents/plans|
|Examples|Business/User/Functional/Non-functional requirements|Workstations, testing labs, staff training, installation procedures, beta testing, marketing, legal/IP protection, SLAs|

> [!important] 🔴 Key rule to memorize **An SRS should NOT include:** design/implementation details (beyond known constraints), project plans, or test plans. Keep requirements development focused on **what** to build, not project logistics.

**Project requirement examples (full list from slide — good for MCQ elimination):** Physical resources (workstations, hardware, labs) • Staff training/documentation • Infrastructure changes • Release/install/config procedures • Beta testing, manufacturing, packaging, marketing, distribution • Customer service-level agreements • Legal protection (patents, trademarks, copyrights)

> [!warning] ⚠️ Common mistake Students see "user training manual" or "installation procedure" and classify it as a **functional requirement** because it sounds like "the system must do X." **It's a project requirement** — it's about delivering the project successfully, not a property of the software itself.

---

## 14. Requirements Engineering = Development + Management 🔴🎯

```
Requirements Engineering
        ├── Requirements Development
        │       ├── Elicitation
        │       ├── Analysis
        │       ├── Specification
        │       └── Validation
        └── Requirements Management
```

> [!important] 🔴 This is a near-guaranteed short question **Requirements Engineering** is the umbrella term. It splits into exactly **two** subdisciplines:
> 
> 1. **Requirements Development** (itself split into 4 phases — see below)
> 2. **Requirements Management**

> [!warning] ⚠️ Common mistake Students think "Requirements Management" is one of the 4 phases alongside Elicitation/Analysis/Specification/Validation. **It is NOT.** Management is a **separate, parallel discipline** to Development — Development has 4 sub-phases; Management sits beside it as its own branch.

---

## 15. Requirements Development — The Four Phases 🔴🎯

|Phase|What happens|
|---|---|
|**1. Elicitation**|Identify user classes/stakeholders; understand user tasks/goals and business objectives; learn the environment; work with user-class reps to gather functionality needs and quality expectations|
|**2. Analysis**|Model the application environment; distinguish task goals into functional reqs/quality expectations/business rules/suggested solutions; decompose high-level reqs into detail; **allocate requirements to software components**; negotiate priority|
|**3. Specification**|BA documents in the **SRS**; transcribe user needs into written requirements/diagrams; adopt templates; **identify requirement origins**; **uniquely label each requirement**|
|**4. Validation**|Review SRS for problems (feasible, **consistent**, **complete**); develop acceptance tests/criteria; **simulate requirements** (e.g., wireframing) to find errors|

> [!important] 🔴 Definitions you must get exactly right (favorite TF trap)
> 
> - **Consistency** = no requirements should be **contradictory**
> - **Completeness** = no needed services/constraints have been **missed out** These two terms get swapped in TF questions constantly — memorize which is which.

**The process is iterative** (Figure 3-1) — phases loop back:

- Analysis → _clarify_ → back to Elicitation
- Specification → _close gaps_ → back to Analysis
- Validation → _rewrite_ → back to Specification
- Validation → _re-evaluate_ → back to Analysis
- Validation → _confirm and correct_ → back to Elicitation

> [!question] 🧠 How it's tested MCQ: _"Which phase involves uniquely labeling each requirement?"_ → **Specification**. _"Which phase involves wireframing to catch errors?"_ → **Validation**.

**Extended 17-step framework (Figure 3-2)** — you don't need to memorize all 17, but know the **first 7** belong to iteration setup and steps **8–17 repeat every iteration**:

1. Define business requirements
2. Identify user classes
3. Identify user representatives
4. Identify requirements decision makers
5. Plan elicitation
6. Identify user requirements
7. Prioritize user requirements _(then repeated each iteration: flesh out user reqs → derive functional reqs → model → specify non-functional reqs → review → prototype → develop/evolve architecture → allocate to components → develop tests → validate)_

**Effort distribution across life cycles (Figure 3-3):**

- **Waterfall/Sequential** → one huge upfront spike of requirements effort, then almost none later
- **Iterative/Phased** → smaller repeated bumps of effort
- **Agile/Incremental** → small, frequent, steady effort in short time-boxes (e.g., 1 month)

> [!question] 🧠 How it's tested _"Which development life cycle shows requirements effort as a single large spike early in the project?"_ → **Waterfall/Sequential.**

---

## 16. Requirements Development: Elicitation — expanded 🟡

(Already covered in table above — but standalone bullets from the slide, good for TF matching):

- Identify expected **user classes** and other stakeholders
- Understand user tasks/goals and business objectives they align with
- Learn about the **environment** the product will be used in
- Work with representatives of each user class for functionality needs + quality expectations

---

## 17. Requirements Development: Analysis — expanded 🟡

- Model the application environment
- Analyze info from users → distinguish into functional reqs, quality expectations, business rules, suggested solutions
- Decompose high-level reqs into appropriate detail
- **Allocate requirements to software components** defined in system architecture
- Negotiate requirements priority and implementation priorities

---

## 18. The Development ↔ Management Boundary 🔴🎯

Figure 1-5 shows the **boundary** between Requirements Development and Requirements Management as a literal line in the diagram:

```
Marketing, Customers, Management
        ↓ (requirements)
   Analyze, Document, Review, Negotiate     ← REQUIREMENTS DEVELOPMENT (above the line)
        ↓
════════ BASELINED REQUIREMENTS ════════   ← THE BOUNDARY
        ↓ current baseline          ↑ revised baseline
   Requirements Change Process              ← REQUIREMENTS MANAGEMENT (below the line)
        ↑ requirements/changes         ↑ project changes
Marketing, Customers, Management      Project Environment
```

> [!important] 🔴 This is your literal exam-flagged topic — memorize this shape
> 
> - **Everything above "Baselined Requirements"** = Requirements Development (gathering, analyzing, documenting, negotiating requirements for the first time)
> - **Everything below "Baselined Requirements"** = Requirements Management (handling _changes_ to requirements that have already been agreed/baselined)
> - The **"Baselined Requirements"** box is the **hinge point** — it's the output of Development and the input to Management.

> [!warning] ⚠️ Common mistake Students think Development and Management are strictly sequential (Development finishes, THEN Management starts, forever). Actually it's a **feedback loop**: the Requirements Change Process produces a **"revised baseline"** which flows back up — meaning management can trigger new baselines continuously throughout the project.

---

## 19. Baselined Requirements 🔴🎯

A **baseline** = the **agreed-upon, frozen snapshot** of requirements at a point in time — the reference point against which all future changes are measured and controlled.

> [!important] 🔴 Why baselining matters (this is your descriptive-answer core)
> 
> - It's the **output of Requirements Development** and the **starting input of Requirements Management**
> - Once baselined, any further change must go through the **Requirements Change Process** (not just be edited freely)
> - A **revised baseline** is produced whenever an approved change is incorporated — so baselines are updated, not static forever
> - Baselining is what makes **requirements traceability, change tracking, and impact analysis** possible — without a baseline, you can't measure "what changed from what"

**Requirements Management activities that revolve around the baseline:**

- Establish a requirements **change control process**
- Perform **impact analysis** on requirements changes
- Track status of each requirement + track requirements issues
- Maintain a **history** of requirements changes
- Maintain a **requirements traceability matrix** — defines relationships/dependencies between requirements, and traces requirements to designs, code, and tests

> [!warning] ⚠️ Common mistake Students confuse "baseline" with "final version." **A baseline is NOT final** — it's simply the current agreed reference point; it gets revised as approved changes come in. TF bait: _"Once requirements are baselined, they can never be changed."_ → **False.**

---

## 20. "Role of Requirements" — The Famous Quote 🟡

> _"The hardest single part of building a software system is deciding precisely what to build... No other part of the work so cripples the resulting system if done wrong. No other part is more difficult to rectify later."_

> [!question] 🧠 How it's tested This quote is often attributed in textbooks to **Fred Brooks** (from _The Mythical Man-Month_ / "No Silver Bullet") — the slide doesn't name the author, but if a question asks "what does this quote emphasize," the answer is: **requirements are the hardest and most consequential part of software development; errors here are the most expensive and hardest to fix later** (ties directly back to the 200:1 cost pyramid in §4).

---

## 21. Reasons Behind Bad Requirements 🔴

- **Insufficient user involvement**
- **Inaccurate planning**
- **Creeping (gradually changing) user requirements** — note: "creeping" specifically means gradual, incremental increase
- **Ambiguous requirements** (e.g., "respond as soon as possible" — no measurable definition)
- **Gold plating** — extra functionality **beyond** the specification (developers/analysts add unrequested features)
- **Overlooked stakeholders**

> [!warning] ⚠️ Common mistake Students confuse **"gold plating"** with **"scope creep."**
> 
> - **Gold plating** = someone (often a developer) adds unnecessary extra features **not requested**
> - **Scope creep / creeping requirements** = the **customer** keeps adding/changing requirements over time These are different sources (developer-driven vs. customer-driven) — a favorite MCQ distinction.

---

## 22. Benefits of a High-Quality Requirements Process 🟡

Fewer defects (in requirements AND product) • Reduced rework • Faster delivery • Fewer unused features • Lower enhancement costs • Fewer miscommunications • Reduced scope creep • Reduced project chaos • Higher satisfaction • Products that do what they're supposed to

> [!question] 🧠 How it's tested Usually appears as a "select all that apply" or TF list — mostly common sense once you understand §2–4, but memorize **"fewer unnecessary and unused features"** specifically, since it directly ties back to the earlier problem _"developers built it, but no one ever uses it."_

---

## 📝 Descriptive Question Bank (Your 6 Flagged Topics)

Use these as answer skeletons — expand each bullet into 1–2 sentences in the exam for a full 10-mark answer.

### 1. Requirement and its levels, with examples

- Define "requirement" (property providing value to a stakeholder)
- Name the 3 levels: Business → User → Functional
- Define each level in one line + give the airline example (kiosk check-in) or the food-delivery example
- Mention **System Requirements** as related but distinct (multi-component products)
- Mention **Non-Functional Requirements** as a separate branch (not part of the linear chain)

### 2. Non-functional requirements

- Define: quality attributes ("-ilities"), describe _how well_ vs _what_
- List dimensions: performance, safety, availability, portability, usability, reliability, interoperability, security
- Explain they cover **external interfaces** (software, hardware, users, communication)
- State they **often conflict** with each other (give an example: security vs usability)
- Note their place in Figure 1-1 (parallel branch feeding into SRS, alongside functional requirements)

### 3. Requirement engineering, Development and Management

- Requirements Engineering = umbrella discipline, splits into 2: Development + Management
- Requirements Development = 4 phases (Elicitation, Analysis, Specification, Validation)
- Requirements Management = handles changes to already-baselined requirements (change control, tracking, traceability)
- Emphasize: Management is NOT a 5th phase of Development — it's a parallel, ongoing discipline

### 4. Different phases of requirement development

- List and define all 4 in order: Elicitation → Analysis → Specification → Validation
- For each, give 2 key activities (see table in §15)
- Mention the process is **iterative**, not linear (Figure 3-1 feedback loops: clarify, close gaps, rewrite, re-evaluate, confirm and correct)
- Mention it can repeat across iterations in Agile/incremental development

### 5. Requirement Development and Management boundary

- Draw/describe Figure 1-5's structure: sources (Marketing/Customers/Management) → Analyze/Document/Review/Negotiate → **Baselined Requirements** → Change Process → revised baseline
- State clearly: Development = everything before the baseline is formed; Management = everything after, dealing with change
- Emphasize it's a **loop**, not a one-way handoff — revised baselines feed back in

### 6. Baselined Requirements

- Define baseline: agreed, frozen reference snapshot of requirements at a point in time
- Explain its role as the hinge between Development and Management
- Explain that changes after baselining must go through the formal **Requirements Change Process**
- List Management activities anchored to it: change control, impact analysis, status/history tracking, traceability matrix
- Clarify: baseline ≠ permanent/final — it gets **revised** over time as changes are approved

---

## ✅ Quick-Fire Self-Test (practice, not real exam questions)

Test yourself — cover the answers below each line first.

1. TF: Requirements can be written in the past tense. → **True**
2. TF: Non-functional requirements are the 4th step after Functional Requirements in a linear chain. → **False** (parallel branch)
3. TF: Business rules are themselves software requirements. → **False**
4. MCQ: Which costs ~200x more to fix a defect than requirements time? → **Maintenance**
5. TF: Requirements Management is one of the four requirements development phases. → **False**
6. MCQ: "The system shall allow users to filter products by price" is a: → **Functional Requirement**
7. TF: Once baselined, requirements are frozen forever. → **False**
8. MCQ: Gold plating refers to: → **Unrequested extra functionality added beyond spec**
9. TF: Dotted arrows in Figure 1-1 mean "are stored in." → **False** (dotted = origin/influence; solid = stored in)
10. MCQ: Consistency in validation means: → **No contradictory requirements**

---

## 📚 Reference

Wiegers, K., & Beatty, J. (2013). _Software Requirements_. Pearson Education.