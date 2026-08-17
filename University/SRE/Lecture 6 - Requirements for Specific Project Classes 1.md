---
title: "Ch. 06 — Requirements for Specific Project Classes"
aliases:
  - Requirements for Specific Project Classes
  - Chapter 6 Requirements
  - SRE Ch06
tags:
  - SRE
  - Ch06
  - QuizPrep
  - RequirementsEngineering
  - Lecture
  - SoftwareRequirements
chapter: 6
chapter_name: Requirements for Specific Project Classes
type: lecture-notes
status: complete
source: "Wiegers, K., & Beatty, J. (2013). Software Requirements. Pearson Education."
course: Software Requirements Engineering
created: 2026-08-17
updated: 2026-08-17
---
---

# 📘 Ch. 06 — Requirements for Specific Project Classes

### Full Lecture-Style Breakdown for Quiz Prep

> [!info] How to use this note This chapter is basically **"one-size-does-not-fit-all requirements gathering."** Depending on _what kind of project_ you're doing, the questions you ask (and the requirements you write) change completely. The slide covers **5 project classes**:
> 
> 1. Packaged Solution Projects (COTS)
> 2. Outsourced Projects
> 3. Business Process Automation Projects
> 4. Business Analytics Projects
> 5. Embedded & Real-Time Systems Projects
> 
> Your quiz is MCQ + case study, so pay special attention to the **examples** — that's exactly the format they'll flip into a case study question.

---

## 1️⃣ PACKAGED SOLUTION PROJECTS (COTS)

### 🔑 The Big Idea

Instead of building software from scratch, many organizations **buy** a ready-made solution — called **COTS (Commercial Off-The-Shelf)** — or use **SaaS/cloud solutions**. You still need requirements! Why? Because requirements are what let you:

- ==Evaluate and compare different vendor solutions== (which one do we pick?)
- ==Adapt/configure the package== to actually fit your business once you've bought it

> [!important] Remember this line — it's a favorite exam trap "COTS packages typically need to be **configured, integrated, and extended** to work in the target environment." — buying software is NOT the end of the requirements process, it's a different _start_ to it.

### Requirements for **Selecting** a Packaged Solution

When you're still shopping around, you need to define:

- **User requirements** — what do the actual users need to do with it?
- **Business rules** — what company-specific rules must it follow?
- **Quality requirements** (this is a classic MCQ list — memorize it):
    - ==Performance==
    - ==Usability==
    - ==Modifiability==
    - ==Interoperability==
    - ==Integrity==
    - ==Security==
- **Evaluating solutions** — comparing candidates against these criteria

### Requirements for **Implementing** a Packaged Solution

This is the **most quiz-able part** of this section — a 4-level spectrum of _how much work_ it takes to get a package running, from easiest to hardest:

|Level|What it means|Example from slide|
|---|---|---|
|**Out-of-the-Box (OOTB)**|Install and use _as-is_, no changes|Deploying **Zoom** company-wide — employees just log in and use default settings|
|**Configured**|Change _settings_ only, **no new code**|Setting up **Salesforce CRM** — admin adds a custom dropdown field ("Lead Priority"), builds pipeline stages, turns on automated emails — all point-and-click|
|**Integrated**|Connect the package to _other existing systems_, usually needs **some custom code**|Connecting **Shopify → QuickBooks** so a sale automatically creates an invoice, no manual data entry|
|**Extended**|Write **custom code** to add new capability the package doesn't have|Writing custom **Apex code inside Salesforce** to run proprietary financial risk formulas that Salesforce can't do out of the box|

> [!tip] Easy memory hook Think of it as a ladder: **Install → Tweak settings → Connect to other tools → Build new code inside it.** Increasing effort = Increasing amount of requirements work needed. That's literally what Figure 22-3 shows: _"Increasing amounts of requirements and development work."_

> [!warning] Likely MCQ trap They will give you a scenario (e.g., "an admin adds a new dropdown field using point-and-click tools") and ask you to identify whether it's OOTB / Configured / Integrated / Extended. The **keyword to hunt for** is: _"no code" = Configured_, _"connects two systems" = Integrated_, _"custom code written from scratch" = Extended_.

