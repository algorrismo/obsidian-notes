# 🎓 SRE Ch.01: The Essential Software Requirement — Master Study & Exam Guide
> **Course:** Software Requirement Engineering (CSC 4160)  
> **Source Material:** Chapter 01 Slide Deck (37 Slides)  
> **Exam Format:** 
> - **MCQ & True/False:** 50 Questions × 1 Mark = 50 Marks  
> - **Descriptive Questions:** 3 out of 6 Questions × 10 Marks = 30 Marks  
> **Target Audience:** Midterm Exam Candidates (Obsidian Ready)

---

## 🏛️ PART 1: FACULTY EXAM STRATEGY & COMMON STUDENT TRAPS

### 📌 How Examiners Grade SRE Exams
1. **Precision over Fluff:** In Software Requirement Engineering, mixing up terms like **User Requirement** and **Functional Requirement** or **Business Rule** and **Business Requirement** will result in **zero marks** for that section.
2. **Key Keywords Required for Full Marks:**
   - **Business Requirement:** Must mention *business objectives, metrics, ROI, why the system is built*.
   - **User Requirement:** Must mention *tasks/goals users perform, Use Cases, User Stories*.
   - **Functional Requirement:** Must mention *system behavior under specific conditions, "shall" statements*.
   - **Business Rules:** Must mention *policies, regulations, standards, algorithms external to software*.
   - **Baselined Requirements:** Must mention *agreed-upon baseline, boundary between Development and Management, formal change control*.
3. **Common Student Mistakes to Avoid:**
   - ❌ **Mistake 1:** Calling a Business Rule a Functional Requirement. (A business rule exists *outside* the system; a functional requirement is what the system *does* to enforce that rule).
   - ❌ **Mistake 2:** Including project deadlines or team staffing in the SRS. (SRS contains *Product Requirements*, NOT *Project Requirements*).
   - ❌ **Mistake 3:** Believing Validation happens only after coding. (Requirements Validation happens during Requirements Development on the SRS before coding begins!).
   - ❌ **Mistake 4:** Thinking Agile eliminates requirements. (Agile distributes requirements effort over time/sprints; Waterfall concentrates it upfront).

---

## 📚 PART 2: COMPREHENSIVE TOPIC-BY-TOPIC STUDY GUIDE

---

### Topic 1: Software Requirements - What, Why, & Current Problems (Slides 1–7, 32–34)

#### 1. Core Summary
* **Why SRE Matters:** The hardest part of building software is deciding *precisely what to build*. Rectifying requirements errors in maintenance is **up to 200 times** more expensive than fixing them during requirements time.
* **Humor vs. Reality (Tree Swing):** Illustrates miscommunication across stakeholders (Customer, Analyst, Developer, Business Consultant, Operations).
* **Top Causes of Project Failures (Standish Group Data):**
  1. Lack of user input (13%)
  2. Incomplete requirements & specifications (12%)
  3. Changing requirements & specifications (12%)
* **Top Factors for Project Success:**
  1. User involvement (16%)
  2. Executive management support (14%)
  3. Clear statement of requirements (12%)
* **The Leakage Problem:**
  - **74%** of defects are found during Requirements Analysis (cheapest to fix).
  - **4%** leak into High-Level Design.
  - **7%** leak into Detailed Design.
  - **4%** leak all the way into Maintenance (most expensive!).
* **Reasons Behind Bad Requirements:** Insufficient user involvement, inaccurate planning, scope creep (creeping requirements), ambiguity, gold plating (adding unrequested extra features), and overlooked stakeholders.

#### 2. Faculty Notes & Mistakes
> **Examiner Trap:** Watch out for percentage questions in MCQs! Know the relative cost ratio (**200:1**) from Requirements phase to Maintenance phase.

#### 3. MCQ & True/False Questions
* **MCQ 1:** According to industry studies, what percentage of requirements-oriented defects are ideally discovered during the requirements analysis phase?
  - A) 12%
  - B) 50%
  - C) 74% ✅
  - D) 90%
