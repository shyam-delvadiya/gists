# Problem Name: Consecutive Numbers
Link: https://leetcode.com/problems/consecutive-numbers

## Question

Table: `Logs`
```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| num         | varchar |
+-------------+---------+
In SQL, id is the primary key for this table.
id is an autoincrement column starting from 1.
```

Find all numbers that appear at least three times consecutively.

Return the result table in any order.

The result format is in the following example.

### Example 1:
```
Input: 
Logs table:
+----+-----+
| id | num |
+----+-----+
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |
+----+-----+
Output: 
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+
Explanation: 1 is the only number that appears consecutively for at least three times.
```

## Answer


```sql
SELECT DISTINCT l1.num AS ConsecutiveNums
FROM Logs l1
JOIN Logs l2 ON l1.id = l2.id + 1
JOIN Logs l3 ON l2.id = l3.id + 1
WHERE l1.num = l2.num
  AND l2.num = l3.num;
```

- I compare each row with the previous two rows using `LAG()`.

- If the same number appears in all three rows, it means it is consecutive.

- I return those numbers using `DISTINCT` to avoid duplicates.