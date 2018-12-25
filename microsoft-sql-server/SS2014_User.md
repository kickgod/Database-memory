### [Sql Server 2014 用户管理](#top) <b id="top"></b> :herb:

-----
`Sql Server 2014 用户管理类，这些都是基本操作啊！`

- [x] [`1.数据库角色`](#juese)

##### [数据库角色](#top) <b id="juese"></b> :triangular_flag_on_post:
`通常我们再开发的时候一个用户对应一个数据库,并且可以为该用户赋予多个角色，来管理数据,Sql server 自带了一些具有各种权限的角色`
<br/>
- [`官方自带角色`](https://docs.microsoft.com/zh-cn/previous-versions/sql/sql-server-2005/ms189121(v%3dsql.90))
  - `db_accessadmin`:` 固定数据库角色的成员可以为 Windows 登录帐户、Windows 组和 SQL Server 登录帐户添加或删除访问权限。`
  - `db_backupoperator`:`固定数据库角色的成员可以备份该数据库。`
  - `db_datareader`:`固定数据库角色的成员可以对数据库中的任何表或视图运行 SELECT 语句。`
  - `db_datawriter`: `固定数据库角色的成员可以在所有用户表中添加、删除或更改数据。`
  - `db_ddladmin`: `固定数据库角色的成员可以在数据库中运行任何数据定义语言 (DDL) 命令。`
  - `db_denydatareader`:`固定服务器角色的成员不能读取数据库内用户表中的任何数据。`
  - `db_denydatawriter`:`固定服务器角色的成员不能添加、修改或删除数据库内用户表中的任何数据。`
  - `db_owner`:`固定数据库角色的成员可以执行数据库的所有配置和维护活动。`
  - `db_securityadmin`:`固定数据库角色的成员可以修改角色成员身份和管理权限。` 
