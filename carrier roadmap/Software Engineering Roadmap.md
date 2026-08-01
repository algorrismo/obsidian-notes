Tags : #carrier
date : 2026-07-14

---
# Your 7-Month Software Engineering Roadmap

### (Written like a senior dev explaining it to a friend, step by step)

---

## Before we start — a few simple words explained

- **Backend** = the part of an app the user doesn't see. It handles data, logins, saving information, etc.
- **Frontend** = the part the user sees and clicks on (buttons, pages, design).
- **API** = a way for the frontend and backend to "talk" to each other. Like a waiter taking your order (frontend) to the kitchen (backend) and bringing food back.
- **Database** = where all the information is stored permanently (like user accounts, posts, orders).
- **DSA (Data Structures & Algorithms)** = the "logic puzzles" companies ask in interviews. It trains your brain to solve problems efficiently.
- **Deploy / Deployment** = putting your project on the internet so anyone can open it with a link, not just on your own laptop.
- **Git/GitHub** = a tool to save versions of your code and show your work to companies.

You don't need to memorize these now. Just come back here whenever a word confuses you.

---

## MONTH 1–2: Finish Frontend + Learn Backend Basics

### Step 1: Finish your current frontend course

Keep going with what you're already learning (React, JWT, login systems). Don't stop halfway. Finish it fully, even the boring parts.

### Step 2: Pick ONE backend language — my recommendation: **Node.js**

Why Node.js and not something else? Because you already know JavaScript (from frontend). Node.js lets you use the _same language_ for backend. This means you learn less new stuff and go faster.

**What to learn in Node.js (in this exact order):**

