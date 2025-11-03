# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
For  Increase the selling price per unit by 3 for all products supplied by supplier ID 4 in the sales table.

<img width="320" height="568" alt="image" src="https://github.com/user-attachments/assets/a33cdeff-46f8-4320-b544-327d3b771f8c" />


```sql
UPDATE SALES
SET sell_price=sell_price+3
WHERE product_id IN
(
    SELECT product_id
    FROM PRODUCTS
    WHERE supplier_id=4
);
```

**Output:**

<img width="1230" height="460" alt="image" src="https://github.com/user-attachments/assets/e375f5d0-aabe-4eda-9dba-a67cf560629d" />


**Question 2**
---
Write a SQL statement to Update the product_name to 'Premium Bread' whose product ID is 5 in the products table.

<img width="150" height="265" alt="image" src="https://github.com/user-attachments/assets/e8a7e887-e34e-4868-9a84-7d51853f3738" />


```sql
UPDATE Products
SET product_name='Premium Bread'
WHERE product_id=5;
```

**Output:**

<img width="1229" height="486" alt="image" src="https://github.com/user-attachments/assets/a3897006-3eea-4411-87b2-122fe6a63f29" />


**Question 3**
---
Write a SQL statement to change the email column of employees table with 'Unavailable' for all employees in employees table.

<img width="171" height="338" alt="image" src="https://github.com/user-attachments/assets/435d43da-6b2b-4c07-8c97-a67203644903" />


```sql
UPDATE Employees
SET email='Unavailable';
```

**Output:**

<img width="1225" height="533" alt="image" src="https://github.com/user-attachments/assets/5730d44f-f868-4dc0-b24b-5c417146eeb5" />


**Question 4**
---
Write a SQL statement to increase the salary of employees under the department 40, 90 and 110 according to the company rules.

Salary will be increased by 25% for the department 40, 15% for department 90 and 10% for the department 110 and the rest of the departments will remain same.

<img width="153" height="354" alt="image" src="https://github.com/user-attachments/assets/6bde0d5c-be7b-415a-ac63-a1e25dcad2d2" />

```sql
UPDATE Employees
SET salary=
    CASE department_id
        WHEN 40 THEN ROUND(salary*1.25)
        WHEN 90 THEN ROUND(salary*1.15)
        WHEN 110 THEN ROUND(salary*1.10)
        ELSE salary
    END;
```

**Output:**

<img width="1226" height="544" alt="image" src="https://github.com/user-attachments/assets/55bafd26-5ae6-458c-8e24-8425fa50835d" />


**Question 5**
---
Decrease the reorder level by 30 percent where the product name contains 'cream' and quantity in stock is higher than reorder level in the products table.

<img width="334" height="338" alt="image" src="https://github.com/user-attachments/assets/4286f3d9-ad64-4567-ba3e-53af99c90ad8" />


```sql
UPDATE PRODUCTS
SET reorder_lvl=reorder_lvl*0.70
WHERE product_name LIKE '%cream%'
AND quantity>reorder_lvl;
```

**Output:**

<img width="1231" height="580" alt="image" src="https://github.com/user-attachments/assets/d5634894-27a1-42f3-81cf-deae82f1f450" />


**Question 6**
---
Write a SQL query to Delete a Specific Surgery whose ID is 3

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date

```sql
DELETE FROM Surgeries
WHERE surgery_id=3;
```

**Output:**

<img width="1229" height="463" alt="image" src="https://github.com/user-attachments/assets/eb672e73-7077-4f8f-be1f-815ea6d66832" />


**Question 7**
---
Write a SQL query to Delete All Doctors with a NULL Last Name

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors
WHERE last_name IS NULL;
```

**Output:**

<img width="1230" height="802" alt="image" src="https://github.com/user-attachments/assets/7f1e98d1-6d6e-4fb4-bbe4-127120ac50bb" />


**Question 8**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.
Sample table: Customer

<img width="1088" height="153" alt="image" src="https://github.com/user-attachments/assets/4aaa85e2-60d6-4b82-a568-af50b84670c3" />
<br>
<img width="409" height="148" alt="image" src="https://github.com/user-attachments/assets/2f3895db-dfe6-4609-baf4-18756ccaac07" />



```sql
DELETE FROM Customer
    WHERE GRADE%2!=0;
```

**Output:**

<img width="1237" height="495" alt="image" src="https://github.com/user-attachments/assets/50916607-9acf-436e-8a88-a9e30c73ad5f" />


**Question 9**
---
Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors
WHERE specialization='Cardiology';
```

**Output:**

<img width="1231" height="471" alt="image" src="https://github.com/user-attachments/assets/1c01da78-b74a-4a5c-b2f2-94ac0f980af7" />


**Question 10**
---
Write a SQL query to Delete all Doctors whose Specialization is either 'Pediatrics' or 'Cardiology' and Last Name is Brown.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors
WHERE (specialization='Pediatrics' OR specialization='Cardiology')
AND last_name='Brown';
```

**Output:**

<img width="1208" height="966" alt="image" src="https://github.com/user-attachments/assets/8d9fb927-4247-495d-bba4-4bd029a94721" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
