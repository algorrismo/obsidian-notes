

# 1. `==` (Double Equal)

👉 Called **loose equality**

> It compares values **but ignores type** (it can convert types automatically)

### Example

```javascript
console.log(5 == "5");
```

Output:

```
true
```

### Why?

Because JavaScript converts `"5"` → `5`

```text
5 == "5"
↓
5 == 5  → true
```

---

# 2. `===` (Triple Equal)

👉 Called **strict equality**

> It compares **value AND type** (no conversion)

### Example

```javascript
console.log(5 === "5");
```

Output:

```
false
```

### Why?

Because:

```text
5      → number
"5"    → string
```

Different types → ❌ false

---

# 3. Side-by-Side Comparison

|Comparison|Result|
|---|---|
|`5 == "5"`|✅ true|
|`5 === "5"`|❌ false|

---

# 4. More Examples (Very Important)

### Example 1

```javascript
console.log(null == undefined);   // true
console.log(null === undefined);  // false
```

👉 `==` treats both as “empty”  
👉 `===` sees different types

---

### Example 2

```javascript
console.log(0 == false);   // true
console.log(0 === false);  // false
```

👉 `==` converts `false → 0`  
👉 `===` does not convert

---

# 5. Easy Way to Remember 🧠

```text
==   → compares value only (does conversion)
===  → compares value + type (no conversion)
```

---

# 6. Which one should you use?

✅ **Always prefer `===` (strict equality)**

Why?

Because `==` can give **unexpected results**.

---

### Example problem

```javascript
console.log("" == 0);  // true 😨
```

This can cause bugs.

---

# 7. Real Developer Rule

```text
Use === in almost all cases
Avoid == unless you REALLY understand it
```

---

# Final Simple Summary

```text
==   → loose (type conversion happens)
===  → strict (no conversion)
```

---

