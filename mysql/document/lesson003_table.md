### <a id="top" href="#top"> MYSQL 数据表的基操 </a> 

----
> 创建Mysql 数据库看似是一件很轻松的事情,可能仅仅是一条语句罢了,但是里面却又很多的学问

- [x]  [`1.创建表的语法`](#start)
- [x]  [`2.使用约束`](#que)
    * [`主键约束`](#one)
    * [`外键约束`](#two)
    * [`非空约束`](#three)
    * [`唯一性约束`](#four)
    * [`默认约束`](#five)
    * [`自动增长`](#six)
    * [`check 约束`](#seven)
- [x]  [`3.查看表结构`](#show)
- [x]  [`4.修改表结构`](#stuc)
- [x]  [`5.表的存储引擎`](#engine)
- [x]  [`6.删除表`](#delete)
---
show create table Teacher;
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
* `约束有七大类`
  * `1.主键约束`:`primary key`  <b id="one"></b>
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
    * `并不是每一个表都需要主键,只是当涉及到多个表的关系的时候需要主键`
  * `2.外键约束`:`foreign key` <b id="two"></b>
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
  * `3.非空约束`:`not null` <b id="three"></b>
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
  * `4.唯一性约束`:`unique` <b id="four"></b>
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
    * `unique 和 主键的区别 在与主键 不允许空值 unique  允许一个空值  主键一个表只有一个  而unique 可以有多个`
  * `5.默认约束`:`default 默认值` <b id="five"></b>
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
  * `6.自动增长`:`auto_increment` <b id="six"></b>
    ```sql
    -- 建表的时候
    TeaherID int primary key unique auto_increment
    -- 建表之后增加
    alter table t_user modify user_id INT(10) AUTO_INCREMENT;

    alter table t_user change user_id user_id INT(10) AUTO_INCREMENT;
    
    -- 删除自增长
    alter table t_user modify user_id INT(10);

    alter table t_user change user_id user_id INT(10);
    ```
    * `自动增长要求必须是 字段类型必须为 int 且满足 unique`
    * `默认自增字段从1 开始 每次添加一条记录 该值自动加 1`
  * `7.check 约束`:`check` <b id="seven"></b>
    ```sql
    -- check 约束
    Sex char(2)NOT NULL  DEFAULT '男' CHECK (Sex IN ('男','女')) 
    Age tinyint(4) NOT NULL DEFAULT '20' CHECK (Age between 15 and 30)
    
    -- 创建表的结尾添加
    create table Teacher(
        TeaherID int primary key auto_increment,
        CollegeID_ int null, -- 这个老师属于哪个学院
        TeacherName varchar(100) not null,
        TeaherAge datetime not null,
        constraint fk_teacher_to_colleage foreign key(CollegeID_) references College(CollegeID),
        check(TeaherAge > 20)
    )
    -- 建表后
    alter table 表名 add constraint CK_字段名 check (条件表达式) --条件表达式中的条件用关系运算符连接
    -- 删除约束
    alter table 表名 drop constraint 约束名 
    ```
#### 3.查看表结构 <b id="show"></b>    
`查看基本表结构`：`Describe 表名` `简写`:`DESC 表名`
```sql
Desc Teacher;
/*
Field, Type, Null, Key, Default, Extra
'TeaherID', 'int(11)', 'NO', 'PRI', NULL, 'auto_increment'
'CollegeID_', 'int(11)', 'YES', 'MUL', NULL, ''
'TeacherName', 'varchar(100)', 'NO', '', NULL, ''
'TeaherAge', 'datetime', 'NO', '', NULL, ''
*/
```
`查看表的详细结构`：`Show Create table table_name`
```sql
show create table Teacher;
/*
CREATE TABLE `teacher` 
(`TeaherID` int(11) NOT NULL AUTO_INCREMENT,
`CollegeID_` int(11) DEFAULT NULL,
`TeacherName` varchar(100) NOT NULL,
`TeaherAge` datetime NOT NULL,
PRIMARY KEY (`TeaherID`),
KEY `fk_teacher_to_colleage` (`CollegeID_`),
CONSTRAINT `fk_teacher_to_colleage` FOREIGN KEY (`CollegeID_`) 
REFERENCES `college` (`collegeid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
*/
```
#### 4.修改表结构 <b id="stuc"></b>  
##### `1. 修改表名称`:`alter table 旧表名 rename to 新名称 `
```sql
Create table Lessons(
	lessonID int primary key auto_increment,
    lessonName varchar(100) not null,
    lessonStatus int default 40
);

alter table Lessons rename to Lesson;
```
##### `2. 修改字段数据类型`:`alter table 表名 modify 字段名称 数据类型 `
```sql
alter table Lesson modify lessonStatus tinyint;
```
##### `3. 修改字段名称`:`alter table <表名> change 旧字段名称 新字段名称 <新数据类型>`
`change 可以一键修改两个内容 字段名称 数据类型`
```sql
alter table Lesson change  lessonStatus status tinyint(4) not null;
```
##### `4. 添加字段`:`alter table <表名> add 新字段名称 数据类型 [not null / default value]  `
```sql
-- 放在第一列
alter table Lesson add column lessonAdministrator int not null first;

desc Lesson;

/*
lessonAdministrator	int(11)	NO		
lessonID	int(11)	NO	PRI		auto_increment
lessonName	varchar(100)	NO			
lessonStatus	tinyint(4)	YES			
*/

-- 放在lessonName 之后
alter table Lesson add column lessonAdministrator int not null after lessonName;

desc Lesson;

/*
lessonID	int(11)	NO	PRI		auto_increment
lessonName	varchar(100)	NO			
lessonAdministrator	int(11)	NO			
lessonStatus	tinyint(4)	YES			
*/
```
##### `5. 删除字段`:`alter table <表名> drop 字段名称  `
```sql
alter table Lesson drop lessonAdministrator;
```
##### `6. 修改字段排列顺序`:`alter table <表名> modify 字段名称 数据类型 first|after 字段  `
`吧某一个字段 放在什么字段之前之后 没什么意义`
```sql
alter table lesson modify lessonAdministrator  int not null  after lessonStatus;

desc Lesson;

/*
lessonID	int(11)	NO	PRI		auto_increment
lessonName	varchar(100)	NO			
lessonStatus	tinyint(4)	YES			
lessonAdministrator	int(11)	NO			
*/
```
#### 5.表的存储引擎 <b id="engine"></b>  
`修改表的存储引擎 可以在创建表的时候指定存储引擎`
* `show engines; 查看存储引擎`
* `select version(); 查看系统版本`
```sql
create table Student(
	StudentID varchar(40) primary key,
	StudentName varchar(60) ,
	StudentPassword varchar(200),
	constraint unique_key_name UNIQUE(StudentID)
)engine = Innodb;

alter table  table_name Engine = MyisAM 
```
#### 6.删除表 <b id="delete"></b>  
`删除表, Drop Table IF Exisit 表1,表2`
```sql
Drop Table Student；
```
