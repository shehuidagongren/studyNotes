# 一、SQL简述

## 前言笔记

查询语句的书写顺序和执行顺序

```
select ===> from ===> where ===> group by ===> having ===> order by ===> limit
```

查询语句的执行顺序

```
from ===> where ===> group by ===> having ===> select ===> order by ===> limi
```





## 1.SQL的概述

Structure Query Language(结构化查询语言)简称SQL，它被美国国家标准局(ANSI)确定为关系型数据库语言的美国标准，后被国际化标准组织(ISO)采纳为关系数据库语言的国际标准。数据库管理系统可以通过SQL管理数据库；定义和操作数据，维护数据的完整性和安全性。



## 2.SQL的优点

1、简单易学，具有很强的操作性
		2、绝大多数重要的数据库管理系统均支持SQL
		3、高度非过程化；用SQL操作数据库时大部分的工作由DBMS自动完成



## 3.SQL的分类

1、DDL(Data Definition Language) 数据定义语言，用来操作数据库、表、列等； 常用语句：CREATE、 ALTER、DROP
		2、DML(Data Manipulation Language) 数据操作语言，用来操作数据库中表里的数据；常用语句：INSERT、 UPDATE、 DELETE
		3、DCL(Data Control Language) 数据控制语言，用来操作访问权限和安全级别； 常用语句：GRANT、DENY
		4、DQL(Data Query Language) 数据查询语言，用来查询数据 常用语句：SELECT

------

# 二、数据库的三大范式

1、第一范式(1NF)是指数据库表的每一列都是不可分割的基本数据线；也就是说：每列的值具有原子性，不可再分割。
		2、第二范式(2NF)是在第一范式(1NF)的基础上建立起来得，满足第二范式(2NF)必须先满足第一范式(1NF)。如果表是单主键，那么	主键以外的列必须完全依赖于主键；如果表是复合主键，那么主键以外的列必须完全依赖于主键，不能仅依赖主键的一部分。
		3、第三范式(3NF)是在第二范式的基础上建立起来的，即满足第三范式必须要先满足第二范式。第三范式(3NF)要求：表中的非主键列必须和主键直接相关而不能间接相关；也就是说：非主键列之间不能相关依赖。

------

# 三、数据库的数据类型

## 1.整数类型

| **数据类型** | **字节数** | **无符号数的取值范围** | **有符号数的取值范围**                   |
| ------------ | ---------- | :--------------------: | ---------------------------------------- |
| TINYINT      | 1          |         0~255          | -128~127                                 |
| SMALLINT     | 2          |        0~65535         | -32768~32768                             |
| MEDIUMINT    | 3          |       0~16777215       | -8388608~8388608                         |
| INT          | 4          |      0~4294967295      | -2147483648~ 2147483648                  |
| BIGINT       | 8          | 0~18446744073709551615 | -9223372036854775808~9223372036854775808 |

## 2.浮点数类型和定点数类型

| **数据类型**   | **字节数** | **有符号的取值范围**                             | **无符号的取值范围**                               |
| -------------- | ---------- | ------------------------------------------------ | -------------------------------------------------- |
| FLOAT          |            | -3.402823466E+38~-1.175494351E-38                | 0和1.175494351E-38~3.402823466E+38                 |
| DOUBLE         |            | -1.7976931348623157E+308~2.2250738585072014E-308 | 0和2.2250738585072014E-308~1.7976931348623157E+308 |
| DECIMAL（M,D） |            | -1.7976931348623157E+308~2.2250738585072014E-308 | 0和2.2250738585072014E-308~1.7976931348623157E+308 |

| 从上图中可以看出：DECIMAL类型的取值范围与DOUBLE类型相同。但是，请注意：DECIMAL类型的有效取值范围是由M和D决定的。其中，M表示的是数据的长 度，D表示的是小数点后的长度。比如，将数据类型为DECIMAL(6,2)的数据6.5243 插入数据库后显示的结果为6.52 |
| ------------------------------------------------------------ |
|                                                              |

## 3.字符串类型

| 插入值 | CHAR(3) | 存储需求 | VARCHAR(3) | 存储需求 |
| ------ | :-----: | -------- | ---------- | -------- |
| ‘’     |   ‘’    | 3个字节  | ‘’         | 1个字节  |
| ‘a’    |   ‘a’   | 3个字节  | ‘a’        | 2个字节  |
| ‘ab’   |  ‘ab’   | 3个字节  | ‘ab’       | 3个字节  |
| ‘abc’  |  ‘ab’   | 3个字节  | ‘abc’      | 4个字节  |
| ‘abcd’ |  ‘ab’   | 3个字节  | ‘abc’      | 4字节    |

