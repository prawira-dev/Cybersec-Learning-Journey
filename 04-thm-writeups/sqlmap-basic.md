# SQLMap: The Basics
## Intro
* **Overview:** Introduces core database concepts, explaining how web applications store, modify, and retrieve data by interacting with Database Management Systems (DBMS) like MySQL, PostgreSQL, SQLite, or Microsoft SQL Server.
* **Database Interactions:** Explains how user inputs (such as login credentials or search fields) prompt web applications to send SQL queries to backend databases for authentication and data retrieval.
* **Structured Query Language (SQL):** Highlights that SQL is the fundamental language used by applications to communicate with and query relational databases.
* **Room Learning Objectives:** Sets the stage for learning about SQL injection vulnerabilities and mastering automated exploitation using the SQLMap tool through a hands-on practical challenge.

## SQL Injection Vulnerability
* **Overview:** Explores how SQL injection (SQLi) vulnerabilities occur when user input is improperly sanitized and directly concatenated into SQL queries executed by the backend database.
* **How Login Authentication Works Normally:**
    * A typical login query checks both username and password using the boolean AND operator:
    * `SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';`
    * For the login to succeed, both conditions must match.
* **Exploiting SQL Injection:**
    * If the application fails to sanitize input, an attacker can manipulate the password field (e.g., entering `abc' OR 1=1;-- -`) to alter the query logic.
    * The resulting query becomes:
    * `SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1 = 1; -- -'`
    * Because the `OR` operator is used alongside a statement that is always true (`1=1`), and the `-- -` comments out the rest of the query, the database validates the statement as true and logs the attacker into the account without needing the correct password.

## Automated SQL Injection Tool
* **Overview:** Explores SQLMap as an automated command-line tool for detecting and exploiting SQL injection (SQLi) vulnerabilities in web applications.
* **Key Features & Modes:**
    * `--help`: Lists all available flags and options.
    * `--wizard`: Guides beginners through an interactive, step-by-step scan prompt.
    * `-u`: Specifies the target URL for HTTP GET-based testing (e.g., examining parameters like `cat=1`).
    * `--cookie`: Includes session tokens or authentication cookies to test authenticated endpoints.
    * `-r`: Takes an intercepted HTTP request text file to perform POST-based testing (such as on login or registration forms).
* **Enumeration & Exploitation Flags:**
    * `--dbs`: Extracts all available database names.
    * `-D database_name --tables`: Enumerates the table names inside a specific database.
    * `-D database_name -T table_name --dump`: Dumps all records and entries from a specific table.

## Practical Exercise
* **Overview:** Provides a hands-on practical challenge to exploit an intentional SQL injection vulnerability on a vulnerable login form using SQLMap.
* **Target Endpoint:** The application uses a GET-based login endpoint parameterized as `http://MACHINE_IP/ai/includes/user_login?email=test&password=test`.
* **Key Command Parameters:**
    * Enclosing the target URL in single quotes (`'http://...'`) is required in the terminal to avoid errors caused by special characters like `?`.
    * Adding `--level=5` ensures an in-depth scan is performed to successfully uncover the vulnerability.
* **Practical Objectives:**
    * Discover available databases using the `--dbs` flag.
    * Enumerate table names within the target database (ai) using `-D ai --tables`.
    * Dump records from the user table to retrieve the target password associated with test@chatai.com.

## Step by step
1. How many databases are available in this web application?
```bash
sqlmap -u 'http://IP_TARGET/ai/includes/user_login?email=test&password=test' --dbs --level=5
```
2. What is the name of the table available in the “ai” database?
```bash
sqlmap -u ‘http://IP_TARGET/ai/includes/user_login?email=test&password=test' -D ai --tables --level=5
```
3. What is the password for user test@chatai.com?
```bash
sqlmap -u ‘http://IP_TARGET/ai/includes/user_login?email=test&password=test' -D ai -T user --dump
```