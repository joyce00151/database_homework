# Homework 4
## 题目一
请问下面的SQL语句是否合法？用实验验证你的想法。你从实验结果能得到什么结论？
```sql
SELECT dept_name, min(salary)
FROM instructor;

SELECT dept_name, min(salary)
FROM instructor
GROUP BY dept_name
HAVING name LIKE '%at%';

SELECT dept_name
FROM instructor
WHERE AVG(salary) > 20000;
```
### 解答：

```txt
解答内容
```
## 题目二
1.找到工资最高员工的名字，假设工资最高的员工只有一位（至少两种写法）。
### 解答：
```txt
内容
```
2.找到工资最高员工的名字，假设工资最高的员工有多位（试试多种写法）。
### 解答：
```sql
内容
```
3.解释下面四句。
```sql
SELECT 1 IN (1);

SELECT 1 = (1);

SELECT (1, 2) = (1, 2);

SELECT (1) IN (1, 2);
```
### 解答：
