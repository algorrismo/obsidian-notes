
Users
 ├── UserID (PK)
 ├── Name
 └── Email

Complaints
 ├── ComplaintID (PK)
 ├── UserID (FK)
 ├── CategoryID (FK)
 ├── StatusID (FK)
 └── Location

Categories
 ├── CategoryID (PK)
 └── Name

Statuses
 ├── StatusID (PK)
 └── Status