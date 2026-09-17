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
Write a SQL statement to change the EMAIL and COMMISSION_PCT column of the following EMPLOYEES table with 'not available' and 0.55 for those employees whose DEPARTMENT_ID is 110.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id

```sql
UPDATE EMPLOYEES
SET EMAIL = 'not available',
    COMMISSION_PCT = 0.55
WHERE DEPARTMENT_ID = 110;
```

**Output:**

<img width="1219" height="452" alt="image" src="https://github.com/user-attachments/assets/81a3a6af-a002-4f21-8cdd-f912c8628f25" />


**Question 2**
---
Write a SQL statement to Update the grade of all customers in Chennai city as  5. 

```sql
UPDATE Customer
SET grade = 5
WHERE city = 'Chennai';
```

**Output:**

<img width="1197" height="555" alt="image" src="https://github.com/user-attachments/assets/34606d45-0673-4243-b96e-aca42fb7349e" />


**Question 3**
---
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.

products table

---------------
product_id
product_name
category_id
availability

```sql
UPDATE products
SET product_name = 'Grapefruit'
WHERE product_id = 4;
```

**Output:**
<img width="1208" height="316" alt="image" src="https://github.com/user-attachments/assets/94615664-2886-4acd-ac30-81a407169273" />


**Question 4**
---
Write a SQL statement to Update the hire_date of employees in department 50 to 2024-01-24.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id

```sql
UPDATE EMPLOYEES
SET hire_date = '2024-01-24'
WHERE DEPARTMENT_ID = 50;
```

**Output:**

<img width="1203" height="349" alt="image" src="https://github.com/user-attachments/assets/6351933c-f915-458f-bcc5-85ed57c1b375" />


**Question 5**
---
Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors
WHERE specialization = 'Pediatrics'
  AND first_name = 'Michael';
```

**Output:**

<img width="1203" height="466" alt="image" src="https://github.com/user-attachments/assets/3f3b4159-be00-4bb5-8d86-3b65fe58e298" />


**Question 6**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_COUNTRY' is neither 'India' nor 'USA'.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |



```sql
DELETE FROM Customer
WHERE CUST_COUNTRY NOT IN ('India', 'USA');
```

**Output:**

<img width="1203" height="553" alt="image" src="https://github.com/user-attachments/assets/86344463-86a4-4a6f-af44-54f45de11687" />


**Question 7**
---
Write a SQL query to Delete customers whose 'GRADE' is greater than 2 and have a 'PAYMENT_AMT' less than the average 'PAYMENT_AMT' for all customers, or whose 'OUTSTANDING_AMT' is greater than 8000:

```sql
DELETE FROM Customer
WHERE (grade > 2 AND PAYMENT_AMT < (SELECT AVG(PAYMENT_AMT) FROM Customer))
   OR OUTSTANDING_AMT > 8000;
```

**Output:**



**Question 8**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is exactly 2.

```sql
DELETE FROM Customer
WHERE grade = 2;
```

**Output:**



**Question 9**
---
Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.

```sql
DELETE FROM Surgeries
WHERE surgery_date = '2024-02-28';
```

**Output:**


**Question 10**
---
Write a query to fetch 3 top salaried records from EmployeePosition table.

```sql
SELECT *
FROM EmployeePosition
ORDER BY Salary DESC
LIMIT 3;
```

**Output:**

<img width="1206" height="360" alt="image" src="https://github.com/user-attachments/assets/edb53b3b-70cc-4493-9efa-692b4873caef" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
