# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)
```sql
SELECT 
    s.name,
    c.cust_name,
    c.city,
    c.grade,
    c.salesman_id
FROM 
    salesman AS s
LEFT JOIN 
    customer AS c
ON 
    s.salesman_id = c.salesman_id;
```

**Output:**

<img width="1284" height="965" alt="image" src="https://github.com/user-attachments/assets/ac42b12f-03e9-4bd2-9d5d-c97f4c2fdf5e" />

**Question 2**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

Sample table: customer

<img width="644" height="661" alt="image" src="https://github.com/user-attachments/assets/e9cfa3a7-7228-4ef2-84f2-c4a6c5fb0776" />

```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    c.cust_name,
    c.city
FROM orders as o
JOIN customer as c
ON o.customer_id=c.customer_id
WHERE purch_amt BETWEEN 500 AND 2000;
```

**Output:**

<img width="1282" height="579" alt="image" src="https://github.com/user-attachments/assets/4645b733-18a6-47fc-bb4b-60b44382b17e" />

**Question 3**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

Sample table: orders

<img width="641" height="916" alt="image" src="https://github.com/user-attachments/assets/a290ced9-aae9-4b47-82e2-6b8e71464be6" />

```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM 
    orders AS o
JOIN 
    customer AS c 
ON 
    o.customer_id = c.customer_id
JOIN 
    salesman AS s 
ON 
    o.salesman_id = s.salesman_id;
```

**Output:**

<img width="1286" height="962" alt="image" src="https://github.com/user-attachments/assets/c72def8f-3256-4f43-ad00-2aca0d0a664e" />

**Question 4**
---
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column. Include conditions to filter for patients discharged between '2024-03-01' and '2024-03-31' but not admitted during the same period.

PATIENTS TABLE:

<img width="273" height="479" alt="image" src="https://github.com/user-attachments/assets/d6d738b9-7e4a-468f-b1f6-3a06653ec3eb" />

```sql
SELECT 
    p.first_name,
    s.surgery_id,
    s.patient_id,
    s.surgeon_id,
    s.surgery_date
FROM 
    patients AS p
INNER JOIN 
    surgeries AS s
ON 
    p.patient_id = s.patient_id
WHERE 
    p.discharge_date BETWEEN '2024-03-01' AND '2024-03-31'
    AND (p.admission_date < '2024-03-01' OR p.admission_date > '2024-03-31');

```

**Output:**

<img width="1285" height="508" alt="image" src="https://github.com/user-attachments/assets/48401084-5c18-4e03-8bec-a46e18977072" />

**Question 5**
---
Write the SQL query that achieves the selection of all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

<img width="779" height="126" alt="image" src="https://github.com/user-attachments/assets/fe8d225b-ba8e-4b8c-9e71-55f80964dd12" />

TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date

<img width="775" height="123" alt="image" src="https://github.com/user-attachments/assets/d65bac1e-c367-4f7c-b298-7374902d5c5a" />


```sql
SELECT 
    t.*
FROM 
    test_results AS t
INNER JOIN 
    patients AS p
ON 
    t.patient_id = p.patient_id
WHERE 
    p.first_name = 'Alice';

```

**Output:**

<img width="1284" height="498" alt="image" src="https://github.com/user-attachments/assets/4f4c5185-a041-4703-8073-6be3037accc1" />

**Question 6**
---
Write the SQL query that accomplishes the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a non-null discharge date.

<img width="291" height="508" alt="image" src="https://github.com/user-attachments/assets/04507730-d080-4eed-b0c4-3ca460878f38" />

```sql
SELECT 
    p.first_name AS patient_name,
    d.first_name AS doctor_name
FROM 
    patients AS p
INNER JOIN 
    doctors AS d
ON 
    p.doctor_id = d.doctor_id
WHERE 
    p.discharge_date IS NOT NULL;

```

**Output:**

<img width="1283" height="484" alt="image" src="https://github.com/user-attachments/assets/ea36bd97-4775-4cf4-9e28-7207415ccfca" />

**Question 7**
---
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

<img width="629" height="304" alt="image" src="https://github.com/user-attachments/assets/0d526af0-746f-4888-bf12-a436edd76978" />
<br>
<img width="577" height="392" alt="image" src="https://github.com/user-attachments/assets/9c9758c0-4f8a-44d5-a76a-ec1ffee027ab" />
<br>
<img width="550" height="263" alt="image" src="https://github.com/user-attachments/assets/d4100e4e-8032-462a-8540-3f8941837eba" />

```sql
SELECT
    T1.cust_name,
    T1.city,
    T2.ord_no ,
    T2.ord_date ,
    T2.purch_amt AS "Order Amount",
    T3.name,
    T3.commission
FROM
    customer AS T1
LEFT JOIN
    orders AS T2 ON T1.customer_id = T2.customer_id
LEFT JOIN
    salesman AS T3 ON T1.salesman_id = T3.salesman_id;
```

**Output:**

<img width="1272" height="872" alt="image" src="https://github.com/user-attachments/assets/6c72b058-ec85-4e7f-8b23-b0077a3e444b" />

**Question 8**
---
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

<img width="599" height="401" alt="image" src="https://github.com/user-attachments/assets/5ebeb552-7b9d-4e40-a5f2-284d33c0e65f" />
<br<
<img width="596" height="297" alt="image" src="https://github.com/user-attachments/assets/3ec8fd09-89a9-4f16-9b7e-7af09660dfaa" />
<br>
<img width="594" height="245" alt="image" src="https://github.com/user-attachments/assets/81d00da4-756b-4781-bd47-d2defc75334c" />

```sql
SELECT 
    o.ord_no,
    o.ord_date,
    o.purch_amt,
    c.cust_name AS "Customer Name",
    c.grade,
    s.name AS "Salesman",
    s.commission
FROM 
    orders AS o
INNER JOIN 
    customer AS c
ON 
    o.customer_id = c.customer_id
INNER JOIN 
    salesman AS s
ON 
    o.salesman_id = s.salesman_id;

```

**Output:**

<img width="1276" height="868" alt="image" src="https://github.com/user-attachments/assets/16fc7061-4b9f-4b32-8232-b0c41b3d64e1" />

**Question 9**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

<img width="647" height="555" alt="image" src="https://github.com/user-attachments/assets/46eb11f0-5eea-4346-a710-cd108fa6ae4c" />


```sql
SELECT 
    c.cust_name,
    c.city,
    c.grade,
    s.name AS Salesman,
    s.city
FROM 
    customer AS c
INNER JOIN 
    salesman AS s
ON 
    c.salesman_id = s.salesman_id
ORDER BY 
    c.customer_id ASC;

```

**Output:**

<img width="1281" height="958" alt="image" src="https://github.com/user-attachments/assets/1dff03b0-afd8-4ea0-a14c-5633ccc4550c" />

**Question 10**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the same city as the salesman.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)


```sql
SELECT 
    c.cust_name,
    s.name
FROM 
    customer AS c
JOIN 
    salesman AS s
ON 
    c.salesman_id = s.salesman_id
AND 
    c.city = s.city;

```

**Output:**

<img width="1285" height="631" alt="image" src="https://github.com/user-attachments/assets/07e776a4-808a-4ff5-a09c-f4e973ae0a51" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
