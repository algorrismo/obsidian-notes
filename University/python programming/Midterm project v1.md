Tags : #python
Date: 2026-07-03

---
# Python Mid-Term Project — Personal Expense & Budget Tracker

### Full A–Z Build Guide (Tkinter + NumPy)

> **Deadline:** 19/7 **Type:** Personal Expense & Budget Tracker (Group Project — CLI first, then Tkinter GUI, with NumPy analysis) **Goal:** Build a small, correct, complete app — not an ambitious half-working one.

---

## 0. Before You Touch Code — Setup Checklist

### Install Python

- [x] Confirm Python 3.10+ is installed: `python --version`
- [x] Tkinter comes bundled with Python — no install needed (on Linux you may need `sudo apt install python3-tk`)

### Install NumPy

```bash
py -m pip install numpy
```

### Recommended editor

- **VS Code** (free, great Python extension, integrated terminal) — this is what most guides/tutorials assume
- Install the official "Python" extension by Microsoft

### Set up version control (recommended by the brief)

```bash
git init
git add .
git commit -m "Initial commit"
```

Push to GitHub — this alone can help with the "clean demo / structure" marks and proves your work timeline if the "own work" question ever comes up.

---

## 1. Libraries You Need (and why)

|Library|Type|Purpose in this project|Install|
|---|---|---|---|
|`tkinter`|Built-in|GUI: windows, buttons, entry fields, tables|Already included|
|`numpy`|External|Statistics: mean, std, sum, max/min category, trends|`pip install numpy`|
|`json`|Built-in|Save/load expense records persistently|Already included|
|`os`|Built-in|Check if data file exists before reading|Already included|
|`datetime`|Built-in|Timestamp each expense, filter by month|Already included|
|`uuid` or `random`|Built-in|Generate unique expense IDs|Already included|

You do **not** need Pandas, Matplotlib, Flask, or any database — these are explicitly banned in Section 10 of your brief.

---

## 2. Project Folder Structure

Set this up first. Clean structure = free marks under "Code readability" and "Structured implementation."

```
expense_tracker/
│
├── main.py                 # Entry point — starts the app
├── models/
│   └── expense.py          # Expense class (the data model)
├── manager/
│   └── budget_manager.py   # BudgetManager class (logic, file I/O, stats)
├── gui/
│   └── app_gui.py          # Tkinter interface
├── data/
│   └── expenses.json       # Saved data (auto-created)
├── utils/
│   └── validators.py       # Input validation helper functions
├── report/
│   └── project_report.md   # Your written report (Section 13 of brief)
└── README.md
```

Keeping model / manager / gui / utils separate directly satisfies **Section 7 (Expected Program Structure)** of your brief. Don't skip this — graders are explicitly told to check for it.

---

## 3. The Roadmap — Build in This Order

Do **not** start with the GUI. Build the "engine" first, test it in the terminal, then wrap a GUI around it. This is the single most important piece of advice for a beginner — it isolates bugs.

```
Phase 1: Data Model (Expense class)
Phase 2: Manager Class (in-memory logic, no file, no GUI)
Phase 3: File Handling (save/load JSON)
Phase 4: Exception Handling (bulletproof the logic)
Phase 5: NumPy Statistics
Phase 6: CLI test menu (temporary, to sanity-check everything)
Phase 7: Tkinter GUI (wraps around what already works)
Phase 8: Polish, sample data, screenshots, report
```

---

## Phase 1 — Data Model: the `Expense` class

**Concepts covered:** variables, data types, OOP

Create `models/expense.py`:

```python
import uuid

class Expense:
    def __init__(self, category, amount, note="", date=None, expense_id=None):
        self.id = expense_id or str(uuid.uuid4())[:8]
        self.category = category
        self.amount = amount
        self.note = note
        self.date = date  # store as string "YYYY-MM-DD"

    def to_dict(self):
        """Convert object -> dictionary, so it can be saved as JSON."""
        return {
            "id": self.id,
            "category": self.category,
            "amount": self.amount,
            "note": self.note,
            "date": self.date
        }

    @classmethod
    def from_dict(cls, data):
        """Convert dictionary (loaded from JSON) -> Expense object."""
        return cls(
            category=data["category"],
            amount=data["amount"],
            note=data.get("note", ""),
            date=data.get("date"),
            expense_id=data.get("id")
        )

    def __str__(self):
        return f"[{self.id}] {self.date} | {self.category} | ${self.amount:.2f} | {self.note}"
```

✅ **Checkpoint:** you can create an `Expense`, print it, convert it to a dict, and back.

---

## Phase 2 — The `BudgetManager` class (core logic, no GUI yet)