| 在MySQL中常用CHAR 和 VARCHAR 表示字符串。两者不同的是：VARCHAR存储可变长度的字符串。 |
| ------------------------------------------------------------ |
| 当数据为CHAR(M)类型时，不管插入值的长度是实际是多少它所占用的存储空间都是M个字节；而VARCHAR(M)所对应的数据所占用的字节数为实际长度加1 |



## 4.字符串类型

| 数据类型   |     储存范围     |
| ---------- | :--------------: |
| TINYTEXT   |    0~255字节     |
| TEXT       |   0~65535字节    |
| MEDIUMTEXT |  0~16777215字节  |
| LONGTEXT   | 0~4294967295字节 |

## 5.日期与时间类型

| 数据类型  | 字节数 | 取值范围                                | 日期格式            | 零值                |
| --------- | ------ | --------------------------------------- | ------------------- | ------------------- |
| YEAR      | 1      | 1901~2155                               | YYYY                | 0000                |
| DATE      | 4      | 1000-01-01~9999-12-31                   | YYYY-MM-DD          | 0000-00-00          |
| TIME      | 3      | -838：59：59~ 838：59：59               | HH:MM:SS            | 00:00:00            |
| DATETIME  | 8      | -838：59：59~ 838：59：59               | YYYY-MM-DD HH:MM:SS | 0000-00-00 00:00:00 |
| TIMESTAMP | 4      | 1970-01-01 00:00:01~2038-01-19 03:14:07 | YYYY-MM-DD HH:MM:SS | 0000-00-00 00:00:00 |



## 6.二进制类型

在MySQL中常用BLOB存储二进制类型的数据，例如：图片、PDF文档等。BLOB类型分为如下四种：

|  数据类型  | 储存范围         |
| :--------: | ---------------- |
|  TINYBLOB  | 0~255字节        |
|    BLOB    | 0~65535字节      |
| MEDIUMBLOB | 0~16777215字节   |
|  LONGBLOB  | 0~4294967295字节 |

------

# 四、数据库、数据表的基本操作

## 1.数据库的基本操作

创 建数据库就是在数据库系统中划分一块空间存储数据，语法如下：

```
create database 数据库名称;
```

删除数据库MySQL命令：

```
drop database 数据库名称;
```

查询出MySQL中所有的数据库MySQL命令：

```
show databases;
```

将数据库的字符集修改为gbk MySQL命令：

```
alter database 数据库名称 character set gbk;
```

运行效果展示：

切换数据库 MySQL命令：

```
use 数据库名称;
```

查看当前使用的数据库 MySQL命令：

```
select database();
```



## 2.数据表的基本操作

### 2.1 创建数据表

数据库创建成功后可在该数据库中创建数据表(简称为表)存储数据。

在操作数据表之前应使用“USE 数据库名;”指定操作是在哪个数据库中进行先关操作，否则会抛出“No database selected”错误。

```
use 数据库名称;
```

2.1 创建数据表
示例：创建学生表 MySQL命令：

```
 create table 表名(
         字段1 字段类型,
         字段2 字段类型,
         …
         字段n 字段类型
);
```

实例：

```
 create table student(
 id int,
 name varchar(20),
 gender varchar(10),
 birthday date
 );
```





### 2.2 查看数据表

示例：查看当前数据库中所有表 MySQL命令：

```sql
show tables;
```

查看表的字段信息 MySQL命令：

```sql
desc student;
```

### 2.3 修改数据表

在MySQL中使用alter table修改数据表.
修改表名 MySQL命令：

```
alter table 数据表原名 rename to 数据表新名;
```

修改字段名 MySQL命令：

```
alter table 数据表表名 change 字段名原名 字段名新名 varchar(10);
```

修改字段数据类型 MySQL命令：

```
alter table 数据表表名 modify 字段名 int; 
```

增加字段 MySQL命令：

```
alter table 数据表表名 add 字段名 varchar(50);
```

删除字段 MySQL命令：

```
alter table 数据表表名 drop 字段名;
```

### 2.4 删除数据表

删除数据表 MySQL命令：

