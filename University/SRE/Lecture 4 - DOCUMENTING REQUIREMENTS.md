---
tags:
  - SRE
  - midterm
title: Documenting Requirements
Date:
---

# Ch.04 — Documenting Requirements | Exam Study Guide

> [!info] Exam Shape
> **MCQ + T/F:** 50 × 1 = 50 marks  
> **Descriptive:** 3 of 6 × 10 = 30 marks

**Confirmed short/descriptive angles for this lecture:**

1. Business Rules taxonomy with examples  
2. Sections of SRS and their purpose  
3. Identify the flaw in a specification and rewrite it correctly
## 1. Business Rules — Why They Matter

A business rule is _not_ itself a requirement — it's the origin of one. Rules come from policy, law, or industry standard, and they **shape** business/user/functional requirements and quality attributes.

|Requirement type|How business rules influence it|Example|
|---|---|---|
|Business requirement|Government regulation → business objective|Chemical Tracking System must enable regulatory compliance reporting|
|User requirement|Privacy policy → who can do what|Only lab managers can generate exposure reports for others|
|Functional requirement|Company policy → system behavior|Unregistered vendor invoice → system emails forms automatically|
|Quality attribute|OSHA/EPA regulation → enforced safety behavior|System must verify safety training before releasing a hazardous chemical|

> [!question] Exam Angle MCQ trap: they'll give you a rule statement and ask **which requirement type it shaped** (business/user/functional/quality) — not what type of _rule_ it is. Read carefully whether the question asks about the **rule taxonomy** (below) or the **requirement type influenced**.

---

## 2. Business Rules Taxonomy ⭐ (HIGH YIELD — confirmed exam topic)

**Figure 9-1:** Business Rules → **Facts | Constraints | Action Enablers | Inferences | Computations**

### 2.1 Facts

- Statement **true about the business at a point in time**; describes relationships between business terms.
- Purely **descriptive**, no action, no restriction.
- _Example:_ "Every chemical container has a unique bar code identifier."

### 2.2 Constraints

- **Restricts actions** the system/users are allowed to perform. Uses "must/must not/may not/only X can."
- Origins: organizational policy, government regulation, industry standard.
- _Example:_ "A loan applicant under 18 must have a co-signer."

### 2.3 Action Enablers

- Triggers an **activity** (action to be taken) when a condition is true. If/then, but the "then" = **do something**.
- _Example:_ "If the customer ordered a book by a multi-book author, offer the other books before completing the order."

### 2.4 Inferences

- Creates a **new fact** from existing facts (derived knowledge). If/then, but the "then" = **a piece of knowledge, NOT an action**.
- _Example:_ "If payment isn't received within 30 days, the account is inactive."

### 2.5 Computations

- **Transforms data into new data** via a formula/algorithm. Often based on external rules (e.g., tax formulas).
- _Example:_ "Total price = item cost − volume discount + tax + shipping + insurance."

> [!warning] Common Mistake — Action Enabler vs. Inference Both are written as "if/then" and students constantly confuse them.
> 
> - **Action Enabler** → then-clause is an **action** ("display," "offer," "email," "sound an alarm")
> - **Inference** → then-clause is a **conclusion/status/label**, not an action ("is inactive," "is back-ordered," "is High Risk") **Trick test:** can you literally _watch the system do something_ in the "then" clause? If yes → Action Enabler. If it's just a new fact/label → Inference.

> [!warning] Common Mistake — Constraint vs. Fact A Fact just states reality ("every order has a shipping charge"). A **Constraint** restricts behavior ("only X may do Y" / "must not"). If you see "must," "must not," "only," "cannot" → Constraint, not Fact.

### Full comparison table (from your slide's healthcare-example table — memorize this cold)

