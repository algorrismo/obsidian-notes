Tags : #SRE
date : 2026-07-10

---

**Working title:** FixMyCity — A Citizen Complaint Reporting and Resolution App

**The problem:** Citizens have no easy way to report civic issues (potholes, streetlight outages, garbage dumps, water leakage, broken drainage) with location proof, and no way to track whether authorities acted on it. Complaints made via phone calls or in-person visits get lost, duplicated, or ignored.

**Users:**

- Citizens (report issues, upload photo + GPS location, track status)
- Municipal staff / field workers (view assigned issues, update status, upload proof of resolution)
- Admin (department head — assigns issues to staff, views analytics, manages categories)

**Core system features (maps to Section 3):**

1. Issue Reporting (photo, geotag, category, description)
2. Issue Tracking & Status Updates (Reported → Assigned → In Progress → Resolved)
3. Duplicate Detection (flag issues reported near same location/category)
4. Notifications (SMS/email/push on status change)
5. Admin Dashboard & Analytics (heatmap of complaints, resolution time stats)
6. User Authentication & Role Management

**Data requirements:** Users, Issues, Categories, Status history, Attachments, Departments **External interfaces:** Mobile app UI, Admin web UI, Maps API (Google Maps/OpenStreetMap), SMS/Email gateway **Quality attributes:** Usability (non-technical citizens), Performance (image upload under poor network), Security (auth, photo privacy), Scalability (city-wide usage)

This gives you rich content for every single section — Introduction, Overall Description, System Features (multiple, each with 3-5 REQ items), Data Requirements, External Interfaces, and Quality Attributes.

Want me to go ahead and **write the full SRS document** for CivicFix directly into your uploaded template (filling in Introduction, Product Scope, User Classes, System Features with numbered requirements, Data Dictionary, etc.), or would you rather I first give you just the content in chat so you can review before I put it into the Word doc?