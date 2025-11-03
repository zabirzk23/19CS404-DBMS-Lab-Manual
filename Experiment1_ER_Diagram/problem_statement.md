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

<img width="492" height="699" alt="image" src="https://github.com/user-attachments/assets/dec31a12-3c5c-43ef-bc6a-9d5e41a63176" />


### Entities and Attributes

| **Entity**                      | **Attributes (PK, FK)**                                                                      | **Notes**                                                 |
| ------------------------------- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| **Member**                      | MemberID (PK), Name, MembershipType, StartDate                                               | Stores gym members and their memberships                  |
| **Program**                     | ProgramID (PK), ProgramName (Yoga, Zumba, Weight Training, etc.)                             | Fitness programs offered by the gym                       |
| **Trainer**                     | TrainerID (PK), Name, Specialization                                                         | Trainers employed by the gym                              |
| **Session (Personal Training)** | SessionID (PK), Date, Time, MemberID (FK) → Member, TrainerID (FK) → Trainer                 | Personal training sessions between a member and a trainer |
| **Attendance**                  | AttendanceID (PK), SessionID (FK) → Session, MemberID (FK) → Member, Status (Present/Absent) | Tracks attendance for sessions                            |
| **Payment**                     | PaymentID (PK), Date, Amount, PaymentType (Membership / Session), MemberID (FK) → Member     | Stores payments made by members                           |
                                          |

### Relationships and Constraints

| Relationship       | Cardinality             | Participation                     | Notes                                                                           |
| ------------------ | ----------------------- | --------------------------------- | ------------------------------------------------------------------------------- |
| Member–Program     | M\:N via MemberProgram  | Member: Partial, Program: Partial | A member can join many programs, a program can have many members                |
| Program–Trainer    | M\:N via ProgramTrainer | Both Partial                      | A program may have multiple trainers, and trainers may handle multiple programs |
| Member–Session     | 1\:N                    | Member: Partial, Session: Total   | A session must belong to one member, but a member can book many sessions        |
| Trainer–Session    | 1\:N                    | Trainer: Partial, Session: Total  | A session must have one trainer, trainer may handle many sessions               |
| Session–Attendance | 1\:N                    | Session: Total, Attendance: Total | Attendance is recorded per session per member                                   |
| Member–Payment     | 1\:N                    | Member: Total, Payment: Total     | Payments must be tied to members                                                |


### Assumptions

1.Each member has exactly one active membership, tracked by MembershipType and StartDate.

2.A program can exist even if no members have joined it yet.

3.A trainer can exist without being assigned to a program.

4.Personal training sessions are strictly one trainer ↔ one member at a time.

5.Attendance is recorded only for scheduled sessions/programs, not for general gym entry.

Payments are tracked for both membership renewals and personal sessions.
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

<img width="493" height="705" alt="image" src="https://github.com/user-attachments/assets/83a24ab5-b776-415c-9150-f70fa8f8a034" />


### Entities and Attributes


| **Entity**  | **Attributes (PK, FK)**                                                                            | **Notes**                               |
| ----------- | -------------------------------------------------------------------------------------------------- | --------------------------------------- |
| **Member**  | MemberID (PK), Name, ContactInfo                                                                   | Stores library members                  |
| **Book**    | BookID (PK), Title, Author, Category, AvailabilityStatus                                           | Tracks all books in the library         |
| **Loan**    | LoanID (PK), LoanDate, DueDate, ReturnDate, FineAmount, MemberID (FK) → Member, BookID (FK) → Book | Tracks book borrowings and fines        |
| **Event**   | EventID (PK), Title, Date, Description, RoomID (FK) → Room                                         | Stores library-organized events         |
| **Speaker** | SpeakerID (PK), Name, Specialization                                                               | Guest speakers/authors for events       |
| **Room**    | RoomID (PK), RoomName, Capacity, RoomType (Event / Study)                                          | Rooms can be booked for events or study |

### Relationships and Constraints