|Rule Type|Primary Goal|Output Type|Nature|Software Impact|
|---|---|---|---|---|
|Fact|Describe a static, permanent reality|Data structure/relationship/schema|Structural/Declarative ("what is always true")|Defines database entities & attributes|
|Constraint|Block/limit/forbid an action|Restriction, hard block, validation error|Restrictive/Governance ("what is forbidden")|Validation logic, input-blocking code|
|Action Enabler|Trigger a process/behavior|Event, notification, workflow step|Procedural/Behavioral ("what to do")|Functional requirements, hooks|
|Inference|Deduce a new fact/state|Data attribute update, tag, classification|Logical/Cognitive ("what to conclude")|Conditional logic / rules engine|
|Computation|Calculate a precise value|Numeric value/balance/rate|Mathematical/Algorithmic ("how to calculate")|Back-end function/formula|

> [!question] Exam Angle **Descriptive Q pattern:** "List and explain the 5 types of business rules with one example each" — you now have this ready below in §9. **MCQ pattern:** they give a one-line rule ("If a patient's BMI > 30, classify as High Risk") and ask you to identify the type → **Inference** (conclusion, not action).

---

## 3. Documenting Business Rules

- Rules should be broken into **atomic** statements, each with a **unique ID**, e.g. `Video.Checkout.Duration`, `Renewal.Video.Times`.
- A **business rules catalog** records each rule with: **ID, Rule definition, Type of rule, Static or dynamic, Source**.
- **Static** rule = fixed value in the rule itself (e.g., "renew up to 2 times").
- **Dynamic** rule = refers out to another table/policy that can change without rewriting the rule (e.g., "as defined in Table BR-060").

> [!warning] Common Mistake Students think "dynamic" means the rule changes often in real time. It actually means the **value is stored externally** (in a referenced table/policy) rather than hard-coded, so it _can_ change without editing the rule text itself.

## 4. Discovering Business Rules (Figure 9-3)

Six discovery angles, each a **question you ask stakeholders**:

- **Policies** → "Why do we have to do it like that?"
- **Regulations** → "What does the government require?"
- **Computations** → "How is that number calculated?"
- **Object Life Cycles** → "What causes a change in the object's state?"
- **System Decisions** → "How does the system know what to do next?"
- **User Decisions** → "What is a user allowed to do next?"
- **Events** → "What must happen? What cannot happen?"
- **Data Models** → "How are these pieces of data related?"

> [!question] Exam Angle T/F bait: "Business rules can only come from government regulation." → **False** — policies, data models, object states, and computations are also sources.

---

## 5. The Software Requirements Specification (SRS)

**Definition — memorize:** The SRS states the **functions/capabilities**, **characteristics**, and **constraints** the system must respect. It describes system behavior under various conditions and desired qualities (performance, security, usability).

- It is the **basis for planning, design, coding, testing, and user documentation**.
- It should **NOT** contain design, construction, testing, or project-management detail (except known design/implementation constraints).

> [!warning] Common Mistake "The SRS should describe HOW the system will be built." → **False.** SRS = _what_, not _how_. Design/construction details are out of scope (except constraints that force a certain implementation).

### Audience of the SRS (know who uses it and why)

|Audience|Uses SRS for|
|---|---|
|Customers/marketing/sales|Know what will be delivered|
|Project managers|Schedule, effort, resource estimates|
|Dev teams|What to build|
|Testers|Requirements-based tests|
|Maintenance/support|Understand what each part should do|
|Documentation writers|User manuals, help screens|
|Trainers|Educational material|
|Legal staff|Compliance with laws/regulations|
|Subcontractors|Legally binding basis of their work|

> [!question] Exam Angle MCQ: "Who bases their test plans on the SRS?" → Testers. "Who ensures legal compliance?" → Legal staff. These get mixed up as distractors — read carefully.

---

## 6. Readability & Labeling of Requirements

### Readability suggestions (quick list)

Use a consistent template; number figures/tables; use cross-references (not hard-coded page numbers); use hyperlinks; use visuals; get an editor for consistency.

### Why labeling matters

Every requirement needs a **unique, persistent identifier** → enables traceability, reuse across projects, and clear discussion in reviews. **Simple numbered/bulleted lists are NOT adequate.**

