### [创建 Sql Server 存储过程](#top) :grey_exclamation: <b id="top"></b>
`存储过程就是一条或者多条sql语句的集合,可视为批处理文件，但是其作用不仅限于批处理。本篇主要介绍变量的使用，存储过程和存储函数的创建，调用，查看，修改以及删除操作。`:white_check_mark:

------

- [x] [`1.创建存储过程`](#target1)
- [x] [`2.参数说明`](#target2)
- [x] [`3.返回值`](#target3)

------

#####  [1.创建存储过程](#top) <b id="target1"></b> 
`概括`:`创建语句如下`
* `尽量不要创建任何使用 sp_'作为前缀的存储过程。 SQL Server 使用 sp_前缀指定系统存储 过程。 sp_;开头的存储过程可能会与 以 后的某些系统过程发生冲突。
`
```sql
create proc|procedure [schema_name.]procedure_name[;number]
@parameter deta_type [input | out | output]
VARYING
...
as
   sql.....
end
Go
```
* `OUTPUT`: `表示参数为输出参数.可以返回给 EXEC[UTE]，使用 OUTPUT 可以将信 息返回调用过程. 也可以写成out`
* `VARYING`: `指定作为输出参数支持的结果集.`
`实例:`
```sql
CREATE PROCEDURE QueryByName
@name char(8) 
AS 
select * FROM xs WHERE "姓名 "=@name
end
Go
```

```sql
CREATE PROCEDURE QueryGrade 
@s_grade char(10)= `14信管`
@grade_count INT OUTPUT 
AS 
SELECT @grade count=COUNT(*) FROM xs where 班级 = @s_grade
end
Go
```

##### [2.参数说明](#top) <b id="target2"></b> 
`概括`:`在Sql Server 2016 中所有的数据类型都可以作为存储过程的参数  但是， cursor 数据类型只能作为 OUTPUT 参数。 如果指定了 cursor 作为数
据类型，那么就必须同时指定 VARYING 和 OUTPUT 关键字. `


#####  [3.返回值](#top) <b id="target3"></b> 
`概括`：`无论是否提供返回值,程序都会受到一个返回值,默认返回0 要传递返回值只需要使用RETURN 语句`

```sql
return [<interger value to return>]
```

--------------------
`作者:` `JxKicker` 
`完成时间`:`2019年2月19日20:10:55`
`备注信息`: `任意使用` 
