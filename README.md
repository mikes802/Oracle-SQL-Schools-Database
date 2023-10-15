# Oracle SQL Schools Database
Oracle SQL project on a "Schools" database schema consisting of eight tables.  

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