**Concepts covered:** list, tuple, set, dictionary, functions, OOP

Create `manager/budget_manager.py`:

```python
CATEGORIES = ("Food", "Transport", "Rent", "Entertainment", "Utilities", "Other")  # tuple = fixed

class BudgetManager:
    def __init__(self):
        self.expenses = []          # list of Expense objects
        self.used_ids = set()       # set = prevents duplicate IDs

    def add_expense(self, expense):
        if expense.id in self.used_ids:
            raise ValueError("Duplicate expense ID detected.")
        self.expenses.append(expense)
        self.used_ids.add(expense.id)

    def delete_expense(self, expense_id):
        for e in self.expenses:
            if e.id == expense_id:
                self.expenses.remove(e)
                self.used_ids.discard(expense_id)
                return True
        return False

    def search_by_category(self, category):
        return [e for e in self.expenses if e.category.lower() == category.lower()]

    def update_expense(self, expense_id, **kwargs):
        for e in self.expenses:
            if e.id == expense_id:
                for key, value in kwargs.items():
                    setattr(e, key, value)
                return True
        return False

    def category_totals(self):
        """Dictionary: category -> total spent."""
        totals = {}
        for e in self.expenses:
            totals[e.category] = totals.get(e.category, 0) + e.amount
        return totals
```

This single file already demonstrates **list, tuple, set, dictionary, and functions** — all required by Section 3 of your brief.

✅ **Checkpoint:** write a throwaway test script that adds 5 expenses and prints `category_totals()`.

---

## Phase 3 — File Handling (Save/Load with JSON)

**Concepts covered:** file handling

Add to `budget_manager.py`:

```python
import json
import os

DATA_FILE = "data/expenses.json"

class BudgetManager:
    # ... (previous code) ...

    def save_to_file(self, filepath=DATA_FILE):
        os.makedirs(os.path.dirname(filepath), exist_ok=True)
        data = [e.to_dict() for e in self.expenses]
        with open(filepath, "w") as f:
            json.dump(data, f, indent=4)

    def load_from_file(self, filepath=DATA_FILE):
        from models.expense import Expense
        if not os.path.exists(filepath):
            print("No saved data found — starting fresh.")
            return
        try:
            with open(filepath, "r") as f:
                data = json.load(f)
            self.expenses = []
            self.used_ids = set()
            for item in data:
                e = Expense.from_dict(item)
                self.expenses.append(e)
                self.used_ids.add(e.id)
        except (json.JSONDecodeError, KeyError):
            print("Data file is corrupted or empty. Starting with empty records.")
            self.expenses = []
```

Why JSON and not CSV? Because your records have nested structure (id, category, amount, note, date) — JSON maps 1:1 with dictionaries, which makes `to_dict()`/`from_dict()` trivial. CSV works too if you prefer it, but JSON is the more natural fit here and easier to debug (Section 8 of the brief accepts either).

✅ **Checkpoint:** save 5 expenses, close the program, reopen, load — data should still be there.

---

## Phase 4 — Exception Handling (this is worth real marks — Section 9)

Go through your brief's table (Section 9) like a checklist. Wrap these specifically:

```python
def get_valid_amount():
    while True:
        try:
            amount = float(input("Enter amount: "))
            if amount <= 0:
                print("Amount must be positive. Try again.")
                continue
            return amount
        except ValueError:
            print("That's not a number. Try again.")

def get_valid_category():
    while True:
        cat = input(f"Category {CATEGORIES}: ").strip()
        if cat in CATEGORIES:
            return cat
        print("Invalid category. Choose from the list.")
```

Required cases to cover somewhere in your app (tick each off):

- [ ] Non-numeric amount entered
- [ ] Negative or zero amount
- [ ] Empty category / invalid menu choice
- [ ] Duplicate ID (handled via `set` in Phase 2)
- [ ] Deleting/searching an ID that doesn't exist (return `False`/empty list, don't crash)
- [ ] Missing data file on first run (handled in `load_from_file`)
- [ ] Corrupted/empty JSON file (handled with `try/except json.JSONDecodeError`)

Put a `utils/validators.py` file for these — keeps `main.py` clean.

---

## Phase 5 — NumPy Analysis (this is your "library/module use" mark — must be _real_ use, not decorative)

Add a `get_statistics()` method to `BudgetManager`:

