<a id="top" href="#top">Mysql 数据库创建  :maple_leaf:</a> 
----
`创建Mysql 数据库看似是一件很轻松的事情,可能仅仅是一条语句罢了,但是里面却又很多的学问`

- [x] :maple_leaf: <a href="#createDataBase">`直接创建数据库`</a>


####  <a id="JqueryIndex" href="#JqueryIndex">直接创建数据库 </a>  :star2: <a href="#top"> :arrow_up: </a>
:one: `创建一个数据库 并指定数据集为utf-8`<br/>
:arrow_lower_right: `如果不指定字符串,那么结果就会使用意大利的字体,然后无法存储中文,会很麻烦` <br/>
:arrow_lower_right: `If 判断,方式数据库名称重复冲突` <br/>
```mysql
 Create DataBase If Not Exists [ _your_dataBase_name ] Charset utf8 collate utf8_general_ci; 
 /*请替换 [ _your_dataBase_name ] 为你的数据库名称 */
```
:two: `创建一个用户,把这个数据库的权限分配给他,以此作为数据库开发的指定使用用户`<br/>
:arrow_lower_right: `为保护和减少对于root账户的使用,防止攻击` <br/>
```mysql
  Create User '[ _your_user_name ]'@'%' Identified by 'root';
  -- host为可以登录的主机地址，如果任何主机都可以，设置为%
  -- CREATE USER 'username'@'host' IDENTIFIED BY 'password';
```
:three: `把这个数据库的所有权限分配给这个用户`
```mysql
  grant all on [ _your_dataBase_name ].* to '[ _your_user_name ]'@'%';
  -- 你也可以分配部分的权限
```
