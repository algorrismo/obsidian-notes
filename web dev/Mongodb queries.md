# 🍃 MongoDB Operators & Queries — Complete Notes

> **Use Case Throughout:** A Job Portal (like LinkedIn/Bdjobs) with 20 job documents in a `jobs` collection.

---

## 📦 Sample Data Structure

Each job document looks like this:

```json
{
  "title": "Software Engineer",
  "company": "TechCorp Bangladesh",
  "location": "Dhaka",
  "salary": 75000,
  "experience": 3,
  "skills": ["JavaScript", "Node.js", "MongoDB"],
  "isRemote": false,
  "applicants": 120,
  "posted": "2024-01-15T00:00:00.000Z",
  "status": "active",
  "department": "Engineering"
}
```

**Insert all 20 fake jobs** then verify:

```js
db.jobs.countDocuments()  // Should return 20
db.jobs.findOne()         // Shows the first document
```

---

## 1️⃣ Comparison Operators

> These filter documents by **comparing field values** to a given number or string.

|Operator|Meaning|
|---|---|
|`$eq`|Equal to|
|`$ne`|Not equal to|
|`$gt`|Greater than|
|`$gte`|Greater than or equal|
|`$lt`|Less than|
|`$lte`|Less than or equal|

---

### `$eq` — Equal

**Think of it as:** "Give me only THIS exact value."

```js
// Find jobs in Dhaka
db.jobs.find({ location: { $eq: "Dhaka" } })

// Shorthand (same result — $eq is MongoDB's default behavior)
db.jobs.find({ location: "Dhaka" })
```

> 💡 You almost never need to write `$eq` explicitly. `{ field: value }` does the same thing.

---

### `$ne` — Not Equal

**Think of it as:** "Give me everything EXCEPT this value."

```js
// All jobs NOT in Dhaka (Chittagong, Sylhet, Rajshahi, Khulna...)
db.jobs.find({ location: { $ne: "Dhaka" } })
```

---

### `$gt` — Greater Than

**Think of it as:** "Salary must be MORE than this number (not including it)."

```js
// Jobs with salary above 70,000
db.jobs.find({ salary: { $gt: 70000 } })
// Returns: Software Engineer (75k), DevOps (90k), Project Manager (95k), etc.
```

---

### `$gte` — Greater Than or Equal

**Think of it as:** "Salary must be THIS number OR more."

```js
// Jobs with salary 70,000 or above (includes 70k itself)
db.jobs.find({ salary: { $gte: 70000 } })
```

> 💡 Difference: `$gt: 70000` skips 70k. `$gte: 70000` includes 70k.

---

### `$lt` — Less Than

**Think of it as:** "Salary must be BELOW this number."

```js
// Entry-level jobs with salary below 50,000
db.jobs.find({ salary: { $lt: 50000 } })
// Returns: QA Engineer (45k), Technical Writer (40k), Intern (15k)
```

---

### `$lte` — Less Than or Equal

**Think of it as:** "Salary must be THIS number OR below."

```js
db.jobs.find({ salary: { $lte: 50000 } })
```

---

### Combining Comparison Operators

**Same field — range query:**

```js
// Salary between 50k and 90k (inclusive)
db.jobs.find({
  salary: { $gte: 50000, $lte: 90000 }
})
```

**Different fields — multiple conditions:**

```js
// Experience > 3 years AND salary > 60k
db.jobs.find({
  experience: { $gt: 3 },
  salary: { $gt: 60000 }
})
```

> 💡 When you put two separate field conditions in one `find()`, MongoDB treats it as AND automatically.

---

## 2️⃣ Logical Operators

> These combine **multiple conditions** together.

|Operator|Meaning|
|---|---|
|`$and`|ALL conditions must be true|
|`$or`|ANY one condition is enough|
|`$not`|Reverses/negates a condition|
|`$nor`|ALL conditions must be false|

---

### `$and` — All Must Be True

**Think of it as:** "I want jobs in Dhaka AND salary above 70k — both must match."

```js
db.jobs.find({
  $and: [
    { location: "Dhaka" },
    { salary: { $gt: 70000 } }
  ]
})

// Shorthand (implicit $and — same result for different fields)
db.jobs.find({ location: "Dhaka", salary: { $gt: 70000 } })
```

> 💡 If two conditions are on **different fields**, you can skip writing `$and`. But if two conditions are on the **same field**, you must use `$and` explicitly.

