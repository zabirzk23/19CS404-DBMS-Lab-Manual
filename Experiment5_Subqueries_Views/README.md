# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
<img width="1119" height="532" alt="image" src="https://github.com/user-attachments/assets/c11b05ec-3afa-447b-8cad-60b4f7328713" />
<br>

```sql
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city FROM customer WHERE id IN (3, 7)
);
```

**Output:**

<img width="1273" height="569" alt="image" src="https://github.com/user-attachments/assets/f094b122-8597-486a-98b7-95b2b1fc8f66" />

**Question 2**
---
<img width="1228" height="606" alt="image" src="https://github.com/user-attachments/assets/cdc74f48-6aaf-4405-9c15-dbe3a248ae6e" />

```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE purch_amt > (
    SELECT AVG(purch_amt)
    FROM orders
    WHERE ord_date = '2012-10-10'
);

```

**Output:**

<img width="1279" height="568" alt="image" src="https://github.com/user-attachments/assets/b8985308-fd79-45cf-8b9a-d7f4da0dcc46" />


**Question 3**
---
<img width="906" height="642" alt="image" src="https://github.com/user-attachments/assets/3a769ef1-77bd-413b-a7f1-7c2239ce32c7" />


```sql
SELECT *
FROM customers
WHERE address = 'Delhi';

```

**Output:**

<img width="1273" height="455" alt="image" src="https://github.com/user-attachments/assets/2cd3e1a9-4ef1-49f1-a5bf-3207e4dac7f6" />

**Question 4**
---
<img width="1198" height="740" alt="image" src="https://github.com/user-attachments/assets/18ec3932-3ff6-4896-96bd-bedbda4fe61e" />

```sql
SELECT o.ord_no, 
       o.purch_amt, 
       o.ord_date, 
       o.customer_id, 
       o.salesman_id
FROM orders o
JOIN salesman s
ON o.salesman_id = s.salesman_id
WHERE s.city = 'London';

```

**Output:**

<img width="1276" height="514" alt="image" src="https://github.com/user-attachments/assets/a6cfe4af-9113-42d8-ac81-64d007e012d4" />

**Question 5**
---
<img width="1224" height="712" alt="image" src="https://github.com/user-attachments/assets/6ba58334-bffc-4f2b-83e2-1177a1ed1015" />

```sql
SELECT s.salesman_id, s.name
FROM salesman s
JOIN customer c
ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id, s.name
HAVING COUNT(c.customer_id) > 1;

```

**Output:**

<img width="1278" height="580" alt="image" src="https://github.com/user-attachments/assets/f8a35ba0-e92c-4a4a-b043-4100b891f53e" />

**Question 6**
---
<img width="1167" height="544" alt="image" src="https://github.com/user-attachments/assets/e99133a5-e32b-404c-9421-405421d03b73" />

```sql
SELECT *
FROM customer
WHERE city <> (
    SELECT city 
    FROM customer 
    WHERE id = (SELECT MAX(id) FROM customer)
);

```

**Output:**

<img width="1275" height="611" alt="image" src="https://github.com/user-attachments/assets/74414b9e-35e1-422a-aef4-74a2cf9d567d" />

**Question 7**
---
<img width="1075" height="567" alt="image" src="https://github.com/user-attachments/assets/09f3159a-034e-4431-b0af-a6df159e6fac" />

```sql
SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(phone) = 1
);

```

**Output:**

<img width="1272" height="564" alt="image" src="https://github.com/user-attachments/assets/c623bf3c-f74a-4232-9e3d-a202ea3ed702" />

**Question 8**
---
<img width="1263" height="618" alt="image" src="https://github.com/user-attachments/assets/b422dc44-27b2-4037-ab87-b5523cc32769" />

```sql
SELECT *
FROM grades g
WHERE g.grade = (
    SELECT MIN(grade)
    FROM grades
    WHERE subject = g.subject
);

```

**Output:**

<img width="1271" height="563" alt="image" src="https://github.com/user-attachments/assets/153ba7ed-aeae-4a0a-8940-08f25b942f0b" />

**Question 9**
---
<img width="1058" height="681" alt="image" src="https://github.com/user-attachments/assets/614b9290-98fa-48a9-9b53-f11d18c000be" />

```sql
SELECT 
    DISTINCT s.commission
FROM 
    salesman AS s
JOIN customer AS c
ON 
    s.salesman_id = c.salesman_id
WHERE 
    c.city = 'Paris';

```

**Output:**

<img width="297" height="241" alt="image" src="https://github.com/user-attachments/assets/634a24e6-8fd0-4829-bbf7-2e3f71ab7b7f" />


**Question 10**
---
<img width="982" height="501" alt="image" src="https://github.com/user-attachments/assets/2c40fdc1-7248-466c-be99-a92aa0529cf2" />

```sql
SELECT medication_id AS medic, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MAX(dosage)
    FROM Medications
);
```

**Output:**

<img width="1279" height="513" alt="image" src="https://github.com/user-attachments/assets/b6d17847-769e-409d-b190-ba3e8191c6d2" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
