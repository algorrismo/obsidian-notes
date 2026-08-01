
# 1. What is `undefined`?

👉 `undefined` means:

> **A variable exists, but it has no value assigned yet**

### Example

```javascript
let name;

console.log(name);
```

Output:

```
undefined
```

✔ JavaScript automatically gives `undefined` when:

- You declare a variable but don’t assign anything
- A function doesn’t return anything
- A parameter is missing

### More examples

```javascript
function test() {}

console.log(test()); // undefined
```

```javascript
function greet(name) {
  console.log(name);
}

greet(); // undefined
```

---

# 2. What is `null`?

👉 `null` means:

> **You intentionally set "no value"**

It’s like saying:

> “I know there should be a value, but right now it's empty.”

---

### Example

```javascript
let user = null;

console.log(user);
```

Output:

```
null
```

✔ You (the developer) assign `null` manually.

---

# 3. Key Difference (Very Important)

|Feature|undefined|null|
|---|---|---|
|Who sets it?|JavaScript|Developer|
|Meaning|Value not assigned|Intentionally empty|
|Type|undefined|object (weird JS behavior)|

---

# 4. Easy Way to Remember 🧠

Think like this:

```text
undefined → "I forgot to give a value"
null      → "I intentionally gave no value"
```

---

# 5. Real-Life Example

```javascript
let phoneNumber;

let address = null;
```

- `phoneNumber` → you didn’t set it yet → `undefined`
- `address` → you set it to empty on purpose → `null`

---

# 6. Comparison (Important)

```javascript
console.log(undefined == null);  // true
console.log(undefined === null); // false
```


---

# 7. When to use what?

✅ Use `undefined`:

- Usually automatically by JS
- You don’t need to set it manually

✅ Use `null`:

- When you want to **clear a value intentionally** 
- Example: resetting data

```javascript
let user = { name: "Ismail" };

user = null; // cleared intentionally
```

---

# Final Simple Summary

```text
undefined = value is missing (JS gives it)
null      = value is empty (you give it)
```

