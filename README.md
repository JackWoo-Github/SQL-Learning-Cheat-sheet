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
***NOTES: Common Constraints**
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
```sql
SELECT column_list 
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

**ORDER BY**
```sql
SELECT column_list 
FROM table_name
ORDER BY column_name ASC|DESC;
```
***NOTES:**
<br/>ASC: Ascending in value
<br/>DESC: Descending in value

**LIMIT**
```sql
SELECT LIMIT number column_list 
FROM table_name;
```

**DISTINCT**
```sql
SELECT DISTINCT column_list 
FROM table_name;
```
***NOTES:** DISTINCT does not ignore NULL

## 4. Aggregation

**Group By Function**
<br/>Aggregate Functions: COUNT, MAX, MIN, SUM, AVG
```sql
SELECT column1_name,
       MAX(column2_name)
FROM table_name
GROUP BY column3_name;
```

**AS Operator**
```sql
SELECT column1_name,
       AVG(column2_name) AS `New_Name`
FROM table_name
GROUP BY column1_name
```

**Having Clause**
<br/> WHERE clause on Aggregated Data
```sql
SELECT column1_name,
       AVG(column2_name)
FROM table_name
GROUP BY column1_name
HAVING AVG(column2_name) > #;
```
**OVER & PARTITION Clause**
<br/>GROUP BY creates an entirely new summary table
<br/>Using OVER allows to reserve the original table, OVER is like an operator
<br/>PARTITION: The category grouped by
```sql
SELECT column1_name,
       RANK() OVER (PARTITION BY column2_name ORDER BY column3_name ASC|DESC) AS `New_Name`
FROM table_name;
```
***NOTES: Common Window Function**
- COUNT()
- SUM()
- ROW_NUMBER()
- RANK()
- DENSE_RANK()
- LEAD()
- LAG()

## 5. Joining

**Inner Join**

**Left Join**

**Right Join**

**Unions**