---

### `$or` — Any One Is Enough

**Think of it as:** "Show me jobs in Dhaka OR Chittagong — either city is fine."

```js
db.jobs.find({
  $or: [
    { location: "Dhaka" },
    { location: "Chittagong" }
  ]
})

// Another example: salary above 1 lakh OR remote job
db.jobs.find({
  $or: [
    { salary: { $gt: 100000 } },
    { isRemote: true }
  ]
})
```

---

### `$not` — Negate a Condition

**Think of it as:** "Give me the opposite of this filter."

```js
// NOT greater than 50k = 50k or below
db.jobs.find({
  salary: { $not: { $gt: 50000 } }
})
```

> 💡 `$not` always wraps another operator expression. You can't use it directly with a plain value.

---

### `$nor` — None Can Be True

**Think of it as:** "I don't want Dhaka AND I don't want Remote — give me everything else."

```js
// Not in Dhaka AND not remote = other cities, office jobs only
db.jobs.find({
  $nor: [
    { location: "Dhaka" },
    { isRemote: true }
  ]
})
// Returns: Chittagong, Sylhet, Rajshahi, Khulna non-remote jobs
```

---

## 3️⃣ Element & Type Operators

> These don't compare **values** — they check if a **field exists** or what **data type** it holds.

---

### `$exists` — Does the Field Exist?

**Think of it as:** "Does this document even have a salary field?"

```js
// Jobs that HAVE a salary field
db.jobs.find({ salary: { $exists: true } })

// Jobs that DON'T have a salary field
db.jobs.find({ salary: { $exists: false } })
```

**Practice — insert a doc without salary:**

```js
db.jobs.insertOne({
  title: "Unpaid Intern",
  company: "StartupXYZ",
  location: "Dhaka",
  experience: 0
})

// Now this query will return only the Unpaid Intern
db.jobs.find({ salary: { $exists: false } })
```

---

### `$type` — What Data Type Is the Field?

**Think of it as:** "Is salary actually stored as a number, or accidentally as a string?"

```js
// salary fields that are numbers
db.jobs.find({ salary: { $type: "number" } })

// skills fields that are arrays
db.jobs.find({ skills: { $type: "array" } })

// posted fields that are dates
db.jobs.find({ posted: { $type: "date" } })
```

**Common BSON Types:**

|Type Name|Number|
|---|---|
|`double`|1|
|`string`|2|
|`object`|3|
|`array`|4|
|`boolean`|8|
|`date`|9|
|`null`|10|
|`int`|16|

> 💡 Best used for **data validation** and **cleaning messy/mixed data**.

---

## 4️⃣ Array Query Operators

> The `skills` field in our data is an **array**. These operators let you search inside arrays.

|Operator|Meaning|
|---|---|
|`$in`|Match ANY one value from a list|
|`$nin`|Match NONE of the values in a list|
|`$all`|Match ALL values in a list|
|`$size`|Match arrays of a specific length|
|`$elemMatch`|Apply multiple conditions to a single array element|

---

### `$in` — Any One Match Is Enough

**Think of it as:** "Show me jobs that need Python OR JavaScript."

```js
// Jobs requiring Python or JavaScript (either one is fine)
db.jobs.find({
  skills: { $in: ["Python", "JavaScript"] }
})

// Works on regular fields too
db.jobs.find({
  location: { $in: ["Dhaka", "Chittagong", "Sylhet"] }
})
```

---

### `$nin` — Not In (None Should Match)

**Think of it as:** "Give me jobs that DON'T require Python or JavaScript."

```js
db.jobs.find({
  skills: { $nin: ["Python", "JavaScript"] }
})
```

---

### `$all` — Every Value Must Be Present

**Think of it as:** "I need jobs that require BOTH Python AND SQL — not just one."

```js
// Jobs that require BOTH Python AND SQL
db.jobs.find({
  skills: { $all: ["Python", "SQL"] }
})
```

> 💡 Key difference:
> 
> - `$in` = "at least one of these"
> - `$all` = "all of these must be present"

---

### `$size` — Exact Array Length

**Think of it as:** "Show me jobs that list exactly 3 required skills."

```js
db.jobs.find({ skills: { $size: 3 } })
```

> 💡 `$size` only works for exact counts. For "more than 3 skills", you need aggregation or `$where`.

---

### `$elemMatch` — Multiple Conditions on ONE Array Element