### Labeling schemes ⭐ (compare pros/cons — common table-style MCQ)

|Scheme|Example|Pros|Cons|
|---|---|---|---|
|**Sequence number**|UC-9, FR-26|Easy to keep unique ID even if requirement moves|No reuse of deleted numbers; no hierarchy/grouping; no clue what it's about|
|**Hierarchical numbering**|3.2.4.3|Simple, compact, familiar|Labels get long; tells nothing about intent; renumber everything if you insert/delete/move a section → breaks all references|
|**Hierarchical textual tags**|Product.Cart.Discount.Error|Meaningful names; can add sequence suffix (Product.Cart.01) for small sets|Tags are longer; must think up meaningful names|

> [!warning] Common Mistake Students assume hierarchical numbering has _no_ downsides because it's "most common." Exam loves testing the con: **inserting/deleting a section renumbers everything and breaks cross-references.**

### Dealing with incompleteness — TBD

- Use **TBD (to be determined)** to flag a knowledge gap — don't guess or leave it blank.
- **Must** record: who is responsible, how it'll be resolved, and by when. **Number the TBDs** to track them to closure.
- Trap phrase from your slide: _"TBDs won't resolve themselves."_

---

## 7. User Interfaces & the SRS

**Conceptual sketches / wireframes** make requirements tangible — good for early exploration.

|Pros|Cons|
|---|---|
|Makes requirements tangible to users & devs|Delaying SRS baseline until UI is done slows development|
|Working mock-ups aid communication|Visual design can end up _driving_ requirements → functional gaps|
||Screens don't replace written functional requirements — devs shouldn't have to _deduce_ logic from a screenshot|

### Case Study: The "Sleek" E-Commerce Checkout (gap analysis) — likely exam scenario

When only the "happy path" UI was designed, four categories of requirements were missed:

1. **Error State** — what happens on a declined card? No error-text location, no retry-limit defined.
2. **Race Condition** — double-clicking "Place Order" on slow internet → duplicate charge/order (no debounce logic specified).
3. **Legal/Compliance** — no checkbox for "I agree to recurring shipping fees," leaving the company legally exposed.
4. **Inventory Discrepancy** — no real-time stock validation if an item sells out while the user is on the checkout page.

**Core lesson (likely to be asked as a concept, not just recall):** _"When UI drives requirements, you design for the eyes, not the architecture."_ A wireframe shows where a button sits — not the database logic, error handling, security, or business rules behind the click.

> [!question] Exam Angle Descriptive-style prompt: "Explain why UI mockups alone are insufficient as requirements, using an example." → Use this exact case study; name at least 2 of the 4 gaps.

---

## 8. SRS Template ⭐ (HIGH YIELD — confirmed exam topic)

|Section|Contents|
|---|---|
|**1. Introduction**|1.1 Purpose (product + readers) · 1.2 Document Conventions (meaning of formatting/notation) · 1.3 Project Scope (short description of the software) · 1.4 References (docs/resources referenced)|
|**2. Overall Description**|2.1 Product perspective (context/origin) · 2.2 User classes & characteristics · 2.3 Operating Environment (hardware, OS, org, location) · 2.4 Design & implementation constraints (e.g., mandated programming language)|
|**3. System Features**|3.1 Description of feature · 3.2 Functional requirements · 3.3 Cross-reference|
|**4. External Interface Requirements**|4.1 User interface · 4.2 Software interface · 4.3 Hardware interface · 4.4 Communication interface · 4.5 Cross-reference|
|**5. Quality Attributes**|5.1 Usability · 5.2 Performance · 5.4 [others] · 5.5 Cross-references|
|**6. Data Requirements**|6.1 Logical data model (UML) · 6.2 Data dictionary|
|**Appendix A**|Glossary|

> [!warning] Common Mistake Students mix up **Section 2** (Overall Description — the big-picture context) with **Section 3** (System Features — the actual functional requirements). If a question gives you "describes user classes and operating environment" → that's **Section 2**, not Section 3. Also: "Design and implementation constraints" live in **2.4**, not in Section 5 (Quality Attributes) — constraints ≠ quality attributes.

