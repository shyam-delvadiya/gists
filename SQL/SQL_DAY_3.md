# Problem Name: Nth Highest Salary
Link: https://leetcode.com/problems/nth-highest-salary

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

Write a solution to find the `nth` highest distinct salary from the `Employee` table. If there are less than `n` distinct salaries, return `null`.

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
n = 2
Output: 
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```

### Example 2:

```
Input: 
Employee table:
+----+--------+
| id | salary |
+----+--------+
| 1  | 100    |
+----+--------+
n = 2
Output: 
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| null                   |
+------------------------+
```

## Answer

```sql
CREATE OR REPLACE FUNCTION NthHighestSalary(N INT) RETURNS TABLE (Salary INT) AS $$
BEGIN
  RETURN QUERY (
    SELECT MAX(t.salary)
    FROM (
        SELECT e.salary,
            DENSE_RANK() OVER (ORDER BY e.salary DESC) AS rnk
        FROM Employee AS e
    ) t
    WHERE rnk = N 
  );
END;
$$ LANGUAGE plpgsql;
```

Just like we used `DENSE_RANK()` in `DAY 2` Same way we can solve this problem just instread of `2nd rank` we use parameter `Nth rank`.