**Think of it as:** "Find a job where a SINGLE interview round has score > 80 AND passed: true — both in the same round."

First, insert test data:

```js
db.jobs.insertOne({
  title: "Senior Developer",
  company: "BigTech",
  interviews: [
    { round: 1, score: 85, passed: true },
    { round: 2, score: 70, passed: false }
  ]
})
```

```js
// Find where ONE interview round has score > 80 AND passed: true
db.jobs.find({
  interviews: {
    $elemMatch: {
      score: { $gt: 80 },
      passed: true
    }
  }
})
```

> 💡 Without `$elemMatch`, MongoDB checks conditions across **different array elements** (score > 80 could match round 1, passed: true could match round 2 — still passes!). `$elemMatch` forces **both conditions on the same element**.

---

## 5️⃣ Update Operators

> These **modify** existing documents. We've been reading data so far — now we change it.

|Operator|Meaning|
|---|---|
|`$set`|Set/change a field's value|
|`$inc`|Increment or decrement a number|
|`$push`|Add an item to an array|
|`$pull`|Remove an item from an array|
|`$addToSet`|Add to array only if not already there (no duplicates)|

---

### `$set` — Set a Field's Value

**Think of it as:** "Change the salary of this job to 80,000."

```js
// Update one job's salary
db.jobs.updateOne(
  { title: "Software Engineer", company: "TechCorp Bangladesh" },
  { $set: { salary: 80000 } }
)

// Update multiple fields at once
db.jobs.updateOne(
  { title: "Software Engineer" },
  { $set: { salary: 80000, status: "hiring", updatedAt: new Date() } }
)
```

> 💡 `$set` can **add a new field** that didn't exist, or **update an existing one**.

---

### `$inc` — Increment or Decrement

**Think of it as:** "10 new people applied to this job — add 10 to the applicants count."

```js
// Add 10 applicants
db.jobs.updateOne(
  { title: "Data Analyst" },
  { $inc: { applicants: 10 } }
)

// Remove 5 applicants (use negative number)
db.jobs.updateOne(
  { title: "Data Analyst" },
  { $inc: { applicants: -5 } }
)
```

> 💡 Perfect for counters, scores, view counts — anything you add/subtract from.

---

### `$push` — Add Item to Array

**Think of it as:** "This job now also requires TypeScript — add it to the skills list."

```js
// Add one skill
db.jobs.updateOne(
  { title: "Frontend Developer" },
  { $push: { skills: "TypeScript" } }
)

// Add multiple skills at once using $each
db.jobs.updateOne(
  { title: "Frontend Developer" },
  { $push: { skills: { $each: ["TypeScript", "GraphQL"] } } }
)
```

---

### `$pull` — Remove Item from Array

**Think of it as:** "Sketch is no longer required for the designer role — remove it."

```js
db.jobs.updateOne(
  { title: "UI/UX Designer" },
  { $pull: { skills: "Sketch" } }
)
```

> 💡 `$pull` removes **all matching values** from the array.

---

### `$addToSet` — Add Only If Not a Duplicate

**Think of it as:** "Add TypeScript to skills, but only if it's not already there."

```js
db.jobs.updateOne(
  { title: "Frontend Developer" },
  { $addToSet: { skills: "TypeScript" } }
)
```

> 💡 Difference from `$push`: `$push` always adds (even duplicates). `$addToSet` skips if it already exists.

---

## 6️⃣ Projection & Sorting

### Projection — Show Only the Fields You Need

> By default, `find()` returns every field. Projection lets you pick only what you want.

**Include fields (use `1`):**

```js
// Show only title, company, salary
db.jobs.find({}, { title: 1, company: 1, salary: 1 })

// Hide _id too
db.jobs.find({}, { title: 1, company: 1, salary: 1, _id: 0 })
```

**Exclude fields (use `0`):**

```js
// Show everything EXCEPT _id and applicants
db.jobs.find({}, { _id: 0, applicants: 0 })
```

> ⚠️ **CRITICAL RULE:** You cannot mix `1` and `0` in the same projection — **except** for `_id`. Either include what you want OR exclude what you don't.

---

### `sort()` — Order the Results

**`1` = ascending (small → big), `-1` = descending (big → small)**

```js
// Jobs sorted by salary: highest first
db.jobs.find({}, { title: 1, salary: 1, _id: 0 }).sort({ salary: -1 })

// Sort by location A→Z, then within same location by salary high→low
db.jobs.find().sort({ location: 1, salary: -1 })
```

