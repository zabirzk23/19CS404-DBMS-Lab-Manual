# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
How many appointments are scheduled for each doctor?

Sample table:Appointments Table

<img width="970" height="159" alt="image" src="https://github.com/user-attachments/assets/36488904-5683-4482-9a9e-600069508760" />


```sql
SELECT
    DoctorID,
    COUNT(AppointmentID) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID;
```

**Output:**

<img width="1235" height="715" alt="image" src="https://github.com/user-attachments/assets/656f98ab-716a-4a51-bd12-ae3d78b9c5e2" />


**Question 2**
---
How many prescriptions were written in each frequency category (e.g., once daily, twice daily)?

Sample tablePrescriptions Table

<img width="943" height="131" alt="image" src="https://github.com/user-attachments/assets/f2f9cd7a-6818-49bb-900f-5c3a9c51b196" />



```sql
SELECT 
    Frequency,
    COUNT(PrescriptionID) AS TotalPrescriptions
FROM Prescriptions
GROUP BY Frequency;

```

**Output:**

<img width="1227" height="618" alt="image" src="https://github.com/user-attachments/assets/ac24b17d-438a-43b6-94f7-044fdc3f5a5f" />

**Question 3**
---
How many medical records are there for each patient?

Sample table:MedicalRecords Table

<img width="955" height="140" alt="image" src="https://github.com/user-attachments/assets/cb91ed78-2a12-4922-b0b0-b7c54d7af6aa" />

```sql
SELECT 
    PatientID,
    COUNT(RecordID) AS TotalRecords
FROM
    MedicalRecords
GROUP BY
    PatientID;

```

**Output:**

<img width="1230" height="735" alt="image" src="https://github.com/user-attachments/assets/916ff66d-a93e-4c3e-97af-dc1f984e8ac3" />

**Question 4**
---
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

<img width="316" height="189" alt="image" src="https://github.com/user-attachments/assets/33968420-cb29-4a37-8ec3-dbb05a9ff4b8" />

```sql
SELECT
    COUNT(DISTINCT age) AS COUNT
FROM employee;
```

**Output:**

<img width="1226" height="403" alt="image" src="https://github.com/user-attachments/assets/bbe450c7-9040-41df-8778-732fea9ccc93" />


**Question 5**
---
Write a SQL query to find  how many employees work in California?

Table: employee

<img width="224" height="216" alt="image" src="https://github.com/user-attachments/assets/e1c3b52c-7792-4913-af76-5705285f45b8" />

```sql
SELECT 
    COUNT(id) AS employees_in_california 
FROM employee
WHERE city='California';
```

**Output:**

<img width="1228" height="390" alt="image" src="https://github.com/user-attachments/assets/134e4a4b-e85e-4213-a079-223259d5da7d" />


**Question 6**
---
Write a SQL query to find the maximum purchase amount.

Sample table: orders

<img width="517" height="194" alt="image" src="https://github.com/user-attachments/assets/4fa2ed0d-5afc-4b2c-95ad-b99118c93672" />


```sql
SELECT 
    MAX(purch_amt) AS MAXIMUM
FROM orders;
```

**Output:**

<img width="1233" height="387" alt="image" src="https://github.com/user-attachments/assets/4871cb07-992d-4957-94e3-f30a6208e81a" />

**Question 7**
---
Write a SQL query to find the total income of employees aged 40 or above.

Table: employee

<img width="213" height="189" alt="image" src="https://github.com/user-attachments/assets/be019a83-76e6-4e8b-8a75-c206ad4fd887" />


```sql
SELECT 
    SUM(income) AS total_income
FROM employee
WHERE age>=40;
```

**Output:**

<img width="1228" height="396" alt="image" src="https://github.com/user-attachments/assets/5b263490-6b1f-449a-90c2-d1e0fac4a332" />

**Question 8**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the minimum work hours for each occupation, and excludes occupations where the minimum work hour is not greater than 8.

Sample table: employee1

<img width="771" height="150" alt="image" src="https://github.com/user-attachments/assets/97093ed1-45fb-4e27-9883-e5d41f092441" />

```sql
SELECT 
    occupation,
    MIN(workhour)
FROM employee1
GROUP BY occupation;
```

**Output:**

<img width="1229" height="559" alt="image" src="https://github.com/user-attachments/assets/b2506deb-9590-4ebe-b92a-afec64f03f5c" />

**Question 9**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the total work hours for each date, and excludes dates where the total work hour sum is not greater than 40.

Sample table: employee1

<img width="773" height="148" alt="image" src="https://github.com/user-attachments/assets/fff40c06-5bb8-4e09-af0a-856a35dbdf32" />

```sql
SELECT 
    jdate,
    SUM(workhour)
FROM employee1
GROUP BY jdate
HAVING SUM(workhour) >=40; 
```

**Output:**

<img width="1223" height="463" alt="image" src="https://github.com/user-attachments/assets/a76d1b62-d737-4133-98df-0a2ff3bad67e" />

**Question 10**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the average work hours for each date, and excludes dates where the average work hour is not less than 10.

Sample table: employee1

<img width="774" height="149" alt="image" src="https://github.com/user-attachments/assets/36742fd0-15df-4177-aac7-470dd0d90801" />

```sql
SELECT 
    jdate,
    AVG(workhour)
FROM employee1
GROUP BY jdate
HAVING AVG(workhour) <10;
```

**Output:**

<img width="1238" height="414" alt="image" src="https://github.com/user-attachments/assets/dfb0ae48-5fed-44af-b663-c2c447415dde" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
