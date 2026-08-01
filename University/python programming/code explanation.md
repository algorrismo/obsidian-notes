---
tags:
  - "#python"
Date: 2026-07-28
---
---
# Python Expense Tracker — Full Code Walkthrough

> These notes explain **every function, variable, and Python concept** in `expense_tracker.py`, in the order the program actually runs. Read top to bottom once, then use the "Questions You Might Get Asked" section at the end to rehearse explaining it out loud.

---

## 1. The Big Picture (Read This First)

Before any code, understand _what the program is_ in one paragraph:

It's a **command-line app** that lets a user log money spent in 9 categories (food, rent, etc.), keeps a **running draft** that survives if the program crashes, and — when the user is done — **permanently appends** a formatted "receipt" of that session to a history file. Everything is wrapped inside one Python **class** called `ExpenseTracker`, which is just a container that bundles related data (the expenses) with the functions that operate on that data (add, update, save, view).

Three files on disk do the work of "memory":

|File|Purpose|Lifespan|
|---|---|---|
|`data/current.txt`|Draft/autosave of the _in-progress_ session|Overwritten constantly while you're entering data|
|`data/last_id.txt`|Just one number: the last used Record ID|Updated once per finished session|
|`data/expenses.txt`|The permanent log of every finished session|Grows forever (append-only)|

Keep this table in your head — almost every method exists to read or write one of these three files.

---

## 2. Imports

```python
import time
import os
import numpy as np
```

- **`time`** — used to grab today's date/time (`time.localtime()`, `time.strftime()`).
- **`os`** — used for filesystem work: building paths (`os.path.join`), checking if a file exists (`os.path.exists`), creating folders (`os.makedirs`), and atomically replacing a file (`os.replace`).
- **`numpy as np`** — a math library, imported here only for four one-line statistics: `np.sum`, `np.mean`, `np.max`, `np.min`. (Worth knowing: for a list of ~9 numbers, plain Python's built-in `sum()`, `max()`, `min()` and `statistics.mean()` would do the exact same job without needing an external library — numpy is really built for large numerical arrays. This is a valid thing to mention if a faculty member asks "why numpy for 9 numbers?")

---

## 3. The Class and Constructor — `class ExpenseTracker: __init__`

```python
class ExpenseTracker:
    def __init__(self):
```

- **`class ExpenseTracker:`** declares a _blueprint_. Nothing runs yet — this just defines what an `ExpenseTracker` **is**.
- **`__init__`** is the _constructor_ — Python automatically calls this the moment you write `ExpenseTracker()`. It's where you set up the object's starting state.
- **`self`** is the first parameter of every method in the class. It's not a keyword — it's just the conventional name for "the specific object this method is being called on." When you later see `self.expenses`, read it as "_this tracker's_ expenses."

### 3.1 Instance variables created here

```python
self.name = ""
```

Will hold the user's name once they type it in (set later in `run()`).

```python
self.expenses = {
    "food": 0,
    "transportation": 0,
    ...
    "others": 0,
}
```

A **dictionary** — the core data structure of the whole program. Each **key** is a category name (a string), each **value** is the running total spent in that category (starts at `0`). Dictionaries give you instant lookup: `self.expenses["food"]` is far faster and more readable than searching a list.

```python
self.expenseCategory = {
    1: "food",
    2: "transportation",
    ...
    9: "others",
}
```

A **second** dictionary that maps the _menu number_ the user types (1–9) to the _key name_ used in `self.expenses`. This is the translation layer between "what the user sees on screen" and "what the code stores internally."

```python
self.dataFile = os.path.join("data", "expenses.txt")
self.idFile = os.path.join("data", "last_id.txt")
self.currentFile = os.path.join("data", "current.txt")
```

`os.path.join` builds a file path the _correct way for whatever operating system_ you're on (Windows uses `\`, Mac/Linux use `/` — this function picks the right one automatically, so the code isn't hardcoded).

```python
os.makedirs("data", exist_ok=True)
```

Creates a folder called `data` if it doesn't already exist. `exist_ok=True` means "don't throw an error if the folder is already there" — without it, running the program twice would crash on the second run.

```python
self.loadCurrentExpenses()
```

The constructor's last act: immediately try to **restore** any unfinished session from last time, so if the program crashed or was closed mid-entry, the user doesn't lose their numbers.

---

## 4. `loadCurrentExpenses(self)` — Restoring the Draft