---

### `limit()` and `skip()` — Pagination

```js
// First 5 jobs only
db.jobs.find().limit(5)

// Page 2 (skip first 5, show next 5)
db.jobs.find().skip(5).limit(5)
```

**Full pagination example — sorted, filtered, paginated:**

```js
// Active jobs, sorted by salary desc, page 2 (items 6–10)
db.jobs.find(
  { status: "active" },
  { title: 1, salary: 1, company: 1, _id: 0 }
).sort({ salary: -1 }).skip(5).limit(5)
```

---

## 7️⃣ Aggregation Pipeline

> `find()` reads data. **Aggregation** analyzes it. Think of it like an **assembly line** — each stage's output becomes the next stage's input.

### `$match` — Filter (Like `find()`)

**Think of it as:** "Before calculating anything, first filter to active jobs only."

```js
db.jobs.aggregate([
  { $match: { status: "active" } }
])
```

> 💡 Always put `$match` **first** in your pipeline — it reduces data early, making all later stages faster.

---

### `$group` — Group and Calculate

**Think of it as:** "Group all jobs by city, then count how many are in each city."

```js
// How many jobs per city?
db.jobs.aggregate([
  { $group: {
    _id: "$location",       // group by this field
    totalJobs: { $sum: 1 }  // count each document as 1
  }}
])

// Average/max/min salary per city
db.jobs.aggregate([
  { $group: {
    _id: "$location",
    avgSalary: { $avg: "$salary" },
    maxSalary: { $max: "$salary" },
    minSalary: { $min: "$salary" },
    totalJobs: { $sum: 1 }
  }}
])
```

**Accumulator operators for `$group`:**

|Operator|Meaning|
|---|---|
|`$sum`|Total (or count with `$sum: 1`)|
|`$avg`|Average|
|`$max`|Highest value|
|`$min`|Lowest value|
|`$push`|Collect all values into an array|
|`$first`|First value in the group|

---

### `$project` — Shape the Output

**Think of it as:** "Clean up the output — rename fields, hide `_id`, create calculated fields."

```js
// Show only title and company, hide _id
db.jobs.aggregate([
  { $project: {
    title: 1,
    company: 1,
    _id: 0
  }}
])

// Create a new calculated field: annual salary
db.jobs.aggregate([
  { $project: {
    title: 1,
    salary: 1,
    annualSalary: { $multiply: ["$salary", 12] }
  }}
])
```

---

### Chaining Pipeline Stages

```js
// Active jobs → group by department → average salary → sort by avg salary
db.jobs.aggregate([
  { $match: { status: "active" } },
  { $group: {
    _id: "$department",
    avgSalary: { $avg: "$salary" },
    jobCount: { $sum: 1 }
  }},
  { $project: {
    department: "$_id",
    avgSalary: { $round: ["$avgSalary", 0] },
    jobCount: 1,
    _id: 0
  }},
  { $sort: { avgSalary: -1 } }
])
```

---

## 8️⃣ Advanced Aggregation

### Setup — Create a `companies` Collection

```js
db.companies.insertMany([
  { name: "TechCorp Bangladesh", founded: 2015, employees: 500, industry: "Software" },
  { name: "Digital Solutions",   founded: 2018, employees: 120, industry: "Web" },
  { name: "AIVentures",          founded: 2020, employees: 80,  industry: "AI/ML" },
  { name: "CloudBase Ltd",       founded: 2017, employees: 200, industry: "Cloud" },
  { name: "CreativeMinds",       founded: 2019, employees: 50,  industry: "Design" }
])
```

---

### `$lookup` — Join Two Collections (Like SQL JOIN)

**Think of it as:** "For each job, also pull in the full company info from the companies collection."

```js
db.jobs.aggregate([
  {
    $lookup: {
      from: "companies",        // the OTHER collection to join
      localField: "company",    // field in jobs collection
      foreignField: "name",     // matching field in companies collection
      as: "companyDetails"      // name of the new joined field (comes as an array)
    }
  },
  { $project: { title: 1, salary: 1, companyDetails: 1, _id: 0 } },
  { $limit: 5 }
])
```

> 💡 `$lookup` result (`companyDetails`) comes as an **array**. Use `$unwind` to flatten it.

---

