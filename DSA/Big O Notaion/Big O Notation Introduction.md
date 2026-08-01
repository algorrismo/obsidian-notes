---
title: "Big O Notation: Introduction"
source: https://algomaster.io/learn/dsa/big-o-introduction
author:
  - "[[Ashish Pratap Singh]]"
published: 2025-08-20
created: 2026-08-01
description: "Big O Notation: Introduction explained with clear examples, visuals, and practice questions in AlgoMaster's Data Structures and Algorithms course."
tags:
  - clippings
  - "#DSA"
---
Listen to this chapter

[Unlock Audio](https://algomaster.io/premium)

**Big O Notation** is a way to measure how efficiently your code performs as the input size grows.

Code that works perfectly on small inputs can slow down, crash, or time out when the input becomes large.

Understanding Big O helps you avoid slow, inefficient solutions and write code that scales.

It’s also one of the most important topics in coding interviews.

You’ll almost always be asked to explain the time and space complexity of your solution. The more efficient your approach, the stronger your chances of passing.

In this chapter, I’ll break down:

- What Big O Notation actually means
- The most common time complexities you’ll come across
- What space complexity is
- And the rules to calculate Big O for any piece of code

Let's get started.

## What is Big O?

What exactly is Big O Notation?

> Big O is a mathematical way to describe how the performance of an algorithm changes as the size of the input grows.

It doesn’t tell you the exact time your code will take.

Instead, it gives you a high-level growth trend, how fast the number of operations increases relative to the input size.

For example: if your input doubles, does your algorithm take twice as long? Ten times as long? Or does it barely change at all?

Big O helps you answer those questions without even running the code, so you can choose the most efficient algorithm for large inputs.

Here is how the common complexities compare as the input `n` grows. The ones near the top barely react to bigger inputs, while the ones near the bottom blow up fast.

### Big-O Notation: How Algorithms Scale

Grow the input size and watch the cost of each complexity class diverge.

<svg viewBox="0 0 960 500" style="display: block; width: 100%; height: auto;" text-rendering="geometricPrecision"><defs></defs><g><rect x="832" y="8" width="108" height="22" rx="5" fill="none" stroke="#00ceff" stroke-width="1.5" opacity="0.95"></rect><text x="886" y="20" text-anchor="middle" dominant-baseline="central" fill="#00ceff" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="12" style="letter-spacing: 0.8px;">n = 1</text></g> <text x="28" y="12" dominant-baseline="hanging" fill="#00ceff" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="14">At n = 1 every class is still cheap</text> <text x="28" y="40" dominant-baseline="hanging" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="11.5">growth rates only separate as n grows</text> <text x="28" y="64" dominant-baseline="hanging" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="11.5" style="letter-spacing: 1px;">OPERATIONS VS N · LOG SCALE</text> <g><line x1="70" y1="418" x2="610" y2="418" stroke="rgba(161,161,170,0.18)" stroke-width="1"></line><text x="64" y="418" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">1</text></g> <g><line x1="70" y1="335.5" x2="610" y2="335.5" stroke="rgba(161,161,170,0.18)" stroke-width="1"></line><text x="64" y="335.5" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">1K</text></g> <g><line x1="70" y1="253" x2="610" y2="253" stroke="rgba(161,161,170,0.18)" stroke-width="1"></line><text x="64" y="253" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">1M</text></g> <g><line x1="70" y1="170.5" x2="610" y2="170.5" stroke="rgba(161,161,170,0.18)" stroke-width="1"></line><text x="64" y="170.5" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">1B</text></g> <g><line x1="70" y1="88" x2="610" y2="88" stroke="rgba(161,161,170,0.18)" stroke-width="1"></line><text x="64" y="88" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">1T</text></g> <text x="70" y="428" text-anchor="middle" dominant-baseline="hanging" fill="#00ceff" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="10.5">1</text> <text x="137.5" y="428" text-anchor="middle" dominant-baseline="hanging" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">2</text> <text x="205" y="428" text-anchor="middle" dominant-baseline="hanging" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">4</text> <text x="272.5" y="428" text-anchor="middle" dominant-baseline="hanging" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">8</text> <text x="340" y="428" text-anchor="middle" dominant-baseline="hanging" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">16</text> <text x="407.5" y="428" text-anchor="middle" dominant-baseline="hanging" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">32</text> <text x="475" y="428" text-anchor="middle" dominant-baseline="hanging" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">64</text> <text x="542.5" y="428" text-anchor="middle" dominant-baseline="hanging" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">128</text> <text x="610" y="428" text-anchor="middle" dominant-baseline="hanging" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10.5">256</text> <line x1="70" y1="88" x2="70" y2="418" stroke="#00ceff" stroke-width="1.25" opacity="0.35" stroke-dasharray="3 3"></line><g><polyline points="70,418 70,418" fill="none" stroke="#69db7c" stroke-width="2.25" stroke-linejoin="round" stroke-linecap="round" opacity="0.92"></polyline><circle cx="70" cy="418" r="3.75" fill="#69db7c" stroke="#1f1f22" stroke-width="1.25"></circle></g><g><polyline points="70,418 70,418" fill="none" stroke="#38d9a9" stroke-width="2.25" stroke-linejoin="round" stroke-linecap="round" opacity="0.92"></polyline><circle cx="70" cy="418" r="3.75" fill="#38d9a9" stroke="#1f1f22" stroke-width="1.25"></circle></g><g><polyline points="70,418 70,418" fill="none" stroke="#3bc9db" stroke-width="2.25" stroke-linejoin="round" stroke-linecap="round" opacity="0.92"></polyline><circle cx="70" cy="418" r="3.75" fill="#3bc9db" stroke="#1f1f22" stroke-width="1.25"></circle></g><g><polyline points="70,418 70,418" fill="none" stroke="#9775fa" stroke-width="2.25" stroke-linejoin="round" stroke-linecap="round" opacity="0.92"></polyline><circle cx="70" cy="418" r="3.75" fill="#9775fa" stroke="#1f1f22" stroke-width="1.25"></circle></g><g><polyline points="70,418 70,418" fill="none" stroke="#ffa94d" stroke-width="2.25" stroke-linejoin="round" stroke-linecap="round" opacity="0.92"></polyline><circle cx="70" cy="418" r="3.75" fill="#ffa94d" stroke="#1f1f22" stroke-width="1.25"></circle></g><g><polyline points="70,409.7216751192405 70,409.7216751192405" fill="none" stroke="#ff8787" stroke-width="2.25" stroke-linejoin="round" stroke-linecap="round" opacity="0.92"></polyline><circle cx="70" cy="409.7216751192405" r="3.75" fill="#ff8787" stroke="#1f1f22" stroke-width="1.25"></circle></g><g><polyline points="70,418 70,418" fill="none" stroke="#da77f2" stroke-width="2.25" stroke-linejoin="round" stroke-linecap="round" opacity="0.92"></polyline><circle cx="70" cy="418" r="3.75" fill="#da77f2" stroke="#1f1f22" stroke-width="1.25"></circle></g><text x="660" y="64" dominant-baseline="hanging" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="11.5" style="letter-spacing: 1px;">AT n = 1</text> <g><rect x="660" y="97" width="11" height="11" rx="3" fill="#69db7c"></rect><text x="679" y="103" dominant-baseline="central" fill="#69db7c" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="13">O(1)</text> <text x="679" y="119" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">Hash table lookup</text> <text x="932" y="103" text-anchor="end" dominant-baseline="central" fill="#f4f4f5" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="700" font-size="13">1</text> <text x="932" y="119" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">1 ns</text></g> <g><rect x="660" y="144" width="11" height="11" rx="3" fill="#38d9a9"></rect><text x="679" y="150" dominant-baseline="central" fill="#38d9a9" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="13">O(log n)</text> <text x="679" y="166" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">Binary search</text> <text x="932" y="150" text-anchor="end" dominant-baseline="central" fill="#f4f4f5" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="700" font-size="13">1</text> <text x="932" y="166" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">1 ns</text></g> <g><rect x="660" y="191" width="11" height="11" rx="3" fill="#3bc9db"></rect><text x="679" y="197" dominant-baseline="central" fill="#3bc9db" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="13">O(n)</text> <text x="679" y="213" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">Linear scan</text> <text x="932" y="197" text-anchor="end" dominant-baseline="central" fill="#f4f4f5" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="700" font-size="13">1</text> <text x="932" y="213" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">1 ns</text></g> <g><rect x="660" y="238" width="11" height="11" rx="3" fill="#9775fa"></rect><text x="679" y="244" dominant-baseline="central" fill="#9775fa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="13">O(n log n)</text> <text x="679" y="260" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">Merge sort</text> <text x="932" y="244" text-anchor="end" dominant-baseline="central" fill="#f4f4f5" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="700" font-size="13">1</text> <text x="932" y="260" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">1 ns</text></g> <g><rect x="660" y="285" width="11" height="11" rx="3" fill="#ffa94d"></rect><text x="679" y="291" dominant-baseline="central" fill="#ffa94d" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="13">O(n²)</text> <text x="679" y="307" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">Bubble sort</text> <text x="932" y="291" text-anchor="end" dominant-baseline="central" fill="#f4f4f5" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="700" font-size="13">1</text> <text x="932" y="307" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">1 ns</text></g> <g><rect x="660" y="332" width="11" height="11" rx="3" fill="#ff8787"></rect><text x="679" y="338" dominant-baseline="central" fill="#ff8787" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="13">O(2ⁿ)</text> <text x="679" y="354" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">Recursive subsets</text> <text x="932" y="338" text-anchor="end" dominant-baseline="central" fill="#f4f4f5" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="700" font-size="13">2</text> <text x="932" y="354" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">2 ns</text></g> <g><rect x="660" y="379" width="11" height="11" rx="3" fill="#da77f2"></rect><text x="679" y="385" dominant-baseline="central" fill="#da77f2" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="800" font-size="13">O(n!)</text> <text x="679" y="401" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">Brute-force TSP</text> <text x="932" y="385" text-anchor="end" dominant-baseline="central" fill="#f4f4f5" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="700" font-size="13">1</text> <text x="932" y="401" text-anchor="end" dominant-baseline="central" fill="#a1a1aa" font-family="'JetBrains Mono', 'Fira Code', monospace" font-weight="600" font-size="10">1 ns</text></g></svg>

1 / 10

| Complexity | Name | What happens when the input doubles |
| --- | --- | --- |
| O(1) | Constant | Nothing, the work stays the same |
| O(log n) | Logarithmic | Adds just one more step |
| O(n) | Linear | The work doubles |
| O(n log n) | Linearithmic | A bit more than doubles |
| O(n²) | Quadratic | The work quadruples |
| O(2ⁿ) | Exponential | The work squares |
| O(n!) | Factorial | The work grows faster than anything above |

Big O is machine-independent. It doesn’t matter whether your code runs on a fast laptop or a slow server, the growth pattern stays the same.

The key variable that drives Big O is the input size `n`. As `n` increases, Big O helps you predict whether the algorithm will still be efficient or become impractical.

## Common Time Complexities

Let's go over the most common time complexities.

Even small differences in complexity (like O(n) vs. O(n log n)) add up quickly as `n` grows.

### 1\. Constant Time – O(1)

This is the fastest and most efficient time complexity.

An algorithm is **O(1)** if it performs a fixed number of operations, meaning the execution time does not depend on the size of the input.

A classic example is accessing an element in an array by index.

It doesn’t matter if the array has 10 elements or 10 million, the time it takes to access an element stays exactly the same.

There’s no looping, no scanning. You jump directly to the value using its index.

### 2\. Logarithmic Time – O(log n)

Next up is logarithmic time, or **O(log n)**.

An algorithm runs in **O(log n)** time when every step reduces the problem size by a constant factor, most often by half.

This means the amount of work grows very slowly, even when the input becomes massive.

The most common example is binary search.

Consider a sorted array of 1 million elements. Instead of scanning linearly:

1. Look at the middle element
2. If it’s not the target, eliminate half the array in one step
3. Repeat on the remaining half

Each step discards half of the remaining data.

To put that into perspective, here is the maximum number of steps binary search takes for different input sizes.

- Input size = 8 → max 3 steps
- Input size = 1,000 → max 10 steps
- Input size = 1,000,000 → max 20 steps
- Input size = 1,000,000,000 → still only 30 steps

Another example of logarithmic time is searching in a balanced binary search tree.

At each node, you eliminate half of the remaining subtree, just like binary search.

### 3\. Linear Time – O(n)

Now let’s talk about linear time, or **O(n)**.

An algorithm is **O(n)** when its running time grows directly in proportion to the size of the input.

If the input doubles, the number of operations also doubles.

A simple example is finding the maximum value in an array:

- You start with some initial max
- Then you scan every element and compare it to the current max
- Each comparison is O(1), but you do it `n` times so the overall time complexity becomes **O(n)**.

So with 10 elements, you do 10 comparisons.

With 1 million elements, you do 1 million comparisons.

Any algorithm that visits every element exactly once is linear time.

Other common examples of O(n) complexity include:

- Summing all values in an array
- Printing every item in a linked list
- Traversing all nodes in a tree or graph

In general, when your algorithm has to look at each element at least once, whether it’s an array, a linked list, a tree, or any collection, you’re most likely dealing with **O(n)** time.

### 4\. Linearithmic Time – O(n log n)

Next is **O(n log n)**, also called linearithmic time.

Algorithms with **O(n log n)** time complexity combine two behaviors:

- A log n factor from repeatedly splitting the input
- An n factor from processing or merging the pieces

It’s often described as logarithmic splitting with linear merging.

The classic example is merge sort:

- First, it recursively splits the array in half over and over. Halving repeatedly creates about log n levels of splitting. That’s the log n part.
- At every level, merging the pieces back together touches all n elements once, which is n work per level.

So you do n work across log n levels, and n × log n gives you **O(n log n)**.

This complexity is slightly slower than linear time but still very efficient, and many fast sorting algorithms run in O(n log n).

### 5\. Quadratic Time – O(n²)

Next up is quadratic time, or **O(n²)**.

In an O(n²) algorithm, the number of operations grows proportionally to the square of the input size. So if you have n elements, you perform roughly n × n operations.

This typically happens when you have nested loops, where for each element you iterate over all the other elements.

Classic examples include simple sorting algorithms like:

- Bubble Sort
- Selection Sort
- Insertion Sort (worst case)

All of them compare or swap elements in nested loops, leading to **O(n²)** behavior.

These algorithms are fine for small inputs, but they become painfully slow as `n` grows:

For `n = 1,000`, you’re doing around 1 million operations. And if `n = 10,000`, you’re looking at 100 million operations.

In coding interviews and wherever performance matters, you’ll often want to avoid O(n²) and look for ways to bring it down to O(n log n) or better.

That said, sometimes quadratic time is acceptable, especially when `n` is small or no better solution exists.

### 6\. Exponential Time – O(2ⁿ)

Next is exponential time, or **O(2ⁿ)**.

Exponential time algorithms usually appear when we try to solve a problem by checking every possible combination, often through brute force or backtracking.

Think of it as the opposite of binary search. Instead of eliminating half the work at each step, you double the work with each extra input element.

This happens in problems where each element can branch into multiple recursive calls.

A classic example is generating all subsets of a set (also called the power set). For each element, we make two recursive choices, include it or exclude it, leading to 2 × 2 ×... × 2 = `2ⁿ` total combinations.

If the set has `n` elements, there are `2ⁿ` possible subsets. That means just 30 elements give you over 1 billion subsets, and 40 elements give you over 1 trillion.

- n = 20 → ~1 million possibilities
- n = 30 → ~1 billion possibilities
- n = 40 → ~1 trillion possibilities

This kind of growth becomes unmanageable very quickly. Even a small increase in `n` makes the runtime explode.

The good news is that many exponential-time problems can be optimized using techniques like memoization or dynamic programming.

These techniques prevent us from recomputing the same subproblems, often reducing the time from **O(2ⁿ)** down to a much more practical polynomial time, which makes the solution usable on real inputs.

In general, exponential algorithms are fine only for very small inputs. For anything larger, you must either optimize or rethink the approach.

### 7\. Factorial Time – O(n!)

Finally, we reach the steepest common complexity: factorial time, or **O(n!)**.

This is what you get when an algorithm tries every possible arrangement of a set of `n` elements.

The number of possibilities grows faster than any other complexity we’ve seen.

By definition, `n!` (n factorial) means n × (n - 1) × (n - 2) ×... × 1, which gives:

- 3! = 3 × 2 × 1 = 6
- 5! = 120
- 10! = about 3.6 million
- 15! = over 1 trillion

Even at n = 15, the numbers are already in the trillions, which makes it completely impractical to compute.

A classic example of O(n!) is generating all permutations of a string.

If you have a string of length 10 and try to print every permutation, that’s already about 3.6 million arrangements. And going from `n` to `n + 1` multiplies the work by `n + 1`, so a string of length 11 takes 11 times longer, and length 12 takes 12 times longer than that.

These kinds of brute-force solutions are mostly used for very small inputs. For anything larger, we rely on smarter techniques like dynamic programming, branch and bound, or heuristics to reduce the problem space.

### Putting Them Side by Side

To see why complexity matters so much, here is roughly how many operations each one takes as the input grows. The numbers in the last two columns are where the difference becomes obvious.

| Complexity | Name | Example | n = 10 | n = 100 | n = 1000 |
| --- | --- | --- | --- | --- | --- |
| O(1) | Constant | Array index access | 1 | 1 | 1 |
| O(log n) | Logarithmic | Binary search | ~3 | ~7 | ~10 |
| O(n) | Linear | Find the max | 10 | 100 | 1,000 |
| O(n log n) | Linearithmic | Merge sort | ~33 | ~700 | ~10,000 |
| O(n²) | Quadratic | Bubble sort | 100 | 10,000 | 1,000,000 |
| O(2ⁿ) | Exponential | All subsets | 1,024 | ~10³⁰ | astronomical |
| O(n!) | Factorial | All permutations | ~3.6 million | astronomical | astronomical |

The top three rows stay manageable no matter how large the input gets. The bottom two become impossible to compute well before the input reaches a few dozen elements.

## Space Complexity

So far, we’ve focused on time complexity, how fast an algorithm runs as input size grows.

But Big O also applies to memory usage, and that is called **space complexity**.

In interviews, you’ll often be asked to analyze both time and space complexity, because in real systems performance is about both speed and how much memory your solution consumes.

Space complexity tells you how much extra memory your algorithm uses in addition to the input itself.

This extra memory can come from:

- Temporary data structures like arrays, hash maps, stacks, and queues
- Recursion call stack frames
- Intermediate buffers used during computation

Even if your algorithm is fast, it may still use more memory than it needs, which can be a serious problem in large-scale systems or environments with limited RAM.

Here are the common space complexities:

### 1) O(1): Constant Space

If you scan an array to find the maximum value, you only store one variable to track the current max.

So while the input size may grow, your extra space stays constant.

### 2) O(n): Linear Space

Now suppose you collect all even numbers from the array into a new list.

If half the numbers are even, that’s roughly `n/2` elements, which still counts as **O(n)** space.

### 3) O(log n): Logarithmic Space

Recursive divide-and-conquer algorithms often use **O(log n)** space because each recursive call adds a frame to the call stack, and the recursion depth grows logarithmically with the input.

For example, recursive binary search halves the search range on each call. On an array of size `n`, the call stack reaches a maximum depth of `log₂n`, so the extra space is **O(log n)**.

### 4) O(n²): Quadratic Space

Storing a full matrix (like an adjacency matrix or DP table) of size `n × n` takes **O(n²)** space.

Here is a 4×4 adjacency matrix as an example. It holds 4 × 4 = 16 entries, and a larger `n × n` matrix scales the same way: storage grows with the square of `n`.

### 5) A Hidden Source of Space: The Recursion Call Stack

Space complexity isn’t only about the extra data structures you create. Recursion also consumes memory through the call stack, and this cost is easy to overlook because you never allocate it yourself.

Every recursive call adds a new frame to the stack, and that frame stays there until the call returns. So the extra space a recursive algorithm uses is set by its maximum recursion depth, which is how many calls are active at the same time. That depth depends entirely on the shape of the recursion.

The earlier binary search example showed this: it recurses only `log₂n` deep, so it uses O(log n) stack space. Other recursion shapes give very different results.

For example, the naive recursive Fibonacci solution branches into two calls each time. It takes **O(2ⁿ)** time, but the stack only ever holds one root-to-leaf path of calls at a time, so its space is **O(n)**.

Depth First Search (DFS) on a tree depends on the height `h` of the tree:

- In a balanced tree, `h = O(log n)`, so space is **O(log n)**
- In the worst case, a completely skewed tree, `h = O(n)`, so space becomes **O(n)**

## Rules for Calculating Big O

Let's talk about how to calculate the complexity of a piece of code.

The simplest way is to break your code down into parts and analyze each part separately.

### Rule 1: Add Complexities of Sequential Operations

If your algorithm performs one block of work after another, you add their time complexities.

Consider code with two separate, sequential loops:

The total runtime is the time for Block A plus the time for Block B, which comes out to O(m) + O(n²). Here `m` and `n` are independent inputs, so neither term dominates the other and we keep both. If both blocks depended on the same `n`, this would simplify to O(n²) using Rule 4 below.

### Rule 2: Multiply Complexities of Nested Operations

If your algorithm has a nested loop with the outer loop running n times and the inner loop running m times, the total complexity is O(n × m).

### Rule 3: Drop Constant Factors

This rule states that we can ignore any constant multipliers in a Big O expression.

When you derive a time complexity expression, you may end up with something like O(2n + 5) or O(n² + n + 10).

Big O captures how fast your algorithm grows with input, not the exact number of steps.

Whether your algorithm takes `n` steps or `5n` steps, both grow linearly as `n` increases, so the constant multiplier doesn’t affect the growth trend. If you double the input, the runtime for both will roughly double.

So we drop constant factors:

- `O(2n²)` simplifies to `O(n²)`
- `O(5n + 100)` becomes `O(n)`
- `O(n/3)` simplifies to `O(n)`, since 1/3 is also just a constant factor

### Rule 4: Drop Lower-Order Terms

If your final expression has multiple terms, you keep only the one that grows the fastest, the dominant term, and drop the rest.

Why? Because as `n` becomes very large, slower-growing terms become insignificant.

Consider the expression O(n² + n + 100) with n = 1,000,000 (one million).

- `n²`, the dominant term, becomes one trillion
- `n` is just one million, and the constant term stays at 100

At scale, the lower-order terms barely make a dent in the overall growth. So we only keep the term that dominates.

Here are more examples:

- `O(n² + n)` simplifies to `O(n²)`
- `O(n³ + 10n)` becomes `O(n³)`
- `O(n³ + n² + n)` simplifies to `O(n³)`

Now that you understand what Big O notation means and how it helps us describe the growth rate of algorithms, it’s time to go one step deeper.

Big O gives us an upper bound. It tells us how fast an algorithm’s running time can grow in the worst case.

But not every input triggers that worst-case behavior. Some inputs make an algorithm run much faster, while others make it much slower.

So how do we capture that difference?

That’s where **best, worst, and average case complexity** comes in, a more nuanced way to describe how an algorithm behaves across different kinds of inputs.

In the next chapter, we’ll explore what these three cases mean, how to identify them, and why they matter when analyzing real-world algorithms.

## Quiz

### Introduction Quiz

10 quizzes

### Get Premium

Subscribe to unlock full access to all premium content

[Subscribe Now](https://algomaster.io/premium)