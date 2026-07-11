Comprehensive DBMS Notes
1. Introduction to DBMS, Need and Advantages
What is a DBMS?
A Database Management System (DBMS) is a software application that interacts with end-users, applications, and the database itself to capture and analyze data. It acts as an intermediary between the user and the database, ensuring data is consistently organized, easily accessible, and secure.

Example: MySQL, Oracle, PostgreSQL, and Microsoft SQL Server are all popular DBMS software. When you log into your bank's mobile app, the app communicates with a DBMS to fetch your balance.

The Need for a DBMS (Why not just use File Systems?)
Before DBMS, data was stored in flat files (like Excel sheets or text files). This led to several severe problems that a DBMS solves:

Problem in File Systems	How DBMS Solves It
Data Redundancy & Inconsistency (Same data copied in multiple files; updates miss some copies).	DBMS enforces data normalization and centralized control to minimize duplication.
Data Isolation (Data scattered across different formats; hard to retrieve combined data).	DBMS provides a unified interface (SQL) to query data from multiple tables simultaneously.
Integrity Problems (Hard to enforce rules like "Age cannot be negative").	DBMS supports constraints (e.g., CHECK, UNIQUE, FOREIGN KEY) at the schema level.
Concurrent Access Anomalies (Two users updating the same file at the same time corrupt data).	DBMS uses Transaction Management and locking mechanisms (ACID properties) to handle concurrency.
Security Issues (Everyone can read the entire flat file).	DBMS provides granular authorization (who can read/update specific columns or tables).
Atomicity Issues (System crashes mid-update leaves data half-changed).	DBMS guarantees Atomicity – either the entire transaction completes or none of it does.
Key Advantages of DBMS
Controlling Data Redundancy: Minimizes duplicate data storage.

Data Sharing: Multiple users and applications can access the same data simultaneously.

Data Security: Protects data through authentication and authorization.

Persistent Storage: Data is stored permanently and survives system restarts.

Backup and Recovery: Provides automated mechanisms to restore data after crashes.

Data Independence: Allows changes in storage structures without rewriting applications (explained next).

2. Data Abstraction & Data Independence
To hide the complexities of how data is stored physically, DBMS uses a three-level architecture. This is called Data Abstraction.

The Three Levels of Abstraction (ANSI-SPARC Architecture)
Physical Level (Internal Level):

What it is: The lowest level. It describes how the data is actually stored on the storage devices (hard drives). It deals with data structures, file organization, indexing, and compression techniques.

Who sees it: Database Administrators (DBAs) and system programmers.

Example: Deciding to store the Employee table using B-Tree indexing on the Employee_ID column to speed up searches.

Logical Level (Conceptual Level):

What it is: The middle level. It describes what data is stored and the relationships among that data. It defines the schema (tables, columns, data types, and constraints) but does not care about how it is physically stored.

Who sees it: Application developers and end-users.

Example: Knowing that there is a table called Students with columns Roll_No (INT) and Name (VARCHAR), without knowing which hard drive sectors these values are on.

View Level (External Level):

What it is: The highest level. It describes only part of the entire database that a specific user is allowed to see. It provides a customized interface for different users.

Who sees it: End-users.

Example: The HR manager sees the Salary column, but a regular employee sees only Name and Department (through a created View).

Data Independence
Data Independence is the capacity to change the schema at one level without having to change the schema at the next higher level.

A. Physical Data Independence
Definition: The ability to modify the physical schema (storage structures) without rewriting or altering the logical schema.

How it helps: If we add new indexes or change the storage algorithm, the application queries (SELECT statements) do not break.

Example:

Change: You add a new B-Tree index on the Last_Name column to speed up searches.

Effect on Application: The application still runs SELECT * FROM Employees WHERE Last_Name = 'Smith'; without any changes. The DBMS internally decides whether to use the new index or not.

B. Logical Data Independence
Definition: The ability to modify the logical schema (tables and columns) without affecting the external schemas (views) or application programs.

How it helps: We can add new columns or change data types without forcing every user to rewrite their code, provided they use views.

Example:

Change: You split the Customer table into Customer_Info and Customer_Address for normalization.

Effect on Application: You create a View called Customer_View that joins these two tables to look exactly like the old Customer table. The old application queries the Customer_View and runs perfectly without code changes.

3. Data Models Overview
A Data Model is a conceptual framework that defines how data is structured, stored, and the relationships between different data entities. It acts as a blueprint for designing the database.

Overview of Major Data Models
Data Model	Description	Structure	Example
Hierarchical Model	Data is organized in a tree-like structure. Parent-child relationship (One-to-Many).	Record-based, uses pointers.	An organization's reporting structure (CEO -> Managers -> Employees).
Network Model	Data is organized as a graph. Allows Many-to-Many relationships via pointers.	Record-based, uses sets/pointers.	A student enrolling in multiple courses, and a course having multiple students.
Relational Model (Most Popular)	Data is organized in two-dimensional tables (Relations) with rows (Tuples) and columns (Attributes).	Table-based, uses primary/foreign keys.	SQL Databases like MySQL. Table: Orders linked to Customers via Customer_ID.
Entity-Relationship (ER) Model	A high-level conceptual model used for design. Represents real-world entities and relationships.	Diagrammatic (Rectangles for entities, diamonds for relationships).	An ER diagram showing "Employee" works_for "Department".
Object-Oriented Model	Data is stored as objects (like OOP). Supports inheritance, encapsulation, and methods.	Object-based.	Multimedia databases or CAD systems.
NoSQL Models	Designed for unstructured, semi-structured, or distributed data. Includes Key-Value, Document, Column-Family, and Graph.	Flexible schemas.	Document: JSON data in MongoDB.
Graph: Nodes and edges in Neo4j (Social Networks).
Detailed Focus: The Relational Model (Most relevant for practical DBMS)
Table (Relation): A collection of data organized in rows and columns.