### `$unwind` — Flatten an Array Field

**Think of it as:** "Turn `companyDetails: [{ ... }]` into `companyDetails: { ... }` — one doc per array element."

```js
db.jobs.aggregate([
  {
    $lookup: {
      from: "companies",
      localField: "company",
      foreignField: "name",
      as: "companyDetails"
    }
  },
  { $unwind: "$companyDetails" },
  {
    $project: {
      title: 1,
      salary: 1,
      "companyDetails.industry": 1,
      "companyDetails.employees": 1,
      _id: 0
    }
  }
])
```

---

### `$facet` — Run Multiple Pipelines in One Query

**Think of it as:** "In one API call, give me: salary buckets, jobs by city, AND jobs by department."

```js
db.jobs.aggregate([
  { $match: { status: "active" } },
  {
    $facet: {
      // Breakdown 1: salary ranges
      salaryBuckets: [
        { $bucket: {
          groupBy: "$salary",
          boundaries: [0, 30000, 60000, 90000, 150000],
          default: "Other",
          output: { count: { $sum: 1 }, avgSalary: { $avg: "$salary" } }
        }}
      ],
      // Breakdown 2: jobs by location
      byLocation: [
        { $group: { _id: "$location", total: { $sum: 1 } } },
        { $sort: { total: -1 } }
      ],
      // Breakdown 3: top 5 departments by avg salary
      byDepartment: [
        { $group: { _id: "$department", avgSalary: { $avg: "$salary" } } },
        { $sort: { avgSalary: -1 } },
        { $limit: 5 }
      ]
    }
  }
])
```

> 💡 `$facet` is great for **dashboards** — one query returns all the analytics data you need.

---

## 🚀 Capstone Query — Everything Together

**Scenario:** HR report — Dhaka or Remote active jobs, 3+ years experience, grouped by department with avg salary, total jobs, and top job by applicants.

```js
db.jobs.aggregate([
  // Step 1: Filter
  { $match: {
    $or: [{ location: "Dhaka" }, { isRemote: true }],
    status: "active",
    experience: { $gte: 3 }
  }},

  // Step 2: Group by department
  { $group: {
    _id: "$department",
    avgSalary:     { $avg: "$salary" },
    totalJobs:     { $sum: 1 },
    maxApplicants: { $max: "$applicants" },
    topJob:        { $first: "$title" }
  }},

  // Step 3: Clean up output
  { $project: {
    department:    "$_id",
    avgSalary:     { $round: ["$avgSalary", 0] },
    totalJobs:     1,
    maxApplicants: 1,
    topJob:        1,
    _id:           0
  }},

  // Step 4: Sort by highest avg salary
  { $sort: { avgSalary: -1 } }
])
```

---

## 📋 Quick Reference Cheatsheet

### Comparison

```
$eq   →  equal
$ne   →  not equal
$gt   →  greater than
$gte  →  greater than or equal
$lt   →  less than
$lte  →  less than or equal
```

### Logical

```
$and  →  all conditions must be true
$or   →  at least one condition must be true
$not  →  negate/reverse a condition
$nor  →  all conditions must be false
```

### Element

```
$exists  →  check if field exists (true/false)
$type    →  check data type of a field
```

### Array

```
$in         →  match ANY value from a list
$nin        →  match NONE of the values in a list
$all        →  ALL listed values must exist in array
$size       →  array must have exactly N elements
$elemMatch  →  multiple conditions on a single array element
```

### Update

```
$set       →  set/create a field value
$inc       →  increment or decrement a number
$push      →  add item to array (allows duplicates)
$pull      →  remove matching item from array
$addToSet  →  add to array only if not duplicate
```

### Aggregation

```
$match    →  filter (like find)
$group    →  group + calculate (sum, avg, max, min)
$project  →  reshape output, add calculated fields
$sort     →  order results
$limit    →  max number of results
$skip     →  skip N results (pagination)
$lookup   →  join with another collection
$unwind   →  flatten array field into separate docs
$facet    →  run multiple pipelines simultaneously
```

---

## 💡 Next Steps

- **MongoDB Indexes** — Speed up queries
- **Mongoose ODM** — Use MongoDB with Node.js
- **MongoDB Atlas** — Cloud database setup
- **Transactions** — Multiple operations atomically
- **Schema Validation** — Enforce data rules

---

_Notes based on MongoDB Operators & Queries module — Job Portal dataset_
