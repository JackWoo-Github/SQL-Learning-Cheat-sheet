# SQL-Learning-Cheat-sheet

## 1. Databases and Tables

**Create a Database:**
```sql
CREATE DATABASE database_name;
```

**Drop the Database:**
```sql
DROP DATABASE IF EXISTS database_name;
```

**Use the Database:**
```sql
USE database_name;
```

**Create a Table:**
```sql
CREATE TABLE table_name(
  column1_name data_type constraints,
  column2_name data_type constraints,
  ...);
```

**NOTES: Common Constraints**
<br/>NOT NULL: The value must be specified when adding a new row, could be followed with DEFAULT 'default_value'
<br/>UNIQUE: The same value cannot appear else where in the column
<br/>PRIMARY KEY: If unspecified will increase the primary key from the previous by 1
<br/>PRIMARY KEY AUTO_INCREMENT: A unique value specific to a row, made to reference the data frame faster

**Drop the Table**
```sql
DROP TABLE IF EXISTS table_name;
```

## 2. Inserting Records

**Insert Multiple Rows**
```sql
INSERT INTO table_name
            (column1_name,column2_name)
VALUES      (value1, value2),
            (value3, value4),
            (value5, value6)
            ...;
```

## 3. Queries

**SELECT**<br/>
Select all columns
```sql
SELECT * FROM table_name;
```
Select specific columns;
```sql
SELECT column1_name, column2_name, column3_name
FROM table_name;
```

**WHERE**
```sql
SELECT column_list 
FROM table_name
WHERE condition;
```

**AND/OR**
```sql
SELECT column_list 
FROM table_name
WHERE condition1 AND condition2;
```

**IN**



**ORDER BY**



**LIMIT**



**DISTINCT**



**NOTES:** DISTINCT does not ignore NULL
