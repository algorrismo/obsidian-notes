The key lesson is:

> **`use()` is for Promises (or React resources), not for normal JavaScript objects.**

### What happened in your code?

You fetched the data:

```jsx
const res = await fetch(...);
const data = await res.json();
```

After `await`, `data` is no longer a Promise.

It's already a normal object:

```js
{
  data: [...]
}
```

Then you passed one food item to `FoodCard`:

```jsx
<FoodCard data={data} />
```

Inside `FoodCard`, `data` is a plain object, so you should use it directly:

```jsx
const FoodCard = ({ data }) => {
  return <h1>{data.name}</h1>;
};
```

Instead, you did:

```jsx
const foodData = use(data);
```

React said:

> "I expected a Promise, but you gave me an Object."

Hence the error:

```txt
An unsupported type was passed to use(): [object Object]
```

---

## A quick rule to remember

Ask yourself:

### Is this a Promise?

```jsx
const userPromise = fetch("/api/user");
```

✅ Then `use()` can be used.

### Is this already the data?

```jsx
const user = await fetch(...).then(res => res.json());
```

✅ Use it directly.

❌ Don't wrap it in `use()`.

---

## Mental model

Think of `use()` as:

```txt
Promise  ---> use() ---> Actual Data
```

Example:

```jsx
const promise = fetch("/api/users").then(res => res.json());

const users = use(promise);
```

But if you already have:

```jsx
const users = await fetch(...).then(res => res.json());
```

then:

```jsx
use(users); // ❌ wrong
```

because the Promise has already been resolved.

---

## How to avoid this mistake in the future

Whenever you see `use(something)`, ask:

1. **What is the type of `something`?**
    
2. Is it a Promise?
    
    - ✅ Yes → `use()` may be correct.
        
    - ❌ No → don't use `use()`.
        

A debugging trick:

```jsx
console.log(data);
```

If the console shows:

```js
Promise { <pending> }
```

then `use(data)` might make sense.

If it shows:

```js
{
  id: 1,
  name: "Burger"
}
```

then it's already data, so don't use `use()`.

---

Since you're learning Next.js, focus first on understanding:

1. **Props** (`<FoodCard data={food} />`)
    
2. **State** (`useState`)
    
3. **Effects** (`useEffect`)
    
4. **Server Components vs Client Components**
    
5. Then learn **React's `use()` hook**
    

`use()` is a newer React feature, and many beginners try to use it where normal props are enough. In your example, you simply received a prop and should read it directly.