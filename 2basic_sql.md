# Homework 2
## 题目一
```txt
假设拟在数据库添加一个关系，其关系模式是 users(name, pswd, gender)，并让name作为主码。
请使用CREATE TABLE命令添加该关系。
```
### 解答：
```sql
CREATE TABLE users(
    name VARCHAR(20) PRIMARY KEY,
    pswd VARCHAR(20) NOT NULL,
    gender CHAR(1) CHECK (gender IN('M','F')),   
);
```
```txt
注：CHECK (gender IN('M','F'))保证了性别只能输入男性（M）或女性（F）
```
## 题目二
```txt
考虑课堂中使用的大学数据库，包括如下关系：
course(course_id, title, dept_name, credits)
instructor(ID, name, dept_name, salary)
teaches(ID, course_id, sec_id, semester, year)
student(ID, name, dept_name, tot_cred)
takes(ID, course_id, sec_id, semester, year, grade)
使用SQL语句完成下面的查询：
1.找到在计算机学院开设的不少于3个学分的课程，并按学分进行升序排序。
```
### 解答：
```sql
SELECT course_id, title
FROM course
WHERE dept_name = '计算机'
  AND credits >= 3
ORDER BY credits ASC;
```
```txt
2.找到所有被名叫图灵的老师教过的学生的学号（ID），并确保结果没有重复。
```
### 解答：
```sql
SELECT DISTINCT takes.ID
FROM takes, teaches, instructor
WHERE instructor.name = '图灵'
  AND instructor.ID = teaches.ID
  AND teaches.course_id = takes.course_id
  AND teaches.sec_id = takes.sec_id
  AND teaches.semester = takes.semester
  AND teaches.year = takes.year;
```
```txt
注：在WHERE的多个条件中，首先筛选instructor.name = '图灵'，减少后续连接所需的计算量。
然后再分别连接instructor和teaches，teaches和takes
```
## 题目三
```txt
考虑题目二提到的关系模式，请问下面的SQL语句的含义是什么？
```
```sql
SELECT DISTINCT T.name
FROM instructor AS T, instructor AS S
WHERE T.salary > S.salary AND S.dept_name = '会计';
```
### 解答：
```txt
分析：S.dept_name = '会计' 表示S包含所有会计学院老师，
      T.salary > S.salary 表示选择那些工资比S这组数据工资高的老师T
      只要某个老师的工资比会计学院某个老师的工资高，就会出现在T中
      因此T中包含了工资高于会计学院任何一名老师的所有老师。
      另外，由于对T的dept_name没有做出限制，查询得到的对象也可以是会计学院的老师。
含义：找到所有工资高于会计学院任何一名老师的老师的姓名，并去重
```


