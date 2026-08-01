
# 🔹 What is `async` and `await` in JavaScript?

👉 `async` and `await` are used to handle **asynchronous operations** in a **clean and simple way**

They make async code look like **normal synchronous code**.

---

# 🔸 Simple Definition

|Keyword|Meaning|
|---|---|
|`async`|makes a function asynchronous|
|`await`|waits for an async task to finish|

---

# 🔸 Why we need async/await?

Some tasks take time ⏳

Examples:

- fetching data from API 🌐
    
- reading database 📂
    
- loading image 🖼️
    
- timer ⏰
    

JavaScript does **not want to stop everything** while waiting.

So it uses **asynchronous behavior**.

---

# 🔸 Basic Example

```javascript
async function example() {
  return "Hello";
}
```

👉 `async` automatically returns a **Promise**

---

# 🔸 Real Example with API (Important)

```javascript
async function getUsers() {

  const response = await fetch("https://jsonplaceholder.typicode.com/users");

  const data = await response.json();

  console.log(data);
}

getUsers();
```

---

# 🔍 Step-by-step: how it works

### 1️⃣ `async function`

```javascript
async function getUsers() {}
```

👉 tells JavaScript:

> this function may take time

---

### 2️⃣ `await fetch(...)`

```javascript
const response = await fetch(url);
```

👉 JS pauses **inside the function only**  
👉 waits until data comes from server

---

### 3️⃣ Convert response to JSON

```javascript
const data = await response.json();
```

👉 API usually sends JSON

---

### 4️⃣ Use the data

```javascript
console.log(data);
```

---

# 🔸 Without async/await (harder)

```javascript
fetch(url)
  .then(response => response.json())
  .then(data => console.log(data));
```

---

# 🔸 With async/await (cleaner)

```javascript
const response = await fetch(url);
const data = await response.json();
```

👉 easier to read  
👉 looks synchronous  
👉 less confusing for beginners

---

# 🔸 Important Rules ⚠️

### Rule 1:

`await` can only be used inside async function

❌ Wrong

```javascript
await fetch(url);
```

✅ Correct

```javascript
async function test() {
  await fetch(url);
}
```

---

### Rule 2:

`async` function always returns Promise

```javascript
async function test() {
  return 10;
}
```

Actually returns:

```javascript
Promise {10}
```

---

# 🔸 Real Life Analogy ☕

Imagine ordering coffee:

### Normal async (Promise style)

You keep checking:  
"Is coffee ready?"  
"Is coffee ready?"  
"Is coffee ready?"

### async/await style

You say:  
"I'll wait here until coffee is ready"

Much simpler 😄

---

# 🔸 When should you use async/await?

Use when working with:

### 🌐 API calls

```javascript
fetch()
```

### 📂 database request

```javascript
getUser()
```

### ⏰ timers

```javascript
setTimeout()
```

### 📡 loading external data

- AI API
    
- weather API
    
- login system
    
- payment system
    

---

# 🔸 Example with error handling (Best Practice)

```javascript
async function getData() {
  try {

    const response = await fetch("https://api.example.com/data");

    const data = await response.json();

    console.log(data);

  } catch (error) {

    console.log("Error:", error);

  }
}
```

👉 `try...catch` handles errors safely

---

# 🔻 One-line summary

👉 `async/await` lets you write asynchronous code in a synchronous style.

---
