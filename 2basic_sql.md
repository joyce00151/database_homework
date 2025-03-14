# Homework 2
## 题目一
```txt
假设拟在数据库添加一个关系，其关系模式是 users(name, pswd, gender)，并让name作为主码。
请使用CREATE TABLE命令添加该关系。
```
### 解答：
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
2.找到所有被名叫图灵的老师教过的学生的学号（ID），并确保结果没有重复。
```
### 解答：
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


