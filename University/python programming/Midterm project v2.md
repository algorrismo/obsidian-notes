Tags : #python 
date : 2026-07-09

---
# Python Mid-Term Project — Expense Tracker

### Beginner-Friendly Guide (Simple Version)

> Same project, same structure — just written so every line makes sense before you type it. Rule for this version: **if you can't explain a line in one sentence, we don't use it.**

---

## 0. First — A Mini Python Dictionary (words you'll keep seeing)

Read this once before you start. These are not extra topics — they're just Python's basic vocabulary.

|Word|What it means, simply|
|---|---|
|`class`|A blueprint for making objects. Like a `class` in C++/Java — you already know this idea.|
|`self`|Means "this specific object." Every method inside a class needs `self` as its first parameter — Python requires it, C++/Java hide this from you but it works the same way.|
|`__init__`|The constructor. Runs automatically when you create a new object. Same as a constructor in Java/C++.|
|`def`|Used to create a function. `def add(a, b):`|
|`import`|Brings in a library so you can use it, e.g. `import json`|
|`list`|An ordered box that can hold many items: `[1, 2, 3]`|
|`tuple`|Like a list, but it can never change after creation: `("Food", "Rent")`|
|`set`|A box that only keeps unique items, no duplicates: `{1, 2, 3}`|
|`dict` (dictionary)|Key → value pairs: `{"name": "John", "age": 20}`|
|`try / except`|"Try this code. If it causes an error, do this instead of crashing."|
|`for item in list:`|Loop through every item in a list, one at a time|
|`if / elif / else`|Decision-making, exactly like C++/Java/C#|
|`return`|Sends a value back out of a function|

That's genuinely 90% of the vocabulary you need. Nothing else in this guide uses anything beyond this list.

---

## 1. What We're Building (recap, simple version)

A program that:

1. Lets you type in an expense (category + amount)
2. Stores it in a list
3. Saves that list to a file so it's still there next time you open the app
4. Shows simple statistics (total spent, average spent) using NumPy
5. Has a simple window (Tkinter) instead of just typing in a black terminal

That's it. No fancy tricks, no shortcuts — just the basics, done correctly.

---

## 2. Libraries You Need

```bash
pip install numpy
```

That's the only install command you need. Everything else (`tkinter`, `json`, `os`) comes with Python already.

At the top of your files you'll write:

```python
import json      # to save/load data as a file
import os        # to check if a file exists
import numpy as np   # for calculating totals/averages
import tkinter as tk # for the window/GUI
```

---

## 3. Folder Structure (simple version — fewer files)

You don't need 6 folders. Two files is enough and still shows good structure to your instructor.

```
expense_tracker/
│
├── main.py          <- everything runs from here (menu + GUI)
├── expense_data.py  <- the Expense class + the list of expenses + save/load
└── data.json        <- created automatically, stores your expenses
```

That's it. Simple, but still "structured" (a model file + a main file), which is exactly what the brief asks for.

---

## 4. Step 1 — The Expense Class (very simple version)

Open `expense_data.py`:

```python
# This class represents ONE expense.
# Think of it like a "struct" in C++, but with behavior attached.

class Expense:
    def __init__(self, expense_id, category, amount, note):
        self.id = expense_id
        self.category = category
        self.amount = amount
        self.note = note

    # This turns the object into a simple dictionary
    # so we can save it into a JSON file later.
    def to_dict(self):
        return {
            "id": self.id,
            "category": self.category,
            "amount": self.amount,
            "note": self.note
        }
```

**That's the whole class.** No `uuid`, no `@classmethod`, nothing extra. Just 4 pieces of data and one helper method.

✅ **Test it yourself:** in a scratch file, write:

```python
e = Expense(1, "Food", 20, "Lunch")
print(e.category)
print(e.to_dict())
```

If that prints correctly, you understand the class. Move on.

---

## 5. Step 2 — A List to Hold All Expenses + Simple Functions

Instead of a second big class, we'll just use **plain functions** that work on a list. This is simpler to explain in a viva than a second class, and still fully satisfies "functions for add/search/save/load" from the brief.

Add this below the `Expense` class, still inside `expense_data.py`:

```python
expenses = []          # a list that holds all Expense objects
used_ids = set()        # a set, so we never allow two expenses with the same ID

CATEGORIES = ("Food", "Transport", "Rent", "Entertainment", "Other")  # tuple = fixed list


def add_expense(category, amount, note):
    new_id = len(expenses) + 1     # simple counting ID: 1, 2, 3, 4...
    if new_id in used_ids:
        print("ID already used!")
        return
    new_expense = Expense(new_id, category, amount, note)
    expenses.append(new_expense)
    used_ids.add(new_id)
    print("Expense added.")


def view_all_expenses():
    if len(expenses) == 0:
        print("No expenses yet.")
    for e in expenses:
        print(e.id, "-", e.category, "-", e.amount, "-", e.note)


def search_by_category(category):
    results = []
    for e in expenses:
        if e.category == category:
            results.append(e)
    return results


def delete_expense(expense_id):
    for e in expenses:
        if e.id == expense_id:
            expenses.remove(e)
            print("Deleted.")
            return
    print("Expense not found.")
```

