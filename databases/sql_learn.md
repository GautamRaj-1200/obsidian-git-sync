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

### Data Types
- The data type of a column defines what value the column can hold: integer, character, money, date and time, binary, and so on.
- Each column in a database table is required to have a name and a data type.

### MySQL Data Types

### String Data Types

| Data Type    | Description                                                                                                                                      |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| CHAR(size)   | A FIXED length string (can contain letters, numbers, and special characters). The size parameter specifies the column length in characters (0 to 255). Default is 1. |
| VARCHAR(size)| A VARIABLE length string (can contain letters, numbers, and special characters). The size parameter specifies the maximum string length in characters (0 to 65535). |
| BINARY(size) | Equal to CHAR(), but stores binary byte strings. The size parameter specifies the column length in bytes. Default is 1.                         |
| VARBINARY(size) | Equal to VARCHAR(), but stores binary byte strings. The size parameter specifies the maximum column length in bytes.                          |
| TINYBLOB     | For BLOBs (Binary Large Objects). Max length: 255 bytes                                                                                          |
| TINYTEXT     | Holds a string with a maximum length of 255 characters                                                                                           |
| TEXT(size)   | Holds a string with a maximum length of 65,535 bytes                                                                                             |
| BLOB(size)   | For BLOBs (Binary Large Objects). Holds up to 65,535 bytes of data                                                                              |
| MEDIUMTEXT   | Holds a string with a maximum length of 16,777,215 characters                                                                                   |
| MEDIUMBLOB   | For BLOBs (Binary Large Objects). Holds up to 16,777,215 bytes of data                                                                          |
| LONGTEXT     | Holds a string with a maximum length of 4,294,967,295 characters                                                                                |
| LONGBLOB     | For BLOBs (Binary Large Objects). Holds up to 4,294,967,295 bytes of data                                                                      |
| ENUM(val1, val2, val3, ...) | A string object that can have only one value, chosen from a list of possible values. Up to 65535 values in the ENUM list. |
| SET(val1, val2, val3, ...) | A string object that can have 0 or more values, chosen from a list of possible values. Up to 64 values in the SET list. |

### Numeric Data Types

| Data Type         | Description                                                                                                           |
|-------------------|-----------------------------------------------------------------------------------------------------------------------|
| BIT(size)         | A bit-value type. The number of bits per value is specified in size. The size parameter can hold from 1 to 64 bits. Default is 1. |
| TINYINT(size)     | A very small integer. Signed range: -128 to 127, Unsigned range: 0 to 255. The size parameter specifies the display width (255). |
| BOOL              | Zero is false, nonzero is true.                                                                                         |
| BOOLEAN           | Equivalent to BOOL.                                                                                                    |
| SMALLINT(size)    | A small integer. Signed range: -32768 to 32767, Unsigned range: 0 to 65535. The size parameter specifies the display width (255). |
| MEDIUMINT(size)   | A medium integer. Signed range: -8388608 to 8388607, Unsigned range: 0 to 16777215. The size parameter specifies the display width (255). |
| INT(size)         | A medium integer. Signed range: -2147483648 to 2147483647, Unsigned range: 0 to 4294967295. The size parameter specifies the display width (255). |
| INTEGER(size)     | Equivalent to INT(size).                                                                                              |
| BIGINT(size)      | A large integer. Signed range: -9223372036854775808 to 9223372036854775807, Unsigned range: 0 to 18446744073709551615. The size parameter specifies the display width (255). |
| FLOAT(size, d)    | A floating point number. The total number of digits is specified in size, and the number of digits after the decimal is specified in d. Deprecated in MySQL 8.0.17. |
| FLOAT(p)          | A floating point number. MySQL uses the p value to decide whether to use FLOAT or DOUBLE. If p is from 0 to 24, FLOAT is used. If p is from 25 to 53, DOUBLE is used. |
| DOUBLE(size, d)   | A normal-size floating point number. The total number of digits is specified in size, and the number of digits after the decimal is specified in d. |
| DOUBLE PRECISION  | Equivalent to DOUBLE.                                                                                                 |
| DECIMAL(size, d)  | An exact fixed-point number. The total number of digits is specified in size, and the number of digits after the decimal is specified in d. The maximum size is 65, and the maximum d is 30. |
| DEC(size, d)      | Equivalent to DECIMAL(size, d).                                                                                        |

**Note:** All the numeric data types may have the extra options `UNSIGNED` (disallows negative values) or `ZEROFILL` (automatically adds the UNSIGNED attribute and pads the column with zeroes).

### Date and Time Data Types

| Data Type       | Description                                                                                                                                          |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| DATE            | A date. Format: YYYY-MM-DD. Range: '1000-01-01' to '9999-12-31'.                                                                                  |
| DATETIME(fsp)   | A date and time combination. Format: YYYY-MM-DD hh:mm:ss. Range: '1000-01-01 00:00:00' to '9999-12-31 23:59:59'. Can use DEFAULT and ON UPDATE for auto-updating. |
| TIMESTAMP(fsp)  | A timestamp. Stored as seconds since the Unix epoch ('1970-01-01 00:00:00' UTC). Format: YYYY-MM-DD hh:mm:ss. Range: '1970-01-01 00:00:01' UTC to '2038-01-09 03:14:07' UTC. Can use DEFAULT CURRENT_TIMESTAMP and ON UPDATE CURRENT_TIMESTAMP. |
| TIME(fsp)       | A time. Format: hh:mm:ss. Range: '-838:59:59' to '838:59:59'.                                                                                      |
| YEAR            | A year in four-digit format. Allowed values: 1901 to 2155, and 0000. MySQL 8.0 does not support two-digit year format.                                 |
