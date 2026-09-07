# SQL Fundamentals
## Intro
* **Overview:** Highlights the ubiquitous nature of databases across cybersecurity fields—from securing web applications and configuring user access control to navigating SIEM logs in a SOC and investigating malware.
* **Offensive & Defensive Value:**
    * **Offensive:** Helps security professionals understand database vulnerabilities (like SQL injections) and construct queries to retrieve or tamper with data during authorized testing.
    * **Defensive:** Aids in navigating databases to detect suspicious activity, uncover relevant evidence, and implement robust access restrictions.
* **Room Objectives:** Outlines the core learning goals for beginners, which include understanding what databases and SQL are, exploring different database types, and mastering SQL CRUD operations, clauses, operators, and functions.

## Databases 101
* **Overview:** Explores the fundamental concepts of databases, distinguishing between different database models and breaking down how relational data is structured.
* **Types of Databases:**
    * **Relational Databases (SQL):** Stores structured data in a tabular format consisting of rows and columns with defined relationships between tables. Ideal for consistent data where accuracy is critical (e.g., e-commerce transactions).
    * **Non-relational Databases (NoSQL):** Stores data in non-tabular formats (such as key-value pairs or documents) to handle information that varies greatly in structure. Ideal for flexible and scalable use cases like social media user-generated content.
* **Tables, Rows, and Columns:**
    * **Tables:** The primary containers for storing structured data collections.
    * **Columns:** Define the specific attributes and data types (like strings, integers, or dates) for records.
    * **Rows:** Represent individual, populated records within a table.
* **Database Keys:**
    * **Primary Keys:** Uniquely identify each distinct record within a table, ensuring no two rows share the same value in that column.
    * **Foreign Keys:** Columns that reference a primary key in another table, creating the relational link between different tables.

## SQL
* **Overview:** Introduces Database Management Systems (DBMS) and SQL (Structured Query Language), highlighting their roles in facilitating interaction with relational databases.
* **Database Management Systems (DBMS):** Software programs that act as the interface between the end user and the database, allowing users to retrieve, update, and manage stored data (examples include MySQL, MariaDB, and Oracle Database).
* **Structured Query Language (SQL):** A plain-English programming language used to query, define, and manipulate data within a relational database.
* **Benefits of SQL:**
    * Fast: Delivers rapid query responses and processing speeds for massive data batches.
    * Easy to Learn: Highly readable and written in plain English.
    * Reliable: Enforces strict data structures to guarantee accuracy.
    * Flexible: Supports powerful data analysis and querying capabilities.
* **Lab Setup:** Guides you through starting the lab machine and connecting to the MySQL monitor via the terminal using root credentials (`mysql -u root -p`).

## Database and Table Statements
* Overview: Focuses on the foundational DDL (Data Definition Language) statements used to create, manage, and modify relational databases and their underlying tables.
* Database Statements:
    * CREATE DATABASE database_name;: Initializes a new database.
    * SHOW DATABASES;: Lists all current databases on the server (including default system databases like mysql and sys).
    * USE database_name;: Sets the active database so subsequent queries target it.
    * DROP DATABASE database_name;: Deletes an entire database and its contents.
* Table Statements:
    * CREATE TABLE table_name (...);: Creates a new table within the active database by defining columns, data types (e.g., INT, VARCHAR, DATE), and constraints (like PRIMARY KEY, AUTO_INCREMENT, and NOT NULL).
    * SHOW TABLES;: Lists all tables present within the currently active database.
    * DESCRIBE table_name; (or DESC): Displays the detailed schema, fields, data types, and keys of a table.
    * ALTER TABLE table_name ADD column_name data_type;: Modifies an existing table's structure, such as adding new columns.
    * DROP TABLE table_name;: Deletes a specific table from the database.

## CRUD Operations
* **Overview:** Explores the four fundamental database operations—CRUD (Create, Read, Update, Delete)—which form the core of data manipulation and management in relational databases using MySQL.
* **Create (INSERT):** Adds new records to a table using the INSERT INTO statement, specifying the target table, columns, and corresponding values.
* **Read (SELECT):** Retrieves data from a table. The SELECT statement can fetch all columns using an asterisk (*) or target specific column names, often paired with the FROM clause.
* **Update (UPDATE):** Modifies existing records within a table. It uses the UPDATE statement along with SET to define new column values, paired with a WHERE clause to target specific rows.
* **Delete (DELETE):** Removes records from a table using the DELETE FROM statement, typically combined with a WHERE clause to prevent deleting entire table contents.

