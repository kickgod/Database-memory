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
    -- 删除主键
    ALTER TABLE College DROP PRIMARY KEY;
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
    -- 删除外键
    alter table 表名 drop foreign key 外键名称;
    -- 例子
    -- alter table Teacher drop foreign key fk_teacher_to_colleage ;
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
    * `外键一般都为null`
  * `唯一性约束`:`unique`
    ```sql
    -- 在创建表的时候添加  
    
    -- 1. 字段后面添加
    create table Teacher(
        TeaherID int primary key unique auto_increment,
        CollegeID int null, -- 这个老师属于哪个学院
        TeacherName varchar(100) not null,
        TeaherAge datetime not null  ,
        constraint fk_teacher_to_colleage foreign key(CollegeID) references College(CollegeID),
        
    );
    -- 2. 结尾声明
    create table Student(
        StudentID varchar(40) primary key,
        StudentName varchar(60) ,
        StudentPassword varchar(200),
        constraint unique_key_name UNIQUE(StudentID)
    );


    -- 创建表之后创建唯一约束
    alter table Student drop index unique_key_name;
    ```
    * `唯一性约束 要求该列唯一,允许为空,但是只能出现一个空值,唯一约束可以确保一列或者几列不出现重复值`
    * `auto_increment 自动增长列 必须要求瞒住 unique 约束`
    * `主键本身 unique 所以你懂的 你给主键 添加unique 没有用`
    * `unique 和 主键的却别 在与主键 不允许空值 unique  允许一个空值  主键一个表只有一个  二unique 可以由多个`
  * `默认约束`:`default 默认值`
    ```sql
    -- 字段名称 数据类型 Default 默认值
    create table lessons(
        lessonID varchar(40) primary key,
        lessonName varchar(200) not null default '系统未添加 占位',
        lessonMark int default 3
    )
    
    -- 创建后
     ALTER TABLE lessons MODIFY lessonMark  int  default 3;
     -- 销毁默认
     ALTER TABLE lessons MODIFY lessonMark  int;
    ```
  * `自动增长`:`auto_increment`
    ```
    ```