### Common Challenges With Packaged Solutions

Five classic failure points — good for a "select all that apply" or matching question:

- ==Too many candidates== — many products look similar at first glance, hard to choose
- ==Too many evaluation criteria== — fix: narrow down to only what matters most using **business objectives**, not deep analysis of everything
- ==Vendor misrepresents package capabilities== — often because the salesperson (non-technical) doesn't fully understand what the customer actually needs
- ==Incorrect solution expectations== — looks amazing in the demo, disappoints after real installation (this is why user feedback matters)
- ==Users reject the solution== — buying it doesn't mean people will _want_ to use it — user involvement in the process matters

---

## 2️⃣ OUTSOURCED PROJECTS

### 🔑 The Big Idea

Here, you (the **Acquirer**) hire someone else (the **Supplier**) to build the software for you. Requirements become the _legal and technical backbone_ of the relationship.

> [!important] Golden quote to remember **"Requirements are the cornerstone of an outsourced project"** (Figure 23-1). Everything the supplier delivers is judged against the requirements you gave them.

### The Acquirer ↔ Supplier Cycle (Figure 23-1)

Think of it as a loop:

1. **Acquirer → Supplier:** sends the _Request for proposal, requirements, acceptance criteria_
2. **Both sides:** _Review, negotiate, agree_ on what's actually going to be built
3. **Supplier → Acquirer:** delivers the _Software, documentation_

### Appropriate Level of Requirement Detail

- You need to plan for **multiple review cycles** — requirements aren't approved in one shot
- A good pattern: **requirements workshops** followed immediately by implementation tasks for a few subsystems (so you catch misunderstandings early)
- **Peer reviews and prototypes** are your early-warning system — they show you how the supplier is _interpreting_ your requirements before it's too late
- ⚠️ Risk to remember: contract development companies work across **many industries**, so they may **lack the specific domain/company knowledge** needed to make the right calls on ambiguous requirements

> [!warning] Likely quiz angle A question might describe a supplier "guessing" at unclear requirements and building the wrong thing — the answer they're looking for is usually **"lack of domain knowledge"** or **"insufficient requirements detail / no prototype review."**

---

## 3️⃣ BUSINESS PROCESS AUTOMATION PROJECTS

### 🔑 The Big Idea

This whole section is about **improving how a business does its work**, and it hinges on **4 acronyms that sound similar but mean very different things**. This is almost guaranteed quiz material — they will test whether you can tell BPA, BPI, BPR, and BPM apart.

> [!important] The core distinction to lock in your head
> 
> - **BPA** = _Look_ at the process (analysis only)
> - **BPI** = _Small_ improvements to the _existing_ process
> - **BPR** = _Total_ redesign, throw the old process away
> - **BPM** = _Ongoing, company-wide_ management of all processes over time

### Business Process Analysis (BPA)

- **Focus:** Examine the _current_ state of a process to find bottlenecks/inefficiencies — this is diagnostic, not fixing yet
- **Example:** A bank studies its loan workflow and discovers applications sit untouched for **4 days** waiting on manual income verification

### Business Process Improvement (BPI)

- **Focus:** Small, **incremental/evolutionary** improvements — the _core framework stays the same_
- **Example:** Same bank keeps its 10-step process, but adds an automated alert if a loan sits idle >24 hrs + an online checklist → cuts time from **10 days → 7 days**

### Business Process Reengineering (BPR)

- **Focus:** **"Clean-sheet design"** — scrap the current process entirely for radical/dramatic transformation
- **Example:** Bank eliminates the _entire_ paper process and builds an AI platform that gives approval/denial in **60 seconds**, zero human involvement

### Business Process Management (BPM)

- **Focus:** The **ongoing, holistic discipline** of managing/monitoring/optimizing _all_ processes across the _whole organization_, continuously
- **Example:** Bank builds live dashboards tracking approval speed, satisfaction, error rates **across all branches nationwide**, continuously tuning as new bottlenecks appear

### Business Process Model and Notation (BPMN)

