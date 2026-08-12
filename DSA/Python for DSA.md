---
title: "Python for DSA"
source: "https://algomaster.io/learn/dsa/python-crash-course"
author:
  - "[[Ashish Pratap Singh]]"
published: 2026-03-30
created: 2026-08-12
description: "Python for DSA explained with clear examples, visuals, and practice questions in AlgoMaster's Data Structures and Algorithms course."
tags:
  - "clippings"
---
Listen to this chapter

[Unlock Audio](https://algomaster.io/premium)

This chapter is a focused crash course on the Python features that come up repeatedly in DSA and preparing for coding interviews. Instead of covering the entire language, we will concentrate only on the parts that matter for solving problems efficiently in interviews.

## Common Imports

On LeetCode, most imports are available automatically. But when writing Python locally or on some interview platforms, you need to know what to import. Here are the imports that cover 95% of DSA problems:

Python

Each of these modules serves a specific purpose in DSA:

| Module | What It Provides | DSA Use Case |
| --- | --- | --- |
| `collections` | `defaultdict`, `Counter`, `deque`, `OrderedDict` | Frequency counting, BFS queues, adjacency lists |
| `heapq` | Min-heap operations | Top-K elements, Dijkstra, merge-K-sorted |
| `bisect` | Binary search on sorted lists | Insertion point, sorted container operations |
| `functools` | `lru_cache`, `cache`, `cmp_to_key` | DP memoization, custom sorting |
| `itertools` | `combinations`, `permutations`, `product`, `accumulate` | Generating subsets, prefix sums |
| `math` | `inf`, `gcd`, `isqrt`, `ceil`, `floor` | Sentinel values, number theory |
| `typing` | Type hints | Code clarity on LeetCode |
| `sys` | `setrecursionlimit` | Deep recursion for DFS/trees |

One line is worth adding up front:

Python

Python's default recursion limit is 1000. Without this line, DFS on a graph with 100,000 nodes or a skewed binary tree raises a `RecursionError`. We will cover recursion in detail later.

There is also one third-party library available on LeetCode that provides sorted container data structures:

Python

This is not part of Python's standard library, but it is available on LeetCode and many interview platforms. We will cover it in the Sorted Containers section.

## Variables, Types, and Python's Integer Advantage

Python is a dynamically typed language. You do not declare types, you just assign values. The interpreter figures out the type at runtime:

Python

For DSA, a small set of types covers most problems:

| Type | Example | DSA Use Case |
| --- | --- | --- |
| `int` | `42`, `2**100` | Array indices, counters, any integer (no overflow!) |
| `float` | `3.14`, `float('inf')` | Sentinel values, rarely used otherwise |
| `bool` | `True`, `False` | Visited arrays, flags |
| `str` | `"hello"` | Immutable character sequences |
| `None` | `None` | Null equivalent, tree/linked list terminators |

Python integers have arbitrary precision, which is a big advantage for DSA. Python integers never overflow.

Python

This means you never need to worry about integer overflow in most DSA problems. The safe binary search midpoint formula `left + (right - left) // 2` is still good practice for clarity and habit, but technically unnecessary in Python because `(left + right) // 2` will never overflow.

### Floor Division vs True Division

This distinction matters:

Python

That last line is important. In Python, `-7 // 2` gives `-4` because floor division rounds toward negative infinity, not toward zero. If you need truncation toward zero, use `int(-7 / 2)` or `math.trunc(-7 / 2)`.

### The Ternary Expression

Python writes conditional expressions inline using `if` / `else`:

Python

### Multiple Assignment and Swap

Python supports multiple assignment, which is handy for DSA:

Python

The swap trick is particularly useful in partition-based algorithms and two-pointer problems where you constantly need to swap elements.

### Type Hints

Python supports optional type hints that make your code clearer on LeetCode:

Python

Type hints have no runtime effect. They are purely for readability. LeetCode uses them in function signatures, so they appear throughout this course.

### Booleans Are Integers

A quirk worth knowing: `bool` is a subclass of `int` in Python. `True` is `1` and `False` is `0`:

Python

This is useful for counting conditions:

Python

## Operators and Control Flow

Most operators in Python work as you would expect, but a few deserve special attention for DSA.

### Modular Arithmetic

The `%` operator in Python always returns a result with the same sign as the **divisor** (the right operand). This is convenient for DSA:

Python

This means you do not need the `((n % m) + m) % m` trick to force a positive modulo result.

Many problems ask you to return the result "modulo 10^9 + 7":

Python

### Bitwise Operators

Bitwise operations come up in several DSA patterns:

Python

Key bitwise operators:

| Operator | Symbol | DSA Use |
| --- | --- | --- |
| AND | `&` | Masking, checking if bit is set: `(n & (1 << i)) != 0` |
| OR | `\|` | Setting bits: `n \| (1 << i)` |
| XOR | `^` | Finding unique elements, toggling bits |
| NOT | `~` | Bit inversion (`~n` equals `-(n+1)` in Python) |
| Left shift | `<<` | Multiply by powers of 2: `1 << n` equals 2^n |
| Right shift | `>>` | Divide by powers of 2 |

A common bit manipulation pattern is checking and setting individual bits, which shows up in problems using bitmasks to represent subsets:

Python

Python also provides helpful built-in functions for bit operations:

Python

Python does not have an unsigned right shift operator. Since Python integers have arbitrary precision, there is no fixed bit width, so unsigned shift does not apply. For problems that specifically require unsigned right shift behavior (like reversing bits of a 32-bit integer), you need to mask with `& 0xFFFFFFFF` to simulate 32-bit unsigned behavior.

### Control Flow

Python offers several loop forms. Use each where it fits:

Python

**Use** `**enumerate()**` **for index-value pairs.** When you need both the index and the value, use `enumerate()` instead of `for i in range(len(nums))`. It is cleaner and less error-prone:

Python

### Short-Circuit Evaluation

Python uses the keywords `and` and `or` for boolean logic:

Python

Python's `or` has a useful idiom for default values:

Python

Be careful with this pattern when `0` or `""` are valid values. In those cases, use `x if x is not None else default`.

### The Walrus Operator:=

Introduced in Python 3.8, the walrus operator assigns and returns a value in a single expression. It can make some DSA patterns more concise:

Python

You do not need to use the walrus operator in interviews, but knowing it exists helps you read others' solutions.

## Functions and Pass-by-Object-Reference

In DSA problems, extracting logic into helper functions keeps the code clean. On LeetCode, your solution lives inside a class:

Python

You can also define nested functions, which is common for DFS/backtracking:

Python

Nested functions can access variables from the enclosing scope (like `results` and `nums` above). This is called a **closure** and it is convenient for DSA. It avoids passing extra parameters through recursive calls.

### Pass-by-Object-Reference

Python passes everything by object reference. This means:

- **Mutable objects** (lists, dicts, sets) can be modified in-place by the called function. The caller sees the changes.
- **Immutable objects** (int, str, tuple, bool) cannot be modified. Any "modification" creates a new object, and the caller's variable is unaffected.

Python

<svg id="mermaid-79zkgkzkfsg-1786527961961" width="100%" xmlns="http://www.w3.org/2000/svg" style="max-width: 827.1500244140625px;" viewBox="0 10 827.1500244140625 592" role="graphics-document document" aria-roledescription="flowchart-v2"><g><marker id="mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-pointEnd" viewBox="0 0 10 10" refX="5" refY="5" markerUnits="userSpaceOnUse" markerWidth="8" markerHeight="8" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-pointStart" viewBox="0 0 10 10" refX="4.5" refY="5" markerUnits="userSpaceOnUse" markerWidth="8" markerHeight="8" orient="auto"><path d="M 0 5 L 10 10 L 10 0 z" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-circleEnd" viewBox="0 0 10 10" refX="11" refY="5" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><circle cx="5" cy="5" r="5" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></circle></marker><marker id="mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-circleStart" viewBox="0 0 10 10" refX="-1" refY="5" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><circle cx="5" cy="5" r="5" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></circle></marker><marker id="mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-crossEnd" viewBox="0 0 11 11" refX="12" refY="5.2" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><path d="M 1,1 l 9,9 M 10,1 l -9,9" style="stroke-width: 2px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-crossStart" viewBox="0 0 11 11" refX="-1" refY="5.2" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><path d="M 1,1 l 9,9 M 10,1 l -9,9" style="stroke-width: 2px; stroke-dasharray: 1px, 0px;"></path></marker><g><g></g><g></g><g></g><g><g transform="translate(0, 20)"><g><g id="Immutable" data-look="classic"><rect style="" x="8" y="-2" width="372.8666687011719" height="576"></rect><g transform="translate(100.2750015258789, 8)"><foreignObject width="188.31666564941406" height="24"><p>Immutable (int, str, tuple)</p></foreignObject></g></g></g><g><path d="M194.433,119.5L194.433,125.75C194.433,132,194.433,144.5,194.433,156.333C194.433,168.167,194.433,179.333,194.433,184.917L194.433,190.5" id="L_E_F_0" style=";" data-edge="true" data-et="edge" data-id="L_E_F_0" data-points="W3sieCI6MTk0LjQzMzMzNDM1MDU4NTk0LCJ5IjoxMTkuNX0seyJ4IjoxOTQuNDMzMzM0MzUwNTg1OTQsInkiOjE1N30seyJ4IjoxOTQuNDMzMzM0MzUwNTg1OTQsInkiOjE5NC41fV0=" marker-end="url(#mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M194.433,258.5L194.433,264.75C194.433,271,194.433,283.5,194.433,295.333C194.433,307.167,194.433,318.333,194.433,323.917L194.433,329.5" id="L_F_G_0" style=";" data-edge="true" data-et="edge" data-id="L_F_G_0" data-points="W3sieCI6MTk0LjQzMzMzNDM1MDU4NTk0LCJ5IjoyNTguNX0seyJ4IjoxOTQuNDMzMzM0MzUwNTg1OTQsInkiOjI5Nn0seyJ4IjoxOTQuNDMzMzM0MzUwNTg1OTQsInkiOjMzMy41fV0=" marker-end="url(#mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M194.433,397.5L194.433,403.75C194.433,410,194.433,422.5,194.433,434.333C194.433,446.167,194.433,457.333,194.433,462.917L194.433,468.5" id="L_G_H_0" style=";" data-edge="true" data-et="edge" data-id="L_G_H_0" data-points="W3sieCI6MTk0LjQzMzMzNDM1MDU4NTk0LCJ5IjozOTcuNX0seyJ4IjoxOTQuNDMzMzM0MzUwNTg1OTQsInkiOjQzNX0seyJ4IjoxOTQuNDMzMzM0MzUwNTg1OTQsInkiOjQ3Mi41fV0=" marker-end="url(#mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path></g><g><g><g data-id="L_E_F_0" transform="translate(0, 0)"></g></g><g><g data-id="L_F_G_0" transform="translate(0, 0)"></g></g><g><g data-id="L_G_H_0" transform="translate(0, 0)"></g></g></g><g><g id="flowchart-E-6" transform="translate(194.43333435058594, 87.5)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-101.24166870117188" y="-32" width="202.48333740234375" height="64"></rect><g style="color:#000 !important" transform="translate(-61.241668701171875, -12)"><rect></rect><foreignObject width="122.48333740234375" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>caller: count = 5</p></span></div></foreignObject></g></g><g id="flowchart-F-7" transform="translate(194.43333435058594, 226.5)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-151.43333435058594" y="-32" width="302.8666687011719" height="64"></rect><g style="color:#000 !important" transform="translate(-111.43333435058594, -12)"><rect></rect><foreignObject width="222.86666870117188" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>function: x points to SAME int</p></span></div></foreignObject></g></g><g id="flowchart-G-9" transform="translate(194.43333435058594, 365.5)"><rect style="fill:#ffa94d !important;stroke:#000 !important" x="-132.76667022705078" y="-32" width="265.53334045410156" height="64"></rect><g style="color:#000 !important" transform="translate(-92.76667022705078, -12)"><rect></rect><foreignObject width="185.53334045410156" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>x += 1 creates NEW int 6</p></span></div></foreignObject></g></g><g id="flowchart-H-11" transform="translate(194.43333435058594, 504.5)"><rect style="fill:#ff8787 !important;stroke:#000 !important" x="-102.6500015258789" y="-32" width="205.3000030517578" height="64"></rect><g style="color:#000 !important" transform="translate(-62.650001525878906, -12)"><rect></rect><foreignObject width="125.30000305175781" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>caller still sees 5</p></span></div></foreignObject></g></g></g></g><g transform="translate(422.8666687011719, 20)"><g><g id="Mutable" data-look="classic"><rect style="" x="8" y="-2" width="388.2833251953125" height="576"></rect><g transform="translate(118.06666564941406, 8)"><foreignObject width="168.14999389648438" height="24"><p>Mutable (list, dict, set)</p></foreignObject></g></g></g><g><path d="M202.142,119.5L202.142,125.75C202.142,132,202.142,144.5,202.142,156.333C202.142,168.167,202.142,179.333,202.142,184.917L202.142,190.5" id="L_A_B_0" style=";" data-edge="true" data-et="edge" data-id="L_A_B_0" data-points="W3sieCI6MjAyLjE0MTY2MjU5NzY1NjI1LCJ5IjoxMTkuNX0seyJ4IjoyMDIuMTQxNjYyNTk3NjU2MjUsInkiOjE1N30seyJ4IjoyMDIuMTQxNjYyNTk3NjU2MjUsInkiOjE5NC41fV0=" marker-end="url(#mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M202.142,258.5L202.142,264.75C202.142,271,202.142,283.5,202.142,295.333C202.142,307.167,202.142,318.333,202.142,323.917L202.142,329.5" id="L_B_C_0" style=";" data-edge="true" data-et="edge" data-id="L_B_C_0" data-points="W3sieCI6MjAyLjE0MTY2MjU5NzY1NjI1LCJ5IjoyNTguNX0seyJ4IjoyMDIuMTQxNjYyNTk3NjU2MjUsInkiOjI5Nn0seyJ4IjoyMDIuMTQxNjYyNTk3NjU2MjUsInkiOjMzMy41fV0=" marker-end="url(#mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M202.142,397.5L202.142,403.75C202.142,410,202.142,422.5,202.142,434.333C202.142,446.167,202.142,457.333,202.142,462.917L202.142,468.5" id="L_C_D_0" style=";" data-edge="true" data-et="edge" data-id="L_C_D_0" data-points="W3sieCI6MjAyLjE0MTY2MjU5NzY1NjI1LCJ5IjozOTcuNX0seyJ4IjoyMDIuMTQxNjYyNTk3NjU2MjUsInkiOjQzNX0seyJ4IjoyMDIuMTQxNjYyNTk3NjU2MjUsInkiOjQ3Mi41fV0=" marker-end="url(#mermaid-79zkgkzkfsg-1786527961961_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path></g><g><g><g data-id="L_A_B_0" transform="translate(0, 0)"></g></g><g><g data-id="L_B_C_0" transform="translate(0, 0)"></g></g><g><g data-id="L_C_D_0" transform="translate(0, 0)"></g></g></g><g><g id="flowchart-A-0" transform="translate(202.14166259765625, 87.5)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-123.75833129882812" y="-32" width="247.51666259765625" height="64"></rect><g style="color:#000 !important" transform="translate(-83.75833129882812, -12)"><rect></rect><foreignObject width="167.51666259765625" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>caller: nums = [1, 2, 3]</p></span></div></foreignObject></g></g><g id="flowchart-B-1" transform="translate(202.14166259765625, 226.5)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-159.14167022705078" y="-32" width="318.28334045410156" height="64"></rect><g style="color:#000 !important" transform="translate(-119.14167022705078, -12)"><rect></rect><foreignObject width="238.28334045410156" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>function: arr points to SAME list</p></span></div></foreignObject></g></g><g id="flowchart-C-3" transform="translate(202.14166259765625, 365.5)"><rect style="fill:#ffa94d !important;stroke:#000 !important" x="-96.7750015258789" y="-32" width="193.5500030517578" height="64"></rect><g style="color:#000 !important" transform="translate(-56.775001525878906, -12)"><rect></rect><foreignObject width="113.55000305175781" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>arr.append(99)</p></span></div></foreignObject></g></g><g id="flowchart-D-5" transform="translate(202.14166259765625, 504.5)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-125.29166412353516" y="-32" width="250.5833282470703" height="64"></rect><g style="color:#000 !important" transform="translate(-85.29166412353516, -12)"><rect></rect><foreignObject width="170.5833282470703" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>caller sees [1, 2, 3, 99]</p></span></div></foreignObject></g></g></g></g></g></g></g></svg>

This distinction matters in recursive and backtracking problems. When you pass a list to a recursive call and add elements to it, those additions are visible to the caller. That is why the backtracking pattern works, adding and removing from a shared list as you explore different branches:

Python

The `path[:]` when saving results creates a copy. If you wrote `results.append(path)` instead, every entry in `results` would be a reference to the same list, and they would all end up empty after backtracking unwinds. This is a common bug in backtracking solutions.

### The Mutable Default Argument Pitfall

This is a Python-specific trap to watch for:

Python

### Modifying Integers in Nested Functions

If you need a nested function to modify an integer from the enclosing scope, you need the `nonlocal` keyword:

Python

Without `nonlocal`, `count += 1` would create a local variable instead of modifying the outer one. Alternatively, you can use a mutable container like a list `[0]` to avoid `nonlocal`, but that is less readable.

## Lists as Arrays

Lists are the foundational data structure in Python and the starting point for almost every DSA problem.

Python

### The 2D Array Trap

Watch for this pattern:

Python

The `[[0] * cols] * rows` pattern is a Python-specific gotcha. Each row is a reference to the same list, so modifying one row modifies all of them. Always use a list comprehension for 2D arrays. This bug indicates a misunderstanding of Python's reference semantics.

### Key List Operations

| Operation | Syntax | Time | DSA Use |
| --- | --- | --- | --- |
| Append | `lst.append(x)` | O(1) amortized | Building result lists |
| Pop last | `lst.pop()` | O(1) | Stack operations |
| Pop at index | `lst.pop(i)` | O(n) | Avoid in tight loops |
| Insert at index | `lst.insert(i, x)` | O(n) | Avoid in tight loops |
| Access | `lst[i]` | O(1) | Random access |
| Update | `lst[i] = x` | O(1) | In-place modification |
| Length | `len(lst)` | O(1) | Loop bounds |
| Contains | `x in lst` | O(n) | Use set for O(1) |
| Reverse in-place | `lst.reverse()` | O(n) | Reverse array |
| Reversed copy | `lst[::-1]` | O(n) | New reversed list |
| Sort in-place | `lst.sort()` | O(n log n) | Sorting |
| Sorted copy | `sorted(lst)` | O(n log n) | New sorted list |
| Extend | `lst.extend(other)` | O(k) | Concatenate lists |
| Count | `lst.count(x)` | O(n) | Count occurrences |
| Index | `lst.index(x)` | O(n) | Find first occurrence |
| Clear | `lst.clear()` | O(1) | Reset list |

### Negative Indexing

Python's negative indexing is one of its most useful features for DSA:

Python

This comes up constantly. Peeking at the top of a stack? `stack[-1]`. Getting the last character of a string? `s[-1]`. Accessing the last row of a matrix? `matrix[-1]`.

### Slicing

Slicing creates a new list from a portion of an existing one. The syntax is `lst[start:stop:step]`, where `start` is inclusive and `stop` is exclusive:

Python

Slicing is particularly useful for:

- **Copying lists:** `copy = lst[:]` or `copy = list(lst)`
- **Reversing:** `reversed_list = lst[::-1]`
- **Taking subarrays:** `subarray = lst[i:j]`

Be aware that slicing creates a **new list**, so it costs O(k) time and space where k is the slice size. Do not slice inside a tight loop if you can avoid it.

### List Comprehensions

List comprehensions are one of Python's most useful features for writing concise DSA code:

Python

### 2D Arrays and the Directions Pattern

2D arrays appear in every matrix problem (BFS on grid, DP tables, etc.):

Python

For DP problems, you often need a table with one extra row and column for the base case:

Python

The 4-directional neighbor pattern is common in matrix problems:

Python

For 8-directional movement (including diagonals), add the four diagonal pairs: `(-1,-1), (-1,1), (1,-1), (1,1)`.

<svg id="mermaid-zg8iip8yfim-1786527961964" width="100%" xmlns="http://www.w3.org/2000/svg" style="max-width: 765.7999877929688px;" viewBox="0 10 765.7999877929688 268" role="graphics-document document" aria-roledescription="flowchart-v2"><g><marker id="mermaid-zg8iip8yfim-1786527961964_flowchart-v2-pointEnd" viewBox="0 0 10 10" refX="5" refY="5" markerUnits="userSpaceOnUse" markerWidth="8" markerHeight="8" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-zg8iip8yfim-1786527961964_flowchart-v2-pointStart" viewBox="0 0 10 10" refX="4.5" refY="5" markerUnits="userSpaceOnUse" markerWidth="8" markerHeight="8" orient="auto"><path d="M 0 5 L 10 10 L 10 0 z" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-zg8iip8yfim-1786527961964_flowchart-v2-circleEnd" viewBox="0 0 10 10" refX="11" refY="5" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><circle cx="5" cy="5" r="5" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></circle></marker><marker id="mermaid-zg8iip8yfim-1786527961964_flowchart-v2-circleStart" viewBox="0 0 10 10" refX="-1" refY="5" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><circle cx="5" cy="5" r="5" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></circle></marker><marker id="mermaid-zg8iip8yfim-1786527961964_flowchart-v2-crossEnd" viewBox="0 0 11 11" refX="12" refY="5.2" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><path d="M 1,1 l 9,9 M 10,1 l -9,9" style="stroke-width: 2px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-zg8iip8yfim-1786527961964_flowchart-v2-crossStart" viewBox="0 0 11 11" refX="-1" refY="5.2" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><path d="M 1,1 l 9,9 M 10,1 l -9,9" style="stroke-width: 2px; stroke-dasharray: 1px, 0px;"></path></marker><g><g><g id="Matrix" data-look="classic"><rect style="" x="8" y="136" width="749.7999839782715" height="134"></rect><g transform="translate(337.8333263397217, 146)"><foreignObject width="90.13333129882812" height="24"><p>matrix[3][3]</p></foreignObject></g></g></g><g><path d="M123.521,106L123.521,110.167C123.521,114.333,123.521,122.667,123.521,131C123.521,139.333,123.521,147.667,151.783,157.925C180.045,168.184,236.57,180.368,264.832,186.46L293.094,192.552" id="L_UP_R1_0" style=";" data-edge="true" data-et="edge" data-id="L_UP_R1_0" data-points="W3sieCI6MTIzLjUyMDgzMjA2MTc2NzU4LCJ5IjoxMDZ9LHsieCI6MTIzLjUyMDgzMjA2MTc2NzU4LCJ5IjoxMzF9LHsieCI6MTIzLjUyMDgzMjA2MTc2NzU4LCJ5IjoxNTZ9LHsieCI6Mjk3LjAwNDE2MTgzNDcxNjgsInkiOjE5My4zOTUyNDc4NjcwODk4NH1d" marker-end="url(#mermaid-zg8iip8yfim-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M299.879,106L299.879,110.167C299.879,114.333,299.879,122.667,299.879,131C299.879,139.333,299.879,147.667,305.758,155.638C311.636,163.609,323.393,171.218,329.272,175.022L335.15,178.827" id="L_DOWN_R1_0" style=";" data-edge="true" data-et="edge" data-id="L_DOWN_R1_0" data-points="W3sieCI6Mjk5Ljg3OTE2MTgzNDcxNjgsInkiOjEwNn0seyJ4IjoyOTkuODc5MTYxODM0NzE2OCwieSI6MTMxfSx7IngiOjI5OS44NzkxNjE4MzQ3MTY4LCJ5IjoxNTZ9LHsieCI6MzM4LjUwODU0NjQ2MTEzODgsInkiOjE4MX1d" marker-end="url(#mermaid-zg8iip8yfim-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M476.029,106L476.029,110.167C476.029,114.333,476.029,122.667,476.029,131C476.029,139.333,476.029,147.667,470.151,155.638C464.272,163.609,452.515,171.218,446.636,175.022L440.758,178.827" id="L_LEFT_R1_0" style=";" data-edge="true" data-et="edge" data-id="L_LEFT_R1_0" data-points="W3sieCI6NDc2LjAyOTE1NTczMTIwMTIsInkiOjEwNn0seyJ4Ijo0NzYuMDI5MTU1NzMxMjAxMiwieSI6MTMxfSx7IngiOjQ3Ni4wMjkxNTU3MzEyMDEyLCJ5IjoxNTZ9LHsieCI6NDM3LjM5OTc3MTEwNDc3OTIsInkiOjE4MX1d" marker-end="url(#mermaid-zg8iip8yfim-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M651.971,106L651.971,110.167C651.971,114.333,651.971,122.667,651.971,131C651.971,139.333,651.971,147.667,623.778,157.92C595.585,168.173,539.2,180.347,511.007,186.433L482.814,192.52" id="L_RIGHT_R1_0" style=";" data-edge="true" data-et="edge" data-id="L_RIGHT_R1_0" data-points="W3sieCI6NjUxLjk3MDgyMTM4MDYxNTIsInkiOjEwNn0seyJ4Ijo2NTEuOTcwODIxMzgwNjE1MiwieSI6MTMxfSx7IngiOjY1MS45NzA4MjEzODA2MTUyLCJ5IjoxNTZ9LHsieCI6NDc4LjkwNDE1NTczMTIwMTIsInkiOjE5My4zNjQzMDgxNjUwODY5fV0=" marker-end="url(#mermaid-zg8iip8yfim-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path></g><g><g><g data-id="L_UP_R1_0" transform="translate(0, 0)"></g></g><g><g data-id="L_DOWN_R1_0" transform="translate(0, 0)"></g></g><g><g data-id="L_LEFT_R1_0" transform="translate(0, 0)"></g></g><g><g data-id="L_RIGHT_R1_0" transform="translate(0, 0)"></g></g></g><g><g id="flowchart-R0-0" transform="translate(138.7249984741211, 213)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-95.7249984741211" y="-32" width="191.4499969482422" height="64"></rect><g style="color:#000 !important" transform="translate(-55.724998474121094, -12)"><rect></rect><foreignObject width="111.44999694824219" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>[0,0] [0,1] [0,2]</p></span></div></foreignObject></g></g><g id="flowchart-R1-1" transform="translate(387.954158782959, 213)"><rect style="fill:#ffa94d !important;stroke:#000 !important" x="-90.94999694824219" y="-32" width="181.89999389648438" height="64"></rect><g style="color:#000 !important" transform="translate(-50.94999694824219, -12)"><rect></rect><foreignObject width="101.89999389648438" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>[1,0] [1,1] [1,2]</p></span></div></foreignObject></g></g><g id="flowchart-R2-2" transform="translate(626.9749870300293, 213)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-95.82499694824219" y="-32" width="191.64999389648438" height="64"></rect><g style="color:#000 !important" transform="translate(-55.82499694824219, -12)"><rect></rect><foreignObject width="111.64999389648438" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>[2,0] [2,1] [2,2]</p></span></div></foreignObject></g></g><g id="flowchart-UP-3" transform="translate(123.52083206176758, 62)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-62.375" y="-44" width="124.75" height="88"></rect><g style="color:#000 !important" transform="translate(-22.375, -24)"><rect></rect><foreignObject width="44.75" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Up<br>(-1, 0)</p></span></div></foreignObject></g></g><g id="flowchart-DOWN-4" transform="translate(299.8791618347168, 62)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-63.98332977294922" y="-44" width="127.96665954589844" height="88"></rect><g style="color:#000 !important" transform="translate(-23.98332977294922, -24)"><rect></rect><foreignObject width="47.96665954589844" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Down<br>(+1, 0)</p></span></div></foreignObject></g></g><g id="flowchart-LEFT-5" transform="translate(476.0291557312012, 62)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-62.166664123535156" y="-44" width="124.33332824707031" height="88"></rect><g style="color:#000 !important" transform="translate(-22.166664123535156, -24)"><rect></rect><foreignObject width="44.33332824707031" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Left<br>(0, -1)</p></span></div></foreignObject></g></g><g id="flowchart-RIGHT-6" transform="translate(651.9708213806152, 62)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-63.775001525878906" y="-44" width="127.55000305175781" height="88"></rect><g style="color:#000 !important" transform="translate(-23.775001525878906, -24)"><rect></rect><foreignObject width="47.55000305175781" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Right<br>(0, +1)</p></span></div></foreignObject></g></g></g></g></g></svg>

Tuple unpacking with `for dr, dc in directions` and the chained comparison `0 <= nr < rows` make grid traversal code compact and readable.

## Strings

Strings in Python are **immutable**. Every time you "modify" a string, Python creates a new object. This has a performance implication for DSA:

Python

### Essential String Methods

| Method | Example | DSA Use |
| --- | --- | --- |
| `s[i]` | `s[0]` | Access character (no `charAt` needed) |
| `len(s)` | `len(s)` | Length (built-in function, not method) |
| `s[a:b]` | `s[0:3]` | Substring via slicing |
| `s.split()` | `s.split(" ")` | Tokenize into list |
| `"sep".join(lst)` | `",".join(lst)` | Build string from list |
| `s.strip()` | `s.strip()` | Remove leading/trailing whitespace |
| `s.isalnum()` | `s.isalnum()` | Alphanumeric check (valid palindrome) |
| `s.isalpha()` | `s.isalpha()` | Letters only |
| `s.isdigit()` | `s.isdigit()` | Digits only |
| `s.lower()` | `s.lower()` | Lowercase conversion |
| `s.upper()` | `s.upper()` | Uppercase conversion |
| `s.startswith(p)` | `s.startswith("ab")` | Prefix check |
| `s.endswith(p)` | `s.endswith("ab")` | Suffix check |
| `s.find(sub)` | `s.find("ab")` | Find substring (-1 if not found) |
| `s.count(sub)` | `s.count("a")` | Count occurrences |
| `s.replace(old, new)` | `s.replace("a", "b")` | Replace all occurrences (returns new string) |
| `sub in s` | `"ab" in "abc"` | Substring check |

### Character Arithmetic with ord() and chr()

Python does not have a separate `char` type. Characters are just strings of length 1. To do arithmetic on characters (which is common in DSA), use `ord()` and `chr()`:

Python

The `ord(c) - ord('a')` pattern works because characters have numeric values. Subtracting `ord('a')` from a lowercase letter gives its zero-based position. This is how you build frequency arrays without a dictionary:

Python

This is faster and more memory-efficient than `Counter(s)` when you know the character set is limited to lowercase (or uppercase, or digits). However, for most interview problems, `Counter` is perfectly acceptable and more readable.

### String Comparison

Python's `==` operator compares string content, not references:

Python

Use `==` for string equality. The `is` operator checks object identity, which is rarely what you want for strings.

### Useful String Patterns

Python

## Dictionaries, Sets, and the Collections Module

Python's built-in dictionaries and sets, combined with the `collections` module, provide the data structures used in nearly every DSA problem. Choosing the right collection is often the difference between an O(n) and an O(n^2) solution.

<svg id="mermaid-i83vja02fkb-1786527961964" width="100%" xmlns="http://www.w3.org/2000/svg" style="max-width: 2258.14599609375px;" viewBox="0 10 2258.14599609375 494" role="graphics-document document" aria-roledescription="flowchart-v2"><g><marker id="mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd" viewBox="0 0 10 10" refX="5" refY="5" markerUnits="userSpaceOnUse" markerWidth="8" markerHeight="8" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointStart" viewBox="0 0 10 10" refX="4.5" refY="5" markerUnits="userSpaceOnUse" markerWidth="8" markerHeight="8" orient="auto"><path d="M 0 5 L 10 10 L 10 0 z" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-i83vja02fkb-1786527961964_flowchart-v2-circleEnd" viewBox="0 0 10 10" refX="11" refY="5" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><circle cx="5" cy="5" r="5" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></circle></marker><marker id="mermaid-i83vja02fkb-1786527961964_flowchart-v2-circleStart" viewBox="0 0 10 10" refX="-1" refY="5" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><circle cx="5" cy="5" r="5" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></circle></marker><marker id="mermaid-i83vja02fkb-1786527961964_flowchart-v2-crossEnd" viewBox="0 0 11 11" refX="12" refY="5.2" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><path d="M 1,1 l 9,9 M 10,1 l -9,9" style="stroke-width: 2px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-i83vja02fkb-1786527961964_flowchart-v2-crossStart" viewBox="0 0 11 11" refX="-1" refY="5.2" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><path d="M 1,1 l 9,9 M 10,1 l -9,9" style="stroke-width: 2px; stroke-dasharray: 1px, 0px;"></path></marker><g><g></g><g><path d="M1255.958,69.929L1129.069,80.107C1002.179,90.286,748.4,110.643,621.51,124.321C494.621,138,494.621,145,494.621,148.5L494.621,152" id="L_BI_SEQ_0" style=";" data-edge="true" data-et="edge" data-id="L_BI_SEQ_0" data-points="W3sieCI6MTI1NS45NTgzNTQ5NDk5NTEyLCJ5Ijo2OS45Mjg2Njc4NzgxNzc5OH0seyJ4Ijo0OTQuNjIwODQxOTc5OTgwNDcsInkiOjEzMX0seyJ4Ijo0OTQuNjIwODQxOTc5OTgwNDcsInkiOjE1Nn1d" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M1354.8,106L1354.8,110.167C1354.8,114.333,1354.8,122.667,1354.8,130.333C1354.8,138,1354.8,145,1354.8,148.5L1354.8,152" id="L_BI_MAP_0" style=";" data-edge="true" data-et="edge" data-id="L_BI_MAP_0" data-points="W3sieCI6MTM1NC44MDAwMjIxMjUyNDQxLCJ5IjoxMDZ9LHsieCI6MTM1NC44MDAwMjIxMjUyNDQxLCJ5IjoxMzF9LHsieCI6MTM1NC44MDAwMjIxMjUyNDQxLCJ5IjoxNTZ9XQ==" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M1453.642,71.896L1552.031,81.747C1650.419,91.597,1847.197,111.299,1945.586,124.649C2043.975,138,2043.975,145,2043.975,148.5L2043.975,152" id="L_BI_SETS_0" style=";" data-edge="true" data-et="edge" data-id="L_BI_SETS_0" data-points="W3sieCI6MTQ1My42NDE2ODkzMDA1MzcsInkiOjcxLjg5NTk5ODc5MTUxODU0fSx7IngiOjIwNDMuOTc1MDI4OTkxNjk5MiwieSI6MTMxfSx7IngiOjIwNDMuOTc1MDI4OTkxNjk5MiwieSI6MTU2fV0=" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M412.338,205.485L381.346,212.071C350.354,218.657,288.371,231.828,257.379,241.914C226.388,252,226.388,259,226.388,262.5L226.388,266" id="L_SEQ_LIST_0" style=";" data-edge="true" data-et="edge" data-id="L_SEQ_LIST_0" data-points="W3sieCI6NDEyLjMzNzUwOTE1NTI3MzQ0LCJ5IjoyMDUuNDg1MzM1Nzc2Nzg3NDV9LHsieCI6MjI2LjM4NzUwNDU3NzYzNjcyLCJ5IjoyNDV9LHsieCI6MjI2LjM4NzUwNDU3NzYzNjcyLCJ5IjoyNzB9XQ==" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M494.621,220L494.621,224.167C494.621,228.333,494.621,236.667,494.621,244.333C494.621,252,494.621,259,494.621,262.5L494.621,266" id="L_SEQ_TUPLE_0" style=";" data-edge="true" data-et="edge" data-id="L_SEQ_TUPLE_0" data-points="W3sieCI6NDk0LjYyMDg0MTk3OTk4MDQ3LCJ5IjoyMjB9LHsieCI6NDk0LjYyMDg0MTk3OTk4MDQ3LCJ5IjoyNDV9LHsieCI6NDk0LjYyMDg0MTk3OTk4MDQ3LCJ5IjoyNzB9XQ==" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M576.904,204.921L609.388,211.601C641.871,218.281,706.838,231.64,739.321,241.82C771.804,252,771.804,259,771.804,262.5L771.804,266" id="L_SEQ_STR_0" style=";" data-edge="true" data-et="edge" data-id="L_SEQ_STR_0" data-points="W3sieCI6NTc2LjkwNDE3NDgwNDY4NzUsInkiOjIwNC45MjA3NTAyMzkxNzYwN30seyJ4Ijo3NzEuODA0MTc2MzMwNTY2NCwieSI6MjQ1fSx7IngiOjc3MS44MDQxNzYzMzA1NjY0LCJ5IjoyNzB9XQ==" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M1277.483,201.101L1234.305,208.418C1191.126,215.734,1104.769,230.367,1061.591,241.184C1018.413,252,1018.413,259,1018.413,262.5L1018.413,266" id="L_MAP_DICT_0" style=";" data-edge="true" data-et="edge" data-id="L_MAP_DICT_0" data-points="W3sieCI6MTI3Ny40ODMzNTY0NzU4MywieSI6MjAxLjEwMTExMDU3MDU5OTk5fSx7IngiOjEwMTguNDEyNTEzNzMyOTEwMiwieSI6MjQ1fSx7IngiOjEwMTguNDEyNTEzNzMyOTEwMiwieSI6MjcwfV0=" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M1289.216,220L1280.677,224.167C1272.137,228.333,1255.058,236.667,1246.519,244.333C1237.979,252,1237.979,259,1237.979,262.5L1237.979,266" id="L_MAP_DD_0" style=";" data-edge="true" data-et="edge" data-id="L_MAP_DD_0" data-points="W3sieCI6MTI4OS4yMTYzOTUzOTQ4NDM5LCJ5IjoyMjB9LHsieCI6MTIzNy45NzkxODcwMTE3MTg4LCJ5IjoyNDV9LHsieCI6MTIzNy45NzkxODcwMTE3MTg4LCJ5IjoyNzB9XQ==" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M1420.384,220L1428.923,224.167C1437.463,228.333,1454.542,236.667,1463.081,244.333C1471.621,252,1471.621,259,1471.621,262.5L1471.621,266" id="L_MAP_CTR_0" style=";" data-edge="true" data-et="edge" data-id="L_MAP_CTR_0" data-points="W3sieCI6MTQyMC4zODM2NDg4NTU2NDQ0LCJ5IjoyMjB9LHsieCI6MTQ3MS42MjA4NTcyMzg3Njk1LCJ5IjoyNDV9LHsieCI6MTQ3MS42MjA4NTcyMzg3Njk1LCJ5IjoyNzB9XQ==" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M1432.117,200.467L1478.148,207.889C1524.179,215.311,1616.242,230.156,1662.273,241.078C1708.304,252,1708.304,259,1708.304,262.5L1708.304,266" id="L_MAP_OD_0" style=";" data-edge="true" data-et="edge" data-id="L_MAP_OD_0" data-points="W3sieCI6MTQzMi4xMTY2ODc3NzQ2NTgyLCJ5IjoyMDAuNDY2NzU1MTk3NTMzODd9LHsieCI6MTcwOC4zMDQxOTE1ODkzNTU1LCJ5IjoyNDV9LHsieCI6MTcwOC4zMDQxOTE1ODkzNTU1LCJ5IjoyNzB9XQ==" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M1987.408,216.518L1977.992,221.265C1968.576,226.012,1949.744,235.506,1940.329,243.753C1930.913,252,1930.913,259,1930.913,262.5L1930.913,266" id="L_SETS_SET_0" style=";" data-edge="true" data-et="edge" data-id="L_SETS_SET_0" data-points="W3sieCI6MTk4Ny40MDgzNjMzNDIyODUyLCJ5IjoyMTYuNTE3ODU0NjU1NzU3Njd9LHsieCI6MTkzMC45MTI1Mjg5OTE2OTkyLCJ5IjoyNDV9LHsieCI6MTkzMC45MTI1Mjg5OTE2OTkyLCJ5IjoyNzB9XQ==" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M2100.542,216.518L2109.958,221.265C2119.374,226.012,2138.206,235.506,2147.622,243.753C2157.038,252,2157.038,259,2157.038,262.5L2157.038,266" id="L_SETS_FS_0" style=";" data-edge="true" data-et="edge" data-id="L_SETS_FS_0" data-points="W3sieCI6MjEwMC41NDE2OTQ2NDExMTMzLCJ5IjoyMTYuNTE3ODU0NjU1NzU3Njd9LHsieCI6MjE1Ny4wMzc1Mjg5OTE2OTksInkiOjI0NX0seyJ4IjoyMTU3LjAzNzUyODk5MTY5OSwieSI6MjcwfV0=" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M147.876,358L140.441,362.167C133.006,366.333,118.136,374.667,110.702,382.333C103.267,390,103.267,397,103.267,400.5L103.267,404" id="L_LIST_DQ_0" style=";" data-edge="true" data-et="edge" data-id="L_LIST_DQ_0" data-points="W3sieCI6MTQ3Ljg3NTY2ODE4MDE2MTYzLCJ5IjozNTh9LHsieCI6MTAzLjI2NjY3MDIyNzA1MDc4LCJ5IjozODN9LHsieCI6MTAzLjI2NjY3MDIyNzA1MDc4LCJ5Ijo0MDh9XQ==" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M304.899,358L312.334,362.167C319.769,366.333,334.639,374.667,342.074,382.333C349.508,390,349.508,397,349.508,400.5L349.508,404" id="L_LIST_HP_0" style=";" data-edge="true" data-et="edge" data-id="L_LIST_HP_0" data-points="W3sieCI6MzA0Ljg5OTM0MDk3NTExMTg0LCJ5IjozNTh9LHsieCI6MzQ5LjUwODMzODkyODIyMjY2LCJ5IjozODN9LHsieCI6MzQ5LjUwODMzODkyODIyMjY2LCJ5Ijo0MDh9XQ==" marker-end="url(#mermaid-i83vja02fkb-1786527961964_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path></g><g><g><g data-id="L_BI_SEQ_0" transform="translate(0, 0)"></g></g><g><g data-id="L_BI_MAP_0" transform="translate(0, 0)"></g></g><g><g data-id="L_BI_SETS_0" transform="translate(0, 0)"></g></g><g><g data-id="L_SEQ_LIST_0" transform="translate(0, 0)"></g></g><g><g data-id="L_SEQ_TUPLE_0" transform="translate(0, 0)"></g></g><g><g data-id="L_SEQ_STR_0" transform="translate(0, 0)"></g></g><g><g data-id="L_MAP_DICT_0" transform="translate(0, 0)"></g></g><g><g data-id="L_MAP_DD_0" transform="translate(0, 0)"></g></g><g><g data-id="L_MAP_CTR_0" transform="translate(0, 0)"></g></g><g><g data-id="L_MAP_OD_0" transform="translate(0, 0)"></g></g><g><g data-id="L_SETS_SET_0" transform="translate(0, 0)"></g></g><g><g data-id="L_SETS_FS_0" transform="translate(0, 0)"></g></g><g><g data-id="L_LIST_DQ_0" transform="translate(0, 0)"></g></g><g><g data-id="L_LIST_HP_0" transform="translate(0, 0)"></g></g></g><g><g id="flowchart-BI-0" transform="translate(1354.8000221252441, 62)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-98.84166717529297" y="-44" width="197.68333435058594" height="88"></rect><g style="color:#000 !important" transform="translate(-58.84166717529297, -24)"><rect></rect><foreignObject width="117.68333435058594" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Python Built-in<br>Data Structures</p></span></div></foreignObject></g></g><g id="flowchart-SEQ-1" transform="translate(494.62084197998047, 188)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-82.28333282470703" y="-32" width="164.56666564941406" height="64"></rect><g style="color:#000 !important" transform="translate(-42.28333282470703, -12)"><rect></rect><foreignObject width="84.56666564941406" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Sequences</p></span></div></foreignObject></g></g><g id="flowchart-MAP-2" transform="translate(1354.8000221252441, 188)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-77.31666564941406" y="-32" width="154.63333129882812" height="64"></rect><g style="color:#000 !important" transform="translate(-37.31666564941406, -12)"><rect></rect><foreignObject width="74.63333129882812" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Mappings</p></span></div></foreignObject></g></g><g id="flowchart-SETS-3" transform="translate(2043.9750289916992, 188)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-56.56666564941406" y="-32" width="113.13333129882812" height="64"></rect><g style="color:#000 !important" transform="translate(-16.566665649414062, -12)"><rect></rect><foreignObject width="33.133331298828125" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Sets</p></span></div></foreignObject></g></g><g id="flowchart-LIST-4" transform="translate(226.38750457763672, 314)"><rect style="fill:#38d9a9 !important;stroke:#000 !important" x="-104.64167022705078" y="-44" width="209.28334045410156" height="88"></rect><g style="color:#000 !important" transform="translate(-64.64167022705078, -24)"><rect></rect><foreignObject width="129.28334045410156" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>list<br>mutable, ordered</p></span></div></foreignObject></g></g><g id="flowchart-TUPLE-5" transform="translate(494.62084197998047, 314)"><rect style="fill:#38d9a9 !important;stroke:#000 !important" x="-113.59166717529297" y="-44" width="227.18333435058594" height="88"></rect><g style="color:#000 !important" transform="translate(-73.59166717529297, -24)"><rect></rect><foreignObject width="147.18333435058594" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>tuple<br>immutable, ordered</p></span></div></foreignObject></g></g><g id="flowchart-STR-6" transform="translate(771.8041763305664, 314)"><rect style="fill:#38d9a9 !important;stroke:#000 !important" x="-113.59166717529297" y="-44" width="227.18333435058594" height="88"></rect><g style="color:#000 !important" transform="translate(-73.59166717529297, -24)"><rect></rect><foreignObject width="147.18333435058594" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>str<br>immutable, ordered</p></span></div></foreignObject></g></g><g id="flowchart-DICT-7" transform="translate(1018.4125137329102, 314)"><rect style="fill:#ffa94d !important;stroke:#000 !important" x="-83.01667022705078" y="-44" width="166.03334045410156" height="88"></rect><g style="color:#000 !important" transform="translate(-43.01667022705078, -24)"><rect></rect><foreignObject width="86.03334045410156" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>dict<br>O(1) lookup</p></span></div></foreignObject></g></g><g id="flowchart-DD-8" transform="translate(1237.9791870117188, 314)"><rect style="fill:#ffa94d !important;stroke:#000 !important" x="-86.55000305175781" y="-44" width="173.10000610351562" height="88"></rect><g style="color:#000 !important" transform="translate(-46.55000305175781, -24)"><rect></rect><foreignObject width="93.10000610351562" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>defaultdict<br>auto-default</p></span></div></foreignObject></g></g><g id="flowchart-CTR-9" transform="translate(1471.6208572387695, 314)"><rect style="fill:#ffa94d !important;stroke:#000 !important" x="-97.09166717529297" y="-44" width="194.18333435058594" height="88"></rect><g style="color:#000 !important" transform="translate(-57.09166717529297, -24)"><rect></rect><foreignObject width="114.18333435058594" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Counter<br>frequency map</p></span></div></foreignObject></g></g><g id="flowchart-OD-10" transform="translate(1708.3041915893555, 314)"><rect style="fill:#ffa94d !important;stroke:#000 !important" x="-89.59166717529297" y="-44" width="179.18333435058594" height="88"></rect><g style="color:#000 !important" transform="translate(-49.59166717529297, -24)"><rect></rect><foreignObject width="99.18333435058594" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>OrderedDict<br>move_to_end</p></span></div></foreignObject></g></g><g id="flowchart-SET-11" transform="translate(1930.9125289916992, 314)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-83.01667022705078" y="-44" width="166.03334045410156" height="88"></rect><g style="color:#000 !important" transform="translate(-43.01667022705078, -24)"><rect></rect><foreignObject width="86.03334045410156" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>set<br>O(1) lookup</p></span></div></foreignObject></g></g><g id="flowchart-FS-12" transform="translate(2157.037528991699, 314)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-93.10832977294922" y="-44" width="186.21665954589844" height="88"></rect><g style="color:#000 !important" transform="translate(-53.10832977294922, -24)"><rect></rect><foreignObject width="106.21665954589844" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>frozenset<br>immutable set</p></span></div></foreignObject></g></g><g id="flowchart-DQ-13" transform="translate(103.26667022705078, 452)"><rect style="fill:#38d9a9 !important;stroke:#000 !important" x="-95.26667022705078" y="-44" width="190.53334045410156" height="88"></rect><g style="color:#000 !important" transform="translate(-55.26667022705078, -24)"><rect></rect><foreignObject width="110.53334045410156" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>deque<br>O(1) both ends</p></span></div></foreignObject></g></g><g id="flowchart-HP-14" transform="translate(349.50833892822266, 452)"><rect style="fill:#38d9a9 !important;stroke:#000 !important" x="-100.9749984741211" y="-44" width="201.9499969482422" height="88"></rect><g style="color:#000 !important" transform="translate(-60.974998474121094, -24)"><rect></rect><foreignObject width="121.94999694824219" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>heapq<br>min-heap on list</p></span></div></foreignObject></g></g></g></g></g></svg>

### dict: Hash Map

`dict` is Python's built-in hash map. It provides O(1) average-case lookups, inserts, and deletes. Since Python 3.7, dictionaries maintain insertion order.

Python

Key operations:

Python

**A safety point:** `d[key]` raises `KeyError` if the key does not exist. Always use `d.get(key, default)` for safe access, or check `key in d` first. Forgetting this guard is a common source of bugs in interview code.

### defaultdict: Auto-Default Values

`defaultdict` from the `collections` module automatically creates a default value when you access a missing key. This eliminates the "check if key exists, create if not" pattern:

Python

Compare this to the verbose alternative:

Python

Common default factories:

| Factory | Default Value | Use Case |
| --- | --- | --- |
| `int` | `0` | Frequency counting |
| `list` | `[]` | Adjacency lists, grouping |
| `set` | `set()` | Unique neighbors, deduplication |
| `lambda: float('inf')` | `inf` | Distance maps in shortest path |

### Counter: Purpose-Built Frequency Counting

`Counter` from `collections` is the most concise way to count frequencies:

Python

Counter arithmetic is useful for DSA:

Python

### set: Hash Set

`set` provides O(1) average-case membership testing:

Python

Unlike some languages, `set.add()` returns nothing, so you detect duplicates by checking membership before adding:

Python

Set operations are useful for certain DSA problems:

Python

### OrderedDict

Since Python 3.7, regular `dict` maintains insertion order. `OrderedDict` from `collections` is still useful for one specific operation: `move_to_end()`, which is used in LRU cache implementations:

Python

### Hashability: What Can Be a Dict Key or Set Element?

Hashability matters for Python DSA. Only **hashable** objects can be dict keys or set elements. The rule is simple: **mutable objects are not hashable, immutable objects are**.

| Type | Hashable? | Can Be Dict Key / Set Element? |
| --- | --- | --- |
| `int`, `float`, `bool` | Yes | Yes |
| `str` | Yes | Yes |
| `tuple` (of hashable elements) | Yes | Yes |
| `frozenset` | Yes | Yes |
| `list` | No | No |
| `dict` | No | No |
| `set` | No | No |

This comes up constantly in DSA:

Python

### Collections Quick Reference

| Collection | Python Type | Key Methods | Time Complexity | DSA Use Case |
| --- | --- | --- | --- | --- |
| Dynamic array | `list` | `append`, `pop`, `[]`, `len` | O(1) append/access | Result lists, stacks |
| Hash map | `dict` | `[]`, `get`, `in`, `items` | O(1) average | Frequency counting, lookups |
| Hash set | `set` | `add`, `in`, `discard` | O(1) average | Visited tracking, duplicates |
| Auto-default map | `defaultdict` | Same as dict + auto-default | O(1) average | Adjacency lists, grouping |
| Frequency map | `Counter` | `most_common`, arithmetic | O(1) average | Anagram, window problems |
| Ordered map | `OrderedDict` | `move_to_end`, `popitem` | O(1) average | LRU cache |
| Double-ended queue | `deque` | `append`, `popleft`, `appendleft` | O(1) both ends | BFS, sliding window |
| Min-heap | `heapq` on `list` | `heappush`, `heappop` | O(log n) push/pop | Top-K, Dijkstra |
| Sorted list | `SortedList` | `add`, `remove`, `bisect` | O(log n) | Sliding window sorted access |
| Immutable sequence | `tuple` | `[]`, `in`, unpacking | O(1) access | Dict keys, heap elements, states |
| Immutable set | `frozenset` | Same as set (read-only) | O(1) lookup | Set of sets, dict keys |

## Tuples: Python's Built-in Pairs

Python tuples are immutable, fixed-size sequences. They are the standard way to group a small number of related values, and they simplify many DSA patterns: coordinates, edges, intervals, and heap entries.

Python

### Why Tuples Matter for DSA

**1\. Tuples are hashable** (unlike lists), so they can be dict keys and set elements:

Python

**2\. Tuples compare lexicographically**, which is useful for heap operations:

Python

This means you can push tuples onto a heap and they will be ordered by the first element, with ties broken by the second element, and so on:

Python

**3\. Tuple unpacking** makes code cleaner:

Python

## deque: BFS and Sliding Window Foundation

`deque` (double-ended queue) from `collections` provides O(1) operations at both ends. Use it for BFS, sliding window problems, and monotonic deque patterns.

Python

### BFS Template

Every BFS implementation starts with a deque:

Python

For level-order BFS (where you need to process all nodes at the current level before moving to the next), capture the queue size:

Python

### deque Operations

Python

<svg id="mermaid-rm4c1t3nnvc-1786527961965" width="100%" xmlns="http://www.w3.org/2000/svg" style="max-width: 620.6832885742188px;" viewBox="0 10 620.6832885742188 194" role="graphics-document document" aria-roledescription="flowchart-v2"><g><marker id="mermaid-rm4c1t3nnvc-1786527961965_flowchart-v2-pointEnd" viewBox="0 0 10 10" refX="5" refY="5" markerUnits="userSpaceOnUse" markerWidth="8" markerHeight="8" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-rm4c1t3nnvc-1786527961965_flowchart-v2-pointStart" viewBox="0 0 10 10" refX="4.5" refY="5" markerUnits="userSpaceOnUse" markerWidth="8" markerHeight="8" orient="auto"><path d="M 0 5 L 10 10 L 10 0 z" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-rm4c1t3nnvc-1786527961965_flowchart-v2-circleEnd" viewBox="0 0 10 10" refX="11" refY="5" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><circle cx="5" cy="5" r="5" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></circle></marker><marker id="mermaid-rm4c1t3nnvc-1786527961965_flowchart-v2-circleStart" viewBox="0 0 10 10" refX="-1" refY="5" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><circle cx="5" cy="5" r="5" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></circle></marker><marker id="mermaid-rm4c1t3nnvc-1786527961965_flowchart-v2-crossEnd" viewBox="0 0 11 11" refX="12" refY="5.2" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><path d="M 1,1 l 9,9 M 10,1 l -9,9" style="stroke-width: 2px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-rm4c1t3nnvc-1786527961965_flowchart-v2-crossStart" viewBox="0 0 11 11" refX="-1" refY="5.2" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><path d="M 1,1 l 9,9 M 10,1 l -9,9" style="stroke-width: 2px; stroke-dasharray: 1px, 0px;"></path></marker><g><g></g><g><path d="M180.667,50L184.833,50C189,50,197.333,50,205.409,51.878C213.486,53.756,221.305,57.512,225.214,59.39L229.124,61.268" id="L_AL_DQ_0" style=";" data-edge="true" data-et="edge" data-id="L_AL_DQ_0" data-points="W3sieCI6MTgwLjY2NjY3MTc1MjkyOTcsInkiOjUwfSx7IngiOjIwNS42NjY2NzE3NTI5Mjk3LCJ5Ijo1MH0seyJ4IjoyMzIuNzI5MDk4NTM3NTEyLCJ5Ijo2M31d" marker-end="url(#mermaid-rm4c1t3nnvc-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M415.921,63L420.431,60.833C424.942,58.667,433.963,54.333,441.973,52.167C449.983,50,456.983,50,460.483,50L463.983,50" id="L_DQ_PL_0" style=";" data-edge="true" data-et="edge" data-id="L_DQ_PL_0" data-points="W3sieCI6NDE1LjkyMDkxMDYxNzc2MTUsInkiOjYzfSx7IngiOjQ0Mi45ODMzMzc0MDIzNDM3NSwieSI6NTB9LHsieCI6NDY3Ljk4MzMzNzQwMjM0Mzc1LCJ5Ijo1MH1d" marker-end="url(#mermaid-rm4c1t3nnvc-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M168.75,164L174.903,164C181.056,164,193.361,164,203.423,162.122C213.486,160.244,221.305,156.488,225.214,154.61L229.124,152.732" id="L_AR_DQ_0" style=";" data-edge="true" data-et="edge" data-id="L_AR_DQ_0" data-points="W3sieCI6MTY4Ljc1LCJ5IjoxNjR9LHsieCI6MjA1LjY2NjY3MTc1MjkyOTcsInkiOjE2NH0seyJ4IjoyMzIuNzI5MDk4NTM3NTEyLCJ5IjoxNTF9XQ==" marker-end="url(#mermaid-rm4c1t3nnvc-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M415.921,151L420.431,153.167C424.942,155.333,433.963,159.667,443.959,161.833C453.956,164,464.928,164,470.414,164L475.9,164" id="L_DQ_PR_0" style=";" data-edge="true" data-et="edge" data-id="L_DQ_PR_0" data-points="W3sieCI6NDE1LjkyMDkxMDYxNzc2MTUsInkiOjE1MX0seyJ4Ijo0NDIuOTgzMzM3NDAyMzQzNzUsInkiOjE2NH0seyJ4Ijo0NzkuOTAwMDAxNTI1ODc4OSwieSI6MTY0fV0=" marker-end="url(#mermaid-rm4c1t3nnvc-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path></g><g><g><g data-id="L_AL_DQ_0" transform="translate(0, 0)"></g></g><g><g data-id="L_DQ_PL_0" transform="translate(0, 0)"></g></g><g><g data-id="L_AR_DQ_0" transform="translate(0, 0)"></g></g><g><g data-id="L_DQ_PR_0" transform="translate(0, 0)"></g></g></g><g><g id="flowchart-AL-0" transform="translate(94.33333587646484, 50)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-86.33333587646484" y="-32" width="172.6666717529297" height="64"></rect><g style="color:#000 !important" transform="translate(-46.333335876464844, -12)"><rect></rect><foreignObject width="92.66667175292969" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>appendleft()</p></span></div></foreignObject></g></g><g id="flowchart-DQ-1" transform="translate(324.3250045776367, 107)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-93.65833282470703" y="-44" width="187.31666564941406" height="88"></rect><g style="color:#000 !important" transform="translate(-53.65833282470703, -24)"><rect></rect><foreignObject width="107.31666564941406" height="48"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>deque<br>[front... back]</p></span></div></foreignObject></g></g><g id="flowchart-PL-3" transform="translate(540.3333358764648, 50)"><rect style="fill:#ff8787 !important;stroke:#000 !important" x="-72.3499984741211" y="-32" width="144.6999969482422" height="64"></rect><g style="color:#000 !important" transform="translate(-32.349998474121094, -12)"><rect></rect><foreignObject width="64.69999694824219" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>popleft()</p></span></div></foreignObject></g></g><g id="flowchart-AR-4" transform="translate(94.33333587646484, 164)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-74.41666412353516" y="-32" width="148.8333282470703" height="64"></rect><g style="color:#000 !important" transform="translate(-34.416664123535156, -12)"><rect></rect><foreignObject width="68.83332824707031" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>append()</p></span></div></foreignObject></g></g><g id="flowchart-PR-7" transform="translate(540.3333358764648, 164)"><rect style="fill:#ff8787 !important;stroke:#000 !important" x="-60.43333435058594" y="-32" width="120.86666870117188" height="64"></rect><g style="color:#000 !important" transform="translate(-20.433334350585938, -12)"><rect></rect><foreignObject width="40.866668701171875" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>pop()</p></span></div></foreignObject></g></g></g></g></g></svg>

### Monotonic Deque Pattern

The monotonic deque is used in "sliding window maximum/minimum" problems:

Python

### Bounded deque

You can create a deque with a maximum size. When full, adding to one end automatically removes from the other:

Python

## heapq: Min-Heap and the Max-Heap Trick

Python's `heapq` module provides heap operations on a regular list. The heap is always a **min-heap**, meaning the smallest element is always at index 0.

Python

### Basic Operations

Python

### The Max-Heap Trick

Python only provides a min-heap. To get a max-heap, **negate the values**:

Python

This works because negating reverses the ordering: if `a < b`, then `-a > -b`.

### Tuples in Heaps

Since tuples compare lexicographically, you can push tuples to sort by multiple fields. The first element of the tuple determines the primary sort order:

Python

**Caution with tuples:** If the first elements are equal, Python compares the second elements. If the second elements are not comparable (e.g., custom objects without `__lt__`), you get a `TypeError`. Always include a tie-breaking field (like an index or counter) as the second element:

Python

### heapq Utility Functions

Python

One important limitation: `heapq` does **not** support efficient removal of arbitrary elements. Removing a specific element that is not at the root requires an O(n) scan, and there is no `remove` method. If you need to invalidate heap elements, use **lazy deletion**: mark elements as deleted and skip them when they surface via `heappop()`. Alternatively, use `SortedList` from `sortedcontainers` which supports O(log n) removal.

## Sorted Containers and bisect

Python does not ship a balanced binary search tree in its standard library, but it offers two ways to work with sorted data: the `bisect` module for binary search on sorted lists, and the third-party `sortedcontainers` library (available on LeetCode) for O(log n) sorted maps and sets.

### bisect: Binary Search on Sorted Lists

The `bisect` module performs binary search to find insertion points in a sorted list:

Python

The difference between `bisect_left` and `bisect_right` matters when the value exists in the list:

- `bisect_left(lst, x)`: returns the index of the **leftmost** position where `x` can be inserted (i.e., the index of the first element `>= x`)
- `bisect_right(lst, x)`: returns the index of the **rightmost** position where `x` can be inserted (i.e., the index of the first element `> x`)

This makes `bisect_left` useful for "find the first element >= target" and `bisect_right` for "find the first element > target":

Python

**Insert while maintaining sort order:**

Python

Note that `insort` is O(log n) for the search but O(n) for the insertion (because shifting elements in a list is O(n)). For large lists with frequent insertions, use `SortedList` instead.

### SortedList, SortedDict, SortedSet

The `sortedcontainers` library provides three O(log n) sorted data structures: `SortedList`, `SortedDict`, and `SortedSet`.

Python

Common neighbor queries on a `SortedList`:

| Query | Expression | Notes |
| --- | --- | --- |
| Floor (largest <= x) | `sl[sl.bisect_right(x) - 1]` | Check index >= 0 first |
| Ceiling (smallest >= x) | `sl[sl.bisect_left(x)]` | Check index < len(sl) first |
| Strictly lower (largest < x) | `sl[sl.bisect_left(x) - 1]` | Check index >= 0 first |
| Strictly higher (smallest > x) | `sl[sl.bisect_right(x)]` | Check index < len(sl) first |
| Smallest element | `sl[0]` | O(1) access |
| Largest element | `sl[-1]` | O(1) access |

## Sorting and Custom Comparators

Sorting is a prerequisite for many algorithms: binary search, two pointers on sorted arrays, merge intervals, and greedy approaches.

Python

### Custom Sorting with key=

The `key` parameter takes a function that extracts a comparison key from each element. This is how you sort by custom criteria:

Python

The tuple trick handles multi-key sorting cleanly. Python compares tuples lexicographically, so `(len(w), w)` sorts by length first, then alphabetically for words of the same length.

To sort one key ascending and another descending, negate the ascending key (for numbers) or reverse the sort:

Python

### cmp\_to\_key: When key= Is Not Enough

For rare problems where the comparison logic cannot be expressed as a simple key extraction, use `cmp_to_key`:

Python

### Sort Stability

Python's sort is **stable** (it uses TimSort). Elements that compare equal retain their relative order from the original list. This is useful for multi-key sorting. You can sort by secondary key first, then by primary key, and the secondary order is preserved within groups of equal primary keys:

Python

## Functional Patterns and Pythonic Idioms for DSA

Python offers several patterns that make DSA code more concise and readable. They reduce the number of lines you write in an interview, leaving more time for the actual algorithm.

### List Comprehensions and Generator Expressions

List comprehensions create lists in a single expression:

Python

Generator expressions are like list comprehensions but lazy. They do not create the entire list in memory:

Python

### zip(): Parallel Iteration

`zip()` pairs up elements from multiple iterables:

Python

### reversed(): Reverse Without Copying

`reversed()` returns an iterator that traverses in reverse. Unlike `lst[::-1]`, it does not create a new list:

Python

### Multiple Assignment and Unpacking

Python

### Counter Arithmetic in Sliding Window

This pattern is useful for sliding window problems:

Python

### map() and filter()

While list comprehensions are generally preferred, `map()` can be useful for type conversions:

Python

## Memoization with lru\_cache and cache

The `@cache` and `@lru_cache` decorators turn any recursive function into a memoized solution with zero boilerplate. Many DP problems that would normally require a manual memo dictionary or a full bottom-up table can be solved with a decorated recursive function.

### Basic Usage

Python

`@cache` is shorthand for `@lru_cache(maxsize=None)`, introduced in Python 3.9. Both cache all results indefinitely.

### 2D DP Example

Python

### Using @cache on LeetCode

On LeetCode, your solution is a class method. Here is how to use `@cache` inside a class:

Python

The nested function approach works cleanly because `coins` is captured from the enclosing scope and does not need to be a parameter (which would affect the cache key).

### Key Constraints

**Arguments must be hashable.** You cannot pass lists to a cached function. Convert them to tuples:

Python

**Remember to clear the cache** if you run multiple test cases and the cached function uses external state. On LeetCode, this is rarely needed because each test case creates a new `Solution` instance. But in local testing:

Python

### When to Use Manual Memo Instead

Sometimes `@cache` is not the best fit:

Python

Use manual memo when:

- You need to pass mutable state that cannot be made hashable
- You want to inspect or modify the cache during computation
- You are working with a very large state space and want to control memory
- The recursion is extremely deep (the decorator adds slight overhead per call)

## Recursion, the Call Stack, and sys.setrecursionlimit

Every function call in Python goes on the **call stack**. Python's default recursion limit is 1000, which is extremely low for DSA problems:

Python

The fix is one line:

Python

### When to Worry About Stack Depth

| Scenario | Typical Depth | Risk |
| --- | --- | --- |
| Balanced binary tree (n nodes) | O(log n) | Safe for n up to 10^6 |
| Linked list / skewed tree (n nodes) | O(n) | Dangerous if n > 1000 (default limit) |
| Backtracking (k choices, depth d) | O(d) | Usually safe (d is small) |
| DFS on graph (n nodes) | O(n) | Set recursionlimit for large n |

### Converting Recursion to Iteration

When recursion depth is proportional to input size and the input can be large, convert to iteration using an explicit stack:

Python

Note that Python does **not** optimize tail recursion. Unlike some functional languages, a tail-recursive function in Python still adds a frame to the call stack on every call.

## Graph Representation Patterns

Graphs appear in a large portion of DSA problems. Python does not have a built-in graph class, so you need to build representations yourself. There are two common approaches.

### Approach 1: defaultdict(list)

Use when node IDs can be anything (integers, strings, etc.):

Python

### Approach 2: List of Lists (when nodes are 0 to n-1)

More memory-efficient when node IDs are contiguous integers:

Python

### Weighted Graphs

Store tuples of `(neighbor, weight)`:

Python

<svg id="mermaid-ydr63bivite-1786527961965" width="100%" xmlns="http://www.w3.org/2000/svg" style="max-width: 981.0999755859375px;" viewBox="0 10 981.0999755859375 662" role="graphics-document document" aria-roledescription="flowchart-v2"><g><marker id="mermaid-ydr63bivite-1786527961965_flowchart-v2-pointEnd" viewBox="0 0 10 10" refX="5" refY="5" markerUnits="userSpaceOnUse" markerWidth="8" markerHeight="8" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-ydr63bivite-1786527961965_flowchart-v2-pointStart" viewBox="0 0 10 10" refX="4.5" refY="5" markerUnits="userSpaceOnUse" markerWidth="8" markerHeight="8" orient="auto"><path d="M 0 5 L 10 10 L 10 0 z" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-ydr63bivite-1786527961965_flowchart-v2-circleEnd" viewBox="0 0 10 10" refX="11" refY="5" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><circle cx="5" cy="5" r="5" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></circle></marker><marker id="mermaid-ydr63bivite-1786527961965_flowchart-v2-circleStart" viewBox="0 0 10 10" refX="-1" refY="5" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><circle cx="5" cy="5" r="5" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></circle></marker><marker id="mermaid-ydr63bivite-1786527961965_flowchart-v2-crossEnd" viewBox="0 0 11 11" refX="12" refY="5.2" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><path d="M 1,1 l 9,9 M 10,1 l -9,9" style="stroke-width: 2px; stroke-dasharray: 1px, 0px;"></path></marker><marker id="mermaid-ydr63bivite-1786527961965_flowchart-v2-crossStart" viewBox="0 0 11 11" refX="-1" refY="5.2" markerUnits="userSpaceOnUse" markerWidth="11" markerHeight="11" orient="auto"><path d="M 1,1 l 9,9 M 10,1 l -9,9" style="stroke-width: 2px; stroke-dasharray: 1px, 0px;"></path></marker><g><g></g><g></g><g></g><g><g transform="translate(0, 20)"><g><g id="AdjList" data-look="classic"><rect style="" x="8" y="-2" width="965.1000061035156" height="298"></rect><g transform="translate(447.5250015258789, 8)"><foreignObject width="86.05000305175781" height="24"><p>List of Lists</p></foreignObject></g></g></g><g><path d="M135.4,119.5L135.4,125.75C135.4,132,135.4,144.5,135.4,156.333C135.4,168.167,135.4,179.333,135.4,184.917L135.4,190.5" id="L_N0_L0_0" style=";" data-edge="true" data-et="edge" data-id="L_N0_L0_0" data-points="W3sieCI6MTM1LjQwMDAwMTUyNTg3ODksInkiOjExOS41fSx7IngiOjEzNS40MDAwMDE1MjU4Nzg5LCJ5IjoxNTd9LHsieCI6MTM1LjQwMDAwMTUyNTg3ODksInkiOjE5NC41fV0=" marker-end="url(#mermaid-ydr63bivite-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M371.675,119.5L371.675,125.75C371.675,132,371.675,144.5,371.675,156.333C371.675,168.167,371.675,179.333,371.675,184.917L371.675,190.5" id="L_N1_L1_0" style=";" data-edge="true" data-et="edge" data-id="L_N1_L1_0" data-points="W3sieCI6MzcxLjY3NTAwMzA1MTc1NzgsInkiOjExOS41fSx7IngiOjM3MS42NzUwMDMwNTE3NTc4LCJ5IjoxNTd9LHsieCI6MzcxLjY3NTAwMzA1MTc1NzgsInkiOjE5NC41fV0=" marker-end="url(#mermaid-ydr63bivite-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M609.425,119.5L609.425,125.75C609.425,132,609.425,144.5,609.425,156.333C609.425,168.167,609.425,179.333,609.425,184.917L609.425,190.5" id="L_N2_L2_0" style=";" data-edge="true" data-et="edge" data-id="L_N2_L2_0" data-points="W3sieCI6NjA5LjQyNTAwMzA1MTc1NzgsInkiOjExOS41fSx7IngiOjYwOS40MjUwMDMwNTE3NTc4LCJ5IjoxNTd9LHsieCI6NjA5LjQyNTAwMzA1MTc1NzgsInkiOjE5NC41fV0=" marker-end="url(#mermaid-ydr63bivite-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M845.7,119.5L845.7,125.75C845.7,132,845.7,144.5,845.7,156.333C845.7,168.167,845.7,179.333,845.7,184.917L845.7,190.5" id="L_N3_L3_0" style=";" data-edge="true" data-et="edge" data-id="L_N3_L3_0" data-points="W3sieCI6ODQ1LjcwMDAwNDU3NzYzNjcsInkiOjExOS41fSx7IngiOjg0NS43MDAwMDQ1Nzc2MzY3LCJ5IjoxNTd9LHsieCI6ODQ1LjcwMDAwNDU3NzYzNjcsInkiOjE5NC41fV0=" marker-end="url(#mermaid-ydr63bivite-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path></g><g><g><g data-id="L_N0_L0_0" transform="translate(0, 0)"></g></g><g><g data-id="L_N1_L1_0" transform="translate(0, 0)"></g></g><g><g data-id="L_N2_L2_0" transform="translate(0, 0)"></g></g><g><g data-id="L_N3_L3_0" transform="translate(0, 0)"></g></g></g><g><g id="flowchart-N0-8" transform="translate(135.4000015258789, 87.5)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-72.92500305175781" y="-32" width="145.85000610351562" height="64"></rect><g style="color:#000 !important" transform="translate(-32.92500305175781, -12)"><rect></rect><foreignObject width="65.85000610351562" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>graph[0]</p></span></div></foreignObject></g></g><g id="flowchart-L0-9" transform="translate(135.4000015258789, 226.5)"><rect style="fill:#38d9a9 !important;stroke:#000 !important" x="-92.4000015258789" y="-32" width="184.8000030517578" height="64"></rect><g style="color:#000 !important" transform="translate(-52.400001525878906, -12)"><rect></rect><foreignObject width="104.80000305175781" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>[(1, w), (2, w)]</p></span></div></foreignObject></g></g><g id="flowchart-N1-10" transform="translate(371.6750030517578, 87.5)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-71.125" y="-32" width="142.25" height="64"></rect><g style="color:#000 !important" transform="translate(-31.125, -12)"><rect></rect><foreignObject width="62.25" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>graph[1]</p></span></div></foreignObject></g></g><g id="flowchart-L1-11" transform="translate(371.6750030517578, 226.5)"><rect style="fill:#38d9a9 !important;stroke:#000 !important" x="-93.875" y="-32" width="187.75" height="64"></rect><g style="color:#000 !important" transform="translate(-53.875, -12)"><rect></rect><foreignObject width="107.75" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>[(0, w), (3, w)]</p></span></div></foreignObject></g></g><g id="flowchart-N2-12" transform="translate(609.4250030517578, 87.5)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-72.75" y="-32" width="145.5" height="64"></rect><g style="color:#000 !important" transform="translate(-32.75, -12)"><rect></rect><foreignObject width="65.5" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>graph[2]</p></span></div></foreignObject></g></g><g id="flowchart-L2-13" transform="translate(609.4250030517578, 226.5)"><rect style="fill:#38d9a9 !important;stroke:#000 !important" x="-93.875" y="-32" width="187.75" height="64"></rect><g style="color:#000 !important" transform="translate(-53.875, -12)"><rect></rect><foreignObject width="107.75" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>[(0, w), (3, w)]</p></span></div></foreignObject></g></g><g id="flowchart-N3-14" transform="translate(845.7000045776367, 87.5)"><rect style="fill:#00ceff !important;stroke:#000 !important" x="-72.81666564941406" y="-32" width="145.63333129882812" height="64"></rect><g style="color:#000 !important" transform="translate(-32.81666564941406, -12)"><rect></rect><foreignObject width="65.63333129882812" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>graph[3]</p></span></div></foreignObject></g></g><g id="flowchart-L3-15" transform="translate(845.7000045776367, 226.5)"><rect style="fill:#38d9a9 !important;stroke:#000 !important" x="-92.4000015258789" y="-32" width="184.8000030517578" height="64"></rect><g style="color:#000 !important" transform="translate(-52.400001525878906, -12)"><rect></rect><foreignObject width="104.80000305175781" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>[(1, w), (2, w)]</p></span></div></foreignObject></g></g></g></g><g transform="translate(0, 368)"><g><g id="AdjDict" data-look="classic"><rect style="" x="8" y="-2" width="965.1000061035156" height="298"></rect><g transform="translate(433.7416687011719, 8)"><foreignObject width="113.61666870117188" height="24"><p>defaultdict(list)</p></foreignObject></g></g></g><g><path d="M135.4,119.5L135.4,125.75C135.4,132,135.4,144.5,135.4,156.333C135.4,168.167,135.4,179.333,135.4,184.917L135.4,190.5" id="L_K0_V0_0" style=";" data-edge="true" data-et="edge" data-id="L_K0_V0_0" data-points="W3sieCI6MTM1LjQwMDAwMTUyNTg3ODksInkiOjExOS41fSx7IngiOjEzNS40MDAwMDE1MjU4Nzg5LCJ5IjoxNTd9LHsieCI6MTM1LjQwMDAwMTUyNTg3ODksInkiOjE5NC41fV0=" marker-end="url(#mermaid-ydr63bivite-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M371.675,119.5L371.675,125.75C371.675,132,371.675,144.5,371.675,156.333C371.675,168.167,371.675,179.333,371.675,184.917L371.675,190.5" id="L_K1_V1_0" style=";" data-edge="true" data-et="edge" data-id="L_K1_V1_0" data-points="W3sieCI6MzcxLjY3NTAwMzA1MTc1NzgsInkiOjExOS41fSx7IngiOjM3MS42NzUwMDMwNTE3NTc4LCJ5IjoxNTd9LHsieCI6MzcxLjY3NTAwMzA1MTc1NzgsInkiOjE5NC41fV0=" marker-end="url(#mermaid-ydr63bivite-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M609.425,119.5L609.425,125.75C609.425,132,609.425,144.5,609.425,156.333C609.425,168.167,609.425,179.333,609.425,184.917L609.425,190.5" id="L_K2_V2_0" style=";" data-edge="true" data-et="edge" data-id="L_K2_V2_0" data-points="W3sieCI6NjA5LjQyNTAwMzA1MTc1NzgsInkiOjExOS41fSx7IngiOjYwOS40MjUwMDMwNTE3NTc4LCJ5IjoxNTd9LHsieCI6NjA5LjQyNTAwMzA1MTc1NzgsInkiOjE5NC41fV0=" marker-end="url(#mermaid-ydr63bivite-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path><path d="M845.7,119.5L845.7,125.75C845.7,132,845.7,144.5,845.7,156.333C845.7,168.167,845.7,179.333,845.7,184.917L845.7,190.5" id="L_K3_V3_0" style=";" data-edge="true" data-et="edge" data-id="L_K3_V3_0" data-points="W3sieCI6ODQ1LjcwMDAwNDU3NzYzNjcsInkiOjExOS41fSx7IngiOjg0NS43MDAwMDQ1Nzc2MzY3LCJ5IjoxNTd9LHsieCI6ODQ1LjcwMDAwNDU3NzYzNjcsInkiOjE5NC41fV0=" marker-end="url(#mermaid-ydr63bivite-1786527961965_flowchart-v2-pointEnd)" fill="none" stroke="currentColor"></path></g><g><g><g data-id="L_K0_V0_0" transform="translate(0, 0)"></g></g><g><g data-id="L_K1_V1_0" transform="translate(0, 0)"></g></g><g><g data-id="L_K2_V2_0" transform="translate(0, 0)"></g></g><g><g data-id="L_K3_V3_0" transform="translate(0, 0)"></g></g></g><g><g id="flowchart-K0-0" transform="translate(135.4000015258789, 87.5)"><rect style="fill:#ffa94d !important;stroke:#000 !important" x="-63.67500305175781" y="-32" width="127.35000610351562" height="64"></rect><g style="color:#000 !important" transform="translate(-23.675003051757812, -12)"><rect></rect><foreignObject width="47.350006103515625" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Key: 0</p></span></div></foreignObject></g></g><g id="flowchart-V0-1" transform="translate(135.4000015258789, 226.5)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-92.4000015258789" y="-32" width="184.8000030517578" height="64"></rect><g style="color:#000 !important" transform="translate(-52.400001525878906, -12)"><rect></rect><foreignObject width="104.80000305175781" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>[(1, w), (2, w)]</p></span></div></foreignObject></g></g><g id="flowchart-K1-2" transform="translate(371.6750030517578, 87.5)"><rect style="fill:#ffa94d !important;stroke:#000 !important" x="-61.875" y="-32" width="123.75" height="64"></rect><g style="color:#000 !important" transform="translate(-21.875, -12)"><rect></rect><foreignObject width="43.75" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Key: 1</p></span></div></foreignObject></g></g><g id="flowchart-V1-3" transform="translate(371.6750030517578, 226.5)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-93.875" y="-32" width="187.75" height="64"></rect><g style="color:#000 !important" transform="translate(-53.875, -12)"><rect></rect><foreignObject width="107.75" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>[(0, w), (3, w)]</p></span></div></foreignObject></g></g><g id="flowchart-K2-4" transform="translate(609.4250030517578, 87.5)"><rect style="fill:#ffa94d !important;stroke:#000 !important" x="-63.5" y="-32" width="127" height="64"></rect><g style="color:#000 !important" transform="translate(-23.5, -12)"><rect></rect><foreignObject width="47" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Key: 2</p></span></div></foreignObject></g></g><g id="flowchart-V2-5" transform="translate(609.4250030517578, 226.5)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-93.875" y="-32" width="187.75" height="64"></rect><g style="color:#000 !important" transform="translate(-53.875, -12)"><rect></rect><foreignObject width="107.75" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>[(0, w), (3, w)]</p></span></div></foreignObject></g></g><g id="flowchart-K3-6" transform="translate(845.7000045776367, 87.5)"><rect style="fill:#ffa94d !important;stroke:#000 !important" x="-63.56666564941406" y="-32" width="127.13333129882812" height="64"></rect><g style="color:#000 !important" transform="translate(-23.566665649414062, -12)"><rect></rect><foreignObject width="47.133331298828125" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>Key: 3</p></span></div></foreignObject></g></g><g id="flowchart-V3-7" transform="translate(845.7000045776367, 226.5)"><rect style="fill:#69db7c !important;stroke:#000 !important" x="-92.4000015258789" y="-32" width="184.8000030517578" height="64"></rect><g style="color:#000 !important" transform="translate(-52.400001525878906, -12)"><rect></rect><foreignObject width="104.80000305175781" height="24"><div style="color: rgb(0, 0, 0) !important; display: table-cell; white-space: nowrap; line-height: 1.5; max-width: 300px; text-align: center;" xmlns="http://www.w3.org/1999/xhtml"><span style="color:#000 !important"><p>[(1, w), (2, w)]</p></span></div></foreignObject></g></g></g></g></g></g></g></svg>

| Approach | Pros | Cons | Use When |
| --- | --- | --- | --- |
| `defaultdict(list)` | Handles any node IDs, no wasted space | Slightly slower due to hashing | Node IDs are large, sparse, or non-numeric |
| `[[] for _ in range(n)]` | Fast index access, no hashing overhead | Wastes space if node IDs are sparse | Nodes are 0 to n-1 |

## Iterating and Modifying Collections Safely

Modifying a dictionary or set while iterating over it causes a `RuntimeError`. Modifying a list during iteration does not raise an error, but it causes silent bugs as indices shift underneath you.

### Dictionaries and Sets

Python

The same applies to sets:

Python

### Lists

Modifying a list while iterating does not raise an error, but it causes subtle bugs because indices shift:

Python

In practice, most DSA problems do not require removing during iteration. You are far more likely to build a new collection with the desired elements.

## Deduplication Patterns

Many DSA problems require avoiding duplicate results (e.g., 3Sum, 4Sum, permutations with duplicates). Python offers two approaches.

### Sort and Skip Duplicates

This is the preferred approach for sorted array problems:

Python

This runs in O(1) extra space (beyond the sort) and produces results in sorted order.

### Set-Based Deduplication

Use a set to collect unique results. Remember that lists are not hashable, so convert to tuples:

Python

The sort-and-skip approach is generally preferred in interviews because it avoids the overhead of hashing and produces cleaner code. But set-based deduplication is simpler to implement and is a valid fallback when the sort-and-skip logic is complex.

## Common DSA Idioms in Python

This section collects the small patterns and utilities that come up repeatedly across many problem types.

### Sentinel Values

Python

### Math Utilities

Python

### Ceiling Division Without Importing math

Python

### Deep Copy vs Shallow Copy

Python

### Type Conversions

Python

### Infinity and Comparison Tricks

Python

## OOP Basics for Design Problems

Many DSA problems use custom node classes. LeetCode typically defines these for you, but you should know the patterns:

### Common Node Definitions

Python

### Custom Comparison for Heaps

If you need to put custom objects in a heap, define `__lt__` (less than):

Python

Alternatively, use a tuple with a counter as a tie-breaker (as shown in the heapq section). The tuple approach is generally preferred because it does not require modifying the class definition.

## Performance Considerations

Python is one of the slower languages used in competitive programming. LeetCode adjusts time limits per language, so this rarely matters in practice, but understanding common performance pitfalls helps you avoid unnecessary TLE (Time Limit Exceeded) verdicts.

### Common Performance Pitfalls

| Operation | Slow | Fast | Why |
| --- | --- | --- | --- |
| BFS queue | `list.pop(0)` | `deque.popleft()` | O(n) vs O(1) |
| String building | `s += char` in loop | `"".join(parts)` | O(n^2) vs O(n) |
| Membership test | `x in list` | `x in set` | O(n) vs O(1) |
| Insert at front | `list.insert(0, x)` | `deque.appendleft(x)` | O(n) vs O(1) |
| Sorted insert | `insort(list, x)` | `SortedList.add(x)` | O(n) vs O(log n) |
| Deep copy | `copy.deepcopy()` | `[row[:] for row in matrix]` | General vs specific |

### Tips for Avoiding TLE in Python

1. **Use the right data structure.** `set` for lookups, `deque` for BFS, `heapq` for priority queues.
2. **Avoid unnecessary copies.** Slicing creates new lists. Use indices instead when possible.
3. **Use** `**@cache**` **for memoization.** It is faster than a manual memo dictionary for most cases.
4. **List comprehensions are faster than building a list with** `**append**` **in a loop.** They avoid the repeated attribute lookup of `.append` and use optimized bytecode.
5. **Local variables are faster than global variables** in Python. If a function accesses a global frequently, assign it to a local variable first.
6. **Avoid** `**str += char**` **in loops.** Use `"".join()`.
7. **Use** `**sys.setrecursionlimit**` for deep recursion rather than converting to iteration (unless the depth is truly massive).

### Get Premium

Subscribe to unlock full access to all premium content

[Subscribe Now](https://algomaster.io/premium)