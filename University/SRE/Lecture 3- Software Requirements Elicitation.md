---
tags:
  - SRE
exam: MCQ+T/F (50×1=50) + Descriptive (3 of 6 × 10 = 30)
---

# SRE — Chapter 3: Software Requirements Elicitation

### Faculty Exam-Prep Notes — Lecture 1

> [!info] How to use this
> This chapter is really **four sub-topics glued together**. Learn them as four separate blocks, don't blur them:
> 
> 1. Business Requirements → Vision & Scope  
> 2. User Classes → Personas → Product Champion  
> 3. The Elicitation Process → Techniques  
> 4. Use Cases & User Stories  
> 
> MCQs on this chapter usually test whether you can **tell two similar‑sounding terms apart** (vision vs. scope, product champion vs. product owner, use case vs. user story). That's the #1 trap. I'll flag every one.

## BLOCK 1 — Business Requirements & Vision/Scope

### 1.1 Business Requirements — the foundation

> [!note] Key definition (memorize verbatim-ish, MCQs love definitions) **Business requirements** = the aggregate information describing a need that leads to a project, plus the desired business outcomes. Made up of: **business opportunities, business objectives, success metrics, vision statement.**

- Business requirement issues must be resolved **before** functional/non-functional requirements can be specified. (Order matters — this is a classic T/F question: "Functional requirements should be defined before business requirements." → **FALSE**)
- Business requirements typically come from: **funding sponsors, corporate executives, marketing managers, product visionaries.**
- The **Business Analyst (BA)** doesn't _own_ business requirements — the BA _facilitates_ elicitation, prioritization, and conflict resolution among the right stakeholders.

> [!warning] Common mistake Students confuse "BA sets the business requirements" with "BA ensures the _right stakeholders_ set them." The BA is a **facilitator**, not the source. Expect a T/F trap here.

**Likely question style:** MCQ — "Which of the following is NOT one of the four components of business requirements?" (distractors will slip in "functional requirements" or "user stories" as fake options.)

---

### 1.2 Vision vs. Scope — THE most-confused pair in this chapter

||Vision|Scope|
|---|---|---|
|What it is|Describes the **ultimate product** — what it is and could become|Draws the **boundary** of what THIS project/iteration will deliver|
|Time horizon|Long-term, aspirational|Bounded, current release|
|Question it answers|"What are we building, ultimately?"|"What part are we building **now**?"|

> [!danger] #1 exam trap in this whole chapter Vision = the _big picture destination_. Scope = the _slice you're building right now_. A question describing "the boundary between what's in and out for this project" is asking about **scope**, not vision — even if it mentions "product." Read carefully.

### 1.3 Vision and Scope Document (⭐ explicitly listed as a likely short-answer topic)

> [!important] YOU TOLD ME THIS IS LIKELY ON THE EXAM — memorize this structure

- **Owner** of the document: the project's **executive sponsor / funding authority** (NOT the BA, NOT the developer).
- Similar deliverables in other orgs: **project charter**, **business case document**, or (for commercial software) a **Market/Marketing Requirements Document (MRD)**.

**Template structure (Figure 5-3) — this is the answer they want:**

```
1. Business Requirements
   1.1 Background
   1.2 Business Opportunity
   1.3 Business Objectives
   1.4 Success Metrics
   1.5 Vision Statement
   1.6 Business Risks
   1.7 Business Assumptions and Dependencies

2. Scope and Limitations
   2.1 Major Features
   2.2 Scope of Initial Release
   2.3 Scope of Subsequent Releases
   2.4 Limitations and Exclusions

3. Business Context
   3.1 Stakeholder Profiles
   3.2 Project Priorities
   3.3 Deployment Considerations
```

