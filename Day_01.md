 # Database Management Systems (DBMS) & SQL Reference Guide

A comprehensive, structured study and reference guide covering fundamental database concepts, Relational Database Management Systems (RDBMS), SQL syntax, database architecture, and relational model theories.

---

## 📌 Table of Contents
1. [Core Database Concepts](#1-core-database-concepts)
2. [DBMS Architecture & Components](#2-dbms-architecture--components)
3. [Relational Model Key Terms & Characteristics](#3-relational-model-key-terms--characteristics)
4. [Types of Keys in RDBMS](#4-types-of-keys-in-rdbms)
5. [Database Languages (SQL Categories)](#5-database-languages-sql-categories)
6. [SQL Syntax & Querying Reference](#6-sql-syntax--querying-reference)
7. [Built-in SQL Functions](#7-built-in-sql-functions)
8. [Integrity Constraints & Functional Dependencies](#8-integrity-constraints--functional-dependencies)

---

## 1. Core Database Concepts

* **Database:** A centralized digital container designed to store, manage, and retrieve related data in an organized and structured format.
* **Analogy:**
  * 📁 **Folder / Directory** -> Database
  * 📄 **File / Spreadsheet Sheet** -> Table
  * 📝 **Row / Line Text** -> Row (Tuple) Data
* **DBMS (Database Management System):** A specialized software engine acting as an interface between end-users/applications and the central database storage. It ensures data is created, updated, read, and deleted (CRUD) securely and efficiently.

### Primary Database Paradigms
1. **Relational DBMS (RDBMS):** Stores structured data inside tables with predefined columns and strict data types. Maintains data integrity through keys, constraints, and relationships. *Example: MySQL, PostgreSQL.*
2. **NoSQL DBMS:** Flexible database engines that do not enforce a fixed schema. Designed to store unstructured or semi-structured data across various formats (documents, key-value, graphs). *Example: MongoDB, Redis.*
3. **Specialized DBMS Variations:** Modern solutions merging ACID compliance with high scalability like NewSQL, Object-Oriented DBMS (*ObjectDB*), Hierarchical Databases (*IBM*), Network Databases (*IDS*), and Cloud Data Warehouses (*Google BigQuery*).

---

## 2. DBMS Architecture & Components

A complete production DBMS ecosystem relies on six core operational building blocks:

* **Hardware:** Physical computational infrastructure including dedicated servers, high-speed RAM, and persistent storage arrays (Hard Disks/SSDs).
* **Software:** The underlying software stack including the core database engine, host Operating System, networking management modules, and application wrapper utilities.
* **Data:** Divided into two distinct categories:
  * *Operational Data:* The real underlying business/user data records.
  * *Metadata:* The dictionary framework storing descriptions about the data structures (schemas, types, constraints).
* **Procedures:** Step-by-step operating guidelines covering setup protocols, access control, validation matrices, disaster backups, and analytical report generations.
* **Database Access Language:** The command interface (such as SQL) utilized to read and write database objects.
* **People:**
  * *Database Administrator (DBA):* Monitors system health, manages security clearances, optimizes performance tuning, and coordinates access boundaries.
  * *Developers:* Build full-stack application logic and design integration schemas.
  * *End Users:* Consume information through final software applications.

---

## 3. Relational Model Key Terms & Characteristics

Relational models strictly adhere to mathematical set theory to represent tabular data.

| Term | Definition |
| :--- | :--- |
| **Attributes** | Individual column headers defining specific properties of an entity. |
| **Tuple** | A single unique row entry within a table. |
| **Relation Schema** | The foundational definition and structural blueprint of a table. |
| **Relation Instance** | A snapshot of data containing a specific set of tuples collected at a precise moment in time. |
| **Degree** | Total count of columns (attributes) defining a table. |
| **Cardinality** | Total count of rows (tuples) present inside a table instance. |

### Core Rules of Relational Models
* **Atomic Values:** Every intersecting cell must retain an individual, indivisible value. Multi-valued or nested array structures inside a single standard relational cell are completely prohibited.
* **Primary Key Mandatory:** Every distinct table structure must declare a unique identifying primary row pointer.

---

## 4. Types of Keys in RDBMS

Keys establish identity and link records together across independent structures.

1. **Super Key:** Any collection of one or more columns that can uniquely pinpoint a row entry within a table.
2. **Candidate Key:** A minimal Super Key containing no redundant attributes. It represents a valid contender for table identification; it enforces `UNIQUE` and `NOT NULL` rules. A table can have multiple candidate keys, but exactly **one** will become the Primary Key.
3. **Primary Key:** The chosen unique identifier for a table. It cannot accept null entries and must remain globally unique across all rows.
4. **Foreign Key:** An attribute located inside a child table that actively points to a primary key column in a parent table, forming relational links.
5. **Composite Key:** An identification key formed by joining two or more distinct columns together when no individual column can guarantee unique row isolation on its own.

---

## 5. Database Languages (SQL Categories)

SQL instructions are sub-classified into distinct specialized sub-languages based on their functional scope:

| Category | Description | Core Operations |
| :--- | :--- | :--- |
| **DDL** *(Data Definition Language)* | Modifies structural blueprints and metadata schemas without touching data entries. | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`, `COMMENT` |
| **DML** *(Data Manipulation Language)* | Coordinates records tracking, structural values, and manipulation of data blocks. | `INSERT`, `UPDATE`, `DELETE`, `MERGE`, `CALL`, `LOCK TABLE` |
| **DQL** *(Data Query Language)* | Reads and extracts filtered analytical data snapshots safely without modification. | `SELECT` |
| **DCL** *(Data Control Language)* | Structures security authorization profiles and data access barriers. | `GRANT`, `REVOKE` |
| **TCL** *(Transaction Control Language)* | Manages transactional boundaries to ensure absolute data consistency (ACID tracking). | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |

---

## 6. SQL Syntax & Querying Reference

### Database & Table DDL

```sql
-- Create a fresh database
CREATE DATABASE ecommerce_db;

-- Set a database as the active default working schema
USE ecommerce_db;

-- Permanently drop a database from the system
DROP DATABASE ecommerce_db;
```

#### Creating Tables with Constraints
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    gender ENUM('Male', 'Female', 'Other'),
    date_of_birth DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Altering Active Table Schemas
```sql
-- Rename an entire table asset
RENAME TABLE users TO app_users;

-- Inject a fresh column into an existing layout
ALTER TABLE app_users ADD COLUMN phone_number VARCHAR(15);

-- Eliminate an outdated column block
ALTER TABLE app_users DROP COLUMN phone_number;

-- Modify column properties or enforce a strict constraint
ALTER TABLE app_users MODIFY COLUMN name VARCHAR(100) NOT NULL;

-- Reposition structural layout location (using FIRST or AFTER)
ALTER TABLE app_users MODIFY COLUMN email VARCHAR(100) AFTER id;

-- Rename a column target accurately
ALTER TABLE app_users RENAME COLUMN date_of_birth TO dob;
```

### Data Modification (DML)

#### Data Insertion
```sql
-- Standard single-row entry insertion
INSERT INTO app_users (id, name, email, gender, dob) 
VALUES (1, 'Harry', 'harry@harry.com', 'Male', '1995-05-12');

-- High-speed multi-row concurrent bulk insertions
INSERT INTO app_users (name, email, gender, dob) VALUES 
('Jenny', 'jenny@jenny.com', 'Female', '1998-11-23'),
('Alex', 'alex@alex.com', 'Other', '2000-01-15');
```

#### Record Updates
```sql
-- Updating matching data items conditional rules
UPDATE app_users 
SET name = 'Harrison', email = 'harrison@gmail.com' 
WHERE id = 1;

-- Running numeric evaluations and batch increments
UPDATE employees 
SET salary = salary + 1000 
WHERE salary <= 60000;
```

#### Data Removal Operations
```sql
-- Target and purge explicit entries safely
DELETE FROM app_users WHERE id = 3;

-- Wipe out all contents while preserving the table structure intact
DELETE FROM app_users;

-- Delete the entire structural object along with all its contents
DROP TABLE app_users;
```

### Data Querying (DQL) & Filtering

#### Core Query Modifiers
```sql
-- Single attribute or wildcard multi-column sweeps
SELECT name, email FROM app_users;
SELECT * FROM app_users;

-- Advanced numeric, nullability and categorical conditions
SELECT * FROM app_users WHERE id >= 5;
SELECT * FROM app_users WHERE gender IS NULL;
SELECT * FROM app_users WHERE gender IS NOT NULL;
SELECT * FROM app_users WHERE gender = 'Female';
```

#### Range, List & Pattern Matching Filters
```sql
-- Chronological and numeric boundary limits
SELECT * FROM app_users WHERE dob BETWEEN '1990-01-01' AND '2000-01-01';

-- Discrete item multi-value listings matching
SELECT * FROM app_users WHERE gender IN ('Male', 'Other');

-- Advanced string wildcard scanning (LIKE operator patterns)
SELECT * FROM app_users WHERE name LIKE 'A%';     -- Starts with 'A'
SELECT * FROM app_users WHERE name LIKE '%a';     -- Ends with 'a'
SELECT * FROM app_users WHERE name LIKE '%Li%';   -- Contains 'Li'
```

#### Sorting & Pagination Control
```sql
-- Ascending (ASC) or Descending (DESC) ordering configurations
SELECT * FROM app_users ORDER BY dob ASC;
SELECT * FROM app_users ORDER BY created_at DESC;

-- High-performance result windowing controls (Pagination)
SELECT * FROM app_users LIMIT 5;                  -- Top 5 records
SELECT * FROM app_users LIMIT 10 OFFSET 5;         -- Bypasses initial 5 rows and delivers next 10
SELECT * FROM app_users LIMIT 5, 10;              -- Skip 5 rows, take 10 rows
```

---

## 7. Built-in SQL Functions

### 1. Aggregate Functions
```sql
SELECT COUNT(*) FROM app_users;
SELECT MIN(salary) AS min_salary, MAX(salary) AS max_salary FROM employees;
SELECT SUM(salary) AS total_pay FROM employees;
SELECT AVG(salary) AS avg_salary FROM employees;

-- Grouping aggregates
SELECT gender, AVG(salary) AS avg_salary FROM employees GROUP BY gender;
```

### 2. String Functions
```sql
SELECT name, LENGTH(name) AS name_len FROM app_users;
SELECT LOWER(name) AS lowercase, UPPER(name) AS uppercase FROM app_users;
SELECT CONCAT(name, ' - ', email) AS user_contact FROM app_users;
```

### 3. Mathematical Functions
```sql
SELECT id, MOD(id, 2) AS remainder FROM app_users;
SELECT salary, ROUND(salary), FLOOR(salary), CEIL(salary) FROM employees;
```

### 4. Date & Temporal Functions
```sql
SELECT NOW(), CURDATE();
SELECT name, YEAR(dob), MONTH(dob), DAY(dob) FROM app_users;
SELECT name, DATEDIFF(CURDATE(), dob) AS days_lived FROM app_users;
SELECT name, TIMESTAMPDIFF(YEAR, dob, CURDATE()) AS age FROM app_users;
```

### 5. Conditional Functions
```sql
SELECT name, gender, IF(gender = 'Female', 'Yes', 'No') AS is_female FROM app_users;
```

---

## 8. Integrity Constraints & Functional Dependencies

### Primary Table Level Integrity Rules
1. **Domain Constraints:** Restricts data cell contents to standardized format and type rules.
2. **Key Integrity:** Enforces absolute unique non-null Primary Key rules.
3. **Referential Integrity:** Enforces Foreign Key connections to point strictly to active Primary Keys in referenced parent layouts.

#### Adding Constraints Post-Creation
```sql
ALTER TABLE app_users ADD CONSTRAINT unique_email UNIQUE (email);
ALTER TABLE app_users ADD CONSTRAINT check_dob CHECK (dob >= '1920-01-02');
ALTER TABLE app_users ALTER COLUMN is_active SET DEFAULT TRUE;
```

### Functional Dependencies (FD)
A functional dependency describes an association between attributes in a relation. It is denoted as: **X -> Y**

* **Meaning:** Attribute X uniquely determines the value of attribute Y. If two rows share an identical value for X, they must share an identical value for Y.
* **Terminology:** X is the *Determinant*, Y is the *Dependent Attribute*.

#### FD Identification Logic Flow
* Check if the X column contains any duplicate values.
  * **No Duplicates:** An automatic Functional Dependency (X -> Y) exists.
  * **Duplicates Exist:** Inspect the matching Y entries.
    * If Y values match exactly across identical X duplicates -> FD (X -> Y) holds true.
    * If Y values differ for identical X duplicates -> No FD exists.
