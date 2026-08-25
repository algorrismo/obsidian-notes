# Case Study Prep: Change Control Process

### Requirements Engineering — Ch. 27/28 (Wiegers & Beatty)

Your quiz covers **one case study** built around 5 pillars. Think of these as 5 lenses you apply, in order, whenever a "someone wants a change" scenario is thrown at you. Below: what each one _means_, the keywords the examiner is listening for, and then 5 worked mini case studies so you can see the pattern repeat.

---

## 1. Change Control Policy

**Main theme (in plain words):** This is the _rulebook_ that a project agrees to _before_ any change ever shows up. It exists so that when someone (a client, a manager, a developer) asks for a change, nobody can just sneak it in informally. Everyone already knows the rules of the game.

Think of it like the constitution of your change process — it doesn't decide any _specific_ change, it just decides _how_ decisions about change will be made.

**The core rules (from your slides), explained simply:**

- No change is considered unless it's submitted through the formal process (no "hallway requests").
- No design/coding work happens on a change until it's _approved_ — only feasibility checking is allowed before that.
- Requesting ≠ getting. The **CCB decides**, not the requester.
- The change database (log of all requests) must be visible to everyone on the project — full transparency.
- **Impact analysis is mandatory** for every single change request.
- Every change that gets built must be traceable back to an approved request (so nobody can say "why did this even change?").
- The reasoning behind every approval/rejection must be written down (accountability).

**Keywords to remember:** _formal process, no work without approval, CCB decides, visibility/transparency, mandatory impact analysis, traceability, documented rationale._

---

## 2. Impact Analysis

**Main theme:** Before you say yes or no to a change, you must understand its _ripple effect_. A "small" change on paper (e.g., "add a payment option") can silently touch the UI, database, tests, documentation, schedule, and budget. Impact analysis is the _investigation phase_ — figuring out everything that change touches, and how much it will cost in time/money/risk.

**What gets analyzed (4 key dimensions — memorize this):**

1. **Scope Impact** — What features/components/SDKs/UI change?
2. **Schedule Impact** — How many extra days/weeks does it add?
3. **Cost Impact** — Extra budget, labor hours, licensing fees?
4. **Risk Impact** — What could go wrong (missed deadlines, quality drop, conflicts with other requirements)?

The slides also give a **worksheet** approach: list every task that might be touched (update SRS, modify design, write new code, write new tests, update docs, update traceability matrix...) and sum the hours — that becomes your effort estimate.

**Keywords:** _ripple effect, scope/schedule/cost/risk, effort estimation worksheet, traceability check, "will it conflict with existing requirements?", impact analysis template/report to CCB._

---

## 3. Change Control Board (CCB)

**Main theme:** The CCB is the **decision-making body** — a small group of representative stakeholders who look at the impact analysis and decide the fate of a change request. It's not one person's call; it's a _cross-functional committee_ so no single department can push through — or block — a change unilaterally.

**Who sits on it (composition):**

- Project/program management
- Business analyst / product management
- Development
- Testing/QA
- Marketing / business / customer reps
- Technical support / help desk

**How it makes decisions (the mechanics):**

- Defines a **quorum** — minimum number of members needed to make a valid decision.
- Has clear **decision rules** (e.g., majority vote, consensus).
- Decides whether the **Chair can overrule** the group.
- Decides whether a **higher authority must ratify** (approve) the CCB's decision.

**Keywords:** _cross-functional committee, representative stakeholders, quorum, decision rules, Chair authority, ratification, reviews impact analysis before deciding._

---

## 4. Decision Options

**Main theme:** After the CCB reviews the request + impact analysis, it must land on **one of three formal outcomes** (sometimes a 4th hybrid appears in practice). This is the "verdict" stage.

|Decision|Meaning|
|---|---|
|**Approved**|Change is accepted, baseline is updated, work begins/proceeds|
|**Rejected**|Change is declined outright; project continues unchanged; reason must be documented|
|**Deferred**|Not now — postponed to a later release/phase (e.g., "Phase 2")|
|**Approved with Conditions** _(seen in the CampBites example)_|A hybrid: approved, but tied to extra budget/time/scope constraints|

**Keywords:** _approved / rejected / deferred, baseline update, documented rationale, "not now" as a softer rejection, conditions attached to approval._

---

## 5. Agile Change Management

**Main theme:** Agile flips the traditional mindset. Instead of treating change as a _risk_ to control with heavy paperwork, Agile treats change as _expected and welcome_ — it's managed through the **backlog**, not a CCB.

**Key contrast to memorize (this is a classic exam table):**

|Dimension|Traditional (Waterfall)|Agile|
|---|---|---|
|Mindset|Change = risk/defect to minimize|Change = competitive advantage|
|Decision Authority|CCB|Product Owner (PO)|
|Primary Tool|Formal Change Request Form|Product Backlog & User Stories|
|Trade-off Model|Expands budget/scope/timeline|Swaps features within a fixed sprint|
|Timing|Ad-hoc or milestone gates|Built into every sprint planning cycle|

**Keywords:** _Product Owner (not CCB), Product Backlog, reprioritization, fixed timebox/sprint, swap instead of expand, no formal CR form needed._

---

## How These 5 Fit Together (the "story" of one change)

```
Request submitted → Impact Analysis (scope/schedule/cost/risk) 
    → CCB reviews it (using the change control policy rules) 
        → CCB issues a Decision (approved/rejected/deferred) 
            → (if Agile: PO + backlog instead of CCB, decision = reprioritize)
```

