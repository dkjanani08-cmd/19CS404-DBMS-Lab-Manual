# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

**Expected Output:**  
Square of 6 is 36

### CODE:
```
CREATE OR REPLACE PROCEDURE find_square(p_num NUMBER)
IS
    v_square NUMBER;
BEGIN
    v_square := p_num * p_num;

    DBMS_OUTPUT.PUT_LINE(
        'Square of ' || p_num || ' is ' || v_square
    );
END;
/
-- Call the procedure
BEGIN
    find_square(6);
END;
/

```
### OUTPUT:

<img width="633" height="241" alt="image" src="https://github.com/user-attachments/assets/28b9f303-f22c-4151-93df-5864b83cf893" />

---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

**Expected Output:**  
Factorial of 5 is 120

### CODE:
```
CREATE OR REPLACE FUNCTION get_factorial(p_num NUMBER)
RETURN NUMBER
IS
    v_factorial NUMBER := 1;
    i NUMBER := 1;
BEGIN
    WHILE i <= p_num LOOP
        v_factorial := v_factorial * i;
        i := i + 1;
    END LOOP;

    RETURN v_factorial;
END;
/

-- Call the function
BEGIN
    DBMS_OUTPUT.PUT_LINE(
        'Factorial of 5 is ' || get_factorial(5)
    );
END;
/

```
### OUTPUT
<img width="712" height="251" alt="image" src="https://github.com/user-attachments/assets/cc3c6d31-de0d-414a-86a0-536a27d0a78e" />

---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
12 is Even

### CODE:
```
CREATE OR REPLACE PROCEDURE check_even_odd(p_num NUMBER)
IS
BEGIN
    IF MOD(p_num, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(p_num || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(p_num || ' is Odd');
    END IF;
END;
/

-- Call the procedure
BEGIN
    check_even_odd(12);
END;
/

```
### OUTPUT

<img width="477" height="230" alt="image" src="https://github.com/user-attachments/assets/9fe8e4d6-f8ab-46d4-8eff-6e2b32d3ebbb" />

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

**Expected Output:**  
Reversed number of 1234 is 4321

### CODE:
```
CREATE OR REPLACE FUNCTION reverse_number(p_num NUMBER)
RETURN NUMBER
IS
    v_num NUMBER := p_num;
    v_reverse NUMBER := 0;
    v_digit NUMBER;
BEGIN
    WHILE v_num > 0 LOOP
        v_digit := MOD(v_num, 10);
        v_reverse := v_reverse * 10 + v_digit;
        v_num := TRUNC(v_num / 10);
    END LOOP;

    RETURN v_reverse;
END;
/

-- Call the function
BEGIN
    DBMS_OUTPUT.PUT_LINE(
        'Reversed number of 1234 is ' || reverse_number(1234)
    );
END;
/

```
### OUTPUT
<img width="712" height="243" alt="image" src="https://github.com/user-attachments/assets/18fef951-e31d-405f-831e-c0647e6e18ea" />

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

### CODE:
```
CREATE OR REPLACE PROCEDURE print_table(p_num NUMBER)
IS
    i NUMBER := 1;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Multiplication table of ' || p_num || ':');

    WHILE i <= 10 LOOP
        DBMS_OUTPUT.PUT_LINE(
            p_num || ' x ' || i || ' = ' || (p_num * i)
        );

        i := i + 1;
    END LOOP;
END;
/

-- Call the procedure
BEGIN
    print_table(5);
END;
/

```
### OUTPUT
<img width="662" height="410" alt="image" src="https://github.com/user-attachments/assets/7bdea9ec-d119-4dba-81d0-7dcd3b225588" />

---

## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