* **T/F 1:** Adding extra unrequested functionality to a product is called scope creep.
  - *Answer:* **False** (It is called **Gold Plating**).

---

### Topic 2: Requirement Definition & Time Dimension (Slide 8)

#### 1. Core Summary
* **Definition:** A requirement is a **property that a product must have to provide value to a stakeholder**. It specifies what should be implemented, system properties/attributes, behavior, or constraints.
* **Two Perspectives:**
  1. **User's View:** External system behavior.
  2. **Developer's View:** Internal characteristics.
* **Time Dimension of Requirements:**
  - **Present Tense:** Current system capabilities.
  - **Near-term / Hypothetical Future:** High-priority or planned features.
  - **Past Tense:** Needs that were once specified and later discarded.

#### 2. MCQ & True/False Questions
* **MCQ:** Which of the following views focuses on external system behavior?
  - A) Developer's view
  - B) User's view ✅
  - C) Architecture view
  - D) Database view
* **T/F:** Software requirements only refer to future capabilities of a system.
  - *Answer:* **False** (They include present capabilities, future expectations, and past discarded requirements).

---

### Topic 3: The Three Levels of Requirements & System Requirements (Slides 9–15)

#### 1. Core Summary
Software requirements are structured in **3 Distinct Levels**:

| Requirement Level | Definition | Focus / Driven By | Format / Artifact | Example |
| :--- | :--- | :--- | :--- | :--- |
| **Business Requirements (BR)** | High-level business objectives & benefits the organization hopes to achieve. | Executive Sponsor, Management, Marketing | Vision & Scope Document | *"Reduce airport counter staff costs by 25%."* |
| **User Requirements (UR)** | Goals/tasks users must be able to perform with the product. | Real Users, User Representatives | Use Cases, User Stories | *"As a passenger, I want to check in online so I can board."* |
| **Functional Requirements (FR)** | Specific software behaviors the system must exhibit under given conditions. | Developers, Analysts, Testers | SRS ("Shall" Statements) | *"The system shall print boarding passes upon successful check-in."* |

* **Hierarchy Alignment:**  
  $$\text{Business Goal (BR)} \longrightarrow \text{User Need (UR)} \longrightarrow \text{Functional Behavior (FR)}$$
* **Constraints:** Restrictions imposed on design/construction choices (e.g., *"The system shall run on Linux OS"*).
* **System Requirements:** Requirements for a product composed of **multiple subsystems** (software, hardware, people, processes). Example: Supermarket cashier workstation (barcode scanner + scale + screen + cashier person).

#### 2. Faculty Notes & Mistakes
> **Crucial Distinction:** 
> - **Use Cases & User Stories** represent **User Requirements**.
> - **"Shall" statements** represent **Functional Requirements**.
> - **Quantitative Business Goals (e.g., % increase/decrease)** represent **Business Requirements**.

#### 3. MCQ & True/False Questions
* **MCQ:** "The system shall encrypt all user passwords using AES-256." What level/type of requirement is this?
  - A) Business Requirement
  - B) User Requirement
  - C) Functional Requirement / Constraint ✅
  - D) Project Requirement
* **T/F:** Use cases and user stories are primary representations of Functional Requirements.
  - *Answer:* **False** (They represent **User Requirements**; Functional Requirements are derived from them).

---

### Topic 4: Non-Functional Requirements (NFRs) (Slide 16)

#### 1. Core Summary
* **Definition:** Also known as **Quality Attributes** or product requirements describing a service/performance characteristic (*"-ities"* and *"-ilities"*).
* **Key Categories:**
  - **Quality Attributes:** Performance, safety, availability, portability, reliability, usability.
  - **External Interfaces:** Connections between system and external software, hardware, or communication protocols (interoperability).
  - **Design & Implementation Constraints:** Restrictions on architectural choices, frameworks, security policies.
