### [MYSQL 视图](#top) <b id="top"></b>

-----
> :arrow_lower_left: `MYSQL 非常常用 是一张虚拟的表，一个有多张表组成的一张表,本质上存储的sql语句 用于也已对视图进行增删改查`

- [x] [`1.创建一个简单的视图`](#aim1)
- [x] [`2.修改视图`](#aim2)
- [x] [`2.删除视图`](#aim3)


----
##### [1.创建一个简单的视图](#top) <b id="aim1"></b>
`视图有两个优点，第一简单化，第二安全性`

`一个简单的视图`
```sql
create view my_view_name as 
select A.Name as Employee from Employee as A 
where 
A.Salary > (select Salary from  Employee where Id = A.ManagerId);
```

`查看视图的结构`
```sql
describe my_view_name;
-- or
desc my_view_name;
```
`视图详细信息`
```sql
show create view my_view_name;
```
##### [2.修改视图](#top) <b id="aim2"></b>
```sql
create or replace view my_view_name
as
sql.....
```
`使用alter语句`

```sql
alter view my_view_name 
as 
sql ...
```

##### [3.删除视图](#top) <b id="aim3"></b>
```sql
drop view [if Exists] my_view_name;
```


