
# Project Prompt

Build a full-stack Inventory Management System using Next.js (App Router), PostgreSQL, Prisma ORM, Tailwind CSS, and Auth.js.

## Project Overview

The system has two parts:

### 1. Customer Side

Customers can only view products.

They cannot:

- Login
    
- Buy products
    
- Add products
    
- Edit products
    
- Delete products
    

Customers can:

- View all products
    
- View available stock
    
- View selling price
    
- Search products
    
- Filter products
    

---

### 2. Admin Dashboard

Only authenticated admins can access the dashboard.

Admins can:

- Add products
    
- Edit products
    
- Delete products
    
- Manage stock
    
- Record sales
    
- Record returned products
    
- View inventory reports
    
- View profit information
    

---

# Product Fields

Each product should contain:

```txt
Date
Company Name
SKU
Product Name
Stock
Buying Price
Transportation Cost
Packaging Cost
Discount Commission
Selling Price
Returned Product
```

---

# Calculated Fields

Do NOT store these directly in the database.

Calculate them automatically.

### Total Cost

```txt
Buying Price +
Transportation Cost +
Packaging Cost
```

### Profit

```txt
Selling Price -
Total Cost -
Discount Commission
```

Display these values wherever necessary.

---

# Database Models

## Product

```txt
id
date
companyName
sku
productName
stock
buyingPrice
transportationCost
packagingCost
discountCommission
sellingPrice
returnedProduct
createdAt
updatedAt
```

---

## Sale

```txt
id
productId
quantity
saleDate
createdAt
```

---

# Customer Pages

## Home Page

Display all products in cards or a table.

Show:

```txt
Product Name
Available Stock
Selling Price
```

Add:

```txt
Search Bar
Filter Option
```

---

## Product Details Page

Dynamic route:

```txt
/products/[id]
```

Display:

```txt
Product Name
Company Name
SKU
Stock
Selling Price
```

---

# Authentication

Use Auth.js.

Create:

```txt
/login
```

Only authenticated admins can access:

```txt
/admin
```

Unauthenticated users should be redirected to login.

---

# Admin Dashboard

Create:

```txt
/ admin
```

Dashboard cards:

```txt
Total Products
Total Stock
Total Sales
Total Returned Products
Total Estimated Profit
```

---

# Product Management

Create:

```txt
/ admin/products
```

Display products in a table.

Columns:

```txt
Product Name
Company Name
SKU
Stock
Selling Price
Actions
```

Actions:

```txt
Edit
Delete
View
```

---

# Add Product Page

Create:

```txt
/admin/products/add
```

Form fields:

```txt
Date
Company Name
SKU
Product Name
Stock
Buying Price
Transportation Cost
Packaging Cost
Discount Commission
Selling Price
```

Validation:

- Required fields
    
- Positive numbers only
    
- Unique SKU
    

---

# Edit Product Page

Create:

```txt
/admin/products/edit/[id]
```

Allow updating all product information.

---

# Delete Product

Allow admins to delete products.

Show confirmation modal before deletion.

---

# Record Sale Feature

Create:

```txt
/admin/sales
```

Admin selects:

```txt
Product
Quantity Sold
```

When a sale is recorded:

```txt
Stock = Stock - Quantity Sold
```

Store the sale in the Sale table.

Prevent negative stock.

---

# Sales History

Display:

```txt
Sale ID
Product Name
Quantity Sold
Sale Date
```

Add pagination.

---

# Returned Products Feature

Create:

```txt
/admin/returns
```

Admin selects:

```txt
Product
Returned Quantity
```

When returned:

```txt
returnedProduct += quantity
stock += quantity
```

Store return history.

---

# Search and Filtering

Allow search by:

```txt
Product Name
Company Name
SKU
```

Allow filtering by:

```txt
Company
Stock Availability
Date
```

---

# UI Requirements

Use:

- Next.js App Router
    
- Tailwind CSS
    
- Responsive Design
    
- Clean Admin Dashboard
    
- Sidebar Navigation
    
- Mobile Friendly Layout
    

Sidebar Items:

```txt
Dashboard
Products
Add Product
Sales
Returns
Settings
Logout
```

---

# Tech Stack

Frontend:

- Next.js
    
- Tailwind CSS
    

Backend:

- Next.js Server Actions
    
- Route Handlers
    

Database:

- PostgreSQL
    

ORM:

- Prisma
    

Authentication:

- Auth.js
    

Deployment:

- Vercel
    

---

# Folder Structure

```txt
src
│
├── app
│   ├── page.jsx
│   ├── login
│   ├── products
│   ├── admin
│   │   ├── page.jsx
│   │   ├── products
│   │   ├── sales
│   │   └── returns
│
├── components
│   ├── Navbar
│   ├── Sidebar
│   ├── ProductCard
│   ├── ProductTable
│   └── Forms
│
├── lib
│   ├── prisma.js
│   └── auth.js
│
└── prisma
    └── schema.prisma
```

---

One suggestion: **don't ask the AI to generate the whole project at once.** Instead, ask:

1. "Create the Prisma schema."
    
2. "Create the Product model."
    
3. "Create the Add Product page."
    
4. "Create the Product List page."
    
5. "Create the Record Sale feature."
    

Building it feature-by-feature will help you learn much more and make debugging far easier.

Did you want this project to use **JavaScript only**, or are you willing to learn **TypeScript** while building it? For a new Next.js project in 2026, I'd lean toward TypeScript if you're comfortable learning it gradually.