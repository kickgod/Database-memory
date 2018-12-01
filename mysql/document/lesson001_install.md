### [MYSQL 安装教程](#top) <b id="top"></b> :maple_leaf:

----
`很多人用了很久的MYSQL 但是还是不知道怎么安装MYSQL 那么我们就开始吧Windows 安装MYSQL 很简单的就不谈了！` [`官方安装地址`](https://dev.mysql.com/doc/refman/8.0/en/installing.html)

- [x] :maple_leaf: [`CentOS7 Yum 安装MYSQL`](#notice)

------
##### [CentOS7 Yum 安装MYSQL 8.0](#top)  :maple_leaf: <b id="notice"></b> 
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