> [!question] Exam Angle Descriptive prompt: "List the main sections of an SRS and briefly explain the purpose of each." Use the table above directly — for 10 marks, name all 6 sections + Appendix, and give 1 line of purpose per section, not just subsection lists.

### Sample nonfunctional requirements (from the slide — good MCQ fodder)

- **Performance:** "95% of catalog database queries shall complete within 3 seconds on a single-user 2-GHz PC with ≥60% resources free."
- **Safety:** "System shall terminate operation within 1 second if tank pressure exceeds 95% of max."
- **Security:** "User must change initial password immediately after first login; initial password may never be reused."

Notice each of these lives conceptually under **SRS Section 5 (Quality Attributes)**.

---

## 9. Characteristics of Good Requirement Statements ⭐

**C.C.F.N.P.U.V.** (make your own mnemonic):

- **Complete**
- **Correct**
- **Feasible**
- **Necessary**
- **Prioritized**
- **Unambiguous**
- **Verifiable**

> [!question] Exam Angle Classic MCQ: give a requirement and ask which characteristic it _violates_. E.g., "The system should be fast" → violates **Verifiable** (and Unambiguous — "fast" is a fuzzy word, see §11).

---

## 10. Guidelines for Writing Requirements

- Write **complete sentences**, correct grammar, short/direct.
- Consistent pattern: **"The system shall"** or **"The user shall"** + action verb + observable result.
- State the **trigger/precondition** that causes the behavior.
- Use **"shall"/"must"** — avoid "should," "may," "might" (these don't clarify if it's actually required).
- Use glossary terms **consistently**.
- Decompose vague top-level requirements into detail.
- Name the **specific actor** (e.g., "The Buyer shall...") instead of generic "user" when possible.

**Generic system-perspective template (memorize):**

> [optional precondition] [optional trigger event] the system shall [expected system response].

> [!warning] Common Mistake Students think "should" is a softer-but-acceptable synonym for "shall." On this exam, **"should/may/might" = ambiguous priority = a flaw to flag** in a "identify and correct the flaw" question.

### Representation techniques (supplemental only)

Lists, tables, visual models, charts, formulas, photos, sound/video clips — these **supplement** but do **not replace** written natural-language requirements.

---

## 11. Avoiding Ambiguity ⭐ (feeds directly into "identify the flaw" question type)

Four ambiguity traps from the slide:

1. **Fuzzy words** — vague, subjective terms (see table in §13).
2. **The A/B construct** — related/synonymous or opposite terms used loosely together, causing confusion about scope.
3. **Boundary values** — unclear whether an endpoint belongs to one range or another.
    - _Example flaw:_ "Requests up to 5 days need no approval. 5–10 days need supervisor approval." → Is exactly 5 or exactly 10 in both ranges?
    - _Fix:_ explicitly state inclusive/exclusive boundaries, e.g., "1–5 days: no approval. 6–10 days: supervisor approval. 11+ days: management approval."
4. **Negative requirements** (double negatives) — confusing "prevent... if not..." phrasing.
    - _Flaw:_ "Prevent the user from activating the contract if the contract is not in balance."
    - _Fix (positive form):_ "The system shall allow the user to activate the contract only if the contract is in balance."

> [!question] Exam Angle This section is your **most likely source for the "identify the flaw and rewrite it" descriptive question.** Practice converting: fuzzy word → quantified value; negative phrasing → positive phrasing; unclear boundary → explicit inclusive range.

## 12. Avoiding Incompleteness

Three classic incompleteness traps:

1. **Complex logic gaps** — not all logical combinations are covered.
    - _Example flaw:_ "If Premium is not selected AND proof of insurance is not provided → default to Basic." → What if Premium is **selected** but proof of insurance is **not provided**? Left unaddressed.