Steps to Discover the Tool:
1. **Set the Active Database:** Make sure you are using the `tools_db` database by running:
`USE tools_db;`
2. **Search for the Tool:** Execute a query to find the tool in the `hacking_tools` table that mentions man-in-the-middle attacks, using:
```
SELECT name FROM hacking_tools WHERE description LIKE '%man-in-the-middle%';

SELECT DISTINCT category FROM hacking_tools WHERE name IN ('USB Rubber Ducky', 'Bash Bunny');
```

## Clauses
* Overview: Focuses on advanced SQL clauses (`DISTINCT`, `GROUP BY`, `ORDER BY`, and `HAVING`) used to refine, group, sort, and filter query results effectively.
* Key Clauses:
    * `DISTINCT`: Excludes duplicate rows from query results to return only unique values (e.g., `SELECT DISTINCT name FROM books;`).
    * `GROUP BY`: Aggregates data from multiple records and groups results by specific columns, commonly used alongside aggregate functions like `COUNT()`.
    * `ORDER BY`: Sorts the rows returned by a query in either ascending (`ASC`) or descending (`DESC`) order based on a specified column.
    * `HAVING`: Filters grouped results based on a condition after aggregation has taken place (unlike the `WHERE` clause, which filters before aggregation).

## Operators
* **Overview:** Focuses on using logical and comparison operators to filter, test, and manipulate data within database queries more precisely.
* **Logical Operators:**
    * `LIKE`: Filters records for specific patterns within text columns using wildcard characters (e.g., matching descriptions containing "guide").
    * `AND`: Combines multiple conditions and returns true only if all conditions are met.
    * `OR`: Combines conditions and returns true if at least one condition is met.
    * `NOT`: Reverses a boolean condition to exclude matching records.
    * `BETWEEN`: Tests whether a value falls within a specific numeric or date range.
* **Comparison Operators:**
    * `=` (**Equal To**): Checks for exact matches.
    * `!=` (**Not Equal To**): Excludes records matching a specific value or criteria.
    * `<` / `>` (**Less Than / Greater Than**): Compares numerical or date values.
    * `<=` / `>=` (**Less Than or Equal To / Greater Than or Equal To**): Evaluates boundaries inclusively.

Steps to Discover the Tool:
```
USE tools_db;
```

1. which tool falls under the **Multi-tool** category and is useful for **pentesters** and **geeks**?
```
SELECT name FROM hacking_tools WHERE category = 'Multi-tool' AND (description LIKE '%pentester%' OR description LIKE '%geek%');
```
2. what is the category of tools with an amount **greater than** or **equal** to **300**?
```
SELECT DISTINCT category FROM hacking_tools WHERE amount >= 300;
```
3. which tool falls under the Network intelligence category with an amount **less than** 100?
```
SELECT name FROM hacking_tools WHERE category = 'Network intelligence' AND amount < 100;
```

## Functions
* Overview: Explores built-in SQL functions used to manipulate data, streamline queries, and compute summary metrics across records.
* String Functions:
    * CONCAT(): Combines two or more text strings or columns together.
    * GROUP_CONCAT(): Concatenates data from multiple rows into a single string, often grouped by a specific category.
    * SUBSTRING(): Extracts a specific portion of a string starting from a defined position with a set length.
    * LENGTH(): Returns the total character count of a string, including spaces and punctuation.
* Aggregate Functions:
    * COUNT(): Counts the total number of records or rows matching a given criteria.
    * SUM(): Calculates the total sum of all values within a numeric column.
    * MAX() / MIN(): Identifies the maximum (latest/highest) or minimum (earliest/lowest) value within a column.

1. Tool with the longest name based on character length: Retrieve from lab using `SELECT name FROM hacking_tools ORDER BY LENGTH(name) DESC LIMIT 1;`

2. Total sum of all tools: Retrieve from lab using `SELECT SUM(amount) FROM hacking_tools;`

3. Tool names where the amount does not end in 0, grouped and concatenated by " & ": Retrieve from lab using `SELECT GROUP_CONCAT(name SEPARATOR ' & ') FROM hacking_tools WHERE amount % 10 != 0;`