- This one is different — it's not a _strategy_, it's a **visual/graphical language** for drawing and documenting workflows so business & technical teams understand each other
- **Example elements:** green circle = start event, swimlanes = separate each actor ("Customer," "Loan Officer," "Underwriting System"), diamond = decision gateway ("Is Credit Score > 700?"), red circle = end event

> [!tip] Quick way to tell them apart on a case study Ask yourself: _"Did they just look at the process (BPA)? Tweak it a bit (BPI)? Blow it up and start over (BPR)? Or is this an ongoing company-wide habit (BPM)?"_ If the question is about **drawing a diagram/flowchart with swimlanes and gateways**, that's **BPMN**, not a strategy question.

|Acronym|Full Name|Nature|Scope|
|---|---|---|---|
|BPA|Business Process Analysis|Diagnose only|One process|
|BPI|Business Process Improvement|Incremental fix|One process|
|BPR|Business Process Reengineering|Radical redesign|One process|
|BPM|Business Process Management|Continuous discipline|Whole org|
|BPMN|Business Process Model & Notation|Visual notation/tool|N/A (a language)|

---

## 4️⃣ BUSINESS ANALYTICS PROJECTS

This is the **longest and most detail-heavy** section — expect several quiz questions from here.

### 4.1 The Business Analytics Framework (Figure 25-1)

Three components that constantly feed into each other in a cycle:

- **Data** → Source, Storage, Management, Governance, Extraction
- **Analysis** → Transformations, Computations
- **Information Usage** → Delivery mechanism, Format, Adaptability

> [!tip] Think of it as a pipeline: **Data in → Analysis happens → Information goes out to people.**

### 4.2 The Business Analytics Spectrum (Descriptive → Prescriptive)

This is a **ladder from "look backward" to "tell me what to do"** — memorize the order, bottom to top, because this is a _very_ common exam structure (matching concept → example).

|Level (low→high)|Type|Concept|Slide Example|
|---|---|---|---|
|1. Standard reports about past data|**Descriptive**|Static, scheduled summary of what already happened|Monthly PDF Sales Report auto-sent on the 1st of each month|
|2. Ad hoc reports in real time|**On-Demand Querying**|One-off custom report answering a _sudden_ question _right now_|Marketing manager queries live cart data during a flash sale|
|3. Alerts when criteria are met|**Operational/Real-Time Alerts**|Automatic warning the _moment_ a threshold is breached|Inventory system SMS-alerts warehouse when stock < 20 units|
|4. Statistical analysis to detect patterns|**Diagnostic**|Stats (correlation, regression, clustering) to find _root causes_|Correlation shows Carrier B has 35% higher return rate due to box damage|
|5. Forecast models|**Predictive**|Uses history + algorithms to estimate the _future_|ML model predicts winter coat demand will rise 22%|
|6. What-if scenarios|**Scenario Analysis**|Simulate multiple _possible futures_ to compare before deciding|CFO compares "+15% shipping cost" vs "+8% storage cost" scenarios|
|7. Optimizations based on predictions|**Prescriptive**|System **automatically prescribes the single best action**|Logistics system auto-generates the most fuel-efficient routes each morning|

> [!important] The pattern you MUST remember **Descriptive = what happened. Diagnostic = why it happened. Predictive = what will happen. Prescriptive = what should we DO about it.** This 4-word chain is one of the most classic analytics exam questions of all time — expect it disguised as a case study.

### 4.3 Big Data

- Defined by **3 characteristics** (easy MCQ — memorize all three):
    - ==Large volume== (a lot of data exists)
    - ==High velocity== (data flows in rapidly)
    - ==Highly complex== (diverse types of data)
- Examples given: data from **GP, Facebook, YouTube, Google**
- If data objects relate to each other logically, you can model them using **Entity-Relationship Diagrams (ERDs)**

### 4.4 Big Data — Structure

Big data is often **NOT neatly organized**. Three categories:

- **Unstructured data** — e.g., voicemails, text messages. No rows/columns. The real challenge: _you don't even know where to begin looking for the information you need._
- **Semi-structured data** — e.g., emails. Has **metadata** (subject, to, content, attachment) that gives _some_ hint of structure, so you _can_ build ERDs and data dictionaries around what you know.
- (Structured data — rows/columns like a spreadsheet/database — is the implied "normal" case, contrasted against these two.)

