---
title:
description: Your first Python program - print output, arguments, separators, and basic script syntax
---

# Hello World

A minimal Python program prints output to the console. This lesson focuses on `print()` basics so you can run and verify your first scripts quickly.

## The print() Function

`print()` sends text to standard output. It accepts one or more arguments and converts them to strings before writing.

```python
print("Hello, World!")
```

**Output:** `Hello, World!`

**Multiple arguments:** Arguments are separated by spaces by default. The `sep` parameter controls the separator.

```python
print("Hello", "World", "!")
```

**Output:** `Hello World !`

```python
print("2", "4", "6", sep="-")
```

**Output:** `2-4-6`

**End parameter:** The `end` parameter controls what is printed after the last argument. The default is a newline (`\n`).

```python
print("Line one", end="")
print("Line two")
```

**Output:** `Line oneLine two`

**No arguments:** `print()` with no arguments prints a single newline.

```python
print()
```

## Common Patterns

**Minimal executable script:**

```python
print("Hello, World!")
```

**Multiple values in one line:**

```python
name = "Alice"
score = 82
print("Name:", name, "Score:", score)
```

**Custom separator for compact output:**

```python
print("2", "4", "6", sep="-")
```

## Python Syntax Basics

**Indentation:** Python uses indentation to define blocks. Four spaces per level is conventional. Mixing tabs and spaces can cause errors.

**Colon:** A colon (`:`) starts a block. The block must be indented.

```python
if True:
    print("indented block")
```

**Comments:** Lines starting with `#` are comments and are ignored.

```python
# This is a comment
print("Hello")  # inline comment
```

## Tricky Points

### Multiple arguments are converted to strings

`print()` stringifies each argument. You can pass numbers, booleans, and other objects directly.

### Separator affects readability

Using a custom `sep` is useful, but overusing separators can make logs harder to scan.

### `print()` adds a newline by default

`print("x")` ends with `\n`. Use `end=""` when you need to continue on the same line.

### Indentation errors

Any block statement in Python must be indented consistently, or `IndentationError` is raised.

## Interview Questions

### How do you pass multiple values to `print()`?

Pass them as separate arguments: `print("a", "b", "c")`. They are separated by spaces by default; use `sep` to change this.

### What is the difference between `sep` and `end` in `print()`?

`sep` controls text between arguments. `end` controls what is printed after the last argument.

### What is the default value of `end` in `print()`?

A newline character (`\n`). Use `end=""` to suppress the trailing newline.

### What does `print()` do with non-string values?

It calls string conversion and prints the result. For example, `print(2, True, [4, 6])` is valid.