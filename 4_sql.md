# Homework 4
## 题目一
* 请问下面的SQL语句是否合法？用实验验证你的想法。你从实验结果能得到什么结论？
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
![error1](1images/4/error1.png)
```txt
不合法。使用聚合函数（min）时，非聚合列（dept_name）必须出现在GROUP BY子句中。
因为聚合函数会对整个表返回单一值，而非聚合列需要明确制定分组依据。
```
![error2](1images/4/error2.png)
```txt
不合法。HAVING 子句引用了未分组的列 name，语法上不正确。
通常，HAVING 中引用的列要么是聚合结果，要么是 GROUP BY 中的列。
```
![error3](1images/4/error3.png)
```txt
不合法。WHERE 子句不能直接使用聚合函数（AVG）。
聚合函数需要在 GROUP BY 和 HAVING 的上下文中使用。
```
合法版本：
```sql
SELECT dept_name, min(salary)
FROM instructor
GROUP BY dept_name;

SELECT dept_name, min(salary)
FROM instructor
WHERE name LIKE '%at%'
GROUP BY dept_name;

SELECT dept_name
FROM instructor
GROUP BY dept_name
HAVING AVG(salary) > 20000;
```
## 题目二
* 1.找到工资最高员工的名字，假设工资最高的员工只有一位（至少两种写法）。
### 解答：
instructor(ID, name, dept_name, salary)
* 方法一：使用子查询和WHERE
```sql
SELECT name
FROM instructor
WHERE salary = (SELECT MAX(salary) FROM instructor);
```
* 方法二：使用ORDER BY和LIMIT

ORDER BY salary DESC 按工资从高到低降序排序。
LIMIT 1 限制只返回第一行，即工资最高的那一行。假设工资最高的员工只有一位，因此第一行就是唯一解。
```sql
SELECT name
FROM instructor
ORDER BY salary DESC
LIMIT 1;
```
* 2.找到工资最高员工的名字，假设工资最高的员工有多位（试试多种写法）。
### 解答：
* 方法一：使用子查询和WHERE
```sql
SELECT name
FROM instructor
WHERE salary = (SELECT MAX(salary) FROM instructor);
```
* 方法二：使用ALL操作符
```sql
SELECT name
FROM instructor
WHERE salary >= ALL (SELECT salary FROM instructor);
```
* 方法三：使用IN 和子查询
```sql
SELECT name
FROM instructor
WHERE salary IN (
    SELECT MAX(salary)
    FROM instructor
);
```
* 3.解释下面四句。
* (1)
```sql
SELECT 1 IN (1);
```
* 含义
检查值‘1’是否包含在右侧的单元素集合（1）中，等价于 1 = 1。
* 返回结果
```txt
true
```
* (2)
```sql
SELECT 1 = (1);
```
* 含义
比较左侧‘1’和右侧的单元素集合（1）的值是否相等。
(1) 表示一个标量值。因此，这是简单的标量比较：1 = 1。
* 返回结果
```txt
true
```
* (3)
```sql
SELECT (1, 2) = (1, 2);
```
* 含义
比较两个元组(1, 2)的相等性。
元组比较要求两个元组的元素数量相同，并且对应位置元素相等。
* 返回结果
```txt
true
```
* (4)
```sql
SELECT (1) IN (1, 2);
```
* 含义
检查左侧的标量值（1）是否在右侧的集合(1, 2)中，等价于 1 = 1 OR 1 = 2。
* 返回结果
```txt
true
```
