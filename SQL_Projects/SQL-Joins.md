SQL Joins Explained: INNER, LEFT, RIGHT & FULL OUTER JOIN

SQL Joins allow you to combine rows from two or more tables based on a related column. This is essential for working with relational databases.

-------------------------------------------------------
Sample Tables

Table A: employees

emp_id | name    | dept_id
-------|---------|---------
1      | Alice   | 10
2      | Bob     | 20
3      | Charlie | NULL
4      | David   | 30

Table B: departments

dept_id | dept_name
--------|-------------
10      | HR
20      | Engineering
40      | Marketing

-------------------------------------------------------
1. INNER JOIN

Returns records with matching values in both tables.

Syntax:
SELECT e.name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;

Output:
name   | dept_name
-------|------------
Alice  | HR
Bob    | Engineering

-------------------------------------------------------
2. LEFT JOIN

Returns all records from the left table, and matched records from the right table. If no match, NULL is returned.

Syntax:
SELECT e.name, d.dept_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id;

Output:
name     | dept_name
---------|------------
Alice    | HR
Bob      | Engineering
Charlie  | NULL
David    | NULL

-------------------------------------------------------
3. RIGHT JOIN

Returns all records from the right table, and matched records from the left table. If no match, NULL is returned.

Syntax:
SELECT e.name, d.dept_name
FROM employees e
RIGHT JOIN departments d
ON e.dept_id = d.dept_id;

Output:
name   | dept_name
-------|-------------
Alice  | HR
Bob    | Engineering
NULL   | Marketing

-------------------------------------------------------
4. FULL OUTER JOIN

Returns all records when there is a match in one of the tables. NULLs are filled in where no match exists.

Note: Not supported directly in MySQL.

Syntax (PostgreSQL / SQL Server):
SELECT e.name, d.dept_name
FROM employees e
FULL OUTER JOIN departments d
ON e.dept_id = d.dept_id;

Output:
name     | dept_name
---------|-------------
Alice    | HR
Bob      | Engineering
Charlie  | NULL
David    | NULL
NULL     | Marketing

-------------------------------------------------------
Summary:

- INNER JOIN: Only matched rows
- LEFT JOIN: All from left + matches
- RIGHT JOIN: All from right + matches
- FULL OUTER JOIN: Everything from both sides, NULLs where unmatched

-------------------------------------------------------
Author: Kalpana From Go1Digital.com

