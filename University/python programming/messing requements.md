Tags : #python 
Date : 2026-07-13

---

## ✅ What you've done correctly

- **Variables & data types** — category, amount, dates stored properly
- **Branching** — `if/elif/else` used for menu logic and validation
- **Loops** — `while True` loops for repeated menu input
- **Dictionary** — `expenses = {"food": 0, ...}` is a real, working use of a dict
- **Basic exception handling** — `try/except ValueError` catches non-numeric input in two places
- **Functions** — logic is split into `addExpnese()`, `updateExpense()`, `viewExpenseDetailes()`, `saveExpense()`
- **File saving** — `saveExpense()` writes formatted records to `data/expenses.txt`
- **FR-1 user interaction** — menu-driven interaction is present and is explicitly allowed by the brief

## ❌ What's missing or doesn't match the requirement

**Data structures (Section 3 + 6 marks in rubric)**

- No **list** anywhere in the code
- No **tuple** anywhere in the code
- No **set** anywhere in the code
- Only the dictionary is used — 3 of 4 required data structures are absent

**OOP (Section 3 + 6 marks)**

- Zero `class` definitions in the whole project
- Brief requires _"at least one meaningful class"_ representing a real entity (e.g. `Expense`) — this is completely missing

**Approved library / module (Section 1, 5, 11 — 5 marks)**

- No `numpy`, `pygame`, or `tkinter` imported anywhere
- This is a **hard requirement** — the project cannot pass without one of these being used purposefully

**Persistent data (FR-3)**

- There is **no load function** — data is never read back from a file
- Every time the program runs, `expenses` resets to all zeros
- Your brief states directly: _"A project that loses all data after exit is incomplete"_ — this currently applies to your project

**FR-2: at least 5 meaningful operations**

- `searchExpense()` exists only as an empty stub (`pass`) — not implemented
- No delete function exists at all
- Realistically only ~3 operations are functional: add, update, view/save

**Analysis / calculation (FR-5)**

- Only `sum(expense.values())` is used — plain Python, not the required library
- No average, no highest/lowest category, no real statistics

**File handling correctness (Section 8)**

- `expenses.txt` is a human-readable log, not something the program can read back in — it can't be used to restore state, which is required
- `json/data.json`, `data/data.txt`, and `data/expense_data.py` are all **empty files**, not actually wired into the project

**Code structure (FR-6)**

- `addExpnese()` and `updateExpense()` duplicate ~30 lines of nearly identical if/elif logic instead of sharing one function
- No separation into model class / manager class / interface functions as suggested in Section 7

**Documentation/submission (Section 12–13)**

- `README.md` — empty
- `requirements.txt` — empty
- No project report written yet

**Minor but important**

- Line 186 has an inappropriate Bengali comment (`#atta chod khabo`) — remove this before submitting, especially before faculty opens the file
- The `৳`/`ট` currency symbol is inconsistent in a couple of print statements

## Bottom line

Right now you have a working **terminal calculator with a dictionary and validation** — that's a real foundation, but three entire rubric categories (OOP, data structures, library use = 17 of 50 marks) are sitting at zero, and persistence (FR-3) technically fails since nothing reloads.

The good news: most of these gaps share one root cause — you're tracking 9 fixed category _totals_ instead of individual expense _records_. Once you introduce an `Expense` class and store entries in a list, list/tuple/set/OOP/search/delete/load all fall into place naturally, and NumPy just needs to be dropped on top for the statistics.

Want me to rewrite `main.py` step by step with you, keeping your existing menu and print style, so it fills these gaps without feeling like a totally different project?