```python
def loadCurrentExpenses(self):
    if not os.path.exists(self.currentFile):
        return
```

If there's no draft file yet (first-ever run), there's nothing to load — exit the function immediately with `return`.

```python
    try:
        with open(self.currentFile, "r", encoding="utf-8") as f:
```

- **`try:`** starts a block where Python will "watch" for errors instead of crashing immediately.
- **`with open(...) as f:`** opens the file and guarantees it gets **closed automatically** once the block ends — even if an error happens inside. This is the standard, safe way to work with files in Python (called a _context manager_).
- **`"r"`** = open in _read_ mode.
- **`encoding="utf-8"`** = read the file as UTF-8 text — important here because the program later uses a Bengali currency symbol (৳), which needs UTF-8 to display/save correctly.

```python
            for line in f:
                line = line.strip()
                if ":" not in line:
                    continue
```

Loops through the file **one line at a time**. `.strip()` removes leading/trailing whitespace and the newline character. If a line doesn't contain a `:`, it's malformed/unreadable — `continue` skips straight to the next line without processing it.

```python
                key, _, value = line.partition(":")
                key = key.strip()
```

`.partition(":")` splits a string like `"food:120.0"` into exactly **three parts**: `("food", ":", "120.0")`. The middle piece (the separator itself) isn't needed, so it's assigned to `_` — a Python convention meaning "I'm intentionally throwing this away."

```python
                if key in self.expenses:
                    try:
                        self.expenses[key] = float(value.strip())
                    except ValueError:
                        pass
```

Only update the dictionary if `key` is a category we actually recognize (defends against a corrupted/hand-edited file introducing junk keys). Converting text to a number can fail (e.g. if the saved value got corrupted) — `except ValueError: pass` means "if that happens, just silently skip this line rather than crashing the whole program."

```python
    except PermissionError:
        print("Could not load previous data: file is open in another program.")
```

On Windows especially, a file can't be read if it's currently open in another app (like Notepad or Excel). This catches that specific case and gives the user a clear message instead of an ugly crash/traceback.

---

## 5. `saveCurrentExpenses(self)` — Writing the Draft

```python
def saveCurrentExpenses(self):
    try:
        with open(self.currentFile, "w", encoding="utf-8") as f:
            for key, value in self.expenses.items():
                f.write(f"{key}:{value}\n")
    except PermissionError:
        print("Could not auto-save: file is open in another program.")
```

