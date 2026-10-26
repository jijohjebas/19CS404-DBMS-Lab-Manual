
# ER Diagram Workshop – Submission Template

## Objective

To learn and implement Entity-Relationship (ER) modeling concepts by designing ER diagrams for practical database applications.

## Purpose

To gain practical knowledge of database design by identifying entities, attributes, relationships, cardinalities, and participation constraints.

---

# Scenario A: City Fitness Club Management
<img width="1298" height="1212" alt="image" src="https://github.com/user-attachments/assets/e00685ba-5aca-46cf-8d9b-8b1dd8db15e5" />

## Business Context

FlexiFit Gym requires a database system to maintain information about its members, trainers, and fitness programs.

## Requirements

- Members register by providing their name, membership type, and joining date.
- A member can enroll in multiple programs, such as Yoga, Zumba, and Weight Training.
- Trainers are assigned to fitness programs, and a program can have more than one trainer.
- Members can schedule personal training sessions with trainers.
- Attendance details must be maintained for every session.
- Payments for memberships and training sessions must be recorded.

### ER Diagram

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|---|---|---|
| User | user_id (PK), name, mobile_no, address | Stores user identification and contact details. |
| Permission | per_id (PK), per_module, per_name | Stores permissions available to users. |
| Trainer | trainer_id (PK), name, mobile, email | Maintains trainer information. |
| Member | mem_id (PK), mem_type, mem_name, mem_mobile, mem_email | Maintains gym member details. |
| Fitness | fit_id (PK), fit_type, fit_desc | Stores information about fitness programs. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|---|---|---|---|
| User - Permission | 1:N | Mandatory (A user must have at least one permission) | One user can be assigned several permissions. |
| User - Trainer | N:M | Optional (User may or may not be a trainer) | Users can manage multiple trainers and vice versa. |
| Trainer - Fitness | 1:N | Mandatory (A trainer must be associated with at least one fitness type) | Trainers are responsible for fitness programs. |
| Member - Fitness | N:M | Optional (Members may or may not be associated with a fitness type) | Members can enroll in different fitness programs. |

### Assumptions

- **Role-Based Access:** Users may have roles such as administrator, trainer, or member, with permissions assigned according to their roles.
- **Trainer-Managed Programs:** Trainers handle fitness programs, and members can join multiple programs under trainer guidance.
- **Flexible Participation:** Members are free to enroll in one or more fitness programs based on their preferences.

---

# Scenario B: City Library Event & Book Lending System

## Business Context

The Central Library needs a database to manage book borrowing activities and organize cultural events efficiently.

## Requirements

- Members borrow books, and the borrowing date and return date are maintained.
- Every book contains details such as title, author, and category.
- The library conducts events, and members can register to participate.
- Each event includes one or more speakers or authors.
- Rooms are reserved for events and study purposes.
- Fines are charged when books are returned after the due date.

### ER Diagram
<img width="1758" height="895" alt="image" src="https://github.com/user-attachments/assets/33fec898-d6a7-4a1a-833b-c50c24214099" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|---|---|---|
| Member | member_id (PK), name | Stores library member information. |
| Book | book_id (PK), title | Represents books available in the library. |
| Loan | loan_id (PK), date, return_date, member_id (FK), book_id (FK) | Records book borrowing transactions. |
| Event | event_id (PK), name, date | Contains details of library events. |
| Speaker | speaker_id (PK), name | Stores information about event speakers. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|---|---|---|---|
| Member - Loan | 1:N | Mandatory (A member must have at least one loan) | A member can borrow multiple books, while each loan belongs to one member. |
| Book - Loan | 1:N | Mandatory (A book must be loaned to at least one member) | A book may appear in several loan records over time, with each loan referring to one book. |
| Member - Event | M:N | Optional (A member may or may not register for an event) | Members can register for several events, and each event can have many participants. |
| Speaker - Event | M:N | Optional (An event may or may not have a speaker) | Speakers can participate in multiple events, and events can feature multiple speakers. |

### Assumptions

- **Member-Book Loan System:** Members can borrow several books, and each borrowing transaction is represented by a Loan record containing the relevant dates.
- **Event Participation:** Members can register for multiple events, and each event can accommodate multiple registered members. Speaker participation is optional.
- **Speaker-Event Association:** An event may feature one or more speakers, and the same speaker may participate in different events.

---

# Scenario C: Restaurant Table Reservation & Ordering

## Business Context

A popular restaurant requires a database system to handle table bookings, food orders, waiter assignments, and customer billing.

## Requirements

- Customers can book tables in advance or visit the restaurant without a reservation.
- Each reservation records the date, time, and number of guests.
- Customers place food orders associated with their reservations.
- Each order includes multiple dishes, and every dish belongs to a category such as starter, main course, or dessert.
- Bills are prepared for each reservation, including food costs and service charges.
- Waiters are assigned to serve reservations.

### ER Diagram
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/dc86f53c-68f0-4ed4-b815-3753cdd2d20c" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|---|---|---|
| Customer | CustomerID (PK), Name, Contact | Stores details of customers making reservations. |
| Reservation | ReservationID (PK), Date, Time, Guests, CustomerID (FK), TableID (FK) | Maintains table booking information. |
| Table | TableID (PK), Capacity, Location | Represents restaurant tables and their details. |
| Order | OrderID (PK), ReservationID (FK), Time | Stores food orders linked to reservations. |
| Dish | DishID (PK), Name, Category, Price | Contains dish names, categories, and prices. |
| OrderDetail | OrderID (FK), DishID (FK), Quantity | Records the dishes and quantities included in an order and resolves the M:N relationship. |
| Bill | BillID (PK), ReservationID (FK), Amount, ServiceCharge | Stores billing and service charge information. |
| Waiter | WaiterID (PK), Name | Maintains waiter details for reservation assignments. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|---|---|---|---|
| Customer–Reservation | 1:N | Partial | A customer can make multiple reservations. |
| Reservation–Table | 1:1 | Total | Each reservation is associated with one table. |
| Reservation–Order | 1:N | Total | A reservation can have multiple linked orders. |
| Order–Dish | M:N | Total | The many-to-many relationship is handled through OrderDetail. |
| Reservation–Bill | 1:1 | Total | Each reservation has one corresponding bill. |
| Reservation–Waiter | 1:1 | Partial | A waiter may be assigned to serve a reservation. |

### Assumptions

- Each reservation is allocated to a single table.
- A bill is generated for every reservation.
- The service charge is calculated using a fixed percentage and is not represented separately in the ER diagram.

---

## Instructions for Students

1. Complete all three scenarios (A, B, and C).
2. Identify the entities, attributes, and relationships for each scenario.
3. Draw the ER diagrams using draw.io / diagrams.net, or create hand-drawn diagrams and scan them.
4. Complete all tables and assumptions for every scenario.
5. Combine the completed Markdown document and its diagrams into a single PDF file.
