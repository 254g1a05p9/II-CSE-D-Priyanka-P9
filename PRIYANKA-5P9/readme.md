# (1a) create the table with out constraints
...
CREATE TABLE Student(
  Name VARCHAR2(20),
  Student_number NUMBER,
  Class NUMBER,
  Major VARCHAR2(20)
);

CREATE TABLE Course(
  Course_name VARCHAR2(40),
  Course_number VARCHAR2(10),
  Credit_hours NUMBER,
  Department VARCHAR2(20)
);

CREATE TABLE Section(
  Section_identifier NUMBER,
  Course_number VARCHAR2(10),
  Semester VARCHAR2(10),
  Year NUMBER,
  Instructor VARCHAR2(20)
);

CREATE TABLE Grade_Report(
  Student_number NUMBER,
  Section_identifier NUMBER,
  Grade CHAR(1)
);

CREATE TABLE Prerequisite(
  Course_number VARCHAR2(10),
  Prerequisite_number VARCHAR2(10)
);
...
![output](op1.png)
# Insert all values inside the table
...
INSERT INTO Student VALUES('Smith', 17, 1, 'CS');
INSERT INTO Student VALUES('Brown', 8, 2, 'CS');
INSERT INTO Student VALUES('Amit', 12, 1, 'ECE');
INSERT INTO Student VALUES('Priya', 20, 3, 'CS');
INSERT INTO Student VALUES('John', 25, 2, 'EEE');

INSERT INTO Course VALUES('Intro to CS', 'CS101', 4, 'CS');
INSERT INTO Course VALUES('Data Structures', 'CS102', 4, 'CS');
INSERT INTO Course VALUES('Database', 'CS131', 4, 'CS');
INSERT INTO Course VALUES('Circuits', 'EE101', 3, 'EEE');

INSERT INTO Section VALUES(101, 'CS101', 'Fall', 2024, 'Prof Rao');
INSERT INTO Section VALUES(102, 'CS102', 'Fall', 2024, 'Prof Kumar');
INSERT INTO Section VALUES(103, 'CS131', 'Spring', 2025, 'Prof Ali');
INSERT INTO Section VALUES(104, 'EE101', 'Fall', 2024, 'Prof Smith');

INSERT INTO Grade_Report VALUES(17, 101, 'A');
INSERT INTO Grade_Report VALUES(8, 102, 'B');
INSERT INTO Grade_Report VALUES(12, 101, 'A');
INSERT INTO Grade_Report VALUES(20, 103, 'C');
INSERT INTO Grade_Report VALUES(25, 104, 'B');

INSERT INTO Prerequisite VALUES('CS102', 'CS101');
INSERT INTO Prerequisite VALUES('CS131', 'CS102');
INSERT INTO Prerequisite VALUES('CS131', 'CS101');
...
![output](op2-1.png)
![output](op2-2.png)
![output](op2-3.png)
# DESC all tables
...
DESC Student;
DESC Course;
DESC Section;
DESC Grade_Report;
DESC Prerequisite;
...
![output](op3.png)
# List the tables
...
SHOW TABLES;
...
![output](op4.png)
# Display the values
...
SELECT * FROM Student;
SELECT * FROM Course;
SELECT * FROM Section;
SELECT * FROM Grade_Report;
SELECT * FROM Prerequisite;
...
![output](op5-1.png)
![output](op5-2.png)
![output](op5-3.png)
![output](op5-4.png)
# Drop the tables
...
DROP TABLE Grade_Report;
DROP TABLE Prerequisite;
DROP TABLE Section;
DROP TABLE Course;
DROP TABLE Student; 
...
![output](op6.png)