```python
import numpy as np

class BudgetManager:
    # ...

    def get_statistics(self):
        if not self.expenses:
            return None

        amounts = np.array([e.amount for e in self.expenses])

        stats = {
            "total_spent": np.sum(amounts),
            "average_expense": np.mean(amounts),
            "highest_expense": np.max(amounts),
            "lowest_expense": np.min(amounts),
            "std_deviation": np.std(amounts),
        }

        totals = self.category_totals()
        if totals:
            top_category = max(totals, key=totals.get)
            stats["top_category"] = top_category
            stats["top_category_amount"] = totals[top_category]

        return stats

    def budget_warning(self, limit):
        total = np.sum([e.amount for e in self.expenses]) if self.expenses else 0
        if total > limit:
            return f"⚠ Over budget by ${total - limit:.2f}"
        return f"✓ Within budget (${limit - total:.2f} remaining)"
```

This satisfies FR-5 (Analysis/calculation) and the "purposeful library use" mark directly — you're using `np.mean`, `np.std`, `np.sum`, `np.max`, `np.min` on real data, not just importing NumPy and never calling it.

---

## Phase 6 — Quick CLI Test Menu (temporary, throwaway, but very useful)

Before building the GUI, write a tiny `main.py` menu loop just to make sure everything works end-to-end. You'll delete/replace this once the GUI works, but it de-risks GUI debugging massively.

```python
from manager.budget_manager import BudgetManager, CATEGORIES
from models.expense import Expense
from utils.validators import get_valid_amount, get_valid_category
from datetime import date

manager = BudgetManager()
manager.load_from_file()

while True:
    print("\n1. Add  2. View All  3. Stats  4. Save & Exit")
    choice = input("Choose: ")

    if choice == "1":
        cat = get_valid_category()
        amt = get_valid_amount()
        e = Expense(category=cat, amount=amt, date=str(date.today()))
        manager.add_expense(e)
        print("Added.")
    elif choice == "2":
        for e in manager.expenses:
            print(e)
    elif choice == "3":
        print(manager.get_statistics())
    elif choice == "4":
        manager.save_to_file()
        break
    else:
        print("Invalid choice.")
```

✅ **Checkpoint:** full add → view → stats → save → reopen → load cycle works with zero crashes, including bad input.

---

## Phase 7 — Tkinter GUI (wrap the working engine)

**Do this last.** The GUI should only call methods you already built and tested — it should contain almost no logic of its own.

Minimal but complete layout plan:

```
┌─────────────────────────────────────┐
│  Personal Expense Tracker            │
├─────────────────────────────────────┤
│ Category: [Dropdown ▼]  Amount: [__] │
│ Note: [______________]  [Add Button] │
├─────────────────────────────────────┤
│  Table / Listbox of expenses         │
│  (id | date | category | amount)     │
├─────────────────────────────────────┤
│ [Search] [Delete] [Show Stats]       │
│ [Save]   [Load]                      │
└─────────────────────────────────────┘
```

Skeleton to start from:

```python
import tkinter as tk
from tkinter import ttk, messagebox
from manager.budget_manager import BudgetManager, CATEGORIES
from models.expense import Expense
from datetime import date

class ExpenseApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Expense Tracker")
        self.manager = BudgetManager()
        self.manager.load_from_file()

        self.category_var = tk.StringVar(value=CATEGORIES[0])
        ttk.Combobox(root, textvariable=self.category_var, values=CATEGORIES).grid(row=0, column=0)

        self.amount_entry = ttk.Entry(root)
        self.amount_entry.grid(row=0, column=1)

        ttk.Button(root, text="Add", command=self.add_expense).grid(row=0, column=2)

        self.listbox = tk.Listbox(root, width=60)
        self.listbox.grid(row=1, column=0, columnspan=3)

        ttk.Button(root, text="Show Stats", command=self.show_stats).grid(row=2, column=0)
        ttk.Button(root, text="Save", command=self.manager.save_to_file).grid(row=2, column=1)

        self.refresh_list()

    def add_expense(self):
        try:
            amount = float(self.amount_entry.get())
            if amount <= 0:
                raise ValueError
        except ValueError:
            messagebox.showerror("Error", "Enter a valid positive number.")
            return

        e = Expense(category=self.category_var.get(), amount=amount, date=str(date.today()))
        self.manager.add_expense(e)
        self.refresh_list()
        self.amount_entry.delete(0, tk.END)

    def refresh_list(self):
        self.listbox.delete(0, tk.END)
        for e in self.manager.expenses:
            self.listbox.insert(tk.END, str(e))

    def show_stats(self):
        stats = self.manager.get_statistics()
        if not stats:
            messagebox.showinfo("Stats", "No data yet.")
            return
        msg = "\n".join(f"{k}: {v:.2f}" if isinstance(v, float) else f"{k}: {v}" for k, v in stats.items())
        messagebox.showinfo("Statistics", msg)

if __name__ == "__main__":
    root = tk.Tk()
    app = ExpenseApp(root)
    root.mainloop()
```

