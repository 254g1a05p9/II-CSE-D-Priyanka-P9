# EXPERIMENT 7a)

## 1. Create Table and Insert Sample Records
> **Note: if table already exit drop it and create it.**

```
SET SERVEROUTPUT ON;

CREATE TABLE student (
    st
udent_id NUMBER(5) PRIMARY KEY,
    student_name VARCHAR2(50),
    course VARCHAR2(30),
    marks NUMBER(5,2)
);

INSERT INTO student VALUES (101, 'Ravi', 'CSE', 85);
INSERT INTO student VALUES (102, 'Sita', 'CSE', 92);
INSERT INTO student VALUES (103, 'Kiran', 'ECE', 78);
INSERT INTO student VALUES (104, 'Anjali', 'EEE', 88);
INSERT INTO student VALUES (105, 'Rahul', 'CSE', 74);

COMMIT;

```
## output of student table creation
![Output1](EXP-7A-1.png)

## Insertion of content in student table
![Output1](EXP-7A-2.png)

## verifying student table Information
![Output1](EXP-7A-3.png)

## 2. Create the Stored Procedure

```
CREATE OR REPLACE PROCEDURE GET_STUDENT_DETAILS (
    p_student_id   IN  student.student_id%TYPE,
    p_student_name OUT student.student_name%TYPE,
    p_marks        OUT student.marks%TYPE
)
IS
BEGIN
    -- Retrieve student details
    SELECT student_name, marks
    INTO p_student_name, p_marks
    FROM student
    WHERE student_id = p_student_id;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        p_student_name := NULL;
        p_marks := NULL;

        DBMS_OUTPUT.PUT_LINE(
            'No student found with ID: ' || p_student_id
        );

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(
            'Error: ' || SQLERRM
        );
END;

```
## Output of Procedure Compiled

![compiled output](EXP-7A-4.png)

## Execution of procedure by creating Anonymous PL/SQL block

```
DECLARE
    -- Variables to receive OUT parameter values
    v_student_name student.student_name%TYPE;
    v_marks        student.marks%TYPE;

BEGIN
    -- Call the procedure
    GET_STUDENT_DETAILS(
        101,
        v_student_name,
        v_marks
    );

    -- Display returned values
    IF v_student_name IS NOT NULL THEN
        DBMS_OUTPUT.PUT_LINE(
            'Student Name : ' || v_student_name
        );

        DBMS_OUTPUT.PUT_LINE(
            'Marks        : ' || v_marks
        );
    END IF;

END;

```
## output by using correct student id
![output](EXP-7A-5.png)

## Output by calling wrong student id

> **Note:** To execute it woring id put it to -101

![output](EXP-7A-6.png)
![output](EXP-7A-7.png)

## Another Method of Execution

1. Enable Server output
2. Create two bind Variables
3. Call the Procudure using exec command
4. Print the two bind variables

### 1. Enable Server output

```

SET SERVEROUTPUT ON;

```
![output](EXP-7A-8.png)

### 2. Create two bind variables

```
VARIABLE v_name VARCHAR2(50);
VARIABLE v_marks NUMBER;

```
![output](EXP-7A-9.png)

### 3. Call the Procedure

```
EXEC GET_STUDENT_DETAILS(101, :v_name, :v_marks);

```
![output](EXP-7A-10.png)

### 4. Print the two binded variables;

```
PRINT v_name;
PRINT v_marks;

```
![output](EXP-7A-11.png)

![output](EXP-7A-12.png)

### Calling Procudure with wrong input

![output](EXP-7A-13.png)
# Experiment - 7b

## Program 1: Calculate Annual Salary Using a Stored Function 

## 1. Create the Employee table

```
CREATE TABLE employee (
    employee_id NUMBER(5) PRIMARY KEY,
    employee_name VARCHAR2(50),
    monthly_salary NUMBER(10,2)
);

```
## Output of Employee table

![output](EXP-7B-1.png)

## 2. Insert Sample Employee Records

```
INSERT INTO employee VALUES (101, 'Ravi', 25000);
INSERT INTO employee VALUES (102, 'Sita', 30000);
INSERT INTO employee VALUES (103, 'Kiran', 35000);
INSERT INTO employee VALUES (104, 'Anjali', 40000);
INSERT INTO employee VALUES (105, 'Rahul', 45000);

COMMIT;

```
## Output of Insertion Employee table

![output](EXP-7B-2.png)

## 3. Create the Stored Function

```
CREATE OR REPLACE FUNCTION CALCULATE_ANNUAL_SALARY (
    p_monthly_salary IN NUMBER
)
RETURN NUMBER
IS
    v_annual_salary NUMBER;
BEGIN
    -- Calculate annual salary
    v_annual_salary := p_monthly_salary * 12;

    -- Return annual salary
    RETURN v_annual_salary;
END;

```
## Output of Compiled Function

![output](EXP-7B-3.png)

## Execute the Function Using SELECT

```

SELECT
    employee_id,
    employee_name,
    monthly_salary,
    CALCULATE_ANNUAL_SALARY(monthly_salary) AS annual_salary
FROM employee;

```
## Output of Function using Select Statement

![output](EXP-7B-4.png)

---