2. **Symmetry** — an operation is specified but its counterpart is missing (e.g., "save" defined, "retrieve" isn't).
3. **Missing exceptions** — the "happy path" is specified, but the failure path isn't.
    - _Example flaw:_ "If the user is working in an existing file and chooses to save, the system shall save it with the same name." → Doesn't say what happens if the save **fails**.
    - _Fix:_ Add a companion requirement: "If the system is unable to save using that name, it shall let the user save with a different name or cancel."

> [!question] Exam Angle Second-most-likely source for "identify the flaw and rewrite." Notice the pattern in both worked examples above: **the fix is a second, explicit requirement covering the exception/edge case** — not just a rewording.

## 13. Ambiguous Terms to Avoid — Memorize This Table

|Term|Why it's bad / what to do instead|
|---|---|
|acceptable, adequate|Define what makes it acceptable and how the system judges it|
|as much as practicable|Don't leave it to developers — mark as **TBD** with a resolution date|
|at least / at a minimum / not more than / not to exceed|Specify exact min/max values|
|between|State whether endpoints are included|
|fast, rapid|Specify minimum acceptable speed|
|flexible|Describe exactly how the system must change and under what conditions|
|improved, better, faster, superior|Quantify the amount of improvement|
|maximize, minimize, optimize|State the actual max/min acceptable value|
|normally, ideally|Also describe abnormal/non-ideal behavior|

> [!question] Exam Angle Very likely MCQ format: "Which of the following words should be avoided in a requirement?" with 4 fuzzy-word options — all four are correct-style traps, so this table format also fits **T/F** ("the word 'flexible' is acceptable in a requirement statement" → False).

## 14. Before & After — Worked Example (study this pattern closely)

**Before (flawed):** _"Charge numbers should be validated on line against the master corporate charge number list, if possible."_

**Flaws identified:**

- "if possible" is vague — feasibility unknown → should be **TBD**, not baked into the requirement.
- "should" — imprecise, not a clear mandate → use "shall/must."
- Doesn't specify what happens when validation **passes or fails**.

**After (corrected) — two requirements:**

1. "At the time the requester enters a charge number, the system **shall** validate it against the master corporate charge number list."
2. "If the charge number is not found on the list, the system **shall** display an error message and **shall not** accept the order."

> [!question] Exam Angle This is _the_ model answer template for "identify the flaw and rewrite it correctly." Structure your answer as: **(a) list each flaw with the specific term/pattern**, **(b) give the corrected requirement(s)**, split into multiple requirements if an exception/success-failure branch is needed.

---

## 15. The Data Dictionary

**Purpose:** binds together the various requirements representations; can be a standalone doc or SRS appendix. Prevents mistakes from differing understandings of key data terms.

### Notation (know all four — common MCQ matching set)

|Construct|Symbol|Meaning|Example|
|---|---|---|---|
|**Primitive**|`* comment *`|Element that can't/needn't be decomposed further; defines type, size, range|`Request ID = * a 6-digit system-generated sequential integer... *`|
|**Composition**|`+` (parentheses = optional)|A structure/record made of multiple data items|`Requested Chemical = Chemical ID + Number of Containers + Grade + Amount + Amount Units + (Vendor)`|
|**Iteration**|`{ }` with `min:max` prefix|Multiple instances of an item allowed|`Request = ... + 1:10 {Requested Chemical}`|
|**Selection**|`[ ]` with `\|` separators|Enumerated primitive — limited discrete values|`Quantity Units = ["grams" \| "kilograms" \| "milligrams" \| "each"]`|

> [!warning] Common Mistake Students mix up **Iteration `{ }`** and **Selection `[ ]`**. Memorize by function: **braces = "repeat me" (how many times)**; **brackets = "choose one" (which value)**. Parentheses `( )` alone = optional single item, not repetition or choice.

### Sample data dictionary table style

Columns typically: **Entity | Attribute | Type/Size | Validation | Key** (e.g., Pupil.PupilID = Number(5), 10000–99999, Primary key)

---

## 16. Modeling the Requirements

List of representation/modeling techniques (recognize names, don't need to draw all): Data Flow Diagram (DFD) · Process/Swimlane diagram · State-Transition Diagram (STD) & state tables · Dialog map · Decision table/tree · Event-response table · Feature tree · Use case diagram · Activity diagram · Entity-Relationship Diagram (ERD) / Class Diagram

### Relating the customer's voice to the analysis model ⭐ (good matching-MCQ material)

|Word type|Examples|Maps to|
|---|---|---|
|**Noun**|people, orgs, systems, data, objects|External entities/data stores/flows (DFD) · Actors (use case) · Entities/attributes (ERD) · Lanes (swimlane) · Objects with states (STD)|
|**Verb**|actions, things done, events|Processes (DFD) · Process steps (swimlane) · Use cases · Relationships (ERD) · Transitions (STD) · Activities · Events (event-response table)|
|**Conditional**|if/then logic|Decisions (decision tree/table, activity diagram) · Branching (swimlane/activity diagram)|

> [!question] Exam Angle MCQ: "A verb in a customer's requirement statement most likely maps to..." → a **process (DFD)** or **use case**, not an entity.

## 17. Specifying Reports

**Dashboard** = a screen/printed report using multiple textual/graphical representations to give a **consolidated, multidimensional view** of an organization/process.

---

## 🎯 High-Priority Ranking for Tonight (if time runs out, study in this order)

1. **Business Rules Taxonomy** (§2) — confirmed short-question topic
2. **SRS sections/template** (§8) — confirmed short-question topic
3. **Avoiding ambiguity + Avoiding incompleteness + Before/After example** (§11, §12, §14) — this is where "identify the flaw and rewrite" comes from
4. **Labeling schemes pros/cons** (§6) — classic comparison-table MCQ
5. **Data dictionary notation** (§15) — classic matching MCQ
6. **Ambiguous terms table** (§13) — easy MCQ points if memorized
7. Everything else (UI/SRS case study, audience table, characteristics list) for T/F breadth

---

## 📝 Model Answers to Your 3 Predicted Short Questions

### Q1. Types of Business Rules taxonomy, with examples

Answer using the full structure in **§2** — 5 types (Facts, Constraints, Action Enablers, Inferences, Computations), one-line definition + one example each. If it's a 10-mark descriptive question, also draw/describe the taxonomy tree (Business Rules → the 5 branches) and note the Action-Enabler-vs-Inference distinction explicitly, since examiners love testing that exact confusion.

### Q2. Different sections of SRS and their purpose

Answer using **§8**'s table — 6 numbered sections + Appendix A, one purpose-sentence each. Mention explicitly that the SRS describes **what**, not **how** (design/construction excluded), since that's often asked as a follow-up clause.

### Q3. Identify flaw in a specification and rewrite it correctly

Use the method from **§14**:

1. Read the given requirement and check it against the ambiguity list (§11) and incompleteness list (§12): fuzzy words? vague modal verb (should/may)? unclear boundary? missing exception/failure path? missing opposite operation?
2. Name the specific flaw(s) explicitly by category.
3. Rewrite using "**shall**," a named actor, a clear trigger, and — if it was an incompleteness flaw — **add a second requirement** covering the exception/failure case, exactly like the charge-number example.

---

## ⚡ Rapid-Fire T/F Traps (self-test before bed)

- "Facts describe restrictions on what a user can do." → **False** (that's Constraints)
- "The then-clause of an Inference is always an action." → **False** (that's Action Enablers)
- "The SRS should describe how the system will be implemented." → **False**
- "Hierarchical numbering has no downsides since it's most common." → **False** (renumbering breaks references)
- "'Should' and 'shall' are interchangeable in requirement writing." → **False**
- "TBD items resolve themselves over time." → **False**
- "Iteration in a data dictionary uses square brackets." → **False** (curly braces `{ }`)
- "UI wireframes can replace written functional requirements." → **False**
- "'Flexible' and 'fast' are acceptable, precise requirement terms." → **False**