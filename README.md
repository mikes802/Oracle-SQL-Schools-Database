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

> Q7. Write a query to obtain the birth date of the oldest student.
<details><summary>Click here for SQL code</summary>
    
```sql
-- Birth date of the oldest student.
SELECT
    MIN(p.birth_date) AS birth_date
FROM people p
INNER JOIN students s
ON p.person_id = s.person_id;
```
| BIRTH_DATE |
|------------|
| 23-SEP-05  |
</details>

> Q8. Write a query to obtain the name, address, and birth date of the oldest student.
<details><summary>Click here for SQL code</summary>
    
```sql
-- Info for oldest student in standalone query.
SELECT
    p.first_name,
    p.last_name,
    p.city,
    p.region AS state,
    p.birth_date AS birth_date
FROM people p
INNER JOIN students s
ON p.person_id = s.person_id
ORDER BY birth_date
FETCH FIRST 1 ROW ONLY;
```
| FIRST_NAME | LAST_NAME | CITY         | STATE | BIRTH_DATE |
|------------|-----------|--------------|-------|------------|
| James      | Smith     | New Hartford | NY    | 23-SEP-05  |
</details>

> Q9. Write a query that returns everyone's full name, role at school, salary (N/A for students), and school name.
<details><summary>Click here for SQL code</summary>
    
```sql
-- Return person's name, role, salary, and school name.
SELECT
    p.first_name || ' ' || p.last_name AS full_name,
    CASE
        WHEN t.teacher_id IS NOT NULL THEN 'teacher'
        WHEN pr.principal_id IS NOT NULL THEN 'principal'
        ELSE 'student' 
    END AS role,
    COALESCE(TO_CHAR(t.salary), TO_CHAR(pr.salary), 'N/A') AS salary,
    s.school_name
FROM people p
FULL OUTER JOIN principals pr
ON p.person_id = pr.person_id
FULL OUTER JOIN teachers t
ON p.person_id = t.person_id
INNER JOIN schools s
ON p.school_id = s.school_id;
```
90 rows returned. Only first and last five shown here:
| FULL_NAME         | ROLE      | SALARY | SCHOOL_NAME            |
|-------------------|-----------|--------|------------------------|
| Jessica Martin    | principal | 77237  | Clinton Central School |
| Virginia Gonzales | student   | N/A    | Clinton Central School |
| Sarah Garcia      | teacher   | 53175  | Clinton Central School |
| Daniel Lewis      | teacher   | 33885  | Clinton Central School |
| Lisa Hall         | teacher   | 48084  | Clinton Central School |
...
| Juan Rivera    | student | N/A   | Fayetteville-Manlius School |
| Wayne Davis    | student | N/A   | Fayetteville-Manlius School |
| Louis Bell     | student | N/A   | Fayetteville-Manlius School |
| Diana Williams | student | N/A   | Fayetteville-Manlius School |
| Dennis Russell | teacher | 39913 | Fayetteville-Manlius School |
</details>

> Q10. Write a query that returns all classroom ID's and teachers, ordering by school name, year, semester, and then subject.
<details><summary>Click here for SQL code</summary>
    
```sql
-- Output classroom information and order by four columns.
SELECT
    c.classroom_id,
    p.first_name || ' ' || p.last_name AS teacher_name,
    c.semester,
    c.year,
    sub.subject,
    sch.school_name
FROM classrooms c
INNER JOIN teachers t
ON c.teacher_id = t.teacher_id 
INNER JOIN people p 
ON t.person_id = p.person_id
INNER JOIN subjects sub
ON c.subject_id = sub.subject_id
INNER JOIN schools sch
ON p.school_id = sch.school_id
ORDER BY
    school_name,
    year,
    semester,
    subject;
```
| CLASSROOM_ID | TEACHER_NAME     | SEMESTER | YEAR | SUBJECT | SCHOOL_NAME                 |
|--------------|------------------|----------|------|---------|-----------------------------|
| 7            | Lisa Hall        | fall     | 2020 | English | Clinton Central School      |
| 5            | Daniel Lewis     | fall     | 2020 | French  | Clinton Central School      |
| 3            | Sarah Garcia     | fall     | 2020 | History | Clinton Central School      |
| 1            | Thomas Thompson  | fall     | 2020 | Math    | Clinton Central School      |
| 9            | Paul Hill        | fall     | 2020 | Science | Clinton Central School      |
| 8            | Lisa Hall        | spring   | 2021 | English | Clinton Central School      |
| 6            | Daniel Lewis     | spring   | 2021 | French  | Clinton Central School      |
| 4            | Sarah Garcia     | spring   | 2021 | History | Clinton Central School      |
| 2            | Thomas Thompson  | spring   | 2021 | Math    | Clinton Central School      |
| 10           | Paul Hill        | spring   | 2021 | Science | Clinton Central School      |
| 27           | Roger Long       | fall     | 2020 | English | Fayetteville-Manlius School |
| 25           | Martha Thomas    | fall     | 2020 | French  | Fayetteville-Manlius School |
| 23           | Kelly Thomas     | fall     | 2020 | History | Fayetteville-Manlius School |
| 21           | Dennis Russell   | fall     | 2020 | Math    | Fayetteville-Manlius School |
| 29           | Megan Gray       | fall     | 2020 | Science | Fayetteville-Manlius School |
| 28           | Roger Long       | spring   | 2021 | English | Fayetteville-Manlius School |
| 26           | Martha Thomas    | spring   | 2021 | French  | Fayetteville-Manlius School |
| 24           | Kelly Thomas     | spring   | 2021 | History | Fayetteville-Manlius School |
| 22           | Dennis Russell   | spring   | 2021 | Math    | Fayetteville-Manlius School |
| 30           | Megan Gray       | spring   | 2021 | Science | Fayetteville-Manlius School |
| 17           | Hannah Davis     | fall     | 2020 | English | New Hartford Central School |
| 15           | Nathan Carter    | fall     | 2020 | French  | New Hartford Central School |
| 13           | Adam Thomas      | fall     | 2020 | History | New Hartford Central School |
| 11           | Douglas Martinez | fall     | 2020 | Math    | New Hartford Central School |
| 19           | Jacqueline Cook  | fall     | 2020 | Science | New Hartford Central School |
| 18           | Hannah Davis     | spring   | 2021 | English | New Hartford Central School |
| 16           | Nathan Carter    | spring   | 2021 | French  | New Hartford Central School |
| 14           | Adam Thomas      | spring   | 2021 | History | New Hartford Central School |
| 12           | Douglas Martinez | spring   | 2021 | Math    | New Hartford Central School |
| 20           | Jacqueline Cook  | spring   | 2021 | Science | New Hartford Central School |
</details>

> Q11. Make a view called `classroom_students_view` from a given query. (Query was provided.)
<details><summary>Click here for SQL code</summary>
    
```sql
-- Create a view.
CREATE VIEW classroom_students_view AS
SELECT ps.first_name || ' ' || ps.last_name AS student, cs.grade,
      pt.first_name || ' ' || pt.last_name AS teacher,
      s.subject, c.semester, c.year
FROM people ps
  JOIN students s ON ps.person_id = s.person_id
  JOIN classroom_students cs ON s.student_id = cs.student_id
  JOIN classrooms c ON c.classroom_id = cs.classroom_id
  JOIN subjects s ON s.subject_id = c.subject_id
  JOIN teachers t ON t.teacher_id = c.teacher_id
  JOIN people pt ON pt.person_id = t.person_id;
```
