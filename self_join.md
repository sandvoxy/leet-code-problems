## Self-Joins ##

### [181. Employees Earning More Than Their Managers](https://leetcode.com/problems/employees-earning-more-than-their-managers/) ###

Table: Products

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| salary      | int     |
| managerId   | int     |

id is the primary key (column with unique values) for this table.
Each row of this table indicates the ID of an employee, their name, salary, and the ID of their manager.
 
Write a solution to find the employees who earn more than their managers.

Return the result table in any order.

**Solution:**
```sql
SELECT
    A.name AS Employee
FROM employee AS A
INNER JOIN employee AS B
ON A.Managerid = B.id
WHERE A.Salary > B.Salary;
```
