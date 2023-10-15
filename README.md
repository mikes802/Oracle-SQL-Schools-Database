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

> Q3. Create a query to output the names of all teachers ordered by last name and then by first name.
<details><summary>Click here for SQL code</summary>

```sql
-- Output names of teachers ordered by last name and then by first name.  
SELECT
    p.first_name,
    p.last_name
FROM teachers t
LEFT JOIN people p
ON t.person_id = p.person_id
ORDER BY p.last_name, p.first_name;
```
| FIRST_NAME | LAST_NAME |
|------------|-----------|
| Nathan     | Carter    |
| Jacqueline | Cook      |
| Hannah     | Davis     |
| Sarah      | Garcia    |
| Megan      | Gray      |
| Lisa       | Hall      |
| Paul       | Hill      |
| Daniel     | Lewis     |
| Roger      | Long      |
| Douglas    | Martinez  |
| Dennis     | Russell   |
| Adam       | Thomas    |
| Kelly      | Thomas    |
| Martha     | Thomas    |
| Thomas     | Thompson  |
</details> 

> Q4. Create a query to output the number of people associated with each school sorted in descending order.
<details><summary>Click here for SQL code</summary>
    
```sql
-- Number of people associated with each school, sort descending order.
SELECT
    s.school_name,
    COUNT(p.school_id) AS num_people
FROM people p
INNER JOIN schools s
ON p.school_id = s.school_id
GROUP BY s.school_name
ORDER BY num_people DESC;
```
| SCHOOL_NAME                 | NUM_PEOPLE |
|-----------------------------|------------|
| Clinton Central School      | 41         |
| New Hartford Central School | 31         |
| Fayetteville-Manlius School | 18         |
</details>

> Q5. Create a query to output the number of students associated with each school sorted in descending order.
<details><summary>Click here for SQL code</summary>
    
```sql
-- Number of students associated with each school, sort descending order.
SELECT
    sc.school_name,
    COUNT(st.student_id) AS num_students
FROM students st
LEFT JOIN people p
ON st.person_id = p.person_id
INNER JOIN schools sc
ON p.school_id = sc.school_id
GROUP BY sc.school_name
ORDER BY num_students DESC;
```
| SCHOOL_NAME                 | NUM_STUDENTS |
|-----------------------------|--------------|
| Clinton Central School      | 35           |
| New Hartford Central School | 25           |
| Fayetteville-Manlius School | 12           |
</details>

> Q6. Create a query to output the full name of the people who live in Clinton with "Washington" in the address.
<details><summary>Click here for SQL code</summary>
    
```sql
-- Output people in city of Clinton with "Washington" in address.
SELECT 
    first_name || ' ' || last_name AS full_name,
    address,
    city
FROM people
WHERE city = 'Clinton'
  AND address LIKE '%Washington%';
```
| FULL_NAME    | ADDRESS               | CITY    |
|--------------|-----------------------|---------|
| Paul Hill    | 1775 Washington St    | Clinton |
| Steven Green | 280 Washington Street | Clinton |
</details>