## Program 2: Find the Total Number of Students in a Course 

## 1. Create the STUDENT Table

```
CREATE TABLE student (
    student_id NUMBER(5) PRIMARY KEY,
    student_name VARCHAR2(50),
    course VARCHAR2(30),
    marks NUMBER(5,2)
);

```
## Output of Student table Creation

![output](EXP-7B-5.png)


## 2. Insert Sample Student Records

```
INSERT INTO student VALUES (101, 'Ravi',   'CSE', 85);
INSERT INTO student VALUES (102, 'Sita',   'CSE', 92);
INSERT INTO student VALUES (103, 'Kiran',  'ECE', 78);
INSERT INTO student VALUES (104, 'Anjali', 'EEE', 88);
INSERT INTO student VALUES (105, 'Rahul',  'CSE', 74);
INSERT INTO student VALUES (106, 'Priya',  'ECE', 95);
INSERT INTO student VALUES (107, 'Arun',   'IT',  81);
INSERT INTO student VALUES (108, 'Sneha',  'CSE', 89);
INSERT INTO student VALUES (109, 'Vijay',  'EEE', 68);
INSERT INTO student VALUES (110, 'Divya',  'IT',  91);
INSERT INTO student VALUES (111, 'Manoj',  'ECE', 76);
INSERT INTO student VALUES (112, 'Kavya',  'CSE', 84);
INSERT INTO student VALUES (113, 'Ramesh', 'IT',  72);
INSERT INTO student VALUES (114, 'Swathi', 'EEE', 87);
INSERT INTO student VALUES (115, 'Ajay',   'ECE', 93);

COMMIT;

```

## Insertion  of values into Student table

![output](EXP-7B-6.png)

## Displaying of Student Information

```

SELECT * FROM student;

```

![output](EXP-7B-7.png)



## 3. Create the Stored Function

```

CREATE OR REPLACE FUNCTION COUNT_STUDENTS (
    p_course IN VARCHAR2
)
RETURN NUMBER
IS
    v_total_students NUMBER;
BEGIN
    -- Count students belonging to the given course
    SELECT COUNT(*)
    INTO v_total_students
    FROM student
    WHERE course = p_course;

    -- Return the count
    RETURN v_total_students;
END;

```
## Output of Compiled Functions

![output](EXP-7B-8.png)

## Invoke the Function Using SQL SELECT

```
SELECT
    'CSE' AS course,
    COUNT_STUDENTS('CSE') AS total_students
FROM dual;

```
## Execution of stored Functions using SELECT

![output](EXP-7B-9.png)

## 5. Test Other Courses

```
SELECT
    'ECE' AS course,
    COUNT_STUDENTS('ECE') AS total_students
FROM dual;

```
## Execution of stored Functions using other test case

![output](EXP-7B-10.png)


## Display Count for All Courses

```

SELECT
    course,
    COUNT_STUDENTS(course) AS total_students
FROM (
    SELECT DISTINCT course
    FROM student
);

```

## Execution of stored Functions using test case as all Courses

![output](EXP-7B-11.png)

## Program 3: Determine Student Grade Using a Complex Stored Function 

## 1. Create the STUDENT Table

```

CREATE TABLE student (
    student_id NUMBER(5) PRIMARY KEY,
    student_name VARCHAR2(50),
    marks NUMBER(5,2)
);

```

## Output of student table creation

![output](EXP-7B-12.png)

## 2. Insert Sample Student Records

```
INSERT INTO student VALUES (101, 'Ravi',   85);
INSERT INTO student VALUES (102, 'Sita',   72);
INSERT INTO student VALUES (103, 'Kiran',  55);
INSERT INTO student VALUES (104, 'Anjali', 45);
INSERT INTO student VALUES (105, 'Rahul',  30);
INSERT INTO student VALUES (106, 'Priya',  91);
INSERT INTO student VALUES (107, 'Arun',   68);
INSERT INTO student VALUES (108, 'Sneha',  58);

COMMIT;
```
##  student table insertion

![output](EXP-7B-13.png)

##  Display Student table

```
SELECT * FROM student;

```
## Output of student details

![output](EXP-7B-14.png)

## 3. Create the Stored Function GET_GRADE

```
CREATE OR REPLACE FUNCTION GET_GRADE (
    p_marks IN NUMBER
)
RETURN VARCHAR2
IS
    v_grade VARCHAR2(20);
BEGIN

    -- Determine grade based on marks
    IF p_marks >= 75 THEN
        v_grade := 'Distinction';

    ELSIF p_marks >= 60 THEN
        v_grade := 'First Class';

    ELSIF p_marks >= 50 THEN
        v_grade := 'Second Class';

    ELSIF p_marks >= 35 THEN
        v_grade := 'Pass';

    ELSE
        v_grade := 'Fail';
    END IF;

    -- Return the calculated grade
    RETURN v_grade;

END;
/

```
##  Compiled Stored Function

![output](EXP-7B-15.png)



## 4. Invoke the Function Using SELECT 

```
SELECT
    student_name,
    marks,
    GET_GRADE(marks) AS grade
FROM student;

```

## Output Invoking  Compiled Stored Function

![output](EXP-7B-16.png)