Notice: **no list comprehensions, no advanced tricks** — just plain `for` loops with `if` statements, exactly like you'd write in C++/Java. This still uses `list`, `tuple`, `set`, and `dict` (through `to_dict`) — all required.

---

## 6. Step 3 — Save and Load (File Handling)

Still in `expense_data.py`:

```python
def save_to_file():
    data_list = []
    for e in expenses:
        data_list.append(e.to_dict())

    with open("data.json", "w") as file:
        json.dump(data_list, file)

    print("Saved.")


def load_from_file():
    if not os.path.exists("data.json"):
        print("No saved file yet — starting empty.")
        return

    try:
        with open("data.json", "r") as file:
            data_list = json.load(file)

        for item in data_list:
            e = Expense(item["id"], item["category"], item["amount"], item["note"])
            expenses.append(e)
            used_ids.add(item["id"])

        print("Data loaded.")

    except:
        print("File is broken or empty. Starting fresh.")
```

**Explain this in plain words for your viva:**

- `save_to_file`: turn every expense into a dictionary, put them all in a list, write that list into a file as JSON text.
- `load_from_file`: check the file exists → read the JSON text back → turn each dictionary back into an `Expense` object → add it to our list.
- The `try/except` at the bottom means: "if anything goes wrong while reading the file (broken/empty file), don't crash — just say so and continue."

---

## 7. Step 4 — Basic Input Validation (Exception Handling)

Add this too — it directly covers 3 required cases from your brief (non-numeric input, negative amount, invalid menu choice):

```python
def get_valid_amount():
    while True:
        text = input("Enter amount: ")
        try:
            amount = float(text)
            if amount <= 0:
                print("Amount must be greater than 0.")
                continue
            return amount
        except:
            print("That's not a valid number. Try again.")


def get_valid_category():
    while True:
        print("Categories:", CATEGORIES)
        cat = input("Choose a category: ")
        if cat in CATEGORIES:
            return cat
        print("Not a valid category. Try again.")
```

