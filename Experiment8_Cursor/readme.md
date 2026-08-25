# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:

- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**Output:**  
The program should display the employee details or an error message.

### CODE

```
-- Create employees table
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);

-- Insert sample data
INSERT INTO employees VALUES (1, 'John', 'Manager');
INSERT INTO employees VALUES (2, 'Alice', 'Developer');
INSERT INTO employees VALUES (3, 'Bob', 'Tester');

COMMIT;

-- PL/SQL program using a simple cursor
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_name, designation
        FROM employees;

    v_emp_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;
BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_emp_name, v_designation;

        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE(
            'Employee Name: ' || v_emp_name ||
            ', Designation: ' || v_designation
        );
    END LOOP;

    -- Raise NO_DATA_FOUND if the table has no rows
    IF emp_cursor%ROWCOUNT = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

    CLOSE emp_cursor;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Error: No employee data found.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Unexpected Error: ' || SQLERRM
        );

        IF emp_cursor%ISOPEN THEN
            CLOSE emp_cursor;
        END IF;
END;
/

```
### OUTPUT:
<img width="542" height="255" alt="image" src="https://github.com/user-attachments/assets/4c539ea8-190c-46e4-a813-260d594fad0f" />


---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.

**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.

### CODE

```
-- Add salary column
ALTER TABLE employees ADD salary NUMBER;

-- Insert salary values
UPDATE employees SET salary = 60000 WHERE emp_id = 1;
UPDATE employees SET salary = 45000 WHERE emp_id = 2;
UPDATE employees SET salary = 35000 WHERE emp_id = 3;

COMMIT;

-- PL/SQL program using a parameterized cursor
DECLARE
    v_min_salary NUMBER := 40000;
    v_max_salary NUMBER := 70000;
    v_count NUMBER := 0;

    CURSOR emp_cursor(p_min_salary NUMBER, p_max_salary NUMBER) IS
        SELECT emp_id, emp_name, designation, salary
        FROM employees
        WHERE salary BETWEEN p_min_salary AND p_max_salary;

    v_emp_id employees.emp_id%TYPE;
    v_emp_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;
    v_salary employees.salary%TYPE;

BEGIN
    OPEN emp_cursor(v_min_salary, v_max_salary);

    LOOP
        FETCH emp_cursor
        INTO v_emp_id, v_emp_name, v_designation, v_salary;

        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'ID: ' || v_emp_id ||
            ', Name: ' || v_emp_name ||
            ', Designation: ' || v_designation ||
            ', Salary: ' || v_salary
        );
    END LOOP;

    CLOSE emp_cursor;

    -- Raise NO_DATA_FOUND if no employees match
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE(
            'Error: No employees found in the salary range ' ||
            v_min_salary || ' to ' || v_max_salary
        );

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Unexpected Error: ' || SQLERRM
        );
END;
/

```
### OUTPUT:
<img width="705" height="237" alt="image" src="https://github.com/user-attachments/assets/8583574d-484a-4631-b15f-dc007dade0eb" />

---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.

**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.

### CODE
```
-- Add department number column
ALTER TABLE employees ADD dept_no NUMBER;

-- Insert department numbers
UPDATE employees SET dept_no = 10 WHERE emp_id = 1;
UPDATE employees SET dept_no = 20 WHERE emp_id = 2;
UPDATE employees SET dept_no = 30 WHERE emp_id = 3;

COMMIT;

-- PL/SQL program using a Cursor FOR Loop
DECLARE
    v_count NUMBER := 0;

    CURSOR emp_cursor IS
        SELECT emp_name, dept_no
        FROM employees;

BEGIN
    FOR emp IN emp_cursor LOOP
        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Employee Name: ' || emp.emp_name ||
            ', Department No: ' || emp.dept_no
        );
    END LOOP;

    -- Raise NO_DATA_FOUND if no employees exist
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE(
            'Error: No employees found in the database.'
        );

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Unexpected Error: ' || SQLERRM
        );
END;
/

```

### OUTPUT:

<img width="663" height="248" alt="image" src="https://github.com/user-attachments/assets/3d2cddda-4fd9-4254-80f1-2edb3234ea06" />
---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**Output:**  
The program should display employee records or the appropriate error message if no data is found.

### CODE

````
-- Create employees table
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    salary NUMBER
);

-- Insert sample data
INSERT INTO employees VALUES (1, 'John', 'Manager', 60000);
INSERT INTO employees VALUES (2, 'Alice', 'Developer', 45000);
INSERT INTO employees VALUES (3, 'Bob', 'Tester', 35000);

COMMIT;

-- PL/SQL program using cursor and %ROWTYPE
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_id, emp_name, designation, salary
        FROM employees;

    emp_record emp_cursor%ROWTYPE;
    v_count NUMBER := 0;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO emp_record;

        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Employee ID: ' || emp_record.emp_id
        );
        DBMS_OUTPUT.PUT_LINE(
            'Employee Name: ' || emp_record.emp_name
        );
        DBMS_OUTPUT.PUT_LINE(
            'Designation: ' || emp_record.designation
        );
        DBMS_OUTPUT.PUT_LINE(
            'Salary: ' || emp_record.salary
        );
        DBMS_OUTPUT.PUT_LINE('--------------------------');
    END LOOP;

    CLOSE emp_cursor;

    -- Raise NO_DATA_FOUND if no records exist
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE(
            'Error: No employees found in the database.'
        );

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Unexpected Error: ' || SQLERRM
        );

        IF emp_cursor%ISOPEN THEN
            CLOSE emp_cursor;
        END IF;
END;
/

````
### OUTPUT


<img width="678" height="460" alt="image" src="https://github.com/user-attachments/assets/0e29d595-bf2d-4f85-a548-699c7b311777" />

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.

**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.

### CODE
```
-- Create employees table
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    salary NUMBER,
    dept_no NUMBER
);

-- Insert sample data
INSERT INTO employees VALUES (1, 'John', 'Manager', 60000, 10);
INSERT INTO employees VALUES (2, 'Alice', 'Developer', 45000, 20);
INSERT INTO employees VALUES (3, 'Bob', 'Tester', 35000, 10);
INSERT INTO employees VALUES (4, 'David', 'Developer', 50000, 30);

COMMIT;

-- PL/SQL program using FOR UPDATE cursor
DECLARE
    v_dept_no NUMBER := 10;
    v_increment NUMBER := 5000;
    v_count NUMBER := 0;

    CURSOR emp_cursor IS
        SELECT emp_id, emp_name, salary
        FROM employees
        WHERE dept_no = v_dept_no
        FOR UPDATE OF salary;

BEGIN
    FOR emp IN emp_cursor LOOP

        UPDATE employees
        SET salary = salary + v_increment
        WHERE CURRENT OF emp_cursor;

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Employee: ' || emp.emp_name ||
            ', Old Salary: ' || emp.salary ||
            ', New Salary: ' || (emp.salary + v_increment)
        );

    END LOOP;

    -- Raise NO_DATA_FOUND if no employees were found
    IF v_count = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

    COMMIT;

    DBMS_OUTPUT.PUT_LINE(
        'Salary updated successfully for department ' || v_dept_no
    );

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        ROLLBACK;
        DBMS_OUTPUT.PUT_LINE(
            'Error: No employees found in department ' || v_dept_no
        );

    WHEN OTHERS THEN
        ROLLBACK;
        DBMS_OUTPUT.PUT_LINE(
            'Unexpected Error: ' || SQLERRM
        );
END;
/

```
### OUTPUT

<img width="662" height="250" alt="image" src="https://github.com/user-attachments/assets/b87975ce-64c3-401b-8737-217ea3f1ba1a" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