Tuple (Row): A single record.

Attribute (Column): A field or characteristic of the record.

Key: Uniquely identifies a row (Primary Key).

Foreign Key: Links one table to another.

Example of Relational Model:
Table: Students

Roll_No (Primary Key)	Name	Dept_ID (Foreign Key)
101	Alice	D01
102	Bob	D02
Table: Departments

Dept_ID (Primary Key)	Dept_Name
D01	Computer Science
D02	Mathematics
4. DDL & DML (Data Definition Language & Data Manipulation Language)
SQL (Structured Query Language) is divided into sublanguages based on functionality. The two most fundamental are DDL and DML.

A. Data Definition Language (DDL)
Definition: DDL is a set of SQL commands used to define and modify the structure (schema) of the database. It deals with the creation, alteration, and deletion of database objects like tables, indexes, and users.

Nature: DDL commands are Auto-Commit in nature. Once executed, the changes are permanently saved to the database immediately (cannot be rolled back easily in most systems).

Key DDL Commands:

CREATE: To create a database or table.

ALTER: To change the structure of an existing table (add, drop, or modify columns).

DROP: To delete the entire table/object structure (removes the table permanently).

TRUNCATE: To remove all records from a table (empties the data, but keeps the table structure).

RENAME: To rename a table or column.

DDL Example Notes:

sql
-- 1. CREATE: Defining a new 'Product' table
CREATE TABLE Product (
    Product_ID INT PRIMARY KEY,
    Product_Name VARCHAR(100) NOT NULL,
    Price DECIMAL(10, 2),
    Manufacture_Date DATE
);

-- 2. ALTER: Adding a new column called 'Category' to the Product table
ALTER TABLE Product ADD (Category VARCHAR(50));

-- 3. ALTER: Modifying the data type of the 'Price' column
ALTER TABLE Product MODIFY (Price DECIMAL(12, 2));

-- 4. DROP: Permanently removing the 'Product' table (including structure and data)
DROP TABLE Product;

-- 5. TRUNCATE: Removing all rows from the 'Product' table (structure remains)
TRUNCATE TABLE Product;
B. Data Manipulation Language (DML)
Definition: DML is a set of SQL commands used to manage the data inside the schema objects. It handles the retrieval, insertion, modification, and deletion of data rows.

Nature: DML commands are Non-Auto-Commit by default (in most DBMS). They operate within transactions. You must explicitly COMMIT to save changes or ROLLBACK to undo them.

Types of DML:

Procedural DML: Specifies what data is needed and how to retrieve it.
Declarative (Non-Procedural) DML: Specifies what data is needed only (e.g., SQL). The system decides how to fetch it.
Key DML Commands:

SELECT: Retrieves data from the table(s).

INSERT: Adds new rows of data into the table.

UPDATE: Modifies existing data in the table.

DELETE: Removes existing rows from the table.

DML Example Notes:
Let's assume we have a table named Employees with columns: Emp_ID, Name, Salary, Dept.

sql
-- 1. INSERT: Adding a new employee record
INSERT INTO Employees (Emp_ID, Name, Salary, Dept) 
VALUES (101, 'John Doe', 55000, 'IT');

INSERT INTO Employees VALUES (102, 'Jane Smith', 65000, 'HR'); -- Simplified (order must match)

-- 2. SELECT: Retrieving all employees from the IT department
SELECT * FROM Employees WHERE Dept = 'IT';

-- SELECT with specific columns and sorting
SELECT Name, Salary FROM Employees ORDER BY Salary DESC;

-- 3. UPDATE: Giving a 10% salary raise to all employees in the HR department
UPDATE Employees 
SET Salary = Salary * 1.10 
WHERE Dept = 'HR';

-- 4. DELETE: Removing an employee with a specific ID
DELETE FROM Employees WHERE Emp_ID = 102;

-- Transaction Management (IMPORTANT for DML)
BEGIN TRANSACTION; -- Start transaction
    INSERT INTO Employees VALUES (103, 'Alice', 70000, 'Finance');
    UPDATE Employees SET Salary = 71000 WHERE Emp_ID = 103;
-- If everything is correct, save permanently:
COMMIT; 
-- If something went wrong, undo everything since BEGIN:
ROLLBACK; 
Summary Comparison: DDL vs DML
Feature	DDL (Data Definition Language)	DML (Data Manipulation Language)
Purpose	Defines the Database Structure (Schema).	Manages the Data within the structure.
Commands	CREATE, ALTER, DROP, TRUNCATE	SELECT, INSERT, UPDATE, DELETE
Works on	Database objects (Tables, Indexes, Schemas).	Table Rows (Records).
Transaction Control	Auto-commit. Cannot be rolled back (usually).	Non-auto-commit. Can be rolled back.
Filter Condition	Conditions are not used (except for constraints).	Conditions (using WHERE clause) are heavily used.