* **Conflict Property:** NFRs frequently conflict with one another (e.g., high security can reduce usability; high portability may impact peak performance).

#### 2. Faculty Notes & Mistakes
> **Student Error:** Confusing Functional vs. Non-Functional. Functional = *WHAT system does*. Non-Functional = *HOW WELL or under what constraints the system performs*.

#### 3. MCQ & True/False Questions
* **MCQ:** Quality attributes like availability, performance, and portability belong to which class of requirements?
  - A) Business Requirements
  - B) Functional Requirements
  - C) Non-Functional Requirements ✅
  - D) Project Requirements
* **T/F:** Non-functional requirements rarely conflict with one another.
  - *Answer:* **False** (Chances of conflicts among non-functional requirements are fairly high).

---

### Topic 5: Business Rules & Features (Slides 17–18)

#### 1. Core Summary
* **Business Rules:** Corporate policies, government regulations, industry standards, and algorithms.
  - **CRITICAL FACT:** Business rules are **NOT** software requirements themselves because they exist **outside and independent of** any software application.
  - Business rules **originate** or dictate functional requirements and quality attributes.
  - *Example:* Bank policy limit of $1,000 ATM withdrawal/day is a Business Rule. The software code checking `if withdrawal > 1000` is the Functional Requirement.
* **Features:** A feature consists of one or more logically related system capabilities that provide value to a user and are described by a set of functional requirements.
  - A feature encompasses multiple user requirements.

#### 2. MCQ & True/False Questions
* **MCQ:** Which statement regarding Business Rules is TRUE?
  - A) Business rules are software requirements stored in the SRS.
  - B) Business rules exist independently of any software application. ✅
  - C) Business rules are written using "shall" statements.
  - D) Business rules are created by software developers.
* **T/F:** A feature is a single functional requirement.
  - *Answer:* **False** (A feature consists of a group of logically related capabilities described by *multiple* functional requirements).

---

### Topic 6: Relationships Among Requirements Artifacts (Slide 19)

#### 1. Core Summary
* **Relationships Map (Wiegers Framework):**
  - **Business Rules** $\rightarrow$ influence Business Requirements, User Requirements, Functional Requirements, Quality Attributes.
  - **Vision & Scope Document** $\rightarrow$ stores Business Requirements.
  - **User Requirements Document** $\rightarrow$ stores User Requirements.
  - **Software Requirements Specification (SRS)** $\rightarrow$ stores Functional Requirements, System Requirements, External Interfaces, Quality Attributes, and Constraints.

---

### Topic 7: Product vs. Project Requirements (Slides 20–21)

#### 1. Core Summary
* **Product Requirements:** Describe properties of the software system to be built. Stored in the **SRS**.
* **Project Requirements:** Activities, deliverables, and expectations necessary for successful project execution but **NOT** part of the software product itself.
* **Items included in Project Requirements:**
  - Physical resources (workstations, testing labs, equipment).
  - Staff training & user documentation.
  - Infrastructure changes.
  - Release, installation, & deployment procedures.
  - Beta testing, packaging, marketing, legal protection (patents/copyrights).
* **GOLDEN RULE FOR SRS:** The SRS must house **product requirements ONLY**. It must **NEVER** contain project plans, test plans, or implementation details.

#### 2. MCQ & True/False Questions
* **MCQ:** Which of the following should be included in a Software Requirements Specification (SRS)?
  - A) Developer hardware workstation allocations
  - B) User training schedules
  - C) System quality attributes and functional behaviors ✅
  - D) Patent legal registration deadlines
* **T/F:** Staff training materials and testing lab equipment are examples of Product Requirements.
  - *Answer:* **False** (They are **Project Requirements**).

---

### Topic 8: Requirements Engineering, Development & Management (Slides 22–31)

#### 1. Subdiscipline Structure
$$\text{Requirements Engineering} = \text{Requirements Development} + \text{Requirements Management}$$

