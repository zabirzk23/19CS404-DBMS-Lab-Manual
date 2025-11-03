# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science

```sql
INSERT INTO Student_details(RollNo,Name,Gender,Subject,Marks)
VALUES(205,'Olivia Green', 'F',NULL,NULL);

INSERT INTO Student_details(RollNo,Name,Gender,Subject,Marks)
VALUES(207,'Liam Smith','M','Mathematics',85);

INSERT INTO Student_details(RollNo,Name,Gender,Subject,Marks)
VALUES(208,'Sophia Johnson','F','Science',NULL); 
```

**Output:**

<img width="1183" height="278" alt="image" src="https://github.com/user-attachments/assets/1642b0f2-f275-4b60-8a14-1d519af64b8f" />


**Question 2**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```sql
CREATE TABLE Orders(
    OrderID INT,
    OrderDate DATE NOT NULL,
    CustomerID INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

**Output:**

<img width="1236" height="376" alt="image" src="https://github.com/user-attachments/assets/7927abf6-9367-46a2-82dc-4a24582ae9f7" />


**Question 3**
---
Write an SQL command can to add a column named email of type TEXT to the customers table

 


```sql
ALTER TABLE customers
ADD COLUMN email TEXT;
```

**Output:**

<img width="1234" height="376" alt="image" src="https://github.com/user-attachments/assets/98d21488-a874-4b4d-a642-a03ddc013c6b" />


**Question 4**
---
Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0

```sql
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
SELECT RollNo,Name,Gender,Subject,MARKS
FROM Archived_students;
```

**Output:**

<img width="1233" height="379" alt="image" src="https://github.com/user-attachments/assets/8bf5c9e3-1e3f-44cb-982b-45028d46c0f0" />


**Question 5**
---
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```sql
CREATE TABLE jobs
(
    job_id INT PRIMARY KEY,
    job_title VARCHAR(100) DEFAULT '',
    min_salary INT DEFAULT 8000,
    max_salary INT DEFAULT NULL
);
```

**Output:**

<img width="1234" height="420" alt="image" src="https://github.com/user-attachments/assets/0a9a0294-dce4-47f7-bce0-a77f6c569151" />


**Question 6**
---
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.
```sql
INSERT INTO Products (ProductID, Name, Category)
VALUES(104,'Tablet','Electronics');
```

**Output:**

<img width="1234" height="326" alt="image" src="https://github.com/user-attachments/assets/16a83f85-e95c-4f3e-9a91-a4dd8f5e4c58" />

**Question 7**
---
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```sql
CREATE TABLE Attendance
(
    AttendanceID INT PRIMARY KEY,
    EmployeeID INT,
    AttendanceDate DATE,
    Status TEXT CHECK (Status IN ('Present', 'Absent', 'Leave')),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1233" height="371" alt="image" src="https://github.com/user-attachments/assets/0b48887f-6edb-4cdf-a813-261f2940ade4" />

**Question 8**
---
Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE
```sql
CREATE TABLE Employees
(
    EmployeeID INTEGER,
    FirstName TEXT,
    LastName TEXT,
    HireDate DATE
);
```

**Output:**

<img width="1233" height="399" alt="image" src="https://github.com/user-attachments/assets/2833ba63-9141-4e09-a33f-b9bf8b7d920d" />


**Question 9**
---
Write a SQL Query  to add attribute ISBN as varchar(30) and domain_dept as varchar(30) in the table 'books'
```sql

ALTER TABLE books ADD ISBN varchar(30);
ALTER TABLE books ADD domain_dept varchar(30);
```

**Output:**

<img width="1232" height="470" alt="image" src="https://github.com/user-attachments/assets/1604c124-3353-4d9e-83dd-8a2735cb4310" />

**Question 10**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
```sql
CREATE TABLE Invoices
(
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    Amount REAL CHECK(Amount>0),
    DueDate DATE CHECK(DueDate > InvoiceDate),
    OrderID INTEGER,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1231" height="371" alt="image" src="https://github.com/user-attachments/assets/152eb888-d6a6-4c41-b402-a38a34a858c3" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