```sql
drop table 数据表表名;
```

------

# 五、数据表的约束

| 约束条件    | 说明                             |
| ----------- | -------------------------------- |
| PRIMARY KEY | 主键约束用于唯一标识对应的记录   |
| FOREIGN KEY | 外键约束                         |
| NOT NULL    | 非空约束                         |
| UNIQUE      | 唯一性约束                       |
| DEFAULT     | 默认值约束，用于设置字段的默认值 |

| 以上五种约束条件针对表中字段进行限制从而保证数据表中数据的正确性和唯一性。 表的约束实际上就是表中数据的限制条件。 |
| ------------------------------------------------------------ |
|                                                              |

## 1.主键约束

主键约束即primary key用于唯一的标识表中的每一行。被标识为主键的数据在表中是唯一的且其值不能为空。
主键约束基本语法：

```
字段名 数据类型 primary key;
```


设置主键约束(primary key)的第一种方式

```
create table student(
    id int primary key,
    name varchar(20)
);
```

**设置主键约束(primary key)的第二种方式**

```sql
create table student01(
id int
name varchar(20),
primary key(id)
);
```



## 2.非空约束

非空约束即 NOT NULL指的是字段的值不能为空，基本的语法格式如下所示：

```sql
字段名 数据类型 NOT NULL;
```

示例：

```sql
create table student02(
    id int
    name varchar(20) not null
);
```

## 3.默认值约束

默认值约束即DEFAULT用于给数据表中的字段指定默认值，即当在表中插入一条新记录时若未给该字段赋值，那么，数据库系统会自动为这个字段插入默认值；其基本的语法格式如下所示：

```
字段名 数据类型 DEFAULT 默认值；
```


示例：

```
create table student03(
id int,
name varchar(20),
gender varchar(10) default 'male'
);
```

## 5.唯一性约束

唯一性约束即UNIQUE用于保证数据表中字段的唯一性，即表中字段的值不能重复出现，其基本的语法格式如下所示：

```
字段名 数据类型 UNIQUE;
```


示例：

```
create table student04(
    id int,
    name varchar(20) unique
);
```

## 6.外键约束

外键约束即FOREIGN KEY常用于多张表之间的约束。基本语法如下：

-- 在创建数据表时语法如下：

```
CONSTRAINT 外键名 FOREIGN KEY (从表外键字段) REFERENCES 主表 (主键字段)
```

-- 将创建数据表创好后语法如下：

```
ALTER TABLE 从表名 ADD CONSTRAINT 外键名 FOREIGN KEY (从表外键字段) REFERENCES 主表 (主键字段);
```


示例：创建一个学生表 MySQL命令：

```
create table student05(
    id int primary key,
    name varchar(20)
);
```

示例：创建一个班级表 MySQL命令：

```
create table class(
classid int primary key,
studentid int
);
```


示例：学生表作为主表，班级表作为副表设置外键， MySQL命令：

```
alter table class add constraint fk_class_studentid foreign key(studentid) references student05(id);
```


------------------------------------------------


### 6.1 数据一致性概念

建立外键是为了保证数据的完整和统一性

### 6.2 删除外键

语法如下：

```sql
alter table 从表名 drop foreign key 外键名；
```

示例：删除外键 MySQL命令：

```sql
alter table class drop foreign key fk_class_studentid;
```



### 6.3 关于外键约束需要注意的细节

 1、从表里的外键通常为主表的主键
		2、从表里外键的数据类型必须与主表中主键的数据类型一致
		3、主表发生变化时应注意主表与从表的数据一致性问题

# 六、数据表插入数据

## 1.为表中所有字段插入数据

每个值、值的顺序、值的类型必须与对应的字段相匹配。但是，各字段也无须与其在表中定义的顺序一致，它们只要与 VALUES中值的顺序一致即可。
语法如下：

```
INSERT INTO 表名（字段名1,字段名2,...) VALUES (值 1,值 2,...);
```

示例：向学生表中插入一条学生信息 MySQL命令：

```
insert into student (id,name,age,gender) values (1,'bob',16,'male');
```

## 2.为表中指定字段插入数据

```
INSERT INTO 表名（字段名1,字段名2,...) VALUES (值 1,值 2,...);
```

## 3.同时插入多条记录

```
INSERT INTO 表名 [(字段名1,字段名2,...)]VALUES (值 1,值 2,…),(值 1,值 2,…),...;
```


