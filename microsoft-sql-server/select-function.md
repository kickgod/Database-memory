##### ROW_NUMBER() 行编码函数
`OW_NUMBER()函数将针对SELECT语句返回的每一行，从1开始编号，赋予其连续的编号。在查询时应用了一个排序标
准后，只有通过编号才能够保证其顺序是一致的，当使用ROW_NUMBER函数时，也需要专门一列用于预先排序以便于进行编号。`

```sql
ROW_NUMBER() over(order by psd) 

//例子:
select email,customerID, ROW_NUMBER() over(order by psd) as rows from QT_Customer
```
##### 随机出现行 NEWID()
··
