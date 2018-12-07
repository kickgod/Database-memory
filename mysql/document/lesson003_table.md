### <a id="top" href="#top"> MYSQL 数据表的基操 </a> 

----
> 创建Mysql 数据库看似是一件很轻松的事情,可能仅仅是一条语句罢了,但是里面却又很多的学问

- [x]  [`1.创建表的语法`](#start)
- [x]  [`2.使用约束`](#que)
---

#### 1.创建表的语法 <b id="start"></b>
* `1.很简单 名称在前 类型随后 约束在右`
* `2.注意创建表之前要先选中数据库`

  ```sql
  create table webconfig(
    id int unique not null primary key auto_increment,
    isOpenSystem varchar(10),
    configuration varchar(100)
  );
  ```
#### 2.使用约束 <b id="que"></b>  
* `约束有六大类`
  * `主键约束`:`primary key`
    ```sql
    -- 创建时候 添加主键约束
    
    -- 1. 在字段后面添加
    UserId int not null primary key 
    -- 2. 统一添加
    create table webconfig(
      id int unique not null auto_increment,
      isOpenSystem varchar(10),
      configuration varchar(100),
      primary key(id)
    );
    -- 创建表之后 添加主键约束
    alter table tableName add primary key(column_name,column_name...);
    
    ```
    * `主键一定非空`
    * `主键一定是唯一 主键默认为聚集索引`
    * `主键可以由多个字段组成`：`Primary key(name,deptid)`
  * `外键约束`:`foreign key`
    ```sql
    create database if not exists Mydb charset  utf8mb4;  

    use Mydb;
    -- 1. 定义语法 表中
    /*
    constraint 外键名称 foreign key(字段名称) references 外键表名(字段名称)
    */
    create table College(
        CollegeID int primary key unique auto_increment,
        CollegeName varchar(100) not null,
        CollegeStatus int 
    );

    create table Teacher(
        TeaherID int primary key auto_increment,
        CollegeID_ int null, -- 这个老师属于哪个学院
        TeacherName varchar(100) not null,
        TeaherAge datetime not null,
        constraint fk_teacher_to_colleage foreign key(CollegeID_) references College(CollegeID)
    )
    -- 创建表之后添加 外键约束 
    ALTER TABLE Teacher ADD CONSTRAINT fk_teacher_to_colleage FOREIGN KEY
    (CollegeID) REFERENCES College(`CollegeID`);
    
    ```
    * `外键 一定要求两个表的字段 类型相同 链接出去的外键必须是主键  例如上面 CollegeID 是主键`
    * `子表的外键必须关联父表的主键`
  * `非空约束`:`not null`
    ```sql
    -- 建表的时候添加非空约束
    create table College(
        CollegeID int primary key unique auto_increment,
        CollegeName varchar(100) not null,
        CollegeStatus int 
    );
    -- 添加非空约束
    ALTER TABLE College modify CollegeName varchar(100) not null;
    -- 删除非空约束
    ALTER TABLE College modify CollegeName varchar(100) not null;
    ``` 
  * `唯一性约束`
  * `默认约束`
  * `自动增长`