#### 2. Requirements Development (4 Phases)
1. **Elicitation:** Discovering needs by identifying user classes, understanding user tasks/goals, and interviewing user representatives.
2. **Analysis:** Modeling the environment, decomposing high-level requirements, allocating requirements to architecture, and negotiating priorities.
3. **Specification:** Documenting requirements into a formal **SRS** using standard templates, unique labeling, and diagrams.
4. **Validation:** Reviewing the SRS to ensure requirements are **feasible, consistent, and complete**, and creating acceptance test cases.
   - *Consistency:* No contradictory requirements.
   - *Completeness:* No missing services or constraints.

#### 3. Requirements Management
- Establishing change control processes.
- Performing impact analysis on proposed changes.
- Tracking requirement status & issues.
- Maintaining requirements traceability matrix (RTM).
- Tracing requirements to design, code, and test cases.

#### 4. The Boundary: Baselined Requirements (Slide 30)
* **What is a Baseline?** A snapshot of agreed-upon requirements (SRS) for a specific release/iteration.
* **Boundary Function:** **Baselined Requirements** serve as the explicit boundary dividing Requirements Development and Requirements Management.
  - *Before Baseline:* Requirements are in **Development** (drafting, analyzing, revising).
  - *After Baseline:* Requirements enter **Management** (change control, impact analysis, versioning).

#### 5. Distribution of Effort Over Time (Slide 31)
* **Waterfall Model:** High single peak of requirements effort concentrated upfront.
* **Iterative / Agile Model:** Requirements effort distributed across multiple smaller peaks throughout cycles/timeboxes.

---

## 📝 PART 3: SOLVED CLASS TASKS (SLIDES 35 & 36)

### Task 1: Classify Requirement Statements (Slide 35)

| Requirement Statement | Correct Requirement Type | Faculty Rationale |
| :--- | :--- | :--- |
| *Increase online sales by 25% within one year.* | **Business Requirement** | Measurable financial/business objective. |
| *Customers should be able to search products by category.* | **User Requirement** | User goal/task capability. |
| *The system shall allow users to filter products by price range.* | **Functional Requirement** | Detailed system behavior ("shall" statement). |
| *Reduce customer service calls by 30%.* | **Business Requirement** | Business cost-reduction objective. |
| *Customers should be able to track order status.* | **User Requirement** | High-level user task. |
| *The system shall send an email when an order is shipped.* | **Functional Requirement** | Automated system response under specific conditions. |

---

### Task 2: Requirement Level Hierarchy Breakdown (Slide 36)

**Business Goal:** *"Reduce patient waiting time in a hospital."*

* **Business Requirement (BR):** Reduce patient wait times by 40% within 6 months.
* **User Requirement (UR):** Patients should be able to view current wait times and book appointments online.
* **Functional Requirement 1 (FR-1):** The system shall calculate and display real-time estimated queue waiting times on the mobile app.
* **Functional Requirement 2 (FR-2):** The system shall send an SMS notification to the patient 15 minutes before their scheduled appointment slot.
* **Functional Requirement 3 (FR-3):** The system shall allow front-desk staff to reassign patients to available doctors dynamically.

---

## 🎯 PART 4: EXPECTED DESCRIPTIVE EXAM QUESTIONS & STANDARD ANSWERS
*(3 out of 6 Questions × 10 Marks = 30 Marks)*

---

### Question 1: Requirement Levels & Hierarchy with Examples (10 Marks)
> **Question:** Explain the three distinct levels of software requirements. Provide a practical example illustrating how a single business goal cascades down to user and functional requirements.

#### Model 10/10 Answer:
1. **Introduction & Definitions (3 Marks):**
   - **Business Requirements (BR):** Represent high-level business goals, target metrics, or financial benefits desired by the sponsoring organization. (Stored in Vision & Scope Document).
   - **User Requirements (UR):** Describe specific tasks or goals users must perform using the system to achieve value. (Represented as Use Cases / User Stories).
   - **Functional Requirements (FR):** Define specific software behaviors, inputs, and output responses under exact conditions. (Written as "shall" statements in the SRS).

