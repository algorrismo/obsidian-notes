If you've already created a Next.js project locally, you can connect it to a GitHub repository in a few steps.

### 1. Check if Git is already initialized

Open your terminal in the project folder:

```bash
git status
```

If you see something like:

```bash
On branch main
```

then Git is already initialized.

If not:

```bash
git init
```

---

### 2. Create a repository on GitHub

Go to:

[GitHub](https://github.com/?utm_source=chatgpt.com)

Click **New Repository** and create:

```text
example-repo
```

**Important:** Don't add README, .gitignore, or license if your local project already exists.

After creating it, GitHub will show commands similar to:

```bash
git remote add origin https://github.com/your-username/example-repo.git
git branch -M main
git push -u origin main
```

---

### 3. Check whether a remote already exists

Run:

```bash
git remote -v
```

If nothing appears, add the GitHub repo:

```bash
git remote add origin https://github.com/your-username/qurbani-hat.git
```

---

### 4. If your project is already connected to another repository

You'll see something like:

```bash
origin  https://github.com/old-user/old-repo.git
```

Remove it:

```bash
git remote remove origin
```

Then add your new repository:

```bash
git remote add origin https://github.com/your-username/qurbani-hat.git
```

---

### 5. Push your code

If you haven't committed yet:

```bash
git add .
git commit -m "Initial project setup"
```

Then:

```bash
git branch -M main
git push -u origin main
```

---

### 6. Verify

Run:

```bash
git remote -v
```

You should see:

```bash
origin  https://github.com/your-username/qurbani-hat.git
origin  https://github.com/your-username/qurbani-hat.git
```

---

If you're unsure whether your current Next.js project is already connected to a repository, paste the output of:

```bash
git remote -v
git status
```

and I'll tell you exactly what command to run next.