Once this runs, add: a Delete button (get selected listbox item → `manager.delete_expense`), a Search field, and an Edit flow. That covers FR-2 (5+ operations: add, view, delete, search, save/load, stats = 6 operations).

---

## Phase 8 — Polish & Submission Prep

### Add sample data (Section 8 recommends 10+ records)

Write a small one-off script to pre-populate `data/expenses.json` with 10–15 realistic entries across all categories, so your stats look meaningful on first demo.

### Take screenshots

- [ ] Main GUI window with data loaded
- [ ] Add expense in action
- [ ] Statistics popup
- [ ] Error message being shown (e.g. invalid input)
- [ ] The saved JSON file open in a text editor

### Write the report (Section 13 — map directly to these headers)

1. Project title and group/member info
2. Problem statement and objectives
3. Feature list and target users
4. Python concepts used (walk through each: variables, operators, branching, loops, functions, list/tuple/set/dict, file handling, exceptions, OOP)
5. Data structure explanation (show where each of list/tuple/set/dict is used — literally point to your code)
6. OOP design: `Expense` (attributes: id, category, amount, note, date) and `BudgetManager` (methods: add, delete, search, update, save, load, stats)
7. File handling & exception handling explanation
8. NumPy use: list each `np.` function you called and what it calculates
9. Screenshots + sample input/output
10. Limitations & future improvements (e.g. "could add monthly trend charts, multi-user support, recurring expenses")

### Final pre-submission checklist

- [ ] App runs with `python main.py` with zero errors on a fresh clone
- [ ] Data persists after closing and reopening
- [ ] All 6+ required operations work
- [ ] Invalid input doesn't crash the app anywhere
- [ ] At least one meaningful class, ideally two (model + manager)
- [ ] NumPy is doing real calculation, not just imported
- [ ] Sample data file included
- [ ] Report finished, following Section 13 structure exactly
- [ ] You can explain every function out loud without looking at notes (viva — Section 15)

---

## 4. Resources to Learn From (official / high-quality only)

|Topic|Resource|
|---|---|
|Python basics refresher|[docs.python.org/3/tutorial](https://docs.python.org/3/tutorial/)|
|Tkinter official docs|[docs.python.org/3/library/tkinter](https://docs.python.org/3/library/tkinter.html)|
|Tkinter widget reference|[TkDocs](https://tkdocs.com/tutorial/index.html)|
|NumPy quickstart|[numpy.org/doc/stable/user/quickstart.html](https://numpy.org/doc/stable/user/quickstart.html)|
|JSON in Python|[docs.python.org/3/library/json.html](https://docs.python.org/3/library/json.html)|
|Exception handling|[docs.python.org/3/tutorial/errors.html](https://docs.python.org/3/tutorial/errors.html)|
|Classes/OOP in Python|[docs.python.org/3/tutorial/classes.html](https://docs.python.org/3/tutorial/classes.html)|

Since you already know OOP from C++/Java/C#, the classes doc will feel like a syntax reference more than new material — skim it, focus on Python-specific quirks (`self`, `@classmethod`, no explicit access modifiers, duck typing).

---

## 5. Common Beginner Mistakes to Avoid

- **Writing everything in one file with no functions/classes** — directly loses FR-6 and "Functions and modularity" marks.
- **Importing NumPy but barely using it** — graders are told explicitly to check this isn't "decorative."
- **Not testing file handling with a missing/corrupted file** — this is a named requirement (Section 9), test it on purpose by deleting/breaking your JSON file once.
- **Building the GUI before the logic works** — you'll end up debugging two problems at once.
- **Forgetting duplicate ID prevention** — the `set` requirement exists specifically for this; don't skip it just because a list also "works."
- **Using global variables instead of class attributes** — coming from C++/Java, keep instincts about encapsulation; Python won't stop you from doing it wrong.

---

## 6. Suggested Timeline (from today to 19/7)

|Days|Focus|
|---|---|
|Day 1–2|Phase 1–2: Expense class + BudgetManager (no file, no GUI)|
|Day 3|Phase 3–4: File handling + exception handling|
|Day 4|Phase 5–6: NumPy stats + CLI test menu, fully debug logic|
|Day 5–6|Phase 7: Tkinter GUI|
|Day 7|Phase 8: Sample data, screenshots, polish, bug fixes|
|Day 8|Write the report|
|Day 9|Rehearse the demo/viva — explain every function out loud|
|Buffer|Keep 1–2 days free before 19/7 for the unexpected|

---

_Good luck — build the boring, correct version first. A working expense tracker with clean structure will outscore an ambitious project that crashes during the demo._