## MySQL Data Types

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
