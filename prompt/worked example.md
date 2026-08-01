Tags : #prompt 
date : 2026-07-05

---

To get the AI to act as a proper mentor rather than a copy-paste machine, you need to use a prompt that explicitly restricts it from writing the final code right away and forces it to focus on the algorithmic steps.

Here is a template you can use whenever you are stuck on a problem:

### The "Worked Example" Prompt Template

> "I am working on the following problem: **[Insert Problem Description/Link Here]**.
> 
> Do **not** give me the final, completed code solution. Instead, provide a **worked example** by breaking down the logic into a clear, step-by-step sequence.
> 
> Walk me through the conceptual steps, the data structures I should use, and the logic required to transition from one step to the next. Explain it like a math problem where each step builds on the last, keeping the cognitive load minimal so I can understand the pattern."

### Why This Works (The Logic)

- **"Do not give me the final code":** This is a hard constraint. It stops the LLM from doing the lazy thing (generating a block of code you'll just copy) and forces it to act like a tutor.
    
- **"Step-by-step sequence":** This ensures the AI breaks down the problem into small, digestible chunks so your working memory doesn't get overloaded.
    
- **"Transition from one step to the next":** This helps your brain build a logical chain of association, making the pattern much easier to retain and apply to future problems.
    

When the AI gives you the steps, read through them, map out the logic in your head (or on paper), and then **write the code yourself** based on those steps. If you get stuck on a specific step, only then ask it to expand on that single part.
