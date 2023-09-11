#SQL 
For get Databases
```sql
SHOW DATABASES;
```
For create new database
```sql
CREATE DATABASE <database name>
```
To select a database for workin
```sql
USE <database name>
```
How to create table
```
CREATE TABLE <table name>(<table content>);
```

Data types

| Data      | Description                                |
| --------- | ------------------------------------------ |
| INT       | Big int range, unsigned available          |
| TINYINT   | 1 byte length, unsigned availability       |
| BIGINT    | Bigger than INT, unsigned availabilty      |
| SMALLINT  | 2 byte lenght, unsigned availability       |
| MEDIUMINT | 3 byte length, unsigned availability       |
| BIGINT    | 8 byte lenght, unsigned available          |
| FLOAT     | Decimal innacurate type                    |
| DOUBLE    | Larger than float, keeps innacuracy        |
| DECIMAL   | FLOAT accuracy fixed (expends more memory) |
| VARCHAR   | 255 string char lenght                     |
| CHAR      | String with fixed length                   |
| TEXT      | Large strings                              |
| ENUM      | Lists                                      |
| BLOB      | Files, RAW byte format                     |
| DATE      | AAAA-MM-DD                                 |
| TIME      | hh:mm:ss                                   |
| DATETIME  | AAAA-MM-DD hh:mm:ss                        |
| YEAR      | AAAA                                       |
Reading from table
```sql

```
Insert in table
```sql
INSERT INTO <table name> ([<column name>...]) VALUES ([<values>]);
```
Updating in table
```sql
UPDATE <table name> SET [<column key>=<value>] WHERE [<match rule>];
```
Deleting in table
```sql
DELETE FROM <table name> WHERE [<match rule>]
```
Modifying table
```sql
ALTER TABLE <table name> <ADD | CHANGE | DROP COLUMN> <key1> <key2?> <data type?> <table rules?>
```
Erasing table
```sql
DROP TABLE <table name>
```