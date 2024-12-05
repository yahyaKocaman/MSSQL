![Team_Logo](https://github.com/yahyaKocaman/MSSQL/blob/a3542b7fd67abee46d8ebdc0a246894e85955eea/0BA559F9-4AA4-4AC5-8F41-237F5890F4B4.webp)


# University Management System SQL Schema

This repository contains SQL scripts for setting up a university management system database using Microsoft SQL Server (MSSQL). The project includes table definitions, data insertion, and queries to manage departments, instructors, students, and courses.

🗂️ Table of Contents

	•	Setup Instructions
	•	Schema Overview
	•	SQL Script Breakdown
	•	Sample Queries
	•	Contributing
	•	License
	•	Author

⚙️ Setup Instructions

1. Prerequisites

	•	Microsoft SQL Server installed.
	•	SQL Server Management Studio (SSMS) for executing SQL scripts.

2. Database Initialization

	1.	Create a new database:

CREATE DATABASE UniversityDB;
USE UniversityDB;


	2.	Execute the provided SQL scripts in SSMS to create tables and insert sample data.

🛠️ Schema Overview

Tables

	•	department: Stores department details.
	•	instructor: Contains instructor information.
	•	student: Manages student records.
	•	courses: Lists courses offered.
	•	stu_Courses: Tracks student course enrollments.

📜 SQL Script Breakdown

🔹 Table Creation

Defines primary and foreign keys to establish relationships between tables.

CREATE TABLE department (
    dept_ID NVARCHAR(5) NOT NULL,
    dept_Name NVARCHAR(40) NOT NULL,
    PRIMARY KEY (dept_ID)
);

CREATE TABLE instructor (
    ins_ID NVARCHAR(5) NOT NULL,
    name NVARCHAR(20) NOT NULL,
    surname NVARCHAR(20) NOT NULL,
    dept_ID NVARCHAR(5) NOT NULL,
    PRIMARY KEY (ins_ID),
    FOREIGN KEY (dept_ID) REFERENCES department(dept_ID)
);

CREATE TABLE student (
    stu_ID NVARCHAR(5) NOT NULL,
    name NVARCHAR(20) NOT NULL,
    surname NVARCHAR(20) NOT NULL,
    dept_ID NVARCHAR(5) NOT NULL,
    PRIMARY KEY (stu_ID),
    FOREIGN KEY (dept_ID) REFERENCES department(dept_ID)
);

CREATE TABLE courses (
    course_ID NVARCHAR(5) NOT NULL,
    course_Name NVARCHAR(20) NOT NULL,
    PRIMARY KEY (course_ID)
);

CREATE TABLE stu_Courses (
    stu_ID NVARCHAR(5) NOT NULL,
    course_ID NVARCHAR(5) NOT NULL,
    semester NVARCHAR(10) NOT NULL,
    PRIMARY KEY (stu_ID, course_ID),
    FOREIGN KEY (stu_ID) REFERENCES student(stu_ID),
    FOREIGN KEY (course_ID) REFERENCES courses(course_ID)
);

🔹 Data Insertion

Populates tables with sample data for testing and demonstration.

INSERT INTO department VALUES ('45098', 'software development');
INSERT INTO department VALUES ('85697', 'management');
INSERT INTO department VALUES ('98562', 'Physics');

INSERT INTO courses VALUES ('854', 'DB15');
INSERT INTO courses VALUES ('61', 'OOP');
INSERT INTO courses VALUES ('98', 'Cyber Security');

INSERT INTO student VALUES ('423', 'John', 'Malone', '45098');
INSERT INTO student VALUES ('211', 'Maur', 'Icardi', '85697');

INSERT INTO instructor VALUES ('98561', 'Kağan', 'Okatan', '45098');
INSERT INTO instructor VALUES ('9842', 'Thomas', 'Edison', '85697');
INSERT INTO instructor VALUES ('9691', 'Graham', 'Derst', '98562');

INSERT INTO stu_Courses VALUES ('423', '854', 'Spring_24');
INSERT INTO stu_Courses VALUES ('423', '61', 'Fall_23');
INSERT INTO stu_Courses VALUES ('211', '98', 'Fall_23');

🔍 Sample Queries

1. Retrieve Instructors in the Software Development Department

SELECT instructor.name, instructor.surname
FROM instructor
JOIN department ON instructor.dept_ID = department.dept_ID
WHERE department.dept_Name = 'software development';

2. List Students in the Management Department

SELECT student.name, student.surname
FROM student
JOIN department ON student.dept_ID = department.dept_ID
WHERE department.dept_Name = 'management';

3. Courses Taken by Students in Software Development

SELECT student.name, student.surname, courses.course_Name
FROM student
JOIN department ON student.dept_ID = department.dept_ID
JOIN stu_Courses ON student.stu_ID = stu_Courses.stu_ID
JOIN courses ON stu_Courses.course_ID = courses.course_ID
WHERE department.dept_Name = 'software development';

🤝 Contributing

	1.	Fork this repository.
	2.	Create a new branch for your feature or bug fix.
	3.	Submit a pull request with a detailed explanation of your changes.

**📜 License

This project is licensed under the MIT License. See the `LICENSE` file for details.

---

## **📝 Author**

**[Yahya Kocaman](https://github.com/yahyaKocaman?tab=repositories)**  

3rd-year Software Development Student at Istanbul Aydın University  
Passionate about AI, Machine Learning, and Software Development.  
LinkedIn: [Yahya Kocaman](https://www.linkedin.com/in/yahyakocaman/)
