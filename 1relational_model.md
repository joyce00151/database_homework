# Homework 1
## 题目一
```txt
考虑一个银行数据库，其关系模式如下所示：
branch (branch_name, branch_city, assets)
customer (ID, customer_name, customer_street, customer_city)
loan (loan_number, branch_name, amount)
borrower (ID, loan_number)
account (account_number, branch_name, balance)
depositor (ID, account_number)
使用关系代数完成下面的查询：
```
### 1.1 找到位于成都市的支行的名字。
### 解答：
```sql
Π_branch_name(σ(branch_city='成都市')(branch))
```
### 1.2 找到在杨柳支行有贷款（loan）的借款人（borrower）的ID。
### 解答：
```sql
Π_ID(σ_branch_name='杨柳支行' (borrower ⨝ loan))
```
```txt
注：由于只有amount>0(有贷款行为）才会录入数据库，因此无需对这一条件进行限制
即假设：数据库中只存储amount>0的贷款数据，因此可以省略amount>0的过滤条件
在这一假设下，无需：Π_ID(σ(branch_name='杨柳'∧amount>0) (borrower ⨝ loan))
```
## 题目二
```txt
假设数据库中存储用户名和密码的关系模式是 users(name, pswd, gender)，
请结合关系代数简述实现用户登录逻辑的思路。
```
### 解答：
```txt
用户登录逻辑为：
用户首先输入以下信息：
-用户名：（输入的用户名）
-密码： （输入的密码）
将输入的用户名和密码分别赋值给'name'和'pswd'
然后使用关系代数进行查询：
```
```sql
σ(name='输入的用户名' ∧ pswd='输入的密码') (users)
```
```txt
-如果查询结果非空，则表示数据库中存在该用户名和密码的匹配记录，用户登录成功；
-如果查询结果返回为空集，则表示用户名或密码错误，登录失败。
```