Almost every exam question is really asking: **"Given this scenario, walk through this pipeline and justify the outcome."**

---

## Worked Case Studies (5 examples with answers)

### 📌 Case Study 1 — The Late Feature Request (Traditional/Waterfall)

**Scenario:** A university library management system is in week 5 of 8. The client requests: "Add a barcode scanner integration for checking out books, instead of manual entry."

**Answer walkthrough:**

- **Policy check:** Client must submit a formal Change Request — no verbal promises acted on.
- **Impact Analysis:** Scope = new hardware SDK integration + UI rework; Schedule = +6 days; Cost = +$800 (SDK license); Risk = testing hardware compatibility across scanner models could slip further.
- **CCB Review:** PM, Dev Lead, QA rep, and client rep meet. Discuss whether missing the original deadline is worse than losing usability.
- **Decision:** **Approved with Conditions** — budget increased by $800, deadline extended 6 days, scanner testing added to QA plan.
- **Why not Agile lens here?** Waterfall project = fixed milestones, so this must go through full CCB flow, not just backlog reprioritization.

---

### 📌 Case Study 2 — The Rejected Request

**Scenario:** Midway through building a hospital appointment app, a nurse requests adding a live video-chat feature with doctors.

**Answer walkthrough:**

- **Impact Analysis:** Scope = massive (new video infrastructure, HIPAA/privacy compliance review, new UI); Schedule = +3 weeks; Cost = +$10,000; Risk = major — introduces regulatory/security risk close to launch.
- **CCB Review:** Sponsor, PM, Dev Lead, Compliance rep. Discussion centers on how this isn't a "tweak" — it's a new subsystem.
- **Decision:** **Rejected** (with the rationale documented: too large a risk/cost this close to release; could be reconsidered as a separate future project — not just "deferred" because it may need its own scoping cycle entirely).
- **Key teaching point:** Rejected ≠ ignored. The _reason_ must be written down and communicated to the requester (per the Change Control Policy rule on documented rationale).

---

### 📌 Case Study 3 — The Deferred Request

**Scenario:** A food-delivery app team is 2 weeks from launch. Marketing asks for a loyalty points system.

**Answer walkthrough:**

- **Impact Analysis:** Scope = new database schema for points, new UI screens; Schedule = +10 days (would blow the launch date); Cost = moderate; Risk = low technically, but high schedule risk.
- **CCB Review:** Team agrees the feature has merit but isn't launch-critical.
- **Decision:** **Deferred** to "Phase 2" (post-launch update) — this keeps the current baseline untouched and avoids delaying the release for a non-essential feature.
- **Key teaching point:** Deferred is the "yes, but not now" option — distinct from rejection because there's an implied future commitment.

---

### 📌 Case Study 4 — CampBites-style Mid-Project Request (the model example from your slides)

**Scenario:** In week 4 of a 6-week mobile ordering app project, the client requests adding Bkash/Nagad mobile wallet payment at checkout.

**Answer walkthrough (matches your slide's own example structure — good template to reuse):**

1. **Request:** Formal CR form filed by the client (not a phone call).
2. **Impact Analysis:** Scope = integrate 2 payment SDKs + redesign checkout UI; Schedule = +5 dev days + 2 QA days; Cost = +$1,500; Risk = 1-week delay might miss start-of-semester launch window.
3. **CCB Review:** Sponsor, PM, Tech Lead debate: "will missing week 1 of school hurt us?" vs. "70% of students use mobile wallets, so skipping it could hurt adoption more."
4. **Decision:** **Approved with Conditions** — budget +$1,500, deadline +4 days.
5. **Implementation:** WBS updated, SDKs coded, QA tests on iOS/Android.
6. **Re-baselining:** Requirements doc, schedule, and budget updated to v1.1; change logged as Closed/Implemented; stakeholders notified.

**Key teaching point:** This shows the **full 6-step lifecycle** end-to-end — the pattern examiners love to test because it touches all 5 pillars in one flow.

---

### 📌 Case Study 5 — The Agile Version (contrast scenario)

**Scenario:** Same CampBites-style request (add mobile wallet payments) — but now imagine the team is running 2-week Agile sprints instead of a fixed waterfall plan.

**Answer walkthrough:**

- **No CCB, no formal CR form.** The client's request goes straight to the **Product Owner**.
- The PO evaluates it as a new **user story**: _"As a student, I want to pay with Bkash/Nagad so that checkout is faster."_
- Instead of expanding the schedule/budget (like the CCB did), the PO **reprioritizes the backlog** — this story gets pulled into the _next sprint_, and a lower-priority story (e.g., "add order history filters") gets pushed out to keep the sprint timebox fixed.
- **Decision-style outcome:** Not "approved/rejected/deferred" in the formal CCB sense — instead it's simply _reprioritized_ into an upcoming sprint.
- **Key teaching point:** This is the exact contrast your Agile-vs-Traditional table is testing — Agile **swaps** work within a fixed timebox rather than **expanding** scope/schedule/cost like the CCB does.

---

## Quick Self-Check Before the Quiz

Ask yourself for any new case study they throw at you:

1. Is this **Waterfall or Agile**? (Decides who has authority — CCB vs. PO.)
2. What does the **Impact Analysis** reveal — scope, schedule, cost, risk?
3. What does the **Change Control Policy** require before any work starts?
4. Who sits on the **CCB**, and what's their reasoning in the discussion?
5. Which **Decision** fits — Approved / Rejected / Deferred / Approved with Conditions — and _why_?

If you can answer these five in order for any scenario, you can handle whatever variant shows up tomorrow.