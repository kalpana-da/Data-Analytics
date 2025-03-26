SQL Subqueries Explained: Practical Examples with Real Tables

A subquery (also called an inner query or nested query) is a query within another SQL query. It helps break complex problems into smaller parts.

-------------------------------------------------------
1. Use Case: Get Employees Earning Above Average Salary

Tables:

employees

emp_id | name    | salary | dept_id
-------|---------|--------|---------
1      | Alice   | 5000   | 10
2      | Bob     | 7000   | 20
3      | Charlie | 6000   | 10
4      | David   | 8000   | 30
5      | Eve     | 4000   | 20

departments

dept_id | dept_name
--------|------------
10      | HR
20      | Engineering
30      | Sales

-------------------------------------------------------
Subquery Example 1: Find employees earning more than the average salary.

Syntax:

SELECT name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);

Output:

name    | salary
--------|--------
Bob     | 7000
David   | 8000

Explanation:
- The subquery calculates the average salary.
- The main query fetches employees earning more than that value.

-------------------------------------------------------
2. Use Case: Find Departments with Employees

Subquery Example 2: List department names that have at least one employee.

Syntax:

SELECT dept_name
FROM departments
WHERE dept_id IN (
    SELECT DISTINCT dept_id
    FROM employees
    WHERE dept_id IS NOT NULL
);

Output:

dept_name
----------
HR
Engineering
Sales

-------------------------------------------------------
3. Use Case: Employees in Highest Paid Department

Step-by-step breakdown:
- First, find the department with the highest average salary.
- Then find employees in that department.

Subquery Example 3:

SELECT name, salary
FROM employees
WHERE dept_id = (
    SELECT dept_id
    FROM employees
    GROUP BY dept_id
    ORDER BY AVG(salary) DESC
    LIMIT 1
);

Output:

name    | salary
--------|--------
David   | 8000

-------------------------------------------------------
4. Use Case: Correlated Subquery – Employees earning above their department's average

Correlated subqueries run row-by-row using data from the outer query.

Syntax:

SELECT name, salary
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE dept_id = e.dept_id
);

Output:

name    | salary
--------|--------
Charlie | 6000
Bob     | 7000

Explanation:
- For each employee, the subquery checks if their salary is above their own department's average.

-------------------------------------------------------
Summary

Types of Subqueries:
1. Single-row subquery
2. Multi-row subquery (uses IN, ANY, ALL)
3. Correlated subquery
4. Subqueries in SELECT or FROM

Use Cases:
✔️ Filter by aggregate
✔️ Find related records
✔️ Compare across groups

-------------------------------------------------------
Author: kalpana @ www.Go1digital.com
