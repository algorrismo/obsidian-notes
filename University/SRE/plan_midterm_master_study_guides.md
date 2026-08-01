# 📋 Implementation Plan: SRE Midterm Master Study Guides (Ch. 01 – Ch. 05)

## 📌 Goal Description
The objective is to create an exhaustive, faculty-grade, Obsidian-ready Markdown Study Guide suite for all 5 lecture slide decks included in the upcoming **CSC 4160 Software Requirement Engineering (SRE)** midterm exam.

### Exam Pattern:
- **MCQ & True/False:** 50 Questions × 1 Mark = **50 Marks**
- **Descriptive Questions:** 3 out of 6 Questions × 10 Marks = **30 Marks**
- **Total Marks:** **80 Marks**

---

## 💡 User Review Required

> [!IMPORTANT]
> **Coverage Scope:** All 5 slide decks will be systematically covered slide-by-slide without skipping any topic:
> 1. **Ch 01:** The Essential Software Requirement (37 slides) — *Completed initial draft, to be unified*
> 2. **Ch 02:** Requirements from Customer, Practice, & Business Analyst Perspective (15 slides)
> 3. **Ch 03:** Software Requirements Elicitation (51 slides)
> 4. **Ch 04:** Documenting Requirements (44 slides)
> 5. **Ch 05:** Finalizing Requirements Development (48 slides)

> [!NOTE]
> **Output Deliverables:** Five individual Obsidian-optimized `.md` files + One Master Midterm Cheatsheet:
> - `SRE_Ch01_Master_Study_Guide.md`
> - `SRE_Ch02_Master_Study_Guide.md`
> - `SRE_Ch03_Master_Study_Guide.md`
> - `SRE_Ch04_Master_Study_Guide.md`
> - `SRE_Ch05_Master_Study_Guide.md`
> - `SRE_Midterm_Ultimate_Cheatsheet.md`

---

## 🎯 Proposed File Structure & Detailed Chapter Breakdown

---

### Component 1: `SRE_Ch01_Master_Study_Guide.md` (Chapter 1)
- **Slide Count:** 37 Slides
- **Key Focus Topics:**
  - Definition & Time Dimension of Requirements
  - 3 Levels of Requirements (BR, UR, FR) & System Requirements
  - Standish Group Failure/Success statistics (13% user input, 16% involvement)
  - Relative cost of defect repair (up to 200:1 ratio) & The Leakage Problem (74%)
  - NFRs, Business Rules vs. Software Requirements, Features
  - Product vs. Project Requirements & SRS Boundaries
  - Requirement Engineering = Development (4 phases) + Management
  - Baselined Requirements as boundary
- **Solved Slide Tasks:** Task 1 (Slide 35 classification) & Task 2 (Slide 36 hospital wait time hierarchy).

---

### Component 2: `SRE_Ch02_Master_Study_Guide.md` (Chapter 2)
- **Slide Count:** 15 Slides
- **Key Focus Topics:**
  - Expectation Gap (Frequent customer engagement vs. gap)
  - Stakeholders (Internal vs. External, Project Team vs. Developing Org)
  - Customer vs. User vs. End User (Direct vs. Indirect users)
  - Customer-Development Partnership Rights (9 rights) & Responsibilities (9 obligations)
  - Decision Making Models (Leader, Majority, Unanimous, Consensus) & Agreement criteria
  - The Business Analyst (BA) Role, Tasks (10 tasks), Skills (14 skills), and Knowledge
  - The Making of a BA (Former user, developer/tester, PM, domain expert)

---

### Component 3: `SRE_Ch03_Master_Study_Guide.md` (Chapter 3)
- **Slide Count:** 51 Slides
- **Key Focus Topics:**
  - Product Vision & Project Scope (Vision & Scope Document / Project Charter / MRD)
  - Business Scope Document Structure (As-Is problem, To-Be goal, In-Scope vs. Out-of-Scope)
  - Scope Representation Techniques: Context Diagram, Ecosystem Map, Feature Tree, Event List
  - User Classes: Favored (priority), Disfavored (restricted access), Ignored (outside scope)
  - User Personas (Archetype, Bio, Pain Points, UR/FR mapping) with examples ("Hungry Harry", "Careful Carla")
  - Product Champion (Role, Activities across Planning/Reqs/Validation/Aids/Change, Traps to avoid)
  - Product Owner in Agile (Backlog prioritization) & Resolving Conflicting Requirements (Table 6-3 rules)
  - Requirements Elicitation Techniques (Interviews, Workshops, Focus Groups, Observations/Ethnography, Questionnaires)
  - Straw Man Model (Draft $\rightarrow$ Present $\rightarrow$ Deconstruct $\rightarrow$ Rebuild $\rightarrow$ Test)
  - Assumed vs. Implied Requirements & Finding Missing Requirements
  - Use Cases (Verb + Object) & User Stories (`As a <user>, I want <goal> so that <reason>`)
  - Essential elements of Use Cases & Use Case Traps to avoid

