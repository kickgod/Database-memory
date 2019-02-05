### [TSQL 编程笔记 ](#top) :grey_exclamation: <b id="top"></b>
`TSQL 是SQL SERVER 的集大成者,没有TSQL 就不会有存储过程 触发器 游标的顺利操作` [`T-SQL 官方教程`](https://docs.microsoft.com/zh-cn/sql/t-sql/language-reference?view=sql-server-2017) :white_check_mark:

------

- [x] [`1.变量的使用`](#target1)
- [x] [`2.系统变量`](#target2)
- [x] [`3.case when then end`](#target3)

------

#####  :octocat: [1.变量的使用](#top) <b id="target1"></b> 
`概括`:`声明一个变量有四个要素`:`关键字 Declare`,`变量名`,`类型`,`初始值 [可有可不有]` [`变量的类型 SQL SERVERL API`](https://docs.microsoft.com/zh-cn/sql/t-sql/data-types/data-types-transact-sql?view=sql-server-2017)
```sql
Declare @name varchar(20) = 'JxKicker';
```
* `一个变量不赋值那么默认它的值是 null`
**`给变量赋值 SET 关键字`**
```sql
Declare @Name varchar(20);
Set @Name = "JxKicker";

//查询赋值
SET @Count = (Select Count(*) From SalesOrder);

//也可以这样赋值
Select @Count = Count(*) From SalesOrder
```
#####  :octocat: [2.系统变量](#top) <b id="target2"></b> 
[`系统变量 官方API`](https://docs.microsoft.com/zh-cn/sql/integration-services/system-variables?view=sql-server-2017)

|`变量`|`用途`|`注释`|
|:-----|:-----|:-----|
|`@@DateFirst`|`返回当前设置的一周的第一天 例如 星期一或星期日`|`可以在系统范围内设置`|
|`@@ERROR`|` 返回当前链接中最后一条TSQL语句错误号 如果无错误那么 为0`|`每次执行一个新的语句就会重新设置`|
|`Index_Current(table_name)`|`返回一个表在最后的标示值`|`多表链接插入一个表那么 结果不是所预期的`|
|`@@RowCount`|`常见系统函数 影响函数 最后一条语句的`|`一般在非运行时错误检查时使用`|
|`@Identity`|`返回当前链接中作为最后一条Insert 或者Select 语句结果插入的标示值`|`如果没有生成标示值 那么为 null`|
|`Scope_Identity()`|`类似于@@Identity 但返回在当前回话和作用域中插入的最后一个标示值`|`对于避免触发器或嵌套的存储过程执行重写预期的标示值的额外插入很有用。如果你尝试检索已经执行的插入的标识值这就是一种采用的方法`|
|`@@Trancount`|`返回当前链接的活动事务数量---实质是事务的嵌套级别`|`你懂的`|

```sql
Insert into TestTable(Name) Values("JxKicker");
Set @Identity = Scope_IDentity();
```

#####  :octocat: [2.case when then end](#top) <b id="target3"></b> 
`Case具有两种格式。简单Case函数和Case搜索函数。`

##### 简单Case函数
```sql
CASE sex
 WHEN '1' THEN '男'
 WHEN '2' THEN '女'
ELSE '其他' END
```
##### Case搜索函数
```sql
CASE 
  WHEN sex = '1' THEN '男'
  WHEN sex = '2' THEN '女'
ELSE '其他' END
```

--------------------
`作者:` `模板` 
`完成时间`:`2018年12月31日18:33:38`
`备注信息`: `禁止转载` 
