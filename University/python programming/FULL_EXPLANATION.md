---
Tags:
  - "#python"
Date: 2026-07-29
---
----



# 🧾 Personal Expense Tracker — Complete Line-by-Line Explanation

> **Author:** Student Project  
> **Language:** Python 3  
> **File:** `main.py` (312 lines)  
> **Purpose:** A CLI (Command-Line Interface) expense tracker that lets users log, update, view, and save expenses across 9 categories with full history tracking.

---

## Table of Contents

1. [Imports (Lines 1–3)](#1-imports-lines-1-3)
2. [Class Definition & Constructor — `ExpenseTracker.__init__` (Lines 4–33)](#2-class-definition--constructor---expensetracker__init__-lines-4-33)
3. [Load Previous Session — `loadCurrentExpenses` (Lines 34–51)](#3-load-previous-session---loadcurrentexpenses-lines-34-51)
4. [Save Current Session — `saveCurrentExpenses` (Lines 52–57)](#4-save-current-session---savecurrentexpenses-lines-52-57)
5. [ID Management — `getNextId` & `saveNextId` (Lines 58–71)](#5-id-management---getnextid--savenextid-lines-58-71)
6. [Show Menu — `showMenu` (Lines 73–84)](#6-show-menu---showmenu-lines-73-84)
7. [Add Expense — `addExpense` (Lines 85–135)](#7-add-expense---addexpense-lines-85-135)
8. [Update Expense — `updateExpense` (Lines 136–179)](#8-update-expense---updateexpense-lines-136-179)
9. [Display Summary — `expenseDetails` (Lines 181–206)](#9-display-summary---expensedetails-lines-181-206)
10. [View History — `viewHistory` (Lines 207–220)](#10-view-history---viewhistory-lines-207-220)
11. [Save to File — `saveExpenseData` (Lines 221–274)](#11-save-to-file---saveexpensedata-lines-221-274)
12. [Main Application Loop — `run` (Lines 276–303)](#12-main-application-loop---run-lines-276-303)
13. [Entry Point — `main()` & `if __name__ == "__main__"` (Lines 305–312)](#13-entry-point---main--if-__name__--__main__-lines-305-312)
14. [Complete Workflow Summary](#14-complete-workflow-summary)
15. [Glossary of Key Concepts](#15-glossary-of-key-concepts)

---

## 1. Imports (Lines 1–3)

```python
import time      # line 1
import os        # line 2
import numpy as np  # line 3
```

### `import time`
- **What it does:** Brings Python's built-in `time` module into the program.
- **Why needed:** To get the current date and time when saving expense records. This gives each record a timestamp so you know *when* the expenses were logged.
- **Real-world analogy:** Like a receipt printer that stamps the date and time on your bill.

### `import os`
- **What it does:** Brings Python's `os` module (Operating System interface).
- **Why needed:** To interact with the file system — creating folders, checking if files exist, and joining file paths correctly regardless of OS (Windows vs Mac vs Linux).
- **Key functions used here:**
  - `os.path.join()` — safely builds file paths
  - `os.makedirs()` — creates folders
  - `os.path.exists()` — checks if a file/folder exists
  - `os.replace()` — atomically replaces a file (safe saving)

### `import numpy as np`
- **What it does:** Imports the NumPy library (Numerical Python) and gives it the alias `np`.
- **Why needed:** To perform mathematical calculations easily:
  - `np.sum()` — add all expense values
  - `np.mean()` — calculate the average
  - `np.max()` / `np.min()` — find highest/lowest expense
- **Why not plain Python?** You could use `sum()`, `max()`, `min()` built-ins, but `np.mean()` is convenient. However, NumPy is **overkill here** — this is a common criticism of this code.

---

## 2. Class Definition & Constructor — `ExpenseTracker.__init__` (Lines 4–33)

```python
class ExpenseTracker:              # line 4
    def __init__(self):            # line 5
```

### `class ExpenseTracker:`
- **What is a class?** A blueprint for creating objects. Think of it as a **template**. Just like a cookie-cutter creates cookies, a class creates objects.
- **ExpenseTracker** is our cookie-cutter. It will create tracker objects that manage expenses.
- **Why use a class?** It bundles all related data (expenses, categories, file paths) and functions (add, update, save, view) into one neat package.

### `def __init__(self):`
- **What is `__init__`?** It's the **constructor** — a special method that runs **automatically** when you create a new ExpenseTracker object.
- **What is `self`?** `self` refers to the **current instance** of the class. If you create `tracker1` and `tracker2`, `self` inside `tracker1`'s methods points to `tracker1`'s data, not `tracker2`'s.
- **Easy analogy:** When you fill out a form, `self` is like saying "**my** name" vs "**your** name". It's the object speaking about itself.

---

### Line 6: `self.name = ""`

- Creates an attribute (variable that belongs to the object) called `name`.
- Initial value is an **empty string** `""`.
- It will be filled later (in `run()`) when the user enters their name.
- **Why empty?** Because when the object is first created, we don't know the user's name yet.

---

### Lines 7–17: `self.expenses = { ... }`

```python
self.expenses = {
    "food": 0,
    "transportation": 0,
    "mobile bill": 0,
    "rent": 0,
    "utilities": 0,
    "groceries": 0,
    "entertainment": 0,
    "health": 0,
    "others": 0,
}
```

- **What is a dictionary (`dict`)?** A collection of **key-value pairs**. Like a real dictionary where you look up a word (key) to find its definition (value).
- Here the **keys** are category names (strings like `"food"`, `"rent"`) and the **values** are expense amounts (numbers, all starting at `0`).
- **Why a dictionary?** So we can quickly look up or update an expense by its category name — `self.expenses["food"]` gives us the food expense.
- **Why 9 categories?** These represent common monthly expense categories. All start at 0 because no expenses have been entered yet.

---

### Lines 18–28: `self.expenseCategory = { ... }`

```python
self.expenseCategory = {
    1: "food",
    2: "transportation",
    3: "mobile bill",
    4: "rent",
    5: "utilities",
    6: "groceries",
    7: "entertainment",
    8: "health",
    9: "others",
}
```

- **Purpose:** Maps **numbers** (1–9) to **category names**.
- **Why?** When the user types `1`, the program needs to know that means `"food"`. This dictionary does that conversion.
- **Notice the direction:** `expenseCategory` maps `number -> name`, while `expenses` maps `name -> amount`. Together they form the bridge: `user types 1 → expenseCategory[1] gives "food" → expenses["food"] gives the amount`.

---

### Lines 29–31: File Paths

```python
self.dataFile = os.path.join("data", "expenses.txt")   # line 29
self.idFile = os.path.join("data", "last_id.txt")        # line 30
self.currentFile = os.path.join("data", "current.txt")   # line 31
```

- **`os.path.join("data", "expenses.txt")`** — Creates the path `data/expenses.txt` on Mac/Linux or `data\expenses.txt` on Windows.
- **Why not just write `"data/expenses.txt"`?** Because different operating systems use different separators (`/` vs `\`). `os.path.join` handles this automatically — your code works everywhere.
- **Three files used:**
  | File | Purpose |
  |------|---------|
  | `data/expenses.txt` | **History file** — stores all past records forever |
  | `data/last_id.txt` | **Counter file** — stores the last used record ID number |
  | `data/current.txt` | **Session file** — saves current expenses so they persist if you close & reopen |

---

### Line 32: `os.makedirs("data", exist_ok=True)`

- **`os.makedirs("data")`** — Creates a folder named `data` in the current directory.
- **`exist_ok=True`** — Means "don't crash if the folder already exists". Without this, Python would raise `FileExistsError` if `data/` is already there.
- **Why create it here?** Because the next line tries to load files from `data/`. If the folder doesn't exist, the load functions handle it gracefully (they just return), but creating it ensures the folder is ready for saving later.

---

### Line 33: `self.loadCurrentExpenses()`

- Calls the `loadCurrentExpenses()` method to load any previously saved session data from `current.txt`.
- **Why call it in `__init__`?** So when the program starts, it automatically restores whatever expenses were last worked on — the user doesn't start from zero every time.

---

## 3. Load Previous Session — `loadCurrentExpenses` (Lines 34–51)

```python
def loadCurrentExpenses(self):                           # line 34
    if not os.path.exists(self.currentFile):             # line 35
        return                                           # line 36
```

### Line 35: `if not os.path.exists(self.currentFile)`
- **`os.path.exists()`** checks if a file exists at the given path.
- **`not`** reverses the condition — so this means "if the file does NOT exist".
- **Why check?** If there's no `current.txt` file (first time running), there's nothing to load, so just `return` (exit the function).

---

### Lines 37–51: Reading and Parsing the File

```python
    try:                                                 # line 37
        with open(self.currentFile, "r", encoding="utf-8") as f:  # line 38
            for line in f:                               # line 39
                line = line.strip()                      # line 40
                if ":" not in line:                      # line 41
                    continue                             # line 42
                key, _, value = line.partition(":")      # line 43
                key = key.strip()                        # line 44
                if key in self.expenses:                 # line 45
                    try:                                 # line 46
                        self.expenses[key] = float(value.strip())  # line 47
                    except ValueError:                   # line 48
                        pass                             # line 49
    except PermissionError:                              # line 50
        print("Could not load previous data: file is open in another program.")  # line 51
```

### Line 38: `with open(self.currentFile, "r", encoding="utf-8") as f:`

- **`open()`** — Opens a file. Parameters:
  - `self.currentFile` — path to `data/current.txt`
  - `"r"` — **read mode** (we only want to read, not write)
  - `encoding="utf-8"` — tells Python the file uses UTF-8 text encoding (handles special characters, currency symbols, etc.)
- **`with ... as f:`** — A **context manager**. It automatically closes the file when the block ends, even if an error occurs. Without `with`, you'd need `f.close()` manually.

### Line 39: `for line in f:`
- Iterates over the file **line by line**. Files are iterable in Python — each iteration gives you one line (including the `\n` newline character at the end).

### Line 40: `line = line.strip()`
- **`.strip()`** removes **whitespace** (spaces, tabs, newlines) from the **beginning and end** of the string.
- `"  hello world\n".strip()` becomes `"hello world"`.
- **Why needed?** File lines end with `\n`. We don't want that trailing newline when we process the data.

### Lines 41–42: `if ":" not in line: continue`

- Skips lines that don't contain a colon (`:`), because the expected format is `category:amount` (e.g., `food:250.50`).
- **`continue`** jumps to the next iteration of the loop — effectively skipping bad lines.

### Line 43: `key, _, value = line.partition(":")`

- **`str.partition(separator)`** splits a string into three parts:
  1. Everything **before** the separator
  2. The **separator itself**
  3. Everything **after** the separator
- Example: `"food:250.50".partition(":")` → `("food", ":", "250.50")`
- **`key, _, value`** — Unpacking the tuple. The `_` is a convention meaning "I don't need this value" (the colon itself).

### Line 44–45: Validation

```python
key = key.strip()
if key in self.expenses:
```

- Strips any extra whitespace from the key.
- Checks if the key (category name) is one of the valid 9 categories by checking if it exists in the `self.expenses` dictionary. This prevents loading corrupted or invalid data.

### Lines 46–49: Safe Conversion

```python
try:
    self.expenses[key] = float(value.strip())
except ValueError:
    pass
```

- **`float(value.strip())`** — Converts the string `"250.50"` to the number `250.50`.
- **`try/except ValueError`** — If the conversion fails (e.g., the value is `"abc"` instead of a number), Python raises a `ValueError`. We **catch** it and `pass` (do nothing, skip that line).
- **Why `pass`?** Silent error handling — if a line is corrupted, we just skip it rather than crashing the program.

### Lines 50–51: PermissionError Handling

- If the file is **open in another program** (like Notepad), Python can't read it and raises `PermissionError`. We catch it and show a friendly message instead of crashing.

---

## 4. Save Current Session — `saveCurrentExpenses` (Lines 52–57)

```python
def saveCurrentExpenses(self):                           # line 52
    try:                                                 # line 53
        with open(self.currentFile, "w", encoding="utf-8") as f:  # line 54
            f.writelines(f"{key}:{value}\n" for key, value in self.expenses.items())  # line 55
    except PermissionError:                              # line 56
        print("Could not auto-save: file is open in another program.")  # line 57
```

### Line 54: `open(self.currentFile, "w", encoding="utf-8")`

- `"w"` means **write mode**. This **overwrites** the file completely (unlike `"a"` which appends).
- **Why overwrite?** Because we're saving the **current state** of expenses. If `food` was 100 and now it's 150, we want the file to contain 150, not both 100 and 150.

### Line 55: Generator Expression

```python
f.writelines(f"{key}:{value}\n" for key, value in self.expenses.items())
```

Let's break this down inside-out:

1. **`self.expenses.items()`** — Returns each key-value pair as a tuple: `("food", 0), ("transportation", 0), ...`
2. **`for key, value in self.expenses.items()`** — Loops through each pair.
3. **`f"{key}:{value}\n"`** — An **f-string** (formatted string literal). It embeds variables directly inside `{}`. Produces lines like `food:0\n`.
4. **The whole expression `(...)`** — A **generator expression**. It's like a list but doesn't store everything in memory at once — it produces items on-the-fly.
5. **`f.writelines(...)`** — Writes each string from the generator to the file, one after another.

**Result file content:**
```
food:0
transportation:0
mobile bill:0
rent:0
utilities:0
groceries:0
entertainment:0
health:0
others:0
```

### Line 56–57: PermissionError Handling

Same pattern — if the file is locked by another program, show a friendly message.

---

## 5. ID Management — `getNextId` & `saveNextId` (Lines 58–71)

### `getNextId` (Lines 58–65)

```python
def getNextId(self):                                     # line 58
    if not os.path.exists(self.idFile):                  # line 59
        return 1                                         # line 60
    try:                                                 # line 61
        with open(self.idFile, "r", encoding="utf-8") as f:  # line 62
            return int(f.read().strip()) + 1             # line 63
    except (ValueError, PermissionError):                # line 64
        return 1                                         # line 65
```

- **Purpose:** Determines the next record ID (1, 2, 3, ...) for saving a new expense record.
- **Line 59:** If `last_id.txt` doesn't exist (first record ever), return `1`.
- **Line 63:** Read the file, convert its contents to an integer, **add 1**. If the file contains `5`, we return `6`.
- **Line 64:** If the file is corrupted (`ValueError`) or locked (`PermissionError`), default to `1`.

### `saveNextId` (Lines 66–71)

```python
def saveNextId(self, recordId):                          # line 66
    try:                                                 # line 67
        with open(self.idFile, "w", encoding="utf-8") as f:  # line 68
            f.write(str(recordId))                       # line 69
    except PermissionError:                              # line 70
        print("Could not update ID counter: file is open in another program.")  # line 71
```

- **Purpose:** After using an ID, save it back so the next record gets the next number.
- **Line 69:** `str(recordId)` converts the integer to a string (files can only store text).
- **Example flow:** First run → `getNextId()` returns `1` → save record with ID 1 → `saveNextId(1)` writes `1` to file → Next run → `getNextId()` reads `1` and returns `2`.

---

## 6. Show Menu — `showMenu` (Lines 73–84)

```python
def showMenu(self):                                      # line 73
    print("Choose your category by entering the number:")  # line 74
    print("1  -> Food")                                  # line 75
    print("2  -> Transportation Cost")                   # line 76
    print("3  -> Mobile Bill")                           # line 77
    print("4  -> Rent")                                  # line 78
    print("5  -> Utilities")                             # line 79
    print("6  -> Groceries")                             # line 80
    print("7  -> Entertainment")                         # line 81
    print("8  -> Health")                                # line 82
    print("9  -> Others")                                # line 83
    print("0  -> Exit")                                  # line 84
```

- **Purpose:** Displays the category menu so the user knows which number to type.
- **Note:** This is a **pure display function** — it only prints, it doesn't take input. The input handling happens in `addExpense()` and `updateExpense()`.
- **Why separate?** Good design — each function has one job. `showMenu` just shows the menu. If you needed to change the menu text, you only change it here.

---

## 7. Add Expense — `addExpense` (Lines 85–135)

This is the **core function** for entering expense data. It's complex, so let's go section by section.

### The Outer Loop (Lines 86–117)

```python
def addExpense(self):                                    # line 85
    while True:                                          # line 86
        categoryInput = input("\nChoose your category: ").strip()  # line 87
```

#### Line 86: `while True:`
- Creates an **infinite loop**. It will keep running until a `break` statement is hit.
- **Why infinite?** Because the user might want to enter multiple expenses in one session. Each iteration lets them enter one expense. They exit by typing `0`.

#### Line 87: `input("\nChoose your category: ").strip()`

- **`input()`** — Python's built-in function that:
  1. Prints the prompt text (`"\nChoose your category: "`)
  2. Waits for the user to type something
  3. Returns whatever the user typed (as a string)
- **`.strip()`** — Removes leading/trailing whitespace (in case user types `" 3 "` instead of `"3"`).
- The result is stored in `categoryInput` (a string).

---

### Input Validation — Category (Lines 88–98)

```python
        try:                                             # line 88
            category = int(categoryInput)                # line 89
        except ValueError:                               # line 90
            print("Category must be a whole number. Please enter 0-9.")  # line 91
            continue                                     # line 92
        if category == 0:                                # line 93
            print("-" * 10 + "Exiting menu" + "-" * 10)  # line 94
            break                                        # line 95
        if category < 1 or category > 9:                 # line 96
            print("Invalid choice! Please enter a number between 1 and 9.")  # line 97
            continue                                     # line 98
```

#### Lines 88–92: Type Conversion & Validation
- **`int(categoryInput)`** — Converts the string to an integer.
- **`try/except ValueError`** — If the user types `"abc"`, `int("abc")` raises a `ValueError`. We catch it, show an error, and `continue` (go back to the top of the loop to ask again).

#### Lines 93–95: Exit Check
- If the user types `0`, print an exit message and `break` out of the loop.
- Note: `"-" * 10` creates the string `"----------"`. This is **string multiplication** — Python's neat trick for repeating strings.

#### Lines 96–98: Range Check
- Ensures the number is between 1 and 9 (inclusive).
- If not (e.g., user typed `15`), show error and `continue` (ask again).

---

### Input Validation — Amount (Lines 99–113)

```python
        amountInput = input("Enter the amount: ").strip()   # line 99
        try:                                                 # line 100
            amount = float(amountInput)                      # line 101
        except ValueError:                                   # line 102
            print("Amount must be a number. Please try again.")  # line 103
            continue                                         # line 104
        if amount == 0:                                      # line 105
            print("Amount cannot be 0. Please enter a value greater than 0.")  # line 106
            continue                                         # line 107
        if amount < 0:                                       # line 108
            print("Invalid amount! Please enter a numerical value > 0.")  # line 109
            continue                                         # line 110
        if amount > 10000000:                                # line 111
            print("Amount too large! Please enter a value under 10,000,000.")  # line 112
            continue                                         # line 113
```

- **Line 99:** Ask user for the amount.
- **Line 101:** `float(amountInput)` — Converts to a **float** (decimal number). Why `float` not `int`? Because expenses can have paisa/cents (e.g., `250.50`).
- **Lines 105–107:** Reject exactly `0` (no point in adding a zero expense).
- **Lines 108–110:** Reject negative numbers (you can't spend negative money... normally).
- **Lines 111–113:** Reject absurdly large amounts (over 10 million). This is a **sanity check** to prevent accidental typos like `99999999999`.

---

### Adding the Expense (Lines 114–117)

```python
        key = self.expenseCategory[category]                # line 114
        self.expenses[key] += amount                        # line 115
        self.saveCurrentExpenses()                          # line 116
        print(f"Added \u09f3 {amount:,.2f} successfully!")  # line 117
```

#### Line 114: Category Lookup
```python
key = self.expenseCategory[category]
```
- `category` is the number the user typed (e.g., `1`)
- `self.expenseCategory[1]` looks up the dictionary and returns `"food"`
- Now `key` holds the string `"food"`

#### Line 115: Accumulate
```python
self.expenses[key] += amount
```
- **`+=`** is the **add-and-assign** operator.
- `self.expenses["food"] += 250.50` means: take the current value of `self.expenses["food"]`, add `250.50` to it, and store the result back.
- **Why `+=` and not `=`?** Because the user might already have expenses in that category from a previous entry. `+=` **adds** to the existing total. If they already had 100 and add 50, it becomes 150.
- If you wanted to **replace**, you'd use `=` instead.

#### Line 116: Auto-Save
```python
self.saveCurrentExpenses()
```
- Saves the updated expenses to `current.txt` immediately after each entry.
- **Why save immediately?** So if the program crashes, only the last entry is lost, not everything.

#### Line 117: Success Message
```python
print(f"Added \u09f3 {amount:,.2f} successfully!")
```
- **`\u09f3`** — Unicode escape for the **Bengali Rupee sign** (৳). In the actual output, this displays as `৳`.
- **`{amount:,.2f}`** — Format specifier:
  - `:` starts the format specification
  - `,` adds comma separators (1,000.50 instead of 1000.50)
  - `.2` shows exactly 2 decimal places
  - `f` means floating-point number
- **Example output:** `Added ৳ 1,250.00 successfully!`

---

### Post-Loop: Summary & Options (Lines 118–135)

```python
    print("-" * 50)                                        # line 118
    print("You have successfully added all your expenses.") # line 119
    print("Do you need any changes in your expense list?")  # line 120
    print("If yes press/type: 1")                          # line 121
    print("If no  press/type: 0")                          # line 122
```

These lines execute **after** the `while True` loop ends (when user types `0`). They ask if the user wants to make changes.

---

#### Lines 123–135: The Choice Loop

```python
    while True:                                            # line 123
        choiceInput = input("Enter your wish: ").strip().lower()  # line 124
        if choiceInput in ("1", "y", "yes"):               # line 125
            self.updateExpense()                           # line 126
            continue                                       # line 127
        elif choiceInput in ("0", "n", "no"):              # line 128
            print("Exiting...")                            # line 129
            print("Let's see total invoice of your list.")  # line 130
            self.expenseDetails()                          # line 131
            self.saveExpenseData()                         # line 132
            break                                          # line 133
        else:                                              # line 134
            print("Enter/press 0 or 1. Nothing else.")     # line 135
```

#### Line 124: `.strip().lower()`
- **`.lower()`** converts the input to lowercase, so `"YES"`, `"Yes"`, and `"yes"` all become `"yes"`.

#### Lines 125–127: Yes — Go to Update
```python
if choiceInput in ("1", "y", "yes"):
    self.updateExpense()
    continue
```
- `in ("1", "y", "yes")` checks if the input matches any of these strings. It's a concise way to check multiple alternatives.
- If yes, call `updateExpense()` (see Section 8), then `continue` goes back to the choice loop (to ask again).
- **Flaw in design:** `continue` goes back to the choice loop, not the main add loop. After updating, the user is asked again "do you need changes?" rather than going back to add more expenses.

#### Lines 128–133: No — Show Summary & Save
```python
elif choiceInput in ("0", "n", "no"):
    print("Exiting...")
    print("Let's see total invoice of your list.")
    self.expenseDetails()
    self.saveExpenseData()
    break
```
- If no: show expense summary (`expenseDetails`), save to history (`saveExpenseData`), then `break` out of the choice loop.
- **`break`** exits the loop entirely, and the function ends.

#### Lines 134–135: Invalid Input
```python
else:
    print("Enter/press 0 or 1. Nothing else.")
```
- If the user types anything else, show an error and loop again.

---

## 8. Update Expense — `updateExpense` (Lines 136–179)

This function lets the user **modify** existing expense values — add more, replace, or delete.

```python
def updateExpense(self):                                   # line 136
    print("\nYou can now update anything in your tracker list.")  # line 137
    self.showMenu()                                        # line 138
```

### Line 138: Show the Category Menu

So the user knows which numbers to type.

---

### The Update Loop (Lines 139–179)

```python
    while True:                                            # line 139
        categoryInput = input("\nChoose your category: ").strip()  # line 140
        try:                                                # line 141
            category = int(categoryInput)                   # line 142
        except ValueError:                                  # line 143
            print("Category must be a whole number. Please enter 0-9.")  # line 144
            continue                                        # line 145
        if category == 0:                                   # line 146
            print("-" * 10 + "Quitting update menu" + "-" * 10)  # line 147
            break                                           # line 148
        if category < 1 or category > 9:                    # line 149
            print("Invalid choice! Please enter a number between 1 and 9.")  # line 150
            continue                                        # line 151
        key = self.expenseCategory[category]                # line 152
```

Lines 139–152 are **identical** in structure to the category selection in `addExpense`. Same validation pattern.

---

### Showing Current Value & Getting Action (Lines 153–154)

```python
        print(f"Current {key}: \u09f3 {self.expenses[key]:,.2f}")  # line 153
        action = input("Type 'add' to add more, 'replace' to overwrite, or 'delete' to clear it: ").strip().lower()  # line 154
```

#### Line 153: Display Current Value
- Shows what the current expense is for that category, e.g., `Current food: ৳ 250.00`
- This helps the user decide what to do.

#### Line 154: Three Operations
- **`add`** — Increase the existing amount.
- **`replace`** — Set a brand new amount (overwrite).
- **`delete`** — Set the amount to `0`.
- Again uses `.strip().lower()` for clean, case-insensitive input.

---

### Delete Operation (Lines 155–159)

```python
        if action in ("delete", "d"):                      # line 155
            oldValue = self.expenses[key]                  # line 156
            self.expenses[key] = 0                         # line 157
            self.saveCurrentExpenses()                     # line 158
            print(f"Cleared {key}: \u09f3 {oldValue:,.2f} -> \u09f3 0.00")  # line 159
            continue                                       # line 160
```

- **Line 155:** Check if user typed "delete" or "d".
- **Line 156:** Store the **old** value before deleting (so we can show what was removed).
- **Line 157:** Set the expense to `0`.
- **Line 158:** Auto-save.
- **Line 159:** Show the change: `"Cleared food: ৳ 250.00 -> ৳ 0.00"`.
- **Line 160:** `continue` — go back to choose another category.

---

### Amount Input for Add/Replace (Lines 161–172)

```python
        amountInput = input("Enter the amount: ").strip()  # line 161
        try:                                                # line 162
            amount = float(amountInput)                     # line 163
        except ValueError:                                  # line 164
            print("Amount must be a number. Please try again.")  # line 165
            continue                                        # line 166
        if amount == 0:                                     # line 167
            print("Amount cannot be 0.")                     # line 168
            continue                                        # line 169
        if amount < 0:                                      # line 170
            print("Invalid amount! Please enter a numerical value > 0.")  # line 171
            continue                                        # line 172
```

Identical pattern to `addExpense` — validate that amount is a positive, non-zero number.

---

### Applying Add vs Replace (Lines 173–179)

```python
        oldValue = self.expenses[key]                      # line 173
        if action in ("add", "a"):                         # line 174
            self.expenses[key] += amount                   # line 175
        else:                                              # line 176
            self.expenses[key] = amount                    # line 177
        self.saveCurrentExpenses()                         # line 178
        print(f"Updated {key}: \u09f3 {oldValue:,.2f} -> \u09f3 {self.expenses[key]:,.2f}")  # line 179
```

#### Line 173: Save Old Value
- Store the current value **before** changing it, for display purposes.

#### Lines 174–177: The Core Logic
```python
if action in ("add", "a"):
    self.expenses[key] += amount    # add to existing
else:
    self.expenses[key] = amount     # replace existing
```
- **Note:** The `else` catches both "replace" and any other input. If the user types something other than "add"/"a"/"delete"/"d", it falls into `else` and performs a **replace**. This is a **bug/design flaw** — there's no validation for unexpected actions.

#### Lines 178: Auto-save.

#### Line 179: Show the Change
- Example output: `"Updated food: ৳ 250.00 -> ৳ 350.00"`

---

## 9. Display Summary — `expenseDetails` (Lines 181–206)

```python
def expenseDetails(self):                                  # line 181
    width = 50                                             # line 182
    print("\n" + "-" * width)                              # line 183
    print(f"| {'Expense Summary':^{width - 4}} |")         # line 184
    print("-" * width)                                     # line 185
```

- **Line 182:** `width = 50` — A constant that controls the width of the display. All borders, alignments, and separators use this value.
- **Line 183:** Print a top border: `--------------------------------------------------` (50 dashes).
- **Line 184:** Centered title.
  - `'Expense Summary'` — the text to display
  - `:^{width - 4}` — center-align (`^`) within a field of `width - 4 = 46` characters
  - The outer `|` characters are literal — they form the side borders of the box
  - Result: `|             Expense Summary              |`
- **Line 185:** Another separator line.

---

### Lines 186–195: Category List

```python
    print(f"| {'1. Food':<25} : \u09f3 {self.expenses['food']:<16,.2f} |")
    print(f"| {'2. Transportation':<25} : \u09f3 {self.expenses['transportation']:<16,.2f} |")
    ...
    print("|" + "-" * (width - 2) + "|")
```

- **`{'1. Food':<25}`** — Left-align (`<`) the label within 25 characters. So `'1. Food'` takes 25 chars with spaces on the right.
- **`{self.expenses['food']:<16,.2f}`** — Right-align the amount within 16 characters, with comma separators and 2 decimal places.
- **Line 195:** Inner separator line (48 dashes between pipes).

**Example output:**
```
| 1. Food                  : ৳ 0.00             |
| 2. Transportation        : ৳ 0.00             |
```

---

### Lines 197–205: Statistics Calculation

```python
    values = list(self.expenses.values())                # line 197
    nonZeroValues = [v for v in values if v > 0]         # line 198
    if not nonZeroValues:                                 # line 199
        print(f"| {'No expenses recorded yet.':<{width - 4}} |")  # line 200
    else:                                                # line 201
        print(f"| {'Total Expense':<25} : \u09f3 {np.sum(values):<16,.2f} |")  # line 202
        print(f"| {'Average Expense':<25} : \u09f3 {np.mean(nonZeroValues):<16,.2f} |")  # line 203
        print(f"| {'Maximum Expense':<25} : \u09f3 {np.max(nonZeroValues):<16,.2f} |")  # line 204
        print(f"| {'Minimum Expense':<25} : \u09f3 {np.min(nonZeroValues):<16,.2f} |")  # line 205
    print("-" * width)                                   # line 206
```

#### Line 197: `values = list(self.expenses.values())`

- **`self.expenses.values()`** — Returns a **view object** of all values in the dictionary: `dict_values([0, 0, 0, 250.0, 0, 0, 0, 0, 0])`.
- **`list(...)`** — Converts it to a Python list: `[0, 0, 0, 250.0, 0, 0, 0, 0, 0]`.

#### Line 198: List Comprehension — `nonZeroValues`

```python
nonZeroValues = [v for v in values if v > 0]
```

This is a **list comprehension** — a compact way to build a list.

**Unrolled version:**
```python
nonZeroValues = []
for v in values:
    if v > 0:
        nonZeroValues.append(v)
```

- It creates a **new list** containing only values greater than 0.
- **Why?** Because calculating average/minimum of zeros is meaningless. If you have 9 categories but only 2 have money spent, the average should be over those 2, not all 9.

#### Lines 199–200: Check for No Expenses

```python
if not nonZeroValues:
```
- Empty lists are **falsy** in Python — they evaluate to `False` in a boolean context. So if `nonZeroValues` is empty (length 0), `not nonZeroValues` is `True`.
- If no expenses exist, display a message.

#### Lines 202–205: NumPy Calculations

```python
np.sum(values)        # Total = sum of ALL values (including zeros)
np.mean(nonZeroValues)  # Average = mean of only NON-ZERO values
np.max(nonZeroValues)   # Maximum = highest non-zero value
np.min(nonZeroValues)   # Minimum = lowest non-zero value
```

- **Why `np.sum(values)` includes zeros but `np.mean(nonZeroValues)` doesn't?**
  - Total should include all categories (zeros and all) — it's the total spent.
  - Average, max, min over only non-zero categories gives useful information (e.g., average spending per active category).

#### Line 206: Bottom Border

---

## 10. View History — `viewHistory` (Lines 207–220)

```python
def viewHistory(self):                                   # line 207
    if not os.path.exists(self.dataFile):                # line 208
        print("No history yet. Add and save some expenses first.")  # line 209
        return                                           # line 210
    try:                                                 # line 211
        with open(self.dataFile, "r", encoding="utf-8") as f:  # line 212
            content = f.read()                           # line 213
    except PermissionError:                              # line 214
        print(f"Could not read history: '{self.dataFile}' is open in another program.")  # line 215
        return                                           # line 216
    if not content.strip():                              # line 217
        print("No history yet. Add and save some expenses first.")  # line 218
    else:                                                # line 219
        print(content)                                   # line 220
```

### Lines 208–210: Check if History File Exists
- If `data/expenses.txt` doesn't exist, there's no history to show.

### Lines 211–216: Read the Entire File
- `f.read()` reads the **entire** file content as a single string.
- **Why `read()` and not line-by-line?** Because we just want to dump the whole file to the screen.
- PermissionError handling as usual.

### Lines 217–220: Display or Say Empty
- `content.strip()` removes whitespace. If the result is empty (`""` is falsy), the file exists but is empty.
- Otherwise, `print(content)` outputs the entire file contents to the console.

---

## 11. Save to File — `saveExpenseData` (Lines 221–274)

This is the most complex function. It creates a **formatted record** and appends it to the history file.

### Getting ID, Date, Time (Lines 222–225)

```python
    recordId = self.getNextId()                          # line 222
    time_tuple = time.localtime()                        # line 223
    date = time.strftime("%m/%d/%Y", time_tuple)         # line 224
    timee = time.strftime("%I:%M %p", time_tuple)        # line 225
```

#### Line 222: Get Record ID
- Calls `getNextId()` which reads the last saved ID and adds 1.

#### Line 223: `time.localtime()`
- Returns the **current date and time** as a `time.struct_time` object — a named tuple containing year, month, day, hour, minute, second, etc.

#### Line 224: `time.strftime("%m/%d/%Y", time_tuple)`
- **`strftime`** = "**str**ing **f**ormat **time**"
- Format codes:
  - `%m` — month as a zero-padded number (01–12)
  - `%d` — day of month (01–31)
  - `%Y` — year with century (2026)
- **Result:** `"07/29/2026"`

#### Line 225: `time.strftime("%I:%M %p", time_tuple)`
- Format codes:
  - `%I` — hour (01–12)
  - `%M` — minute (00–59)
  - `%p` — AM or PM
- **Result:** `"02:30 PM"`

**Why `timee` not `time`?** Because `time` is already the name of the imported module. Using `time` as a variable would **shadow** (override) the module, causing errors if you tried to use `time.localtime()` later.

---

### Calculating Statistics (Lines 229–234)

```python
    values = list(self.expenses.values())                # line 229
    nonZeroValues = [v for v in values if v > 0]         # line 230
    total = np.sum(values)                               # line 231
    average = np.mean(nonZeroValues) if nonZeroValues else 0  # line 232
    maximum = np.max(nonZeroValues) if nonZeroValues else 0   # line 233
    minimum = np.min(nonZeroValues) if nonZeroValues else 0   # line 234
```

- Same calculations as `expenseDetails`.
- **Ternary expressions** (lines 232–234): `value_if_true if condition else value_if_false`
  - `np.mean(nonZeroValues) if nonZeroValues else 0` means: if there are non-zero values, calculate the mean; otherwise, use 0.

---

### Building the Record String (Lines 235–257)

```python
    lines = [                                           # line 235
        "=" * width,                                    # line 236
        f"| {'Record ID : ' + str(recordId):<{width - 4}} |",  # line 237
        f"| {'Date      : ' + date:<{width - 4}} |",          # line 238
        f"| {'Time      : ' + timee:<{width - 4}} |",         # line 239
        f"| {'Name      : ' + self.name:<{width - 4}} |",     # line 240
        "-" * width,                                    # line 241
        f"| {'Expense Summary':^{width - 4}} |",        # line 242
        "-" * width,                                    # line 243
        f"| {'1. Food':<25} : {self.expenses['food']:<18,.2f} |",  # line 244
        ... (similar for other categories)              # lines 245-250
        "|" + "-" * (width - 2) + "|",                  # line 251
        f"| {'Total Expense':<25} : \u09f3 {total:<16,.2f} |",     # line 252
        f"| {'Average Expense':<25} : \u09f3 {average:<16,.2f} |",  # line 253
        f"| {'Maximum Expense':<25} : \u09f3 {maximum:<16,.2f} |",  # line 254
        f"| {'Minimum Expense':<25} : \u09f3 {minimum:<16,.2f} |",  # line 255
        "=" * width,                                    # line 256
        "",                                             # line 257
    ]
```

- **`lines`** is a **list of strings**, each representing a line to be written to the file.
- **Line 236:** Top border made of `=` signs.
- **Lines 237–240:** Header with ID, Date, Time, Name. Left-aligned within 46 chars.
- **Line 241:** Separator with `-`.
- **Line 242:** Centered "Expense Summary" title.
- **Line 243:** Another separator.
- **Lines 244–250:** Each category, left-aligned label 25 chars, right-aligned amount 18 chars.
- **Line 251:** Inner separator.
- **Lines 252–255:** Statistics.
- **Line 256:** Bottom border of `=`.
- **Line 257:** Empty string (creates a blank line between records).

**Note:** The categories here don't include the ৳ symbol (unlike `expenseDetails`). This is **inconsistent** — a bug in formatting.

---

### Safe File Writing (Lines 258–272)

```python
    tempFile = self.dataFile + ".tmp"                    # line 258
    try:                                                 # line 259
        oldContent = ""                                  # line 260
        if os.path.exists(self.dataFile):                # line 261
            with open(self.dataFile, "r", encoding="utf-8") as f:  # line 262
                oldContent = f.read()                    # line 263
        with open(tempFile, "w", encoding="utf-8") as f:  # line 264
            f.write(oldContent + "\n".join(lines) + "\n")  # line 265
        os.replace(tempFile, self.dataFile)              # line 266
    except PermissionError:                              # line 267
        print(f"Could not save: '{self.dataFile}' is open in another program. Please close it and try again.")  # line 268
        return                                           # line 269
    except OSError as e:                                 # line 270
        print(f"Could not save record: {e}")              # line 271
        return                                           # line 272
```

#### Line 258: Temporary File
```python
tempFile = self.dataFile + ".tmp"
```
- Creates a path like `data/expenses.txt.tmp`.
- **Why a temp file?** This is a **safe write** pattern:

#### Lines 260–263: Read Existing Content
```python
oldContent = ""
if os.path.exists(self.dataFile):
    with open(self.dataFile, "r", encoding="utf-8") as f:
        oldContent = f.read()
```
- If the history file already exists, read all its content.
- **Why read it?** Because we're **appending** — we want the new record to go **after** all existing records, not replace them.

#### Lines 264–265: Write to Temp File
```python
with open(tempFile, "w", encoding="utf-8") as f:
    f.write(oldContent + "\n".join(lines) + "\n")
```
- **`"\n".join(lines)`** — Joins all strings in the `lines` list with newline characters between them. This creates one big string.
- So we write: old content + new record + trailing newline.

#### Line 266: Atomic Replace
```python
os.replace(tempFile, self.dataFile)
```
- **`os.replace()`** atomically replaces the destination file with the source file.
- **Why not just write directly to `self.dataFile`?** Because if the program crashes mid-write, `data/expenses.txt` would be **corrupted** — half-written. With the temp file approach:
  1. Write to temp file (if crash happens here, original file is safe)
  2. Only after successful write, replace the original with the temp file (this is **atomic** — it either fully succeeds or fully fails)

#### Lines 267–272: Error Handling
- `PermissionError` — file locked by another program.
- `OSError as e` — catches other OS-level errors (disk full, path too long, etc.) and shows the actual error message.

---

### Finalize (Lines 273–274)

```python
    self.saveNextId(recordId)                             # line 273
    print(f"\n\u2713 Record saved as ID {recordId} in '{self.dataFile}'")  # line 274
```

- **Line 273:** Save the used ID so the next record gets a new number.
- **Line 274:** Success message with a checkmark (`\u2713` = ✓) and the record ID.

---

## 12. Main Application Loop — `run` (Lines 276–303)

```python
def run(self):                                           # line 276
    line_width = 50                                      # line 277
    print("-" * line_width)                              # line 278
    print(f"| {'Welcome to your personal expense tracker!':<{line_width - 4}} |")  # line 279
```

### Lines 278–279: Welcome Banner
- Prints a bordered welcome message.

---

### Lines 280–285: Date & Time

```python
    time_tuple = time.localtime()                        # line 280
    date = time.strftime("%m/%d/%Y", time_tuple)         # line 281
    timee = time.strftime("%I:%M %p", time_tuple)        # line 282
    print(f"| {'Todays Date : ' + date:<{line_width - 4}} |")  # line 283
    print(f"| {'Todays Time : ' + timee:<{line_width - 4}} |")  # line 284
    print("-" * line_width)                              # line 285
```

- Shows the current date and time when the program started.
- **Note:** `time_tuple` is fetched **once** here and also again in `saveExpenseData`. If the program runs for hours, the save time could be different — this is actually correct behavior (you want the save time, not the start time).

---

### Getting User Name (Lines 286–288)

```python
    self.name = input("\nEnter your name: ").strip()     # line 286
    print(f"\nWelcome, {self.name}!")                    # line 287
    print("-" * line_width)                              # line 288
```

- Prompts for the user's name and stores it in `self.name`.
- **`self.name`** was initialized as `""` in `__init__`. Now it gets the real value.
- **Why store as an attribute?** So `saveExpenseData` can access it (`self.name` in the record header).

---

### The Main Menu Loop (Lines 289–303)

```python
    while True:                                          # line 289
        print("\n1 -> Add Expenses")                     # line 290
        print("2 -> View History")                       # line 291
        print("0 -> Exit")                               # line 292
        choice = input("Enter your choice: ").strip()    # line 293
        if choice == "1":                                # line 294
            self.showMenu()                              # line 295
            self.addExpense()                            # line 296
        elif choice == "2":                              # line 297
            self.viewHistory()                           # line 298
        elif choice == "0":                              # line 299
            print("Goodbye!")                            # line 300
            break                                        # line 301
        else:                                            # line 302
            print("Please enter 0, 1, or 2.")            # line 303
```

#### How this loop works:

1. **Display options** — Add Expenses (1), View History (2), Exit (0)
2. **Get user choice**
3. **Route to the correct function:**
   - `"1"` → Show category menu, then run `addExpense()`
   - `"2"` → Run `viewHistory()`
   - `"0"` → Print goodbye and `break` (exit the loop, ending the program)
   - Anything else → Show error and loop again

#### Important Design Note:
- `showMenu()` and `addExpense()` are called **every time** the user picks option 1, even if they already chose a category and want to add more. This is fine — `addExpense()` starts its own inner loop for multiple entries.
- After `addExpense()` completes (user typed `0` and chose not to update), control returns to this main loop, where the user can add more, view history, or exit.
- **Bug:** After `addExpense()`, if the user had previously added expenses (before this invocation), any updates they made would be added to the existing `self.expenses` dictionary. But when they enter `addExpense` again, the dictionary still has the old values from the previous session plus any new additions. This is actually correct behavior — it's a running tally.

---

## 13. Entry Point — `main()` & `if __name__ == "__main__"` (Lines 305–312)

```python
def main():                                              # line 305
    tracker = ExpenseTracker()                           # line 306
    try:                                                 # line 307
        tracker.run()                                    # line 308
    except KeyboardInterrupt:                            # line 309
        print("\n\nInterrupted by user. Goodbye!")       # line 310
                                                         # line 311
if __name__ == "__main__":                               # line 311
    main()                                               # line 312
```

### Line 306: Create the Tracker Object
```python
tracker = ExpenseTracker()
```
- **`ExpenseTracker()`** calls the `__init__` constructor.
- This creates an object with:
  - `name = ""`
  - `expenses` dictionary (all zeros)
  - `expenseCategory` dictionary (number-to-name mapping)
  - File paths set
  - Loaded previous session data (if available)

### Lines 307–310: Run with Error Protection
```python
try:
    tracker.run()
except KeyboardInterrupt:
    print("\n\nInterrupted by user. Goodbye!")
```
- **`KeyboardInterrupt`** is raised when the user presses `Ctrl+C`.
- Without this `try/except`, pressing `Ctrl+C` would show an ugly traceback error.
- With it, the program exits gracefully with a friendly message.

### Lines 311–312: The Python Entry Point Idiom

```python
if __name__ == "__main__":
    main()
```

#### What is `__name__`?
- `__name__` is a **special built-in variable** that Python sets automatically.
- When you run a Python file **directly** (like `python main.py`), Python sets `__name__` to `"__main__"`.
- When the file is **imported** by another file (like `import main`), `__name__` is set to the module's name (`"main"`).

#### Why is this check needed?
- **Protection on import:** If someone writes `import main` in another Python file, `main()` won't automatically run — it only runs when `main.py` is the **entry point** of the program.
- **Good practice:** It allows the file to be both used as a script (`python main.py`) and imported as a module without side effects.

---

## 14. Complete Workflow Summary

Here's the **full flow** of the program from start to finish:

```
┌─────────────────────────────────────────────────────────────────────┐
│                        PROGRAM START                                │
│              python main.py (or python expense_tracker.py)          │
└─────────────────────────────────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────┐
│                    1.  ExpenseTracker.__init__()                    │
│                                                                     │
│    • Initialize name = ""                                           │
│    • Create expenses dict with 9 categories (all set to 0)         │
│    • Create expenseCategory mapping (number → name)                 │
│    • Set file paths (data/expenses.txt, data/last_id.txt,           │
│      data/current.txt)                                              │
│    • Create data/ folder if it doesn't exist                        │
│    • Load previously saved current expenses from current.txt        │
└─────────────────────────────────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────┐
│                       2.  tracker.run()                             │
│                                                                     │
│    • Show welcome banner with date/time                             │
│    • Ask user for name → stored in self.name                        │
│    • Enter MAIN LOOP:                                               │
│                                                                     │
│        ┌───────────────────────────────────────────────┐            │
│        │  Main Menu Options:                            │            │
│        │  1 → Add Expenses                              │            │
│        │  2 → View History                              │            │
│        │  0 → Exit                                      │            │
│        └───────────────────────────────────────────────┘            │
│                     │                    │                          │
│          ┌──────────┘                    └──────────┐               │
│          ▼                                           ▼              │
│  ┌──────────────────┐                     ┌──────────────────┐      │
│  │ Option 1:        │                     │ Option 2:        │      │
│  │ Add Expenses     │                     │ View History     │      │
│  │                  │                     │                  │      │
│  │  • Show category │                     │  • Read and      │      │
│  │    menu          │                     │    display       │      │
│  │  • Enter ADD     │                     │    expenses.txt  │      │
│  │    LOOP:         │                     │    file contents │      │
│  │    - Pick cat    │                     └──────────────────┘      │
│  │      (1-9)       │                                              │
│  │    - Enter amt   │                                              │
│  │    - Repeat or 0 │                                              │
│  │  • Ask: change?  │                                              │
│  │    - Yes → Update│                                              │
│  │    - No → Show   │                                              │
│  │      Summary &   │                                              │
│  │      Save to     │                                              │
│  │      history     │                                              │
│  └──────────────────┘                                              │
└─────────────────────────────────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────┐
│                  3.  SAVING A RECORD (saveExpenseData)              │
│                                                                     │
│    • Get next record ID (e.g., 1, 2, 3...)                         │
│    • Get current date & time                                        │
│    • Calculate total, average, max, min                             │
│    • Build formatted record string                                  │
│    • Safe-write: write to temp file → atomically replace original   │
│    • Save the used ID back to last_id.txt                           │
│    • Confirm to user with record ID                                 │
└─────────────────────────────────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────┐
│                       4.  PROGRAM END                               │
│                                                                     │
│    • User selects 0 from main menu                                  │
│    • "Goodbye!" message                                             │
│    • Program exits                                                  │
│    • (Note: current.txt is NOT auto-saved on exit — only           │
│      saved within addExpense after choosing not to update)          │
└─────────────────────────────────────────────────────────────────────┘
```

### Data File States

```
╔═══════════════════════════════════════════════════════════════╗
║                    FILE SYSTEM OVERVIEW                      ║
╠═══════════════════════════════════════════════════════════════╣
║                                                               ║
║  data/                                                        ║
║  ├── current.txt        ← Current session expenses            ║
║  │   Format:                                                  ║
║  │   food:250                                             ║
║  │   transportation:0                                     ║
║  │   ... (all 9 categories, one per line)                    ║
║  │                                                           ║
║  ├── expenses.txt       ← History of all saved records       ║
║  │   Format:                                                  ║
║  │   ==================================================      ║
║  │   | Record ID : 1                                  |      ║
║  │   | Date      : 07/29/2026                        |      ║
║  │   | Time      : 02:30 PM                          |      ║
║  │   | Name      : John                              |      ║
║  │   --------------------------------------------------      ║
║  │   |           Expense Summary                     |      ║
║  │   --------------------------------------------------      ║
║  │   | 1. Food                  : 250.00             |      ║
║  │   | ...                                            |      ║
║  │   | Total Expense           : 250.00              |      ║
║  │   | Average Expense          : 250.00              |      ║
║  │   | Maximum Expense          : 250.00              |      ║
║  │   | Minimum Expense          : 250.00              |      ║
║  │   ==================================================      ║
║  │                                                           ║
║  ├── last_id.txt        ← Last used record ID (just a number)║
║  │   Example: 1                                              ║
║  │                                                           ║
╚═══════════════════════════════════════════════════════════════╝
```

---

## 15. Glossary of Key Concepts

### Python Language Concepts

| Concept | Line(s) | Explanation |
|---------|---------|-------------|
| **Import** | 1–3 | Bringing external modules into your program |
| **Class** | 4 | A blueprint for creating objects |
| **`__init__`** | 5 | Constructor method — runs automatically when object is created |
| **`self`** | 5 | Reference to the current instance of the class |
| **Dictionary** | 7–17 | Key-value pairs: `{"key": value}` |
| **f-string** | 55 | Formatted string: `f"text {variable}"` |
| **String multiplication** | 94 | `"-" * 10` → `"----------"` |
| **`.strip()`** | 40 | Removes leading/trailing whitespace |
| **`.lower()`** | 124 | Converts to lowercase |
| **`.partition()`** | 43 | Splits string at a separator into 3 parts |
| **`with` statement** | 38 | Context manager — auto-closes files |
| **`try/except`** | 37 | Error handling — catch and handle exceptions |
| **List comprehension** | 198 | Compact loop to create a list: `[x for x in list if condition]` |
| **Generator expression** | 55 | Like a list comprehension but lazy (on-demand) |
| **`if __name__ == "__main__"`** | 311 | Guard that runs code only when file is executed directly |
| **Ternary operator** | 232 | `x if condition else y` — inline if-else |

### Programming Patterns Used

| Pattern | Where | Why |
|---------|-------|-----|
| **Infinite loop with `break`** | Lines 86, 123, 139, 289 | Keep asking until user decides to stop |
| **Input validation loop** | Lines 88–113 | Don't proceed until valid input received |
| **Safe file write** | Lines 258–266 | Write to temp file then atomically replace to avoid corruption |
| **Persistence** | `loadCurrentExpenses`, `saveCurrentExpenses` | Save state so data survives program restarts |
| **Menu-driven interface** | `run`, `showMenu` | Simple CLI navigation pattern |

### Data Flow Summary

```
User Input
    │
    ▼
addExpense() / updateExpense()
    │
    ├──► Updates self.expenses dictionary (in-memory)
    │
    ├──► saveCurrentExpenses() → writes to data/current.txt (for persistence)
    │
    └──► After user confirms "no changes":
            │
            ├──► expenseDetails() → shows summary on screen
            │
            └──► saveExpenseData() → appends formatted record to data/expenses.txt
                    │
                    └──► Updates data/last_id.txt with used ID
```

---

### Potential Bugs / Design Flaws (for Discussion)

1. **No automatic save on exit** — If the user presses `Ctrl+C` or selects "Exit" from the main menu, the current expenses in `self.expenses` are lost unless they went through the full "Add → No changes" flow.

2. **Update action validation** — In `updateExpense`, if the user types something other than "add", "a", "delete", or "d", it defaults to "replace" without warning.

3. **NumPy overkill** — The code imports NumPy just for `sum`, `mean`, `max`, `min`. Python built-ins `sum()`, `max()`, `min()` could do the same, and `statistics.mean()` could replace `np.mean()`.

4. **File path hardcoding** — Paths are relative (`"data/..."`), which means the program must be run from the directory that contains the `data/` folder.

5. **Inconsistent currency symbol** — `expenseDetails` uses ৳ symbol, but `saveExpenseData` does not include the symbol in the saved record.

6. **`current.txt` not saved on exit** — If user adds expenses but exits without going through the "no changes" flow, `current.txt` won't have the latest state.

---

> **End of Explanation**
