### [MYSQL 安装教程](#top) <b id="top"></b> 

----
`很多人用了很久的MYSQL 但是还是不知道怎么安装MYSQL 那么我们就开始吧Windows 安装MYSQL 很简单的就不谈了！` [`官方安装地址`](https://dev.mysql.com/doc/refman/8.0/en/installing.html)

- [x] [`CentOS7 Yum 安装MYSQL`](#notice)
- [x] [`新版本MYSQL的变化`](#change)
- [x] [`MYSQL 大小写敏感问题`](#ignore)

------
##### [CentOS7 Yum 安装MYSQL 8.0](#top)  <b id="notice"></b> 
`使用Yum 安装MYSQL` [`MYSQL YUM源`](https://dev.mysql.com/downloads/repo/yum/) `安装其他版本只需要替换yum包就行了`
* `下载 rpm 包`:`使用上面的命令就直接下载了安装用的Yum Repository，大概25KB的样子，然后就可以直接yum安装了。`
```c#
 wget -i -c https://repo.mysql.com//mysql80-community-release-el7-1.noarch.rpm
```
* `安装mysql rpm`
```powershell
yum -y install https://repo.mysql.com//mysql80-community-release-el7-1.noarch.rpm
```
* `安装MYSQL 服务器`
```powershell
yum -y install mysql-community-server
```
* `安装好了之后 打开MYSQL服务 `
```powershell
systemctl start  mysqld.service
systemctl status mysqld.service //查看服务状态
```
* `不过要想进入MySQL还得先找出此时root用户的密码，通过如下命令可以在日志文件中找出密码：`
```c#
grep "password" /var/log/mysqld.log
登陆mysql
mysql -uroot -p  
```
* `修改密码 运行远程连接mysql`
```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';
update user set host = '%' where user = 'root';
```
##### [新版本MYSQL的变化](#top)  <b id="change"></b> 
* `新版本的mysql 配置文件 my.ini文件 不在 安装根目录下 了  而在另一个文件夹下面 ` `C:\ProgramData\MySQL\MySQL Server 8.0`


##### [MYSQL 大小写敏感问题](#top)   <b id="ignore"></b>

* `C:\ProgramData\MySQL\MySQL Server 8.0 找打my.ini 文件 将里面的 lower_case_table_names 设置为2` `因为mysql 数据库信息存放在表中 所以表对
大小写敏感 所有信息都对大小写敏感了`
* `大消息不敏感可以设置为 1 `

```xml
lower_case_table_names=2
```