> [!warning] Common confusion Don't mix up "unstructured" (no clue where to look — like a voicemail) with "semi-structured" (has some metadata hooks, like an email's subject/sender fields).

### 4.5 Information Usage by People

Three things a Business Analyst must think through when delivering info to end-users:

- **Delivery mechanism** — HOW does it physically reach the user? (email, portal, mobile app, etc.)
- **Format** — WHAT form is it in? (reports, dashboards, raw data)
- **Flexibility** — how much can the user **manipulate** the info after they receive it?

### 4.6 Data-Based Requirements

Four sub-categories of questions a BA must ask (this is a great "list the categories" MCQ target):

**Data sources**

- What data attributes are needed, and where do they come from?
- Do you already have access to those sources, or where's the data currently sitting?
- What external/internal systems provide the data? (slide example: SIM registration with NID)
- How likely is the source to change over time?
- Do you need to **migrate historical data** from an old system to a new one?

**Data storage**

- How much data exists _today_, and how much growth is expected — over what time period?
- What _types_ of data need storing?
- How long must it be retained, and how securely?

**Data management and governance**

- What's the structure of the data, and how might that structure/values change over time?
- What transformations are needed _before_ storing or analyzing raw data, and to standardize data coming from different systems?
- Under what conditions can old data be deleted / archived / destroyed?
- What **integrity requirements** protect the data from unauthorized access, loss, or corruption?

**Data extraction**

- How fast must queries return results?
- Do you need **real-time** or **batched** data — and if batched, at what frequency?
- ==Batch processing== needs _separate_ programs for input, process, and output (classic examples: **payroll** and **billing systems**)

### 4.7 Defining Analyses That Transform the Data (Past / Present / Future)

This is the **capstone framework** of the analytics section — expect this exact table format on the quiz.

|Time Frame|Analytics Type|Goal|Core Question|Slide Example|
|---|---|---|---|---|
|**Past**|Descriptive / Diagnostic|Understand _what_ happened and _why_|"Why did complaints rise 15% last quarter?"|Aggregates 12 months of transactions into a Customer Retention Dashboard → finds 70% of unhappy customers got a defective June batch|
|**Present**|Real-Time / Operational|Monitor _now_ to take _immediate_ action|"What's stuck right now?"|Warehouse dashboard refreshes every 60 sec, flags orders stuck >20 min → manager reassigns 3 workers immediately|
|**Future**|Predictive / Prescriptive|Forecast what _will_ happen and decide what to _do_|"How many units should we order?"|ML demand model recommends ordering 15% more headphones ahead of Black Friday|

> [!tip] Exam shortcut If a question mentions **"immediate action" / "right now" / "real-time refresh"** → it's **Present/Operational**. If it mentions **"root cause" / "why"** → **Past/Diagnostic**. If it mentions **"forecast" / "recommend ordering X amount"** → **Future/Predictive-Prescriptive**.

---

## 5️⃣ EMBEDDED AND OTHER REAL-TIME SYSTEMS PROJECTS

### 🔑 The Big Idea

These are systems where **timing is a hard requirement**, not just a "nice to have" — think elevators, medical devices, industrial control systems.

### System Architecture — 3 Elements (Figure 26-1 territory)

A system's architecture always consists of:

- ==Components== of the system — could be a **software object/module, a physical device, OR a person**
- ==Externally visible properties== of those components
- ==Connections== between the components

### Requirements Decomposition & Allocation (Figure 26-1)

**System Requirements** get broken down (_decomposition and derivation_) into three streams, and each is then _allocated_ to a specific owner:

```
System Requirements
   ├── Software Requirements → allocated to → Component A, Component B
   ├── Manual Requirements   → allocated to → People
   └── Hardware Requirements → allocated to → Component C, Component D
```

> [!important] Key takeaway Not everything becomes code! **Manual requirements get allocated to PEOPLE**, not software. This is a classic "which of these is allocated to hardware vs. software vs. people" MCQ setup.

### Timing Requirements — Core Definitions (memorize these three — very testable)