2. **Alignment Hierarchy Diagram (2 Marks):**
   $$\text{Business Goal (Why)} \xrightarrow{\quad\quad} \text{User Task (Who/What)} \xrightarrow{\quad\quad} \text{System Behavior (How system reacts)}$$

3. **Cascading Example (5 Marks):**
   - **Context:** E-Commerce Food Delivery Platform.
   - **Business Requirement (BR-1):** Increase food delivery order volume by 30% within 12 months.
   - **User Requirement (UR-1):** Customers should be able to track the real-time location of their food delivery on a map.
   - **Functional Requirement (FR-1.1):** The system shall update the delivery driver’s GPS coordinates on the customer map view every 10 seconds.
   - **Functional Requirement (FR-1.2):** The system shall send a push notification when the driver is within 100 meters of the delivery destination.

---

### Question 2: Requirements Development vs. Requirements Management & The Baseline Boundary (10 Marks)
> **Question:** Differentiate between Requirements Development and Requirements Management. Explain the concept of "Baselined Requirements" and how it acts as the boundary between these two subdisciplines.

#### Model 10/10 Answer:
1. **Definitions & Differences (4 Marks):**
   - **Requirements Engineering** consists of two complementary subdisciplines: Development and Management.
   - **Requirements Development:** The process of discovering, analyzing, specifying, and validating requirements. It consists of 4 phases: Elicitation, Analysis, Specification, and Validation.
   - **Requirements Management:** The set of activities for establishing change control, managing versioning, conducting impact analysis, and tracking traceability after requirements are defined.

2. **Comparison Table (2 Marks):**

| Aspect | Requirements Development | Requirements Management |
| :--- | :--- | :--- |
| **Primary Focus** | Creating and defining requirements. | Controlling changes and maintaining integrity. |
| **Key Activities** | Elicitation, Analysis, SRS writing, Validation. | Change control, Impact analysis, Traceability (RTM). |
| **Timeline** | Active before baseline approval. | Active after baseline approval across lifecycle. |

3. **The Baselined Requirements Boundary (4 Marks):**
   - A **Requirement Baseline** is an agreed-upon, reviewed set of requirements (SRS) frozen at a specific milestone.
   - **Role as Boundary:**
     - Prior to baselining, proposed requirements are fluid and undergo iterative refinement within **Requirements Development**.
     - Once the SRS is formally reviewed and signed off by stakeholders, it becomes the **Current Baseline**.
     - Beyond this point, any new request enters **Requirements Management**, requiring formal change request submission, impact analysis, and approval before creating a **Revised Baseline**.

---

### Question 3: Phases of Requirements Development (10 Marks)
> **Question:** Detail the four phases of Requirements Development. Discuss how iteration occurs among these phases.

#### Model 10/10 Answer:
1. **The 4 Phases (6 Marks):**
   - **1. Elicitation:** Gathering raw user needs by identifying user classes, conducting interviews, workshops, and reviewing existing domain processes.
   - **2. Analysis:** Processing raw input to decompose high-level needs, build environment models, resolve conflicts, and negotiate feature priorities.
   - **3. Specification:** Translating analyzed requirements into structured, unambiguous documentation (SRS) using standard templates, visual diagrams, and unique identifiers.
   - **4. Validation:** Rigorously evaluating the SRS with stakeholders to ensure correctness, completeness, consistency, and feasibility before development starts.

2. **Iterative Process Framework & Feedback Loops (4 Marks):**
   - Requirements development is **inherently iterative**, not strictly linear.
   - **Feedback Loops:**
     - *Analysis $\rightarrow$ Elicitation:* Analysis reveals missing information, requiring further elicitation to **clarify**.
     - *Specification $\rightarrow$ Analysis:* Writing detailed specs uncovers logical gaps, requiring re-analysis to **close gaps**.
     - *Validation $\rightarrow$ Specification/Analysis:* Validation reviews detect errors/contradictions, requiring spec **rewriting** or requirement **re-evaluation**.