在该方式中：(字段名1,字段名2,…)是可选的，它用于指定插入的字段名；(值 1,值 2,…),(值 1,值 2,…)表示要插入的记录，该记录可有多条并且每条记录之间用逗号隔开。
		示例：向学生表中插入多条学生信息 MySQL命令：

```
insert into student (id,name,age,gender) values (2,'lucy',17,'female'),(3,'jack',19,19,'male'),(4,'tom',18,'male');
```

# 七、更新数据

## 1.UPDATE基本语法

```
UPDATE 表名 SET 字段名1=值1[,字段名2 =值2,…] [WHERE 条件表达式];
```

## 2.UPDATE更新部分数据

示例：将name为tom的记录的age设置为20并将其gender设置为female MySQL命令：

```sql
update student set age=20,gender='female' where name='tom';
```

## 3.UPDATE更新全部数据

示例：将所有记录的age设置为18 MySQL命令：

```sql
update student set age=18;
```

# 八、删除数据



## 1.DELETE基本语法

表名用于指定要执行删除操作的表；[WHERE 条件表达式]为可选参数用于指定删除的条件。

```sql
DELETE FROM 表名 [WHERE 条件表达式];
```

## 2.DELETE删除部分数据

删除age等于14的所有记录 MySQL命令：

```sql
delete from student where age=14;
```

## 3.DELETE删除全部数据

删除student表中的所有记录 MySQL命令：

```sql
delete from student;
```

## 4.TRUNCATE和DETELE的区别

1、DELETE语句后可跟WHERE子句，可通过指定WHERE子句中的条件表达式只删除满足条件的部分记录；但是，TRUNCATE语句只能用于删除表中的所有记录。
2、使用TRUNCATE语句删除表中的数据后，再次向表中添加记录时自动增加字段的默认初始值重新由1开始；使用DELETE语句删除表中所有记录后，再次向表中添加记录时自动增加字段的值为删除时该字段的最大值加1
3、DELETE语句是DML语句，TRUNCATE语句通常被认为是DDL语句

------

# 九、MySQL数据表简单查询

## 1.简单查询概述

简单查询即不含where的select语句。



## 2.查询所有字段（方法不唯一只是举例）

select * from student;

## 3.查询指定字段（sid、sname）

select sid,sname from student;

## 4.常数的查询

常数的查询日期标记 MySQL命令：

```sql
select sid,sname,'2021-03-02' from student;
```

## 5.从查询结果中过滤重复数据

在使用DISTINCT 时需要注意：
**在SELECT查询语句中DISTINCT关键字只能用在第一个所查列名之前。**

```sql
select distinct gender from student;
```

## 6.算术运算符（举例加运算符）

查询学生10年后的年龄 MySQL命令：

```sql
 select sname,age+10 from student;
```

# 十、函数

## 1.聚合函数

### 1.1、count（）

统计表中数据的行数或者统计指定列其值不为NULL的数据个数
*查询有多少该表中有多少人*

```
select count(*) from student;
```

### 1.2、max（）

计算指定列的最大值，如果指定列是字符串类型则使用字符串排序运算

```sql
select max(age) from student;
```

### 1.3、min（）

计算指定列的最小值，如果指定列是字符串类型则使用字符串排序运算

```sql
select sname,min(age) from student;
```

### 1.4、sum（）

计算指定列的数值和，如果指定列类型不是数值类型则计算结果为0

```sql
select sum(age) from student;
```

### 1.5、avg（）

计算指定列的平均值，如果指定列类型不是数值类型则计算结果为

```sql
select avg(age) from student;
```

## 2.其他常用函数

### 2.1、时间函数

```
SELECT NOW();
SELECT DAY (NOW());
SELECT DATE (NOW());
SELECT TIME (NOW());
SELECT YEAR (NOW());
SELECT MONTH (NOW());
SELECT CURRENT_DATE();
SELECT CURRENT_TIME();
SELECT CURRENT_TIMESTAMP();
SELECT ADDTIME('14:23:12','01:02:01');
SELECT DATE_ADD(NOW(),INTERVAL 1 DAY);
SELECT DATE_ADD(NOW(),INTERVAL 1 MONTH);
SELECT DATE_SUB(NOW(),INTERVAL 1 DAY);
SELECT DATE_SUB(NOW(),INTERVAL 1 MONTH);
SELECT DATEDIFF('2019-07-22','2019-05-05');
```