> [!tip] How to answer this if asked descriptively Structure your answer as: **(1) Purpose** — one deliverable collecting business requirements to set the stage for development → **(2) Owner** — executive sponsor/funding authority → **(3) The 3 major sections** — Business Requirements, Scope and Limitations, Business Context → **(4) One-line description of each subsection** (don't just list numbers — examiners want to see you understand what goes in 1.2 vs 1.6, etc.)

> [!warning] Common mistake Students memorize the numbers but forget **who owns the document**. That single fact ("executive sponsor") is a very common isolated MCQ.

### 1.4 Business Scope Document Structure — the As-Is / To-Be model

- **As-Is Problem**: what's broken/slow/expensive _right now_ (e.g., "invoices take 25 minutes each")
- **To-Be Goal**: the _quantitative_ target for success (e.g., "reduce processing time by 15%")
- **Boundary Lines**: clear In-Scope vs. Out-of-Scope sections — prevents **"Scope Creep"** (developers building unfunded/unprioritized features)

> [!tip] Exam tip If a question gives you a scenario and asks "what should go in the As-Is section?" — look for the **current pain point stated as a number/fact**, not a solution. If it asks for To-Be, look for a **measurable target**.

### 1.5 Samples 1 & 2 — know the pattern, not the specific numbers

You don't need to memorize the 15%/20%/45-minutes figures. You DO need to understand the **shape**: Executive Summary → Business Benefits & Success Metrics → In-Scope → Out-of-Scope. This shape is reusable for any scenario question they invent.

### 1.6 ⭐ The In-Scope/Out-of-Scope Exercise — HIGH PROBABILITY OF A SIMILAR QUESTION

This is a classic "apply the rule to a new scenario" question type. Here's the reasoning pattern, worked out:

|#|Request|Verdict|Why|
|---|---|---|---|
|1|Live map with real-time truck GPS blinking dot|**Out of Scope**|Explicitly excluded: "GPS/real-time location tracking... handled by existing third-party fleet software"|
|2|Block manager from assigning Level-1 tech to a job needing Level-3 Fiber-Optic cert|**In Scope**|Matches core in-scope item: "automatically matches technician certifications... against open client tickets"|
|3|Check if a student's **Python (.py)** assignment was AI-written|**Out of Scope**|Explicitly excluded: "compiled software code (.java, .py)"|
|4|Scan **Apple Pages (.pages)** essays for plagiarism|**Out of Scope**|In-scope list only names `.docx, .pdf, .txt` — `.pages` was never included|
|5|Auto-change grade to F + lock out student at 95% AI match|**Out of Scope**|Explicitly excluded: "Automated disciplinary actions... penalization must be executed manually by the professor"|

> [!danger] The pattern to learn (not just memorize the 5 answers) A new feature request is **In-Scope** only if it clearly matches something on the In-Scope list. It's **Out-of-Scope** if it's (a) explicitly excluded, or (b) simply never mentioned anywhere (like the `.pages` file case — don't assume "similar to .docx" counts). **When in doubt between "not mentioned" and "in scope," the safe/correct answer is almost always Out-of-Scope** — that's the whole point of scope discipline.

### 1.7 Scope Representation Techniques — 3 diagram types, don't mix them up

|Technique|What it shows|Look for|
|---|---|---|
|**Context Diagram**|The system in the center, connected to **external entities/actors** (people/systems that send/receive data) via labeled data flows|One circle (the system) + boxes around it|
|**Ecosystem Map**|How the system fits among **other systems/applications** in the org (system-to-system, not actor-to-system)|Boxes connected to boxes, system-level view|
|**Feature Tree**|Hierarchical breakdown of **features/functions** the system offers|Tree/branch structure, product name as root|

> [!warning] Common mistake Context Diagram and Ecosystem Map look almost identical (boxes + arrows) in a rushed glance. The distinguishing test: **Context Diagram = people/external entities interacting with the system. Ecosystem Map = other systems interacting with the system.**

### 1.8 Event List

- Identifies **external events** that trigger system behavior: user-triggered, **time-triggered (temporal)**, or **signal events** (from hardware/external components).
- Used to **cross-check** the Context Diagram and Ecosystem Map for completeness — every external entity should be traceable to at least one event, and vice versa.

> [!tip] Likely MCQ "Time to generate OSHA compliance report arrives" — what kind of event is this? → **Temporal/time-triggered event** (not a user event, not a signal event).

### 1.9 Vision & Scope on Agile Projects

- Iteration scope = user stories pulled from a **dynamic product backlog**, based on priority + team's delivery capacity per timebox.
- Two flavors: (a) fixed iteration count, controlled scope per iteration OR (b) fixed overall duration, flexible scope across remaining iterations.

---

## BLOCK 2 — User Classes, Personas & Product Champion

### 2.1 User Classes — the 8 dimensions of difference (⭐ explicitly listed as likely topic)

Users can differ by:

1. Access privilege/security level (ordinary/guest/admin)
2. Tasks performed
3. Features used
4. Frequency of use
5. Application domain experience / technical expertise
6. Platform (desktop, tablet, smartphone, specialized device)
7. Native language
8. **Direct vs. indirect** interaction with the system

> [!tip] How to answer "define user classes and give examples" Structure: **(1) Definition** — groups of users distinguished by shared characteristics/needs → **(2) List 3-4 of the 8 dimensions** → **(3) Give the Favored/Disfavored/Ignored classification** (below) → **(4) One worked example** (LMS or Banking App, from the slides).

### 2.2 Classifying Users — Favored / Disfavored / Ignored (⭐ core of user-classes question)

|Class|Meaning|
|---|---|
|**Favored user**|Their satisfaction is _aligned with the business goal_ — the system is built primarily for them|
|**Disfavored user**|Deliberately **restricted access/privilege** — not given full capability|
|**Ignored user**|The product is simply **not designed for them** — outside consideration entirely|

**Memorized examples straight from your slides:**

_Example 1 — University LMS:_

- Favored: Administrators, Professors/Instructors
- Disfavored: Students
- Ignored: Parents of students

_Example 2 — Digital Banking App:_

- Favored: The everyday account holder
- Disfavored: Compliance/Risk Auditor
- Ignored: Non-customer recipients (unregistered users)

> [!warning] Common mistake Don't confuse "Disfavored" with "Ignored." **Disfavored = they DO use the system but with restrictions** (e.g., Students CAN use the LMS, just with fewer privileges than professors). **Ignored = they don't interact with the system at all** (Parents never touch the LMS). This distinction is a favorite T/F trap: _"In the LMS example, Students are an ignored user class." → FALSE (they're disfavored)._

**Hierarchy to remember (Figure 6-1):** `Stakeholders → Customers → Direct & Indirect Users → {Favored, Disfavored, Ignored, Other} User Classes`

### 2.3 Identifying User Classes

Study the org chart for:

- Departments that participate in / are affected by the business process
- Departments/roles containing direct or indirect users
- User classes spanning multiple departments
- Departments interfacing with external stakeholders

### 2.4 User Personas (⭐ explicitly listed as likely topic)

> [!note] Definition A **persona** = description of a **hypothetical/fictional** but generic person standing in for a group of users with similar characteristics and needs.

**The textbook example: "Fred" (Chemical Tracking System)**

- 41-year-old chemist, low patience with computers, works 2 projects at once, needs ~4 chemicals/day from stockroom, wants MSDS emailed automatically on first purchase, wants a monthly chemical-usage report auto-emailed.

**Slide-added examples worth knowing (they show the _format_ a persona should follow):**

- **"Hungry Harry"** (Campus Cafeteria App) — high-speed power user → wants "Favorite Order" one-click reorder → maps to a functional requirement about tokenized payment storage.
- **"Careful Carla"** (Fitness Tracking App) — privacy-conscious → wants location tracking disabled without breaking the app → maps to "private by default" functional requirement.

> [!tip] How to answer "explain user persona with an example" Structure: **(1) Definition** (fictional stand-in for a user class) → **(2) Why it's useful** (makes an abstract user class concrete/relatable for the design team) → **(3) Give ONE full example** (Fred is safest — it's the textbook's own example) → **(4) Mention it typically includes: bio, goals/motivations, pain points, tech-savviness, and how it maps to actual requirements** (this last point — the Harry/Carla format — is what makes an answer stand out vs. one that just repeats Fred's paragraph).

> [!warning] Common mistake A persona is **not a real user** and not a "user class" itself — it's a **fictional representative OF** a user class. Don't say "persona and user class are the same thing" on a T/F question.

### 2.5 Connecting with User Representatives

Communication chain (Figure 6-3): **User → Product Champion / Trainer / Focus Group / Help Desk / User Manager / Procuring Customer → (Marketing/Sales) → Business Analyst / Product Manager → Developer.**

- Know that there are _multiple possible pathways_, not one single line — real users rarely talk to developers directly.

### 2.6 The Product Champion (⭐ explicitly listed as likely topic)

> [!note] Definition **Product Champions** = key members of the user community who **provide requirements**; each one is the primary interface between **one user class** and the BA.

- Best champions: have a **clear vision** of the new system, and are **fully empowered to make binding decisions** on behalf of their user class.

**Product Champion activities (memorize the 5 categories, examples optional):**

|Category|Sample activities|
|---|---|
|Planning|Refine scope/limitations, evaluate business impact, define transition path|
|Requirements|Collect input, develop use cases/user stories, resolve conflicts, set priorities|
|Validation & Verification|Review specs, define acceptance criteria, do UAT|
|User Aids|Write docs/help text, contribute to training|
|Change Management|Evaluate/prioritize enhancement requests, adjust scope of future releases|

**Product Champion traps to avoid (know at least 2-3):**

1. Managers overriding a duly-authorized champion's decisions → frustrates champions, upsets users
2. A champion who only represents **their own** opinion, not the whole user class
3. A champion with no clear vision who just rubber-stamps whatever the BA proposes
4. A senior user "delegating" the role to a junior person but still backseat-driving

> [!tip] How to answer "explain the product champion role" Structure: **(1) Definition** → **(2) Key requirement for success** (empowered to make binding decisions) → **(3) 2-3 categories of activities** → **(4) 1-2 traps to avoid.** This shows both the _ideal_ and the _failure modes_ — examiners reward both sides.

### 2.7 ⚠️ Product Champion vs. Product Owner — DO NOT MIX THESE UP

||Product Champion|Product Owner|
|---|---|---|
|Context|Traditional/plan-driven projects|**Agile** projects|
|Represents|ONE user class|The customer/business as a whole|
|Core job|Gather & validate requirements from their user class|Define vision, **own and prioritize the product backlog**|

> [!danger] Very likely MCQ trap "Who is responsible for prioritizing the product backlog in an agile project?" → **Product Owner**, NOT Product Champion. This distinction (traditional role vs. agile role) is prime MCQ territory.

### 2.8 Resolving Conflicting Requirements (Table 6-3) — just recognize the pattern

|Disagreement between|Resolved by|
|---|---|
|Individual users|Product champion or product owner decides|
|User classes|**Favored** user class gets preference|
|Market segments|Segment with greatest business impact wins|
|Corporate customers|Business objectives dictate|
|Users & user managers|Product owner/champion for that class decides|
|Development & customers|Customers win, but aligned with business objectives|
|Development & marketing|Marketing wins|

> [!tip] Trick to remember it fast: "the more strategic/business-aligned party generally wins" — except individual disputes, which go to the designated decision-maker (champion/owner).

### 2.9 Finding the Voice of the User — 3 steps

1. Identify user classes
2. Select/work with representatives of each class + stakeholder group
3. Agree on who the actual requirements decision-makers are

---

## BLOCK 3 — The Requirements Elicitation Process

### 3.1 The Elicitation Cycle (Figure 7-1)

```
Elicitation → Analysis → Specification → (back to) Elicitation
```

It's **cyclic**, not a one-time event — a very common T/F question tests exactly this ("Elicitation is a one-time activity performed only at project start" → **FALSE**).

### 3.2 Elicitation Activities — the 6-step flow (Figure 7-2)

**Prepare** → Decide scope/agenda → Prepare resources → Prepare questions/straw-man models **Perform** → Perform the elicitation session **Follow up** → Organize/share notes → Document open issues

**Straw Man Model process:** Draft → Present → Deconstruct → Rebuild → Test & Iterate

> [!tip] MCQ likely tests ORDER — e.g., "Which comes first: preparing questions, or performing the elicitation session?" Know the 3 phase groupings above.

### 3.3 Elicitation Techniques — match technique to its key rule

|Technique|Key rules to remember|
|---|---|
|**Interviews**|Establish rapport, stay in scope, prepare questions, listen actively|
|**Workshops**|Enforce ground rules, fill all team roles, timebox discussions, keep team small but right|
|**Focus groups**|A _representative group_ of users convened to generate input on functional/quality requirements|
|**Observations / Ethnography**|Watch users in their real environment|
|**Interface analysis** (system & user)|Study existing interfaces for clues to requirements|
|**Document analysis**|Study existing documentation|
|**Questionnaires**|Mutually exclusive + exhaustive answer choices; no leading questions; consistent scales; test before distributing; don't overload with questions|

> [!warning] Common mistake Students mix up "focus group" (a _group discussion_, generates ideas) with "questionnaire" (individual, written, good for _statistical_ analysis). If a question emphasizes "structured, closed-ended, used for statistical analysis" → that's **Questionnaire**, not Focus Group.

### 3.4 Planning Elicitation (Figure 7-3 table) — just know the general logic

Different project types (mass-market software, internal corporate software, replacing an existing system, embedded systems, etc.) favor **different combinations** of techniques. You don't need the exact X's — just understand: _mass-market software leans on interviews/focus groups/questionnaires (reaching many anonymous users), while internal/replacement systems lean more on workshops/interviews/interface & document analysis (fewer, known stakeholders)._

### 3.5 Classifying Customer Input (Figure 7-7) — 8 categories

When a stakeholder talks, sort what they say into: **Business Requirements, User Requirements, Business Rules, Functional Requirements, Quality Attributes, External Interface Requirements, Constraints, Data Requirements, Solution Ideas**

**If it doesn't fit any category, it might be:**

- A non-software project requirement (e.g., "train users")
- A project constraint (cost/schedule — different from design/implementation constraints)
- An assumption or dependency
- Background/context information
- Extraneous, no-value info

> [!tip] Likely MCQ: given a stakeholder statement, classify it. E.g. "The system must integrate with our existing SAP database" → **External Interface Requirement** (or Constraint, depending on phrasing) — NOT a functional requirement.

### 3.6 How Do You Know You're Done Eliciting? (memorize 3-4 signals)

- Users can't think of new use cases/stories
- New scenarios don't produce new functional requirements
- Users repeat previously-covered issues
- New suggestions are consistently **out of scope** or **low priority**
- Devs/testers reviewing requirements raise few questions

### 3.7 Cautions About Elicitation

- **Balance stakeholder input** — don't just listen to the loudest/most opinionated customer
- **Define scope appropriately** — poorly defined scope derails everything
- **Avoid the requirements-vs-design argument** — requirements = _what_ the system does; design = _how_ it's implemented. Prototypes/screen sketches are illustrative only, not final design commitments.
- **Research within reason** — too much exploratory research disrupts elicitation momentum

### 3.8 Assumed & Implied Requirements (⭐ explicitly listed as likely topic — know the difference cold)

|Type|Definition|Example (from slides)|
|---|---|---|
|**Assumed requirement**|Expected without being explicitly stated — "obvious" to the customer, may not be obvious to the developer|Client asks for e-commerce checkout; assumes it auto-emails a receipt but never says so|
|**Implied requirement**|Necessary _because of_ another stated requirement, though not itself stated|Client asks for profile-picture upload; implies file-size limits, image compression, malware scanning|

> [!danger] The distinguishing test (this IS the exam question) **Assumed** = the customer forgot to mention it because it felt too obvious to say. **Implied** = a _logical consequence/dependency_ of something they DID say — a competent developer should infer it's needed even without being told. If asked to write your own example: pick something with a clear "stated requirement → necessary follow-on requirement" chain for **implied**, and something that's a natural unstated expectation of a stated feature for **assumed**.

> [!tip] How to answer this descriptively Structure: **(1) Define both terms clearly, side by side** → **(2) Give the textbook example for each** (checkout/receipt for assumed; profile picture/file-size-compression-malware for implied) → **(3) Explain WHY this distinction matters** (developers can't implement what they don't know about — this is why finding these gaps proactively matters, connects to "Finding Missing Requirements" below).

### 3.9 Finding Missing Requirements — 7 techniques (know 3-4)

- Decompose high-level requirements into detail
- Ensure ALL user classes gave input
- Trace requirements → functional requirements (nothing should be an orphan)
- Check boundary values
- Represent info in more than one way (text + diagram)
- Watch complex Boolean logic (AND/OR/NOT) — often incomplete
- Use a checklist of common functional areas / a data model to reveal gaps

---

## BLOCK 4 — Use Cases & User Stories

### 4.1 Definitions

> [!note] **Use case**: a sequence of interactions between a system and an external **actor** that results in the actor achieving a valuable outcome. Named as **verb + object** (e.g., "Update Customer Profile").
> 
> **User story**: `As a <type of user>, I want <some goal> so that <some reason>.`

**Figure 8-1 flow (know both halves):**

- Use Case Name → (conversations) → Use Case Specification → (analysis) → **Functional Requirements** + **Tests**
- User Story → (conversations) → Refined User Stories → (conversations) → **Acceptance Tests**

> [!warning] Common mistake A **use case** leads to functional requirements _and_ tests via analysis. A **user story** leads _directly_ to acceptance tests through ongoing conversation — there's no separate "specification → analysis" step shown for user stories. Don't merge the two diagrams in your head.

### 4.2 Identifying Actors (ask these 3 questions)

1. Who/what is **notified** when something occurs?
2. Who/what **provides** information/services to the system?
3. Who/what **helps** the system complete a task?

### 4.3 Essential Elements of a Use Case (know all 6 — good MCQ fodder)

1. Unique identifier + concise name (verb + object)
2. Brief textual description
3. **Trigger condition**
4. Zero or more **preconditions**
5. One or more **post-conditions**
6. Numbered steps (the actor↔system dialog)

### 4.4 Identifying Use Cases — 6 approaches (know 3)

- Identify actors first, then business processes, then use cases at actor-system interaction points
- Write a specific scenario, then generalize into a use case
- Ask "what tasks convert inputs to outputs?"
- Map external events → actors → use cases
- **CRUD analysis** on data entities (Create/Read/Update/Delete)
- Ask what each external entity in the Context Diagram wants to achieve

### 4.5 Use Case Traps to Avoid

Too many use cases · Overly complex use cases · Including **design** in use cases · Including **data definitions** in use cases · Use cases users don't understand

### 4.6 Benefits/Priority of Usage-Centric Requirements — why a use case/story is high priority

- Core to a business process the system enables
- Used frequently by many users
- Requested by a **favored** user class
- Required for regulatory compliance
- Other system functions depend on it

---

## 🎯 Your 5 Flagged Likely Short-Answer Topics — Quick-Recall Cheat Sheet

> [!important] Practice writing these from memory, closed-book, before the exam.

1. **Vision & Scope Document Structure** → 3 major sections (Business Requirements / Scope & Limitations / Business Context), 14 subsections total, owned by the executive sponsor. _(See §1.3)_
2. **User Classes + Types with Examples** → 8 differentiating dimensions; Favored/Disfavored/Ignored classification; LMS and Banking App examples. _(See §2.1–2.2)_
3. **User Persona with Example** → fictional stand-in for a user class; use "Fred" (chemist) as your safe textbook example; mention it should tie to actual requirements. _(See §2.4)_
4. **Product Champion** → user-community member who's the requirements interface for one user class; needs empowerment to make binding decisions; 5 activity categories; know it's NOT the same as a Product Owner (agile). _(See §2.6–2.7)_
5. **Assumed vs. Implied Requirements with Examples** → Assumed = unstated "obvious" expectation (checkout → auto-receipt email); Implied = logical necessity of a stated feature (profile picture upload → file-size limit/compression/malware scan). _(See §3.8)_

---

## 🧠 General Exam-Taking Strategy for MCQ/T-F on This Chapter

- **When two options both "sound right,"** check if one is describing **vision vs. scope**, **product champion vs. product owner**, or **use case vs. user story** — this chapter's writers clearly love these three pairs.
- **For T/F questions with absolute words** ("always," "only," "never," "one-time") — be suspicious. Elicitation is explicitly **cyclic**, requirements are explicitly **not** all gathered in one interview, etc.
- **For scope-related scenario questions** (like the in-scope/out-of-scope exercise), default to **out-of-scope unless it's clearly and explicitly listed** as in-scope.
- **For "who owns/decides X" questions**, go back to Table 6-3 and the Vision & Scope ownership fact — these are compact, high-yield memorization targets because they're single, unambiguous facts.

---

_Good luck tomorrow — once you've reviewed this, if you want, tell me which of the four blocks feels shakiest and we can drill it with a quick self-test before you move to Chapter 4._