1. What Node.js actually is (just watch one 20-minute explainer video, don't overthink it)
2. **Express.js** — a tool that makes it easy to build APIs with Node. Learn:
    - How to create a simple server (a program that "listens" for requests from users)
    - How to create routes (basically: "when someone visits /login, do this")
    - How to read data sent from the frontend (called "request body")
3. **Databases** — learn ONE of these:
    - **PostgreSQL** (recommended — most companies use it, and it's good to learn "real" databases)
    - Learn: what a table is, what a row/column is, how to write basic queries (SELECT, INSERT, UPDATE, DELETE — these are just commands to get/add/change/remove data)
4. **Prisma** (a tool that lets you talk to your database using simple JavaScript instead of complicated database language) — learn this after you understand basic database queries, not before. Understanding the manual way first will make you much stronger than students who skip straight to the shortcut tool.
5. **Authentication (you already started this with JWT — good!)**
    - Learn how to store passwords SAFELY (never store plain passwords — always "hash" them using a tool called bcrypt)
    - Learn "role-based access" fully (e.g., admin vs normal user — you mentioned you're already doing this, so just go deeper)

### Step 3: Build your first real backend project

Don't build a to-do list app — everyone does that and it won't impress anyone. Instead build ONE of these:

- A small **booking system** (like booking a doctor's appointment)
- A small **e-commerce backend** (products, cart, orders, admin panel)

It should have: login/signup, different user roles (admin/customer), and a database saving everything.

**Daily time needed:** 2–3 hours a day is enough if consistent.

---

## MONTH 3: Start DSA (Problem-Solving Training) + Git

### Why start DSA now and not later?

Because DSA takes months to get comfortable with. If you start in month 6, you'll panic. Starting now means by interview time, it feels normal, not scary.

### Step 1: Learn Git and GitHub properly (takes about 1 week)

This is just a tool to save your code's history and show it online. Learn:

- How to save your code changes (called a "commit")
- How to upload your project online (called "push")
- How to make a copy of someone else's project to practice (called "fork" or "clone")

You don't need to be an expert. Just comfortable enough to use it daily.

### Step 2: DSA — Start with the basics, 1 hour a day, no exceptions

Learn in this order (don't jump ahead):

1. **Arrays** — a list of items, like a row of boxes
2. **Strings** — basically text, and how to manipulate/search within text
3. **Hashmaps / Hash tables** — a super-fast way to look things up (like a phonebook: name → number)
4. **Recursion** — a function that calls itself to solve a problem step by step (confusing at first, gets easier with practice — don't panic if it feels hard)
5. **Basic Trees** — data organized like a family tree (used a lot in real systems)
6. **Basic Graphs** — data organized like a map of connections (like how Facebook friends are connected)

**Where to practice:** LeetCode (search "Easy" difficulty problems first). Do NOT jump to "Medium" until you've solved at least 40-50 Easy problems comfortably.

**Golden rule:** If you get stuck on a problem for more than 25-30 minutes, look at the solution, understand it fully, then try to write it yourself without looking. This is normal — even senior developers do this when learning something new.

---

## MONTH 4: One Big Impressive Project

### Why one BIG project instead of many small ones?

Companies care more about ONE well-built project than five half-finished ones. It shows you can actually finish things — a rare and valuable skill.

### What to include (pick features that make sense for your project idea):

- Full login system (you already know this)
- A real feature that solves a real problem (not just "practice" — think of something people would actually use)
- **File uploads** (e.g., users can upload a profile picture or a document)
- **Payments** — use Stripe's "test mode" (it's free, lets you simulate real payments without needing actual money)
- **Email notifications** (e.g., "Your order was placed" email) — there are simple free tools for this (like Nodemailer or Resend)

### Step: Deploy it (put it on the internet)

Use free/cheap tools like:

- **Vercel** or **Render** or **Railway** — these let you upload your project and get a real link, like `myproject.vercel.app`
- Connect a database that's hosted online too (many of these tools give you a free database)

This matters A LOT. A project only on your laptop is invisible to companies. A project with a real link they can click is proof you can build real things.

---

## MONTH 5: More DSA (Medium level) + System Design Basics

### DSA — Step up to "Medium" difficulty problems

By now, Easy problems should feel manageable. Move to Medium problems on LeetCode. Keep doing 1 hour daily — consistency matters way more than doing 5 hours once a week.

### System Design — just the basics, don't overwhelm yourself

This is about understanding how big apps (like Facebook, Instagram) are built behind the scenes. You don't need to be an expert — just understand the IDEAS:

1. **Caching** = saving frequently-used data somewhere super fast so the app doesn't have to look it up from scratch every time (like keeping your most-used books on your desk instead of the library)
2. **Load balancing** = spreading traffic across multiple servers so one server doesn't get overwhelmed (like having multiple checkout counters at a supermarket instead of one)
3. **Database scaling** = what happens when a database gets too big or too busy, and simple ways to handle that
4. **Message queues** = a way for different parts of a system to send tasks to each other without waiting (like leaving a note for someone instead of waiting for them to be free right now)

Just watch a few good YouTube explainer videos on these — you don't need to build these yourself yet. Just understand what they mean and why they exist, because interviewers will ask about them even for junior/intern roles sometimes.

---

## MONTH 6: Resume, Portfolio, Open Source, Practice Interviews

### Step 1: Fix your resume

- Don't just list "I know JavaScript, Node.js, React"
- Instead say what you BUILT: "Built a booking system backend handling user roles, authentication, and payments, deployed live at [link]"
- Numbers help: "Reduced page load time by X%" or "Handled X number of test users" (even rough estimates are fine if honest)

### Step 2: Contribute to open source (helps a LOT for internships)

Open source = public projects on GitHub that anyone can help improve.

- Find small, beginner-friendly issues labeled "good first issue" on GitHub
- Fix something small — even fixing a typo in documentation counts as a start
- This shows companies you can work with other people's code, which is a real job skill

### Step 3: Start applying — don't wait to feel "ready"

You will never feel 100% ready. Nobody does. Apply to internships now, even if you feel unprepared. Internships are looking for potential, not perfection.

### Step 4: Practice interviews with a friend or classmate

Ask each other questions like:

- "Tell me about a project you built"
- "What was the hardest bug you fixed?"
- Practice explaining your project out loud — this feels awkward at first but gets much easier with practice

---

## MONTH 7: Final Push — Applications + Interview Prep

### Daily plan for this month:

- **Morning:** 1 hour DSA revision (go back to Easy/Medium problems you've already solved to keep them fresh)
- **Afternoon:** Apply to jobs/internships (aim for at least 3-5 applications a day, don't just apply to 2 dream companies and wait)
- **Evening:** Read about common interview questions for your target companies, practice explaining your projects clearly

### Where to apply:

- Local companies in Bangladesh (good for first experience, understand your market)
- Remote-friendly international companies (often pay significantly more — worth trying even if it feels like a long shot)

---

## Quick Reference: What "Good Enough" Looks Like at Each Stage

|Month|You should be able to...|
|---|---|
|2|Build a simple API with login and a database|
|3|Solve Easy DSA problems in 15-20 min, use Git comfortably|
|4|Have one deployed, full-featured project with a real link|
|5|Solve Medium DSA problems, explain caching/load balancing in simple words|
|6|Have a clean resume, one open-source contribution, applications going out|
|7|Be actively interviewing, confident explaining your projects|

---

## A note from me (not as a mentor, just honestly)

You already know more than you think — frontend, JWT, role-based login. Most students your year haven't touched auth systems properly. The confusion you're feeling right now is completely normal for someone at this stage; it's not a sign you're behind, it's a sign you're paying attention to how big the field is.

Go one month at a time. Don't look at the whole 7-month list and panic — just focus on what Month 1-2 needs from you today.

You've got this, Inshallah.