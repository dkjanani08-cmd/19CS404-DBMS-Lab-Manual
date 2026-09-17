# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="1100" height="662" alt="Screenshot 2026-09-08 140941" src="https://github.com/user-attachments/assets/ad036d12-250e-4c40-b316-fa57b11b3b67" />


### Entities and Attributes

<img width="1105" height="372" alt="Screenshot 2026-09-08 140959" src="https://github.com/user-attachments/assets/dfef9204-a1df-4e2e-8595-9ef0267fbd40" />


### Relationships and Constraints

<img width="1107" height="377" alt="Screenshot 2026-09-08 141020" src="https://github.com/user-attachments/assets/11acf043-099e-4749-8380-2b5bcedc4688" />


### Assumptions
- Each session involves exactly one trainer and one member.
- Programs are predefined (Yoga, Zumba, Weight Training, etc.).
- Payments are only for membership or session bookings.
---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:

<img width="1056" height="702" alt="Screenshot 2026-09-08 141043" src="https://github.com/user-attachments/assets/9c52a6aa-7b3c-4e1e-b903-34d9902ab5fb" />


### Entities and Attributes

<img width="928" height="305" alt="Screenshot 2026-09-08 141055" src="https://github.com/user-attachments/assets/366707a3-bb27-4414-999b-055eeac30c81" />


### Relationships and Constraints

<img width="762" height="175" alt="Screenshot 2026-09-08 141108" src="https://github.com/user-attachments/assets/b4d65aec-95bb-4064-83db-6c94cfd0c302" />


### Assumptions
- Books can be borrowed multiple times by different Members.
- Each Event happens in one Room at a specific time.
- A Speaker can participate in multiple Events.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:

<img width="1102" height="545" alt="Screenshot 2026-09-08 141211" src="https://github.com/user-attachments/assets/1003fdb5-07d7-4e1e-a4d1-ee7cec2bd3b4" />


### Entities and Attributes

<img width="927" height="266" alt="Screenshot 2026-09-08 141219" src="https://github.com/user-attachments/assets/3e791302-b11e-484d-9dcc-5696cf47969c" />


### Relationships and Constraints

<img width="802" height="205" alt="Screenshot 2026-09-08 141230" src="https://github.com/user-attachments/assets/b23b7c81-7b33-4352-b82d-066bcac40051" />


### Assumptions
- One reservation uses one table and one waiter.
- Bill is generated automatically after service.
- Customer details stored for every reservation.
---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
