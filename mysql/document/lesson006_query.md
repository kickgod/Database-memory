### [MYSQL 数据查询及基本语句](#top) <b id="top"></b>

-----
> :arrow_lower_left: `MYSQL 数据查询是最核心的SQL要求无论你使用什么数据库都需要学会 SQL语句 增删改查`

- [x] [`1.基本语句`](#aim1)


----
##### [1.基本语句](#top) <b id="aim1"></b>

`几个简单的查询`
```sql
select A.Name as Employee from Employee as A 
where 
A.Salary > (select Salary from  Employee where Id = A.ManagerId);
```

```mysql
select class from courses group by class having count(distinct student) >= 5
```

##### 增删改

##### 增
`Employee 的表结构` `Id为自增的`
```sql
# Field, Type, Null, Key, Default, Extra
Id, int(11), YES, , , 
Name, varchar(255), YES, , , 
Salary, int(11), YES, , , 
ManagerId, int(11), YES, , , 
```


```sql
/*带列名*/
insert into `Employee`(Name，Salary，ManagerId) values ('wangchenggui',60000, 3); /* Id 自动赋值*/

/*不带列名*/
insert into `Employee` values (4,'wangchenggui',60000, 3);
/*每个列的值都要给上并且数据类型对于列的类型 Id要手动赋予*/
```

##### 删
`delete from table_name where 条件` :`不加where 条件会删除整张表哟，而且不会自动回复自增ID`

`MySql运行在safe-updates模式下，该模式会导致非主键条件下无法执行update或者delete命令。`
```sql
SET SQL_SAFE_UPDATES = 0; -- 执行命令 修改下数据库模式 就可以了
```

```sql
delete from deprive.Employee where deprive.Employee.Id = 1;
```