### 2.2、字符串函数

```
--连接函数
SELECT CONCAT ()
--
SELECT INSTR ();
--统计长度
SELECT LENGTH();
```



### 2.3、数学函数

```
-- 绝对值
SELECT ABS(-136);
-- 向下取整
SELECT FLOOR(3.14);
-- 向上取整
SELECT CEILING(3.14);
```

# 十一、条件查询

## 1.使用关系运算符查询

| 关系运算符 |   说明   |
| ---------- | :------: |
| =          |   等于   |
| <>         |  不等于  |
| !=         |  不等于  |
| <          |   小于   |
| <=         | 小于等于 |
| >          |   大于   |
| >=         | 大于等于 |

```
select * from student where age>=17;





 '
 
 '
```

## 2.使用IN关键字查询

IN关键字用于判断某个字段的值是否在指定集合中。如果字段的值恰好在指定的集合中，则将字段所在的记录将査询出来。

查询sid为S_1002和S_1003的学生信息 MySQL命令：

```
select * from student where sid in ('S_1002','S_1003');
```

查询sid为S_1001以外的学生的信息 MySQL命令：

```sql
select * from student where sid not in ('S_1001');
```

## 3.使用BETWEEN AND关键字查询

BETWEEN AND用于判断某个字段的值是否在指定的范围之内。如果字段的值在指定范围内，则将所在的记录将查询出来
查询15到18岁的学生信息 MySQL命令：

```sql
select * from student where age between 15 and 18;
```

## 4.使用空值查询

在MySQL中，使用 IS NULL关键字判断字段的值是否为空值。请注意：空值NULL不同于0，也不同于空字符串
由于student表没有空值就不演示查询空值的了
查询sname不为空值的学生信息 MySQL命令：

```
select * from student where sname is not null;
```



## 5.使用AND关键字查询

在MySQL中可使用AND关键字可以连接两个或者多个查询条件。
查询年纪大于15且性别为male的学生信息 MySQL命令：

```sql
select * from student where age>15 and gender='male';
```

## 6.使用OR关键字查询

在使用SELECT语句查询数据时可使用OR关键字连接多个査询条件。在使用OR关键字时，只要记录满足其中任意一个条件就会被查询出来
查询年纪大于15或者性别为male的学生信息 MySQL命令：

```
select * from student where age>15 or gender='male';
```


## 7.使用LIKE关键字查询

MySQL中可使用LIKE关键字可以判断两个字符串是否相匹配

### 7.1 普通字符串

查询sname中与wang匹配的学生信息 MySQL命令：

```sql
select * from student where sname like 'wang';
```

### 7.2 含有%通配的字符串

%用于匹配任意长度的字符串。例如，字符串“a%”匹配以字符a开始任意长度的字符串
查询学生姓名以li开始的记录 MySQL命令：

```sql
select * from student where sname like 'li%';
```

查询学生姓名以g结尾的记录 MySQL命令：

```sql
select * from student where sname like '%g';
```

### 7.3 含有_通配的字符串

下划线通配符只匹配单个字符，如果要匹配多个字符，需要连续使用多个下划线通配符。例如，字符串“ab_”匹配以字符串“ab”开始长度为3的字符串，如abc、abp等等；字符串“a__d”匹配在字符“a”和“d”之间包含两个字符的字符串，如"abcd"、"atud"等等。

查询学生姓名以zx开头且长度为4的记录 MySQL命令：

```sql
select * from student where sname like 'zx__';
```

## 8.使用LIMIT限制查询结果的数量

当执行查询数据时可能会返回很多条记录，而用户需要的数据可能只是其中的一条或者几条
查询学生表中年纪最小的3位同学 MySQL命令：

```sql
select * from student order by age asc limit 3;
```

## 9.使用GROUP BY进行分组查询

### 9.1 GROUP BY和聚合函数一起使用

统计各部门员工个数 MySQL命令：

```sql
select count(*), departmentnumber from employee group by departmentnumber;
```

统计部门编号大于1001的各部门员工个数 MySQL命令：

```
select count(*), departmentnumber from employee where departmentnumber>1001 group by departmentnumber;
```

 

### 9.2 GROUP BY和聚合函数以及HAVING一起使用

GROUP BY和聚合函数以及HAVING一起使用统计工资总和大于8000的部门 MySQL命令：

