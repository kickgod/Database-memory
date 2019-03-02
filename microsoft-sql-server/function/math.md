### [Sql Server 数学函数](#top) <b id="top"></b>
`文章简单介绍概括`:white_check_mark:

------

- [x] [`1.ceiling(number)`](#target1)
- [x] [`2.floor(number)`](#target2)
- [x] [`3.rand([整数表达式])`](#target3)
- [x] [`4.round(数值表达式[,长度[,操作方式]])`](#target4)
- [x] [`5.convert(数据类型[(长度)]，表达式[，样式]）`](#target5)

------

#####  [1.ceiling(number)](#top) <b id="target1"></b> 
`概括`:`向上取整函数`
```sql
select ceiling(5.22);  //6
```


#####  [2.floor(number)](#top) <b id="target2"></b> 
`概括`:`向下取整函数`
```sql
select ceiling(5.22);  //5
```


#####  [3.rand([整数表达式])](#top) <b id="target3"></b> 
`概括`:`随机数生成 返回从0 到 1 之间的随机 float 值。整数表达式为种子，使用相同的种子产生随机数相同。即使用同一个种子
值重复调用RAND() 会返回相同的结果。不指定种子则系统会随机生成种子。`
```sql
select rand(100) //0.715436657367485

select rand() //0.28463380767982

select rand() //0.0131039082850364
```
#####  [4.round(数值表达式[,长度[,操作方式]])](#top) <b id="target4"></b> 
`返回一个数值，舍入到指定的长度。注意返回的数值和原数值,操作方式：默认为 0 遵循四舍五入，指定其他整数值则直接截断。`

```sql
select round(1236.555,2,0) //1236.560

select round(1236.555,2,1) //1236.550

select round(1236.555,0) //1237.000

select round(1236.555,-1) //1240.000

select round(1236.555,-1,1) //1230.000

select round(1236.555,-2) //1200.000

```
#####  [5.convert(数据类型[(长度)]，表达式[，样式]）](#top) <b id="target5"></b> 
`类型转换`
```sql
select convert(nvarchar,123)  // 123

select convert(nvarchar ,getdate(),101)  //04/28/2009
```
--------------------
`作者:` `模板` 
`完成时间`:`2018年12月31日18:33:38`
`备注信息`: `任意使用` 
