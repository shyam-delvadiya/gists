# Problem Name: Second Highest Salary
Link: https://leetcode.com/problems/second-highest-salary

## Question

Table: `Employee`
```
+-------------+------+
| Column Name | Type |
+-------------+------+
| id          | int  |
| salary      | int  |
+-------------+------+
id is the primary key (column with unique values) for this table.
Each row of this table contains information about the salary of an employee.
```

Write a solution to find the second highest distinct salary from the `Employee` table. If there is no second highest salary, return `null (return None in Pandas)`.

The result format is in the following example.

### Example 1:
```
Input: 
Employee table:
+----+--------+
| id | salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
Output: 
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
```

Example 2:
```
Input: 
Employee table:
+----+--------+
| id | salary |
+----+--------+
| 1  | 100    |
+----+--------+
Output: 
+---------------------+
| SecondHighestSalary |
+---------------------+
| null                |
+---------------------+
```

## Answer

```sql
SELECT MAX(salary) AS SecondHighestSalary
FROM (
    SELECT salary,
           DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM Employee
) t
WHERE rnk = 2;
```

Previously, I tried to solve this problem using `RANK()`, but then I remembered that `RANK()` skips rank values when duplicate values exist.

For example, if two employees have the same highest salary, the next salary will get rank `3` instead of `2`.
 
Because of this behavior, I decided to use `DENSE_RANK()`, which does not skip rank numbers and correctly assigns the second distinct salary a rank of `2`.

But, one more edge case remained:
if a second-highest salary does not exist, the query would return no rows.
To handle this scenario and return `NULL` as required, I wrapped the result with `MAX()`, since `MAX()` over an empty result set naturally returns `NULL`.