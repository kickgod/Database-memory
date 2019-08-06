#### <a id="top" href="#top"> MYSQL 数据库创建  </a> 

----
`创建Mysql 数据库看似是一件很轻松的事情,可能仅仅是一条语句罢了,但是里面却又很多的学问`

- [x] [`1.启动和关闭数据库`](#start)
- [x] [`2.查看已有数据库`](#show)
- [x] <a href="#createDataBase">`3.直接创建数据库`</a>
- [x] [`4.删除数据库`](#drop)
- [x] [`5.知识点`](#engine)
- [x] [`6.数据库存储引擎`](#storage)


##### [1.启动和关闭数据库](#top) <b id="start"></b> 
`Windows 环境下`
```powershell
net start mysql //启动
net stop mysql //关闭
```
* `也可以通过服务启动`

`linux 环境下`
```powershell
service mysql start  //启动
service mysql restart //重启
service mysql stop  //关闭
```
##### [2.查看已有数据库](#top) <b id="show"></b> 
`通过一条 命令就可以查看了 Mysql 默认带一些数据库 里面存储着数据库信息和 用户权限信息` <br/>
[`Show databases`](#top)
```sql
show databases;

/*
information_schema
mysql
performance_schema
sakila
sys
world
*/
```
#####  [3.查看数据库创建语句](#top)  

[`Show Create database database_name`](#top)

```sql
show create database sakila;

'sakila', 'CREATE DATABASE `sakila` /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci */'
```

#####  <a id="top" href="#createDataBase">4.直接创建数据库 </a>  
 `如果不指定字符串,那么结果就会使用意大利的字体,然后无法存储中文,会很麻烦` <br/>
 `If 判断,方式数据库名称重复冲突` <br/>
```mysql
 Create DataBase If Not Exists [ _your_dataBase_name ] Charset utf8mb4 ; 
 /*请替换 [ _your_dataBase_name ] 为你的数据库名称 推荐使用 utf8mb4 而不再是utf-8 */
```
:two: `创建一个用户,把这个数据库的权限分配给他,以此作为数据库开发的指定使用用户`<br/>
      `为保护和减少对于root账户的使用,防止攻击` <br/>
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
#####  [5.删除数据库](#top) <b id="drop"></b> 
`删除数据库`: `drop database database_name`

#####  [6.知识点](#top) <b id="engine"></b> 
`MYSQL 具有存储引擎 但是不是为数据库这个单位制定 而是制定给表` `例如为用户表制定 memory 存储引擎`

```mysql
create table users
(
    id smallint unsigned not null auto_increment,
    username varchar(15) not null,
    pwd varchar(15) not null,
    index using btree (username),
    primary key (id)
)engine=memory;
```

#####  [7.数据库存储引擎](#top) <b id="storage"></b> 
[`show engines`](#top) :`查看数据库支持的存储引擎`

* `设置InnoDB为默认引擎：`
  * `在配置文件my.cnf中的 [mysqld] 下面加入 default-storage-engine=INNODB 一句`

------

[`2018/11/30 19:39`](#top)

