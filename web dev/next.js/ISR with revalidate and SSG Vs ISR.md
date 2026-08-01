**This is one of the most important Next.js concepts.**

# SSG (Static Site Generation)

Imagine you have a blog.

During **build time** (`npm run build`), Next.js fetches the data and generates the HTML.

```jsx
async function Page() {
  const posts = await getPosts();

  return <div>{posts.length}</div>;
}
```

### Build Time

```text
Database/API
      ↓
  npm run build
      ↓
 Static HTML generated
```

### After Deployment

```text
User
  ↓
Static HTML
```

No API calls.

Very fast.

### Problem

Suppose:

```text
Build time = 10 posts
```

Then later:

```text
Database = 15 posts
```

Users still see:

```text
10 posts
```

until you rebuild the app.

---

# ISR (Incremental Static Regeneration)

ISR solves this problem.

```jsx
async function Page() {
  const posts = await fetch(
    "https://api.com/posts",
    {
      next: { revalidate: 60 }
    }
  );

  return <div>...</div>;
}
```

### What happens?

Build time:

```text
API
 ↓
HTML generated
 ↓
Cached
```

Users get static pages (fast).

After 60 seconds:

```text
Cache becomes stale
```

The next visitor triggers a refresh:

```text
Visitor
   ↓
Next.js
   ↓
Fetch new data
   ↓
Update cache
```

Now everyone sees the updated page.

---

# Visual Comparison

## SSG

```text
Build
 ↓
Generate page
 ↓
Deploy
 ↓
Serve same page forever
```

No updates until rebuild.

---

## ISR

```text
Build
 ↓
Generate page
 ↓
Deploy
 ↓
Serve cached page
 ↓
Revalidate interval reached
 ↓
Fetch fresh data
 ↓
Update cached page
```

Updates automatically.

---

# SSG vs ISR

|Feature|SSG|ISR|
|---|---|---|
|Generated at build time|✅|✅|
|Fast|✅|✅|
|Updates automatically|❌|✅|
|Needs rebuild for new data|✅|❌|
|Uses `revalidate`|❌|✅|
|Best for|Docs, portfolio|Blogs, products, news|

---

# Real Example

Suppose you have an e-commerce store.

### SSG

```text
10:00 Build
Product price = $100

12:00 Admin changes price to $120

User visits
↓
Still sees $100
```

until you redeploy.

---

### ISR (`revalidate: 60`)

```text
10:00 Cache created
Price = $100

12:00 Admin changes price to $120

12:01 First visitor after cache expires
↓
Next.js fetches fresh data
↓
Cache updated

New visitors
↓
See $120
```

---

# Interview Answer

**SSG** generates pages once at build time and serves the same static page until the next deployment.

**ISR** is SSG plus automatic regeneration. Pages are generated statically, but Next.js refreshes them after a specified `revalidate` period, allowing users to see updated content without rebuilding the application.