```
select sum(salary),departmentnumber from employee group by departmentnumber having sum(salary)>8000;
```


## 10.使用ORDER BY对查询结果排序

```
SELECT 字段名1,字段名2,…
FROM 表名
ORDER BY 字段名1 [ASC 丨 DESC],字段名2 [ASC | DESC];
```

参数 ASC表示按照升序排序，DESC表示按照降序排序；默认情况下，按照ASC方式排序。

查询所有学生并按照年纪大小升序排列 MySQL命令：

```sql
select * from student order by age asc;
```

# 十二、别名设置

## 1.为表取别名

在查询操作时，假若表名很长使用起来就不太方便，此时可为表取一个別名，用该别名来代替表的名称。语法格式如下所示：

```
SELECT * FROM 表名 [AS] 表的别名 WHERE .... ;
```


将student改为stu查询整表 MySQL命令：

```
select * from student as stu;
```

## 2.为字段取别名

在查询操作时，假若字段名很长使用起来就不太方便，此时可该字段取一个別名，用该别名来代替字段的名称。语法格式如下所示：

```
SELECT 字段名1 [AS] 别名1 , 字段名2 [AS] 别名2 , ... FROM 表名 WHERE ... ;
```

将student中的name取别名为“姓名” 查询整表 MySQL命令：

```
select name as '姓名',id from student;
```

# 十三、表的关联关系

## 1.关联查询

查询Java班的所有学生 MySQL命令：

```sql
select * from student where classid=(select cid from class where cname='Java');
```

## 2.关于关联关系的删除数据

班级表和学生表之间存在关联关系；要删除Java班级，应该先删除学生表中与该班相关联的学生。否则，假若先删除Java班那么学生表中的cid就失去了关联
删除Java班 MySQL命令：

```
delete from student where classid=(select cid from class where cname='Java');
delete from class where cname='Java';
```



# 十四、多表连接查询

## 1.交叉连接查询

笛卡儿积

## 2.内连接查询

返回的结果只包含符合查询条件和连接条件的数据

内连接(Inner Join)又称简单连接或自然连接，是一种非常常见的连接查询。内连接使用比较运算符对两个表中的数据进行比较并列出与连接条件匹配的数据行，组合成新的 记录。也就是说在内连接查询中只有满足条件的记录才能出现在查询结果中。其语法格式如下：

```
SELECT 查询字段1,查询字段2, ... FROM 表1 [INNER] JOIN 表2 ON 表1.关系字段=表2.关系字段
```

在该语法中：INNER JOIN用于连接两个表，ON来指定连接条件；其中INNER可以省略。

示例：查询员工姓名及其所属部门名称 MySQL命令：

```
select employee.ename,department.dname from department inner join employee on department.did=employee.departmentid;
```


## 3.外连接查询

有时还需要在返回查询结果中不仅包含符合条件的数据，而且还包括左表、右表或两个表中的所有数据，此时我们就需要使用外连接查询。外连接又分为左(外)连接和右(外)连接。

```
SELECT 查询字段1,查询字段2, ... FROM 表1 LEFT | RIGHT [OUTER] JOIN 表2 ON 表1.关系字段=表2.关系字段 WHERE 条件
```


由此可见，外连接的语法格式和内连接非常相似，只不过使用的是LEFT [OUTER] JOIN、RIGHT [OUTER] JOIN关键字。其中，关键字左边的表被称为左表，关键字右边的表被称为右表；OUTER可以省略。
在使用左(外)连接和右(外)连接查询时，查询结果是不一致的，具体如下：
1、LEFT [OUTER] JOIN 左(外)连接：返回包括左表中的所有记录和右表中符合连接条件的记录。
2、RIGHT [OUTER] JOIN 右(外)连接：返回包括右表中的所有记录和左表中符合连接条件的记录。

### 3.1 左（外）连接查询

左(外)连接的结果包括LEFT JOIN子句中指定的左表的所有记录，以及所有满足连接条件的记录。如果左表的某条记录在右表中不存在则在右表中显示为空。
查询每个班的班级ID、班级名称及该班的所有学生的名字 MySQL命令：

```
select class.cid,class.cname,student.sname from class left outer join student on class.cid=student.classid;
```


### 3.2 右（外）连接查询

右(外)连接的结果包括RIGHT JOIN子句中指定的右表的所有记录，以及所有满足连接条件的记录。如果右表的某条记录在左表中没有匹配，则左表将返回空值。
查询每个班的班级ID、班级名称及该班的所有学生的名字 MySQL命令：

