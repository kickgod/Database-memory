### [MYSQL 数据查询及基本语句](#top) <b id="top"></b>

-----
> :arrow_lower_left: `MYSQL 数据查询是最核心的SQL要求无论你使用什么数据库都需要学会 SQL语句 增删改查`

- [x] [`1.基本语句`](#aim1)


----
##### [1.基本语句](#top) <b id="aim1"></b>

`一个简单的子查询`
```sql
select A.Name as Employee from Employee as A 
where 
A.Salary > (select Salary from  Employee where Id = A.ManagerId);
```