- **Predictability** — the **repeated, consistent** timing of a _recurring (periodic)_ event
    - _Example:_ "the system shall archive all data on the last day of every month" (it happens reliably, on schedule)
- **Execution time** — the elapsed time from when a task **starts** to when it **completes**
    - _Example:_ "the system shall archive all data every last day of the month **from 3–4 am**" (i.e., the archiving _takes_ that window to finish)
- **Latency** — the time lag between a **trigger event** occurring and the system **beginning to respond** to it

> [!warning] These three get mixed up constantly on quizzes
> 
> - **Predictability** = _does it happen on a reliable schedule?_
> - **Execution time** = _how long does the task itself take once it starts?_
> - **Latency** = _how long before the system even starts reacting to the trigger?_

### Timing & Scheduling Requirements — Full Checklist

This is a long "explore these issues" list from the slide — good for a "select all correct considerations" MCQ:

- ==Periodicity (frequency)== of task execution
- ==Deadlines and tolerances (float)== for each task's completion
- ==Typical vs. worst-case execution time== for each task
- Consequences of **missing a deadline**
- **Minimum, average, and maximum arrival rate** of data in each relevant system state
- Maximum time before the **first input/output** is expected after a task starts
- What happens if data isn't received in time (**timeout** handling)
- The **sequence** in which tasks must run
- Tasks that must **begin/end before** other tasks can begin
- **Task prioritization** — which tasks can interrupt/preempt others, and on what basis
- Functions that depend on the system's **current mode** (e.g., an elevator's _normal mode_ vs. _firefighter service mode_ — same hardware, totally different rules)

---

## 🧠 FULL CHAPTER CHEAT-SHEET (Fast Recall Table)

|Project Class|What Makes It Unique|Core Framework to Remember|
|---|---|---|
|**Packaged Solutions (COTS)**|Buy instead of build|OOTB → Configured → Integrated → Extended|
|**Outsourced**|Someone else builds it for you|Acquirer ↔ Supplier cycle; requirements = the cornerstone|
|**Business Process Automation**|Improving how work gets done|BPA (analyze) → BPI (tweak) → BPR (rebuild) → BPM (ongoing); BPMN = the diagram language|
|**Business Analytics**|Turning data into decisions|Data → Analysis → Info Usage; Descriptive → Diagnostic → Predictive → Prescriptive; Past/Present/Future|
|**Embedded/Real-Time Systems**|Timing is a hard requirement|Predictability, Execution time, Latency + full scheduling checklist|

---

## ✅ Fast Self-Quiz (cover the answers and test yourself)

1. What's the difference between "Configured" and "Integrated" COTS implementation? → _No code vs. some custom code to connect systems_
2. Name the 6 quality requirements for selecting a packaged solution. → _Performance, Usability, Modifiability, Interoperability, Integrity, Security_
3. What's the difference between BPI and BPR? → _Incremental fix to existing process vs. total clean-sheet redesign_
4. What does BPMN actually represent — a strategy or a tool? → _A visual notation/language, not a strategy_
5. Order the Business Analytics Spectrum from lowest to highest. → _Standard reports → Ad hoc → Alerts → Statistical analysis → Forecast models → What-if scenarios → Optimizations_
6. What are the 3 defining traits of Big Data? → _Volume, velocity, complexity_
7. Unstructured vs. semi-structured data — give an example of each. → _Voicemail (unstructured) vs. email (semi-structured, has metadata)_
8. What are the 3 components of a system's architecture? → _Components, externally visible properties, connections_
9. Difference between Latency and Execution Time? → _Latency = delay before response starts; Execution time = how long the task itself takes_
10. In Figure 26-1, what do Manual Requirements get allocated to? → _People, not hardware/software_

---

> [!success] You're ready If you can explain each row of the cheat-sheet table out loud without looking, and you can correctly slot a random scenario into OOTB/Configured/Integrated/Extended _or_ BPA/BPI/BPR/BPM _or_ Descriptive/Diagnostic/Predictive/Prescriptive — you're in great shape for the case study section too, since those are just this same content wrapped in a story.

**Source:** Wiegers, K., & Beatty, J. (2013). _Software Requirements_. Pearson Education.