- **`"w"`** = write mode, which **overwrites** the whole file every time (not append). That's fine here because we're always writing the _complete current state_ of all 9 categories.
- **`self.expenses.items()`** gives you `(key, value)` pairs from the dictionary, so you can loop through both at once.
- Each line written looks like `food:120.0` — this is exactly the format `loadCurrentExpenses` expects to read back later. They're a matched pair.
- Called after **every single change** to `self.expenses` (you'll see it called inside `addExpense` and `updateExpense`) — this is what makes the "autosave/crash recovery" feature work.

---

## 6. `getNextId(self)` and `saveNextId(self, recordId)` — The Record Counter

```python
def getNextId(self):
    if not os.path.exists(self.idFile):
        return 1
    try:
        with open(self.idFile, "r", encoding="utf-8") as f:
            return int(f.read().strip()) + 1
    except (ValueError, PermissionError):
        return 1
```

- No ID file yet → this must be Record #1.
- Otherwise, read the single number stored in the file, convert it to an `int`, and add 1 (i.e., "last ID used" → "next ID to use").
- `except (ValueError, PermissionError):` catches **two different exception types in one line** — either the file's content isn't a valid number, or the file can't be accessed. Either way, falls back to `1`. _(Worth flagging as a possible improvement: this fallback could accidentally reuse an ID if the file gets briefly locked — a good thing to mention if asked about edge cases/limitations.)_

```python
def saveNextId(self, recordId):
    try:
        with open(self.idFile, "w", encoding="utf-8") as f:
            f.write(str(recordId))
    except PermissionError:
        print("Could not update ID counter: file is open in another program.")
```

Simply writes the given ID (converted to a string, since `.write()` only accepts text) into the ID file, overwriting whatever was there.

---

## 7. `showMenu(self)` — Printing the Category List

```python
def showMenu(self):
    print("Choose your category by entering the number:")
    print("1  -> Food")
    ...
```

No logic here — purely a **display** function. It exists as its own method (rather than being copy-pasted) so it can be called from two different places: once at the start of `run()`, and again at the top of `updateExpense()`.

---

## 8. `addExpense(self)` — The Main Data-Entry Loop

This is the longest and most important method. Break it into two halves.

### 8.1 Half One — Entering expenses

```python
while True:
    categoryInput = input("\nChoose your category: ").strip()
    try:
        category = int(categoryInput)
    except ValueError:
        print("Category must be a whole number. Please enter 0-9.")
        continue
```

- `while True:` = an **infinite loop** — it only stops when something inside explicitly `break`s out of it.
- `input()` always returns a **string**, even if the user typed a number. `int(categoryInput)` attempts to convert it; if the user typed letters instead, that raises `ValueError`, which is caught and handled by printing an error and `continue`-ing (jumping straight back to the top of the loop to ask again).

```python
    if category == 0:
        print("-" * 10 + "Exiting menu" + "-" * 10)
        break
    if category < 1 or category > 9:
        print("Invalid choice! Please enter a number between 1 and 9.")
        continue
```

`0` is the designated "I'm done entering" signal → `break` exits the `while True` loop entirely. Anything outside 1–9 is invalid → loop again.

```python
    amountInput = input("Enter the amount: ").strip()
    try:
        amount = float(amountInput)
    except ValueError:
        print("Amount must be a number. Please try again.")
        continue
```

Same pattern as above, but converting to `float` (decimals allowed) instead of `int`.

```python
    if amount == 0:
        print("Amount cannot be 0. Please enter a value greater than 0.")
        continue
    if amount < 0:
        print("Invalid amount! Please enter a numerical value > 0.")
        continue
    if amount > 10000000:
        print("Amount too large! Please enter a value under 10,000,000.")
        continue
```

Three separate **input validation** guards: reject zero, reject negatives, and reject anything above a sanity-check ceiling (10 million) to catch accidental typos like an extra zero.

```python
    key = self.expenseCategory[category]
    self.expenses[key] += amount
    self.saveCurrentExpenses()
    print(f"Added ৳ {amount:,.2f} successfully!")
```

- Translate the number the user typed (`category`) into the dictionary key (`key`) using the lookup table from `__init__`.
- `self.expenses[key] += amount` **adds to** the running total (not overwrite) — this is why you can enter "food" multiple times in one session and it accumulates.
- `saveCurrentExpenses()` immediately persists this change to disk (the autosave in action).
- `f"...{amount:,.2f}"` is an **f-string** with a **format specifier**: `,` inserts thousands separators (e.g. `1,000.00`), `.2f` forces exactly 2 decimal places. `\u09f3` is the Unicode escape for **৳**, the Bengali Taka currency symbol.

### 8.2 Half Two — "Do you need changes?"

```python
print("-" * 50)
print("You have successfully added all your expenses.")
...
while True:
    choiceInput = input("Enter your wish: ").strip().lower()
    if choiceInput in ("1", "y", "yes"):
        self.updateExpense()
        continue
    elif choiceInput in ("0", "n", "no"):
        print("Exiting...")
        self.expenseDetails()
        self.saveExpenseData()
        break
    else:
        print("Enter/press 0 or 1. Nothing else.")
```

Once the entry loop is done, the program asks if the user wants to revise anything.

- `.lower()` makes the check **case-insensitive** — "YES", "Yes", "yes" all work the same.
- `choiceInput in ("1", "y", "yes")` checks membership in a **tuple** — a compact way to accept several equivalent answers.
- Saying yes calls `updateExpense()`, then `continue`s this _outer_ while loop, asking "do you need changes?" again — so you can update multiple times.
- Saying no shows the on-screen summary (`expenseDetails`), permanently saves the session (`saveExpenseData`), and `break`s out — finishing `addExpense` entirely.

---

## 9. `updateExpense(self)` — Editing Existing Totals

```python
def updateExpense(self):
    print("\nYou can now update anything in your tracker list.")
    self.showMenu()
    while True:
        categoryInput = input("\nChoose your category: ").strip()
        ...
        if category == 0:
            break
```

Same validated-input pattern as `addExpense`'s first half: pick a category 1–9, or `0` to quit updating.

```python
        key = self.expenseCategory[category]
        print(f"Current {key}: ৳ {self.expenses[key]:,.2f}")
        action = input("Type 'add' to add more, 'replace' to overwrite, or 'delete' to clear it: ").strip().lower()
```

Shows the current value for that category, then asks **what kind of edit** to make — this is the key difference from `addExpense`, which only ever adds.

```python
        if action in ("delete", "d"):
            oldValue = self.expenses[key]
            self.expenses[key] = 0
            self.saveCurrentExpenses()
            print(f"Cleared {key}: ৳ {oldValue:,.2f} -> ৳ 0.00")
            continue
```

`delete` resets that one category to zero. Storing `oldValue` first lets the confirmation message show the "before → after" change.

```python
        amountInput = input("Enter the amount: ").strip()
        try:
            amount = float(amountInput)
        except ValueError:
            ...
        if amount == 0: ...
        if amount < 0: ...
        oldValue = self.expenses[key]
        if action in ("add", "a"):
            self.expenses[key] += amount
        else:
            self.expenses[key] = amount
        self.saveCurrentExpenses()
        print(f"Updated {key}: ৳ {oldValue:,.2f} -> ৳ {self.expenses[key]:,.2f}")
```

Validates the new amount exactly like before. If the action was `"add"`, accumulate; **for anything else (including `"replace"` or a typo)**, it falls through to `else` and **overwrites** the value. _(Note: this means typing a random word instead of "replace" still behaves as replace — worth mentioning as a minor design quirk if asked.)_

---

## 10. `expenseDetails(self)` — On-Screen Summary Table

```python
def expenseDetails(self):
    width = 50
    print("\n" + "-" * width)
    print(f"| {'Expense Summary':^{width - 4}} |")
```

Builds a simple text "box" using repeated dash characters. `{'Expense Summary':^{width - 4}}` is an f-string alignment trick: `^` **centers** the text within a field that's `width - 4` characters wide (the `-4` accounts for the `|` and `|` on each side).

```python
    print(f"| {'1. Food':<25} : ৳ {self.expenses['food']:<16,.2f} |")
    ...
```

Repeated 9 times (once per category). `<25` and `<16` mean **left-align** within a fixed-width field — this is what makes every row line up into neat columns, like a real table, using only plain text.

```python
    values = list(self.expenses.values())
    nonZeroValues = [v for v in values if v > 0]
```

- `.values()` grabs just the numbers from the dictionary (ignoring the category names), turned into a plain list.
- `[v for v in values if v > 0]` is a **list comprehension** — a compact loop that builds a new list containing only the values greater than 0. This matters for the statistics below: you don't want unused categories (still `0`) dragging down the average or falsely becoming the "minimum."

```python
    if not nonZeroValues:
        print(f"| {'No expenses recorded yet.':<{width - 4}} |")
    else:
        print(f"| {'Total Expense':<25} : ৳ {np.sum(values):<16,.2f} |")
        print(f"| {'Average Expense':<25} : ৳ {np.mean(nonZeroValues):<16,.2f} |")
        print(f"| {'Maximum Expense':<25} : ৳ {np.max(nonZeroValues):<16,.2f} |")
        print(f"| {'Minimum Expense':<25} : ৳ {np.min(nonZeroValues):<16,.2f} |")
```

Notice the subtlety: **Total** uses `values` (all 9, including zeros — correct, since total spending should include everything), but **Average/Max/Min** use `nonZeroValues` (only categories actually used).

---

## 11. `viewHistory(self)` — Reading Past Sessions

```python
def viewHistory(self):
    if not os.path.exists(self.dataFile):
        print("No history yet. Add and save some expenses first.")
        return
    try:
        with open(self.dataFile, "r", encoding="utf-8") as f:
            content = f.read()
    except PermissionError:
        ...
        return
    if not content.strip():
        print("No history yet. Add and save some expenses first.")
    else:
        print(content)
```

Straightforward: if the permanent log file exists, open it, read the **entire file at once** with `.read()` (fine here since it's just text, not huge data), and print it. Handles the "file exists but is completely empty" case separately from "file doesn't exist at all."

---

## 12. `saveExpenseData(self)` — Committing a Session Permanently

This is the most technically interesting method — it's where the program guards against **data corruption**.

```python
recordId = self.getNextId()
time_tuple = time.localtime()
date = time.strftime("%m/%d/%Y", time_tuple)
timee = time.strftime("%I:%M %p", time_tuple)
```

- `time.localtime()` captures the current date/time as a structured object.
- `time.strftime(format, time_tuple)` converts that into a readable string using **format codes**: `%m/%d/%Y` → `07/28/2026`; `%I:%M %p` → `03:45 PM` (12-hour clock with AM/PM).

```python
values = list(self.expenses.values())
nonZeroValues = [v for v in values if v > 0]
total = np.sum(values)
average = np.mean(nonZeroValues) if nonZeroValues else 0
```

Same stats logic as `expenseDetails`, but written as a **conditional (ternary) expression**: `X if condition else Y` — "use the mean of nonZeroValues, _unless there are none, in which case just use 0_" (this avoids a crash, since `np.mean([])` on an empty list would error).

```python
lines = [
    "=" * width,
    f"| {'Record ID : ' + str(recordId):<{width - 4}} |",
    ...
]
```

Builds the entire formatted "receipt" as a **list of strings**, one per line, rather than printing each line individually. This is a deliberate choice — it lets the whole block get joined and written to the file in one shot below.

```python
tempFile = self.dataFile + ".tmp"
try:
    oldContent = ""
    if os.path.exists(self.dataFile):
        with open(self.dataFile, "r", encoding="utf-8") as f:
            oldContent = f.read()
    with open(tempFile, "w", encoding="utf-8") as f:
        f.write(oldContent + "\n".join(lines) + "\n")
    os.replace(tempFile, self.dataFile)
except PermissionError:
    ...
except OSError as e:
    ...
```

This is the **"safe write" / atomic-write pattern** — genuinely worth understanding well, since it's the kind of detail that impresses in a code review:

1. Read whatever's already in `expenses.txt` (`oldContent`) — because we're appending a new record, not replacing the whole history.
2. Write `oldContent + the new record` into a **separate temporary file** (`expenses.txt.tmp`), _not_ directly into the real file.
3. Only once that write fully succeeds, call `os.replace(tempFile, self.dataFile)` — this **atomically** renames the temp file on top of the real one.

**Why bother?** If the program crashed or lost power _while writing directly_ to `expenses.txt`, you could end up with a half-written, corrupted file and lose your entire history. By writing to a throwaway temp file first and only swapping it in at the very end, the real file is never in a "half-written" state — it's either the old complete version or the new complete version, never something in between.

```python
self.saveNextId(recordId)
print(f"\n✓ Record saved as ID {recordId} in '{self.dataFile}'")
```

Only updates the ID counter **after** the write succeeded — so a failed save doesn't "burn" an ID number.

---

## 13. `run(self)` — The Program's Entry Point (Main Menu)

```python
def run(self):
    ...
    print(f"| {'Todays Date : ' + date:<{line_width - 4}} |")
    print(f"| {'Todays Time : ' + timee:<{line_width - 4}} |")
    ...
    self.name = input("\nEnter your name: ").strip()
```

Prints a welcome banner with today's date/time, then asks for and stores the user's name (used later in the saved record).

```python
    while True:
        print("\n1 -> Add Expenses")
        print("2 -> View History")
        print("0 -> Exit")
        choice = input("Enter your choice: ").strip()
        if choice == "1":
            self.showMenu()
            self.addExpense()
        elif choice == "2":
            self.viewHistory()
        elif choice == "0":
            print("Goodbye!")
            break
        else:
            print("Please enter 0, 1, or 2.")
```

The **top-level menu loop** — this is the "control center" that ties every other method together. Note this is a _different, higher-level_ menu than the 1–9 category menu — here, `1` means "go add expenses" (which internally shows the 1–9 menu), `2` means "view saved history," `0` exits the whole program.

---

## 14. `main()` and the `if __name__ == "__main__":` Idiom

```python
def main():
    tracker = ExpenseTracker()
    try:
        tracker.run()
    except KeyboardInterrupt:
        print("\n\nInterrupted by user. Goodbye!")

if __name__ == "__main__":
    main()
```

- `main()` is a plain function (outside the class) that creates one `ExpenseTracker` object and starts it.
- `except KeyboardInterrupt:` catches the user pressing **Ctrl+C**, so the program exits with a friendly message instead of an ugly error trace.
- `if __name__ == "__main__":` is a standard Python idiom. Every Python file has a built-in variable `__name__`. If you _run this file directly_ (`python expense_tracker.py`), Python sets `__name__` to `"__main__"`, so `main()` runs. If instead someone _imports_ this file into another script (`import expense_tracker`), `__name__` is set to `"expense_tracker"` instead, so `main()` does **not** auto-run. This lets the file be reused as a module without immediately starting the interactive program.

---

## 15. The Full Program Flow (Visual)

```mermaid
flowchart TD
    A[Program starts: main()] --> B[Create ExpenseTracker\nloadCurrentExpenses restores any draft]
    B --> C[run(): show banner, ask name]
    C --> D{Main Menu}
    D -->|1| E[showMenu + addExpense]
    D -->|2| F[viewHistory: print expenses.txt]
    D -->|0| G[Goodbye — program ends]

    E --> H{Enter category 1-9}
    H -->|amount entered| I[Validate + add to self.expenses\nautosave to current.txt]
    I --> H
    H -->|0| J{Need changes?}
    J -->|yes| K[updateExpense: add/replace/delete a category]
    K --> J
    J -->|no| L[expenseDetails: print summary]
    L --> M[saveExpenseData:\nwrite temp file, os.replace, update last_id.txt]
    M --> D
    F --> D
```

---

## 16. Glossary — Every Python Concept Used, In One Place

|Concept|Where used|Plain-English meaning|
|---|---|---|
|`class` / `self`|whole file|A blueprint for objects; `self` = "this particular object"|
|`__init__`|constructor|Runs automatically when the object is created|
|`dict` (`{}`)|`self.expenses`, `self.expenseCategory`|Key → value lookup table|
|List comprehension|`[v for v in values if v > 0]`|Compact way to filter/build a list in one line|
|`f-string`|everywhere (`f"..."`)|Embed variables/expressions directly inside a string|
|Format specifier|`:,.2f`, `:<25`, `:^`|Controls thousands separators, decimals, alignment, width|
|`try` / `except`|file I/O, input parsing|Catch and handle errors instead of crashing|
|`with open(...) as f:`|all file access|Opens a file and auto-closes it safely|
|`os.path.join`|file paths|Builds OS-correct file paths|
|`os.path.exists`|multiple methods|Checks if a file/folder is there before touching it|
|`os.makedirs(..., exist_ok=True)`|`__init__`|Creates a folder, no error if it already exists|
|`os.replace`|`saveExpenseData`|Atomically swaps a temp file in as the real file (crash-safe writing)|
|`.strip()`|input handling|Removes extra whitespace/newlines|
|`.partition(":")`|`loadCurrentExpenses`|Splits a string into (before, separator, after)|
|`.lower()`|menu choices|Case-insensitive comparisons|
|`in (a, b, c)`|validation|Checks membership in a tuple of acceptable values|
|`numpy` (`np.sum/mean/max/min`)|stats|Aggregate calculations over a list of numbers|
|`time.localtime()` / `strftime`|timestamps|Get and format the current date/time|
|`if __name__ == "__main__":`|bottom of file|Only auto-run the program if this file is executed directly|

---

## 17. Questions You Might Get Asked (with ready answers)

**Q: Why three separate files instead of one?** A: They serve different purposes and lifecycles: `current.txt` is a disposable draft overwritten constantly during entry (crash recovery); `last_id.txt` is a single persistent counter; `expenses.txt` is the permanent append-only history. Separating them keeps each file's job simple and avoids accidentally corrupting your whole history while just autosaving a draft.

**Q: What's the point of the temp-file + `os.replace` pattern in `saveExpenseData`?** A: It makes the save "atomic" — the real history file is never left half-written if the program crashes or loses power mid-save, because we only swap the temp file in once it's fully and successfully written.

**Q: Why use a dictionary for expenses instead of a list?** A: Categories are named, not ordered by index — a dictionary lets you look up "food" directly by name (`self.expenses["food"]`) instead of remembering "food is index 0."

**Q: Why filter out zero values before computing average/min?** A: Because unused categories default to `0`. Including them would artificially drag the average down and make `0` always win as the "minimum," even though the user never actually spent `0` on purpose in that category.

**Q: What would happen if two people ran this program on the same files at once?** A: It isn't designed for that — there's no locking beyond catching `PermissionError`, so concurrent writes from two separate processes could still overwrite each other's changes. This is a single-user, single-process tool.

**Q: Why does `numpy` get used for such small lists?** A: It doesn't strictly need to be — Python's built-in `sum()`, `max()`, `min()`, and the `statistics.mean()` function would do the same job here without an external dependency. `numpy` is generally reserved for large numerical arrays, so this is a stylistic choice rather than a necessity.

---

## 18. Possible Improvements (good discussion points)

- No input length caps on the name field.
- `updateExpense`'s `action` check treats _any_ non-"add"/"delete" input as "replace" — a typo silently replaces instead of erring.
- `getNextId`'s fallback to `1` on a corrupted ID file could theoretically reuse a Record ID.
- No unit tests currently exist for the validation logic.