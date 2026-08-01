
---

# 🔹 Synchronous vs Asynchronous in JavaScript

## 1️⃣ Synchronous Function (Sync)

👉 **Runs step by step**  
👉 Each line **waits** for the previous line to finish

### Example

```javascript
console.log("Task 1");
console.log("Task 2");
console.log("Task 3");
```

### Output:

```
Task 1
Task 2
Task 3
```

🧠 Explanation:

- JS executes line 1 → finishes
    
- then line 2 → finishes
    
- then line 3 → finishes
    

Everything happens **in order**

---

## 2️⃣ Asynchronous Function (Async)

👉 Does **NOT wait**  
👉 Some tasks run in the background ⏳  
👉 JS continues executing next lines

Used when task takes time:

- API request (fetch)
    
- timer
    
- reading file
    
- database query
    

---

### Example with `setTimeout`

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Hello after 2 sec");
}, 2000);

console.log("End");
```

### Output:

```
Start
End
Hello after 2 sec
```

🧠 Explanation:

- JS runs "Start"
    
- `setTimeout` takes 2 seconds → runs in background
    
- JS doesn't wait → prints "End"
    
- after 2 sec → prints message
    

---

# 🔸 Visual Comparison

### Synchronous 🧱

```
Task 1 → Task 2 → Task 3
(wait)   (wait)   (wait)
```

### Asynchronous ⚡

```
Task 1 → Task 2 → Task 3
            ↓
         runs later
```

---

# 🔸 Async Example with fetch()

```javascript
fetch("https://api.example.com/data")
  .then(response => response.json())
  .then(data => console.log(data));

console.log("This runs first!");
```

👉 API takes time → so JS continues running other code

---

# 🔸 async / await (Modern Way)

```javascript
async function getData() {
  const response = await fetch("https://api.example.com/data");
  const data = await response.json();

  console.log(data);
}
```

👉 `await` makes async code look like sync (easier to understand)

---

# 🔻 One-line Difference

|Type|Meaning|
|---|---|
|Synchronous|runs line by line (waits)|
|Asynchronous|runs in background (does not wait)|

---

# 🔥 Real Life Example

### Synchronous 🚶

Ordering tea and **waiting** until ready before doing anything else

### Asynchronous 🏃

Ordering tea and **checking your phone while waiting**

---