| Relationship    | Cardinality                | Participation                | Notes                                                                                            |
| --------------- | -------------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------ |
| Member – Loan   | 1\:N                       | Member: Partial, Loan: Total | A member can borrow many books; each loan tied to one member                                     |
| Book – Loan     | 1\:N                       | Book: Partial, Loan: Total   | A book can be borrowed many times but only one loan at a time                                    |
| Member – Event  | M\:N via EventRegistration | Both Partial                 | A member can register for multiple events; an event can have many members                        |
| Event – Speaker | M\:N via EventSpeaker      | Both Partial                 | An event can have multiple speakers; a speaker can appear in many events                         |
| Event – Room    | 1:1                        | Event: Total, Room: Partial  | Each event must have one room; a room may be free or used by different events at different times |


### Assumptions

1.Each book is borrowed by only one member at a time.

2.Fines are recorded in the Loan entity and apply only if the return date is after the due date.

3.Members must exist before borrowing a book or registering for an event.

4.Rooms can be used for events or study, identified by RoomType.

5.A room can host only one event at a time.

6.Speakers are independent entities .

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

<img width="498" height="705" alt="image" src="https://github.com/user-attachments/assets/594e5d5d-4235-4e5f-b75a-fa1426ea5d8c" />



### Entities and Attributes

| Entity          | Attributes (PK, FK)                                                                     | Notes                                                                  |
| --------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| **Customer**    | CustomerID (PK), Name, ContactInfo                                                      | Customers may reserve tables or walk in                                |
| **Reservation** | ReservationID (PK), Date, Time, NumGuests, CustomerID (FK), TableID (FK), WaiterID (FK) | Each reservation tied to a customer, a table, and served by one waiter |
| **Table**       | TableID (PK), TableNumber, Capacity                                                     | Tracks restaurant tables                                               |
| **Waiter**      | WaiterID (PK), Name, Shift                                                              | Each reservation assigned one waiter                                   |
| **Order**       | OrderID (PK), ReservationID (FK), OrderTime                                             | Orders are linked to reservations                                      |
| **OrderItem**   | OrderItemID (PK), OrderID (FK), DishID (FK), Quantity                                   | An order consists of multiple order items                              |
| **Dish**        | DishID (PK), DishName, Price, CategoryID (FK)                                           | Menu items                                                             |
| **Category**    | CategoryID (PK), CategoryName (Starter/Main/Dessert)                                    | Dishes grouped by category                                             |
| **Bill**        | BillID (PK), ReservationID (FK), TotalAmount, ServiceCharge, BillDate                   | One bill per reservation                                               |


### Relationships and Constraints

| Relationship           | Cardinality | Participation                         | Notes                                                  |
| ---------------------- | ----------- | ------------------------------------- | ------------------------------------------------------ |
| Customer – Reservation | 1\:N        | Customer: Partial, Reservation: Total | A customer can have multiple reservations              |
| Reservation – Table    | 1:1         | Reservation: Total, Table: Partial    | Each reservation is for one table; a table may be free |
| Reservation – Waiter   | 1\:N        | Waiter: Partial, Reservation: Total   | A waiter serves many reservations                      |
| Reservation – Order    | 1\:N        | Reservation: Total, Order: Total      | Every reservation may have multiple orders             |
| Order – OrderItem      | 1\:N        | Order: Total, OrderItem: Total        | Each order has one or more items                       |
| Dish – OrderItem       | 1\:N        | Dish: Partial, OrderItem: Total       | A dish can appear in multiple order items              |
| Category – Dish        | 1\:N        | Category: Total, Dish: Total          | Every dish belongs to exactly one category             |
| Reservation – Bill     | 1:1         | Reservation: Total, Bill: Total       | One bill generated per reservation                     |


### Assumptions

1.A customer must exist before making a reservation.

2.Walk-in customers are recorded as reservations with immediate start time.

3.Each reservation is tied to exactly one table at a given time.

4.A waiter is responsible for serving a reservation (one waiter per reservation).

5.A dish must belong to one category (starter, main, dessert).

6.Bills are generated per reservation (not per order).

7.Service charges are included in the Bill entity along with food charges.

---