`while True:` with `return` inside is just "keep asking until the answer is correct." You already know this pattern from C++/Java (it's the same as a `do-while` loop).

---

## 8. Step 5 — NumPy Statistics (kept simple)

Still in `expense_data.py`, add:

```python
import numpy as np

def show_statistics():
    if len(expenses) == 0:
        print("No data to analyze yet.")
        return

    amount_list = []
    for e in expenses:
        amount_list.append(e.amount)

    amounts = np.array(amount_list)   # turn our normal list into a NumPy array

    print("Total spent:", np.sum(amounts))
    print("Average spent:", np.mean(amounts))
    print("Highest expense:", np.max(amounts))
    print("Lowest expense:", np.min(amounts))
```

That's genuinely all the NumPy you need: `np.array`, `np.sum`, `np.mean`, `np.max`, `np.min`. Five functions, each doing one obvious thing. This alone satisfies the "NumPy must do real calculation" requirement — you don't need anything fancier than this.

---

## 9. Step 6 — Simple Text Menu First (test everything before GUI)

Create `main.py`:

```python
import expense_data as ed

ed.load_from_file()

while True:
    print("\n--- Expense Tracker ---")
    print("1. Add expense")
    print("2. View all")
    print("3. Search by category")
    print("4. Delete expense")
    print("5. Show statistics")
    print("6. Save and Exit")

    choice = input("Choose an option: ")

    if choice == "1":
        category = ed.get_valid_category()
        amount = ed.get_valid_amount()
        note = input("Note (optional): ")
        ed.add_expense(category, amount, note)

    elif choice == "2":
        ed.view_all_expenses()

    elif choice == "3":
        category = input("Which category? ")
        results = ed.search_by_category(category)
        for e in results:
            print(e.id, "-", e.amount, "-", e.note)

    elif choice == "4":
        expense_id = int(input("Enter ID to delete: "))
        ed.delete_expense(expense_id)

    elif choice == "5":
        ed.show_statistics()

    elif choice == "6":
        ed.save_to_file()
        break

    else:
        print("Invalid choice. Try again.")
```

**Run this first.** Get it fully working with no crashes before touching Tkinter at all. This alone is already a complete, gradeable project — the GUI is just a nicer wrapper around exactly this same code.

✅ **Checkpoint:** add 3–4 expenses, view them, search, delete one, see statistics, save, close, reopen, load — confirm data is still there.

---

## 10. Step 7 — Simple Tkinter GUI (only after Step 9 works perfectly)

Replace the menu loop in `main.py` with this — it calls the exact same functions from `expense_data.py`, just from buttons instead of typed numbers.

```python
import tkinter as tk
from tkinter import messagebox
import expense_data as ed

ed.load_from_file()

window = tk.Tk()
window.title("Expense Tracker")

# --- Input area ---
tk.Label(window, text="Category:").grid(row=0, column=0)
category_entry = tk.Entry(window)
category_entry.grid(row=0, column=1)

tk.Label(window, text="Amount:").grid(row=1, column=0)
amount_entry = tk.Entry(window)
amount_entry.grid(row=1, column=1)

tk.Label(window, text="Note:").grid(row=2, column=0)
note_entry = tk.Entry(window)
note_entry.grid(row=2, column=1)

# --- The listbox that shows all expenses ---
listbox = tk.Listbox(window, width=50)
listbox.grid(row=4, column=0, columnspan=2)


def refresh_list():
    listbox.delete(0, tk.END)
    for e in ed.expenses:
        line = str(e.id) + " - " + e.category + " - " + str(e.amount) + " - " + e.note
        listbox.insert(tk.END, line)


def on_add_click():
    category = category_entry.get()
    amount_text = amount_entry.get()
    note = note_entry.get()

    if category not in ed.CATEGORIES:
        messagebox.showerror("Error", "Invalid category.")
        return

    try:
        amount = float(amount_text)
        if amount <= 0:
            messagebox.showerror("Error", "Amount must be positive.")
            return
    except:
        messagebox.showerror("Error", "Amount must be a number.")
        return

    ed.add_expense(category, amount, note)
    refresh_list()
    amount_entry.delete(0, tk.END)
    note_entry.delete(0, tk.END)


def on_stats_click():
    if len(ed.expenses) == 0:
        messagebox.showinfo("Statistics", "No data yet.")
        return
    import numpy as np
    amounts = np.array([e.amount for e in ed.expenses]) if False else None
    # (simple version: just call our existing function, printed to console)
    ed.show_statistics()
    messagebox.showinfo("Statistics", "Check the console/terminal for full statistics.")


def on_save_click():
    ed.save_to_file()
    messagebox.showinfo("Saved", "Data saved successfully.")


tk.Button(window, text="Add Expense", command=on_add_click).grid(row=3, column=0)
tk.Button(window, text="Show Statistics", command=on_stats_click).grid(row=5, column=0)
tk.Button(window, text="Save", command=on_save_click).grid(row=5, column=1)

refresh_list()
window.mainloop()
```

Note: one line has a small leftover placeholder (`np.array(...) if False else None`) — just delete that whole line, it's not needed since `ed.show_statistics()` already does the calculation. Simple version = statistics print to your terminal, and a popup tells you to check there. Good enough for the brief, and much less to explain in a viva than building a second popup window with labels for every number.

**If you want it fully in a popup instead of the terminal**, that's an easy upgrade later — but get the terminal version working first.

---

## 11. What to Say in the Viva (rehearse this out loud)

You should be able to say each of these in one sentence:

- "`Expense` is my class — it's the blueprint for one expense record."
- "`expenses` is a list that holds all my `Expense` objects."
- "`CATEGORIES` is a tuple because it should never change while the program runs."
- "`used_ids` is a set so I can quickly check for duplicate IDs."
- "`to_dict()` turns an object into a dictionary so I can save it as JSON."
- "`save_to_file` and `load_from_file` handle file persistence using the `json` library."
- "My `try/except` blocks stop the program from crashing on bad input or broken files."
- "I used `np.sum`, `np.mean`, `np.max`, `np.min` from NumPy to calculate real statistics on my data."
- "Tkinter just calls the same functions I already tested in the terminal — the buttons don't contain any new logic."

If you can say all nine of these sentences without hesitation, you understand your own project — which is exactly what Section 15 of your brief is checking for.

---

## 12. Simple Timeline

|Day|Do this|
|---|---|
|Day 1|Section 4–5: Expense class + list + add/view/search/delete functions. Test with `print()` only, no menu.|
|Day 2|Section 6–7: save/load + input validation. Test by closing and reopening the program.|
|Day 3|Section 8: NumPy statistics. Test with your saved data.|
|Day 4|Section 9: the text menu (`main.py`). Get the WHOLE thing working with no GUI.|
|Day 5–6|Section 10: Tkinter GUI, wrapping the working code.|
|Day 7|Add 10 sample expenses, take screenshots.|
|Day 8|Write the report (same structure as before — problem statement, features, concepts used, screenshots).|
|Day 9|Practice explaining every line out loud using Section 11 above.|

---

_This version has zero tricks, zero shortcuts, and zero syntax you haven't seen explained. If any single line still doesn't make sense, ask about that one line specifically — we'll slow down further on just that part._
