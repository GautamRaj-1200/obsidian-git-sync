## Introduction
- SQL is a standard language for storing, manipulating and retrieving data in databases.
- SQL stands for Structured Query Language.
- Although SQL is an ANSI/ISO standard, there are different versions of the SQL language.
- However, to be compliant with the ANSI standard, they all support at least the major commands (such as `SELECT`, `UPDATE`, `DELETE`, `INSERT`, `WHERE`) in a similar manner.

## RDBMS
- RDBMS stands for Relational Database Management System.
- RDBMS is the basis for SQL, and for all modern database systems such as MS SQL Server, IBM DB2, Oracle, MySQL, and Microsoft Access.
- *The data in RDBMS is stored in database objects called* **tables**. 
	- A **table** is a collection of related data entries and it consists of columns and rows.
	- Every table is broken up into smaller entities called **fields**.
		- A **field** is a column in a table that is designed to maintain specific information about every record in the table.
	- A **record**, also called a row, is each individual entry that exists in a table. It is a horizontal entity in a table.
	- A **column** is a vertical entity in a table that contains all information associated with a specific field in a table.

## SQL Statements
- Most of the actions we need to perform on a database are done with SQL statements.
- SQL statements consist of keywords that are easy to understand.
- The following SQL statement returns all records from a table named "Customers":
```sql
SELECT * FROM Customers;
```
- SQL keywords are NOT case sensitive: `select` is the same as `SELECT`
- **Semicolon after SQL Statements?**
	- Some database systems require a semicolon at the end of each SQL statement.
	- Semicolon is the standard way to separate each SQL statement in database systems that allow more than one SQL statement to be executed in the same call to the server.
## Some of The Most Important SQL Commands
- `SELECT` - extracts data from a database
- `UPDATE` - updates data in a database
- `DELETE` - deletes data from a database
- `INSERT INTO` - inserts new data into a database
- `CREATE DATABASE` - creates a new database
- `ALTER DATABASE` - modifies a database
- `CREATE TABLE` - creates a new table
- `ALTER TABLE` - modifies a table
- `DROP TABLE` - deletes a table
- `CREATE INDEX` - creates an index (search key)
- `DROP INDEX` - deletes an index

### Create Database
- The `CREATE DATABASE` statement is used to create a new SQL database.
- SYNTAX:
```sql
CREATE DATABASE databasename;
```
- EXAMPLE:
```sql
CREATE DATABASE testdb;
```

### Show Databases
- To show all the databases
```sql
SHOW DATABASES
```

### Drop Database
- The `DROP DATABASE` statement is used to drop an existing SQL database.
- SYNTAX:
```sql
DROP DATABASE databasename;
```
- EXAMPLE:
```sql
DROP DATABASE testdb;
```

### Use Database
- Let's first create a database: 
```sql
CREATE DATABASE record_company;
```
-  The use command is used when there are multiple databases in the SQL and the user or programmer specifically wants to use a particular database.
- SYNTAX:
```sql
USE database_name;
```
- EXAMPLE:
```sql
USE record_company
```

### Create Table
- The `CREATE TABLE` statement is used to create a new table in a database.
- SYNTAX:
```sql
CREATE TABLE _table_name_ (  
    column1 datatype,  
    column2 datatype,  
    column3 datatype,  
   ....  
);
```
- The column parameters specify the names of the columns of the table.
- The datatype parameter specifies the type of data the column can hold (e.g. varchar, integer, date, etc.).
- EXAMPLE
```sql
CREATE TABLE Persons (  
    PersonID int,  
    LastName varchar(255),  
    FirstName varchar(255),  
    Address varchar(255),  
    City varchar(255)  
);
```
- The PersonID column is of type int and will hold an integer.
- The LastName, FirstName, Address, and City columns are of type varchar and will hold characters, and the maximum length for these fields is 255 characters.
### Data Types
- The data type of a column defines what value the column can hold: integer, character, money, date and time, binary, and so on.
- Each column in a database table is required to have a name and a data type.
### Drop Table
- The `DROP TABLE` statement is used to drop an existing table in a database.
- SYNTAX:
```sql
DROP TABLE table_name;
```
- EXAMPLE:
```sql
DROP TABLE Persons
```