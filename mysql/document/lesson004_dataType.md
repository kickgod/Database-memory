### [MYSQL 数据类型和运算符](#top) :herb: <b id="top"></b>

-----
> :arrow_lower_left: `MYSQL 支持很多的数据类型，但是不要慌,我们只需要完全掌握重要常用的，明白数据类型中的坑`

- [x] [`1.介绍概括一下`](#intro)

----

##### :triangular_flag_on_post: [介绍概括一下](#top) <b id="intro"></b> 
`MYSQL 支持的数据类型啊 大概分为三种 来概括现在的所有数据`
* `数值数据类型`:`TinyInt SmallInt MediumInt Int BigInt Float Double Decimal`
* `日期/时间类型`:`Year Time Date DateTime TimeStamp`
* `字符串类型`:`Char Varchar binary varbinary Blob Text Enum Set 字符串又分为二进制字符串 文本字符串 等等`


##### [整型数据](#top)
`来看看整形`

|`类型名称`|`说明`|`存储需求`|`显示宽度`|`表示范围`|
|---------|:---|:----|:----|-----|
|TinyInt |`很小的整数 很少用` |`一个字节` | `默认显示宽度 4：tinyint(4) `| 2^8 |
|SmallInt|`几乎没用过 很少用`|`两个字节`|`默认显示宽度 6: smallint(6)`|2^16|
|MediumInt|`几乎没用过 很少用`|`三个字节`|`默认显示宽度 9: mediumint(9)`|2^24|
|Int(Interger)|`整数 很常用`|`四个字节`|`默认显示宽度 11: int(11)`|2^32|
|BigInt|`大整数 常用`|`八个字节`|`默认显示宽度 20: bigint(20)`|2^64|




* `1. 注意: Int() 括号里面是可以跟位数的 表示的意思是整数想显示宽度`
   * `Int(9)`:`数据的显示宽度是九位  如果数字宽度超过九位 那么将会原样显示`
* `2. 注意: 主要记住Int 和BigInt 就行了,其他的数据类型很少用`
