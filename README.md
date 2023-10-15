# Oracle SQL Schools Database
Oracle SQL project on a "Schools" database schema consisting of eight tables.  
> Q1. Create queries that can be used on all eight tables to find a record count.
<details><summary>Click here for SQL code</summary>  
    
```sql
/*
Eight queries that return one row and one column 
showing record count from each table.
*/

SELECT
    COUNT(*) AS record_count
FROM classroom_students;
```
RECORD_COUNT  
440
```sql
SELECT
    COUNT(*) AS record_count
FROM classrooms;
```
RECORD_COUNT  
30
```sql
SELECT
    COUNT(*) AS record_count
FROM people;
```
RECORD_COUNT  
90
```
SELECT
    COUNT(*) AS record_count
FROM principals;
```
RECORD_COUNT  
3
```sql
SELECT
    COUNT(*) AS record_count
FROM schools;
```
RECORD_COUNT  
3
```sql
SELECT
    COUNT(*) AS record_count
FROM students;
```
RECORD_COUNT  
72
```sql
SELECT
    COUNT(*) AS record_count
FROM subjects;
```
RECORD_COUNT  
5
```sql
SELECT
    COUNT(*) AS record_count
FROM teachers;
```
RECORD_COUNT  
15  
</details>  

> Q2. Create a query to output the names and record counts of four different tables.
<details><summary>Click here for SQL code</summary>  
    
```sql
-- Query outputting table names and record count for four tables in database
SELECT 
    'people' AS table_name,
    COUNT(*) AS num_records
FROM people
UNION
SELECT
    'principals' AS table_name,
    COUNT(*) AS num_records
FROM principals
UNION
SELECT
    'students' AS table_name,
    COUNT(*) AS num_records
FROM students
UNION
SELECT
    'teachers' AS table_name,
    COUNT(*) AS num_records
FROM teachers;
```
| TABLE_NAME | NUM_RECORDS |
|------------|-------------|
| people     | 90          |
| principals | 3           |
| students   | 72          |
| teachers   | 15          |
</details> 
