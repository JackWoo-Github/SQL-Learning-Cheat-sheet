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

**OFFSET**
```sql
SELECT column_list 
FROM table_name
LIMIT [Number to limit by] OFFSET [Number of rows to skip];
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
***NOTES:**
<br/>Neither COUNT() nor DISTINCT() ignore Null
<br/>However, COUNT(DISTINCT column1_name, column2_name, column3_name) will skip Null
<br/>which means, if a Null exists in any of the three columns, the whole entry would not be counted.

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

## 5. Joining

**Inner Join / Join**
<br/>Preserve the rows where column values match in the both tables
```sql
SELECT column_list
FROM table1_name a
INNER JOIN table2_name b
ON a.column1_name = b.column2_name;
```

**Left Join**
<br/>Preserve everything from the left table and what matches from the right
```sql
SELECT column_list
FROM table1_name a
LEFT JOIN table2_name b
ON a.column1_name = b.column2_name;
```

**Left Join Except**
<br/>Only left Records that do not appear in the right table
```sql
SELECT column_list
FROM table1_name a
LEFT JOIN table2_name b
ON a.column1_name = b.column2_name
WHERE b.column2_name IS NULL;
```

**Right Join**
<br/>Preserve everything from the right table and what matches from the left
```sql
SELECT column_list
FROM table1_name a
RIGHT JOIN table2_name b
ON a.column1_name = b.column2_name;
```

**Right Join Except**
<br/>Only Right Records that do not appear in the left table
```sql
SELECT column_list
FROM table1_name a
RIGHT JOIN table2_name b
ON a.column1_name = b.column2_name
WHERE a.column1_name IS NULL;
```

**Cross Join**
<br/>Combine each row from the first table with each row from the second table, returning all possible combinations of all rows.
<br/>It has no ON clause.
```sql
SELECT column_list
FROM table1_name a
CROSS JOIN table2_name b;
```

**Unions**
<br/>Joins combine columns while Unions combine rows.
<br/>Tables must have same fields.
<br/>UNION: only keeps unique records
```sql
SELECT column_list
FROM table1_name
UNION
SELECT column_list
FROM table2_name;
```
UNION ALL: keeps all records, including duplicates
```sql
SELECT column_list
FROM table1_name
UNION ALL
SELECT column_list
FROM table2_name;
```

## 6. CASE Operator
```sql
SELECT column_list,
       CASE WHEN condition1 THEN 'result1'
            WHEN condition2 THEN 'result2'
       ELSE 'result3' END AS Column_name
FROM table1_name;
```

## 7. Subqueries
Can be seen inside these states
- SELECT statement
- WHERE statement
- Used in comparison <, >, =, IN, ANY, ALL
- Nested in INSERT, UPDATE, DELETE
```sql
SELECT column_list
FROM table1_name
WHERE column1_name NOT IN
      (SELECT column2_name
       FROM table2_name);
```

## 8. Common Table Expressions (CTEs)
Ability to call a subquery by a name
```sql
WITH CTE_name1 AS ( query1 ),
     CTE_name2 AS ( query2 )
SELECT *
FROM CTE_name2;
```

## 9. Window Functions

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

**ROWS/RANGE Clause**
<br/>Allows sliding window frame calculations
<br/>ROWS/RANGE BETWEEN lower_bound AND upper_bound
<br/>Both ROWS and RANGE specify the window frame in relation to the current row
<br/>The ROW clause does it by specifying a fixed number of rows that precede or follow the current row.
<br/>While the RANGE clause limits the rows logically; it specifies the range of values in relation to the value of the current row.

```sql
SELECT column1_name,
       SUM(column2_name) OVER (order by date_column ASC ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS `New_Name`
FROM table_name;
```

```sql
SELECT column1_name,
       SUM(column2_name) OVER (order by date_column ASC RANGE BETWEEN INTERVAL n DAY PRECEDING AND CURRENT ROW) AS `New_Name`
FROM table_name;
```

***NOTES: The bounds can be any of these options**
- UNBOUNDED PRECEDING
- n PRECEDING
- BETWEEN INTERVAL n DAY PRECEDING (Used only in RANGE clause)
- CURRENT ROW
- n FOLLOWING
- UNBOUNDED FOLLOWING


## 10. String Function & Regular Expression