```
select class.cid,class.cname,student.sname from class right outer join student on class.cid=student.classid;
```



# 十五、子查询

## 1.带比较运算符的子查询

查询比张三同学所在班级编号还大的班级的信息 MySQL命令：

```sql
select * from class where cid>(select classid from student where sname='张三');
```

## 2.带EXISTS关键字的子查询

EXISTS关键字后面的参数可以是任意一个子查询， 它不产生任何数据只返回TRUE或FALSE。当返回值为TRUE时外层查询才会 执行
假如王五同学在学生表中则从班级表查询所有班级信息 MySQL命令：

```
select * from class where exists (select * from student where sname='王五');
```


## 3.带ANY关键字的子查询

ANY关键字表示满足其中任意一个条件就返回一个结果作为外层查询条件。

查询比任一学生所属班级号还大的班级编号 MySQL命令：

```sql
select * from class where cid > any (select classid from student);
```

## 4.带ALL关键字的子查询

LL关键字与ANY有点类似，只不过带ALL关键字的子査询返回的结果需同时满足所有内层査询条件。

查询比所有学生所属班级号还大的班级编号 MySQL命令：

```
select * from class where cid > all (select classid from student);
```


# 十六、数据库的导入导出

## 1、导入sql文件

1. 在命令窗口输入mysql -uroot -ppassword,接着输入show databases；

2. 接着输入 databasename ，然后执行source d:/地址/databasename.sql，执行show tables复查；

3. 或者直接拖拽入mysql数据库管理工具选择确定连接名与数据库名执行sql语句

   ------

   

## 2、导出sql文件

导出sql文件可以使用mysqldump。主要有如下几种操作：
			①导出整个数据库（包括数据库中的数据）：

```
 mysqldump -u username -ppassword dbname > dbname.sql；
```


​			②导出数据库中的数据表（包括数据表中的数据）：

```
mysqldump -u username -ppassword dbname tablename > tablename.sql；
```


​			③导出数据库结构（不包括数据，只有创建数据表语句）：

```
mysqldump -u username -ppassword -d dbname > dbname.sql；
```


​			④导出数据库中数据表的表结构（不包括数据，只有创建数据表语句）：

```
mysqldump -u username -ppassword -d dbname tablename > tablename.sql
```

------



## 3、注意

mysqldump导出提示：

```
 Couldn't execute 'SELECT COLUMN_NAME,                       JSON_EXTRACT(HISTOGRAM, '$."number-of-buckets-specified"')                FROM information_schema.COLUMN_STATISTICS                WHERE SCHEMA_NAME = 'mydatabase2' AND TABLE_NAME = 'my_auto';': Unknown table 'column_statistics' in information_schema (1109)
```

**mysqldump命令：**

　　导出数据库：

```
mysqldump  -uroot -proot mydatabase2 > f:/mydb.sql
```

**错误提示：**

```
　`mysqldump: Couldn't execute 'SELECT COLUMN_NAME, JSON_EXTRACT(HISTOGRAM, '$."number-of-buckets-specified"') FROM information_schema.COLUMN_STATISTICS`
```

**原因：**

　　因为新版的mysqldump默认启用了一个新标志，通过- -column-statistics=0来禁用它

**解决方法：**

　　导出数据库：mysqldump --column-statistics=0 -uroot -proot mydatabase2 > f:/mydb.sql

       导出多个表：mysqldump --column-statistics=0 -uroot -proot mydatabase2 my_student my_int >f:/my_student_int.sql
还原数据库：

        前提：先在mysql下创建一个mydb：create database mydb;
    
        mysql -uroot -proot mydb < f:/mydb.sql

还原数据表：

        在mysql环境下：source f:/my_student_int.sql;

**注意：语句结尾有 ; 表示是在mysql环境下的语句，没有则表示在cmd控制面板下的命令**

# 十七、多列索引和单列索引

在数据库中表的某个字段创建索引，所带来的最大益处就是将该字段作为检索条件时可以极大地提高检索效率，加快检索时间，降低检索过程中须要读取的数据量，降低数据的排序成本。。

在多个列上建立独立的索引大部分情况下并不能提高MySQL的查询性能。

这种算法有三个变种：OR条件的联合（union），AND条件的相交（intersection），组合前两种情况的联合及相交