---

### Component 4: `SRE_Ch04_Master_Study_Guide.md` (Chapter 4)
- **Slide Count:** 44 Slides
- **Key Focus Topics:**
  - Business Rules Taxonomy: Facts, Constraints, Action Enablers, Inferences, Computations (Comparison Table & Healthcare Examples)
  - Cataloging & Documenting Business Rules (Atomic IDs, Static vs. Dynamic)
  - The SRS Document Structure (IEEE Standard 6 Sections) & Audience Needs (9 stakeholder perspectives)
  - Requirements Labeling Schemes: Sequence Numbers (UC-9), Hierarchical Numbering (3.2.4.3), Hierarchical Textual Tags (Product.Cart.01)
  - Dealing with Incompleteness (TBD notation rules & traps)
  - Conceptual User Interfaces (Sketches, Wireframes, Mock-ups/Horizontal vs. Proof of Concept/Vertical)
  - UI Driving Requirements Trap (4 Gaps in "Sleek Checkout": Error state, Race condition, Legal compliance, Inventory discrepancy)
  - Guidelines for Writing Requirements ("The system shall [response]"), Avoiding Ambiguity (Fuzzy words, boundary values, double negatives)
  - Data Dictionary Notations (DeMarco): Primitive (`* comment *`), Composition (`+`), Optional (`()`), Iteration (`{}`), Selection (`[] | []`)
  - Analysis Models (DFD, Swimlane, STD, Dialog Map, Decision Table/Tree, ERD) & Mapping Nouns (Entities/Actors), Verbs (Processes/Use Cases), Conditionals (Decisions).

---

### Component 5: `SRE_Ch05_Master_Study_Guide.md` (Chapter 5)
- **Slide Count:** 48 Slides
- **Key Focus Topics:**
  - Purposes of Prototypes (Clarify, explore design, evolutionary subset)
  - Types of Prototypes: Paper vs. Electronic, Throwaway (Mock-up/Wireframe) vs. Evolutionary (Proof of Concept)
  - Incorporating Prototypes into SDLC & Dialog Map (State transition UI navigation)
  - Risks of Prototyping (Pressure to release, distraction by details, performance expectations) & Success Factors
  - Prioritization Pragmatics & Why Prioritize (High customer expectations, limited resources, 6 issues)
  - Prioritization Techniques: In/Out (Binary), Pairwise Comparison & Rank Ordering (Matrix calculation example $A=37.5\%, B=12.5\%, C=50\%, D=0$), Weighted Grid Analysis (Windsurfing car example)
  - MoSCoW Method (Must, Should, Could, Won't) & ZestyBites Food App case study
  - Three-Level Scale (Importance vs. Urgency matrix) & Multipass Prioritization (handling dependencies)
  - $100 Imaginary Dollars Technique & Value/Cost/Risk Model ($\text{Priority} = \frac{\text{Value}\%}{\text{Cost}\% + \text{Risk}\%}$)
  - Verification ("doing the thing right") vs. Validation ("doing the right thing")
  - Requirements Review: Informal (Peer Desk Check, Pass Around, Walkthrough) vs. Formal (Inspection)
  - Inspection Process: Roles (Author, Moderator, Reader, Recorder), Entry Criteria, 6 Stages, Exit Criteria
  - Defect Checklists (Completeness, Correctness, Quality Attributes) & Testing Requirements (V-Model of SDLC, Acceptance Criteria & Tests).

---

### Component 6: `SRE_Midterm_Ultimate_Cheatsheet.md`
- **Purpose:** Quick-ref guide summarizing all 5 chapters on a single page for rapid revision 1 hour before the exam.
- **Includes:**
  - All numerical stats & ratios to memorize (200:1, 74%, 13%, 16%, scale 1-9, etc.)
  - High-yield MCQ & True/False cheat table
  - 10-Mark Descriptive question answer blueprints for all 5 chapters.

---

## 🔍 Verification Plan

### Manual Verification
1. Verify that all 5 Markdown files + 1 Master Cheatsheet are generated in `C:\Users\Hp\Desktop\SRE\`.
2. Inspect markdown formatting for Obsidian compatibility (tables, LaTeX equations, callouts, bold highlights).
3. Validate that every single slide topic from Ch.01 to Ch.05 is represented without omission.
