### [MYSQL 系统函数调用](#top) <b id="top"></b>

-----
> :arrow_lower_left: `MYSQL 支持很多的函数，在我们查询的过程中经常需要借助函数完成复杂的查询`

- [x] [`1.和NULL有关的`](#aim1)


----

#####  [1.和NULL有关的](#top) <b id="aim1"></b>

##### [1.IFNULL(expression, alt_value)](#top)
* `expression` 	`必须，要测试的值`
* `alt_value` 	`必须，expression 表达式为 NULL 时返回的值`
```sql
SELECT IFNULL(NULL, "RUNOOB");

-- RUNOOB
```