---

### Question 4: Non-Functional Requirements, Quality Attributes & Constraints (10 Marks)
> **Question:** Define Non-Functional Requirements (NFRs). Explain the difference between quality attributes and constraints, and explain why NFRs often conflict with each other.

#### Model 10/10 Answer:
1. **Definition of NFRs (3 Marks):**
   - NFRs (Quality Attributes) specify *how well* the system performs its functions, rather than what functions it performs. They describe performance, reliability, security, and operational attributes.

2. **Quality Attributes vs. Constraints (3 Marks):**
   - **Quality Attributes:** Desirable system characteristics measured along a spectrum (e.g., system response time $< 2$ seconds, 99.9% uptime).
   - **Design/Implementation Constraints:** Absolute restrictions placed on developer options during design or construction (e.g., system must run on Docker containers, must use Postgres DB).

3. **Why NFRs Conflict (4 Marks):**
   - NFRs operate in trade-off spaces where enhancing one attribute negatively impacts another.
   - **Examples:**
     - *Security vs. Usability:* Requiring multi-factor authentication (MFA) and frequent password renewals increases security but lowers user convenience/usability.
     - *Performance vs. Portability:* Writing code in low-level platform-specific C++ maximizes speed/performance but destroys multi-platform portability.

---

### Question 5: Product Requirements vs. Project Requirements & SRS Scope (10 Marks)
> **Question:** Differentiate clearly between Product Requirements and Project Requirements. What items belong in an SRS, and what items must be strictly excluded?

#### Model 10/10 Answer:
1. **Core Distinction (4 Marks):**
   - **Product Requirements:** Define capabilities, behaviors, constraints, and quality attributes of the software system being delivered.
   - **Project Requirements:** Describe the operational environment, resources, training, schedules, and administrative activities needed to successfully complete the software development project.

2. **Classification Table (3 Marks):**

| Item | Requirement Category |
| :--- | :--- |
| System response time under 1 sec | Product Requirement (SRS) |
| Purchase of 10 test mobile devices | Project Requirement (Excluded from SRS) |
| User password encryption algorithm | Product Requirement (SRS) |
| Developer team training on React.js | Project Requirement (Excluded from SRS) |

3. **Strict SRS Scope Guidelines (3 Marks):**
   - **Included in SRS:** Functional requirements, non-functional requirements, external system interfaces, design constraints, business rule implementations.
   - **Excluded from SRS:** Project schedules, budget allocations, testing plans, developer assignments, code design patterns, and legal patent filings.

---

### Question 6: Business Rules vs. Functional Requirements (10 Marks)
> **Question:** "Business rules are not software requirements." Evaluate this statement. Explain how business rules originate functional requirements with concrete examples.

#### Model 10/10 Answer:
1. **Statement Evaluation (4 Marks):**
   - **True.** Business rules exist **externally and independently** of any software system. They represent real-world corporate policies, government legislation, industry standards, or mathematical algorithms.
   - A business rule exists whether software is built or not (e.g., tax laws exist even if done on paper).

2. **Relationship & Derivation (3 Marks):**
   - Software systems are built to **enforce** or **comply with** business rules.
   - Therefore, a single business rule can be the **origin** of multiple functional requirements and quality constraints.

3. **Concrete Practical Examples (3 Marks):**
   - **Business Rule:** *"Government Regulation: Customers under 18 years old cannot purchase alcoholic products."*
   - **Derived Functional Requirement 1:** The system shall require users to input their date of birth during checkout when cart contains alcoholic items.
   - **Derived Functional Requirement 2:** The system shall prevent payment processing and display an error message if the calculated user age is under 18.
