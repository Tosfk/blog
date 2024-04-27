---
title: MySQL入门2——数据类型、运算符与完整性约束
date: 2024-04-27 21:39:10
categories:
- MySQL
tags:
- DataBase
- MySQL
---

<!-- toc -->

## 2.数据库基础

> 尽量让MySQL server做最少的事情，因为他最先触及性能（磁盘IO）瓶颈，让其把精力放在核心的增删改查业务上。
>

### 2.1 数据类型

MySQL数据类型定义了数据的大小范围，因此使用时选择合适的类型，不仅会降低表占用的磁盘空间，间接减少了磁盘I/O的次数，提高了表的访问效率，而且索引的效率也和数据的类型息息相关。

#### 2.1.1 数值类型

| 整数类型       | 字节     | 最小值                                  | 最大值                                                    |
| -------------- | -------- | --------------------------------------- | --------------------------------------------------------- |
| TINIINT        | 1        | 有符号：-128  无符号：0                 | 有符号：127  无符号：255                                  |
| SMALLINT       | 2        | 有符号：-32768  无符号：0               | 有符号：32767  无符号：65535                              |
| MEDIUMINT      | 3        | 有符号：-8388608  无符号：0             | 有符号：8388607  无符号：1677215                          |
| INT、INTEGER   | 4        | 有符号：-2147483648  无符号：0          | 有符号：2147483647  无符号：4294967295                    |
| BIGINT         | 8        | 有符号：-9223372036854775808  无符号：0 | 有符号：9223372036854775807  无符号：18446744073709551615 |
| **浮点数类型** | **字节** | **最小值**                              | **最大值**                                                |
| FLOAT          | 4        | +1.175494351E-38                        | +3.402823466E+38                                          |
| DOUBLE         | 8        | +2.2250738585072014E-308                | +1.7976931348623157E+308                                  |

FLOAT和DOUBLE溢出截断时不会报错，

浮点类型推荐使用decimal类型(保存为字符串格式)，数据溢出、越界会报错。

例：

```
create table user(age TINYINT unsigned not null default 0)
```

 `unsigned not null default 0`：字段的**完整性约束条件**（见2.3节）



#### 2.1.2 字符串类型

| 字符串类型   | 字节 | 描述及存储需求                                      |
| ------------ | ---- | --------------------------------------------------- |
| CHAR(M)      | M    | M为 0~255 之间的整数                                |
| VARCHAR(M)   |      | M为0~65535之间的整数，值的长度+1个字节              |
| TINYBLOB     |      | 允许长度0~255字节，值的长度+1个字节                 |
| BLOB         |      | 允许长度0~65535字节，值的长度+2个字节               |
| MEDIUMBLOB   |      | 允许长度0~167772150字节，值的长度+3个字节           |
| LONGBLOB     |      | 允许长度0~4294967295字节，值的长度+4个字节          |
| TINYTEXT     |      | 允许长度0~255字节，值的长度+2个字节                 |
| TEXT         |      | 允许长度0~65535字节，值的长度+2个字节               |
| MEDIUMTEXT   |      | 允许长度0~167772150字节，值的长度+3个字节           |
| LONGTEXT     |      | 允许长度0~4294967295字节，值的长度+4个字节          |
| VARBINARY(M) |      | 允许长度0~M个字节的变长字节字符串，值的长度+1个字节 |
| BINARY(M)    | M    | 允许长度 0~M个字节的定长字节字符串                  |



> 面试问题：
>
> age INT(9)
>
> 整形占用内存的大小是固定的，和具体的类型时强相关的。(M)只是代表整数==显示的宽度==。



 存一个`“hello”`时，用`Char(12) `占用内存12b，用`Varchar(12)`占5b，超过则截断。



#### 2.1.3 时间戳

| 日期和时间类型 | 字节 | 最小值              | 最大值              |
| -------------- | ---- | ------------------- | ------------------- |
| DATE           | 4    | 1000-01-01          | 9999-12-31          |
| DATETIME       | 8    | 1000-01-01 00:00:00 | 9999-12-31 23:59:59 |
| TIMESTAMP      | 4    | 19700101080001      | 2038年的某个时刻    |
| TIME           | 3    | -838:59:59          | 838.39:59           |
| YEAR           | 1    | 1901                | 2155                |


日期类型也是做项目过程中，经常使用的类型信息，尤其是TIMESTAMP和DATETIME两个类型，但是注意TIMESTAMP会自动更新时间，非常适合那些需要记录最新更新时间的场景，而DATETIME需要手动更新。



**时间戳：**

```
mysql> select now();		//时间函数now
+---------------------+
| now()               |
+---------------------+
| 2024-03-19 15:27:58 |
+---------------------+
1 row in set (0.01 sec)
```

**unix时间戳：**

```
mysql> select unix_timestamp(now());
+-----------------------+
| unix_timestamp(now()) |
+-----------------------+
|            1710833330 |
+-----------------------+
1 row in set (0.00 sec)
```

`1710833330`代表从1970年开始到现在时刻的秒数，代码上很方便的转换成日期。

timestamp会自动更新时间，适合记录最新更新日期的场景，datatime需要手动更新。



#### 2.1.4 枚举(enum)与执行(set)

这两个类型，都是限制该字段只能取固定的值，但是枚举字段只能取一个唯一的值，而集合字段可以取任意个值。

```
sex enum('M','W') default 'M'
```

只能选‘M‘ or ’W‘  不能选’A’。



### 2.2 MySQL运算符

#### 2.2.1 算术运算符

| 运算符 | 作用           |
| ------ | -------------- |
| +      | 加法           |
| -      | 减法           |
| *      | 乘法           |
| /, DIV | 除法，返回商   |
| %, MOD | 除法，返回余数 |

学生年龄加1：

```
Update user set age = age +1;
```

查询成绩高于90的男生：

```
select * from user where sex='M' and score>=90.0;
```



#### 2.2.2 逻辑运算符

| 运算符     | 作用   |
| ---------- | ------ |
| NOT 或 ！  | 逻辑非 |
| AND 或 &&  | 逻辑与 |
| OR 或 \|\| | 逻辑或 |



#### 2.2.3 比较运算符

| 运算符         | 作用                      |
| -------------- | ------------------------- |
| =              | 等于                      |
| <> 或 !=       | 不等于                    |
| <=>            | NULL安全的等于(NULL-safe) |
| <              | 小于                      |
| <=             | 小于等于                  |
| >              | 大于                      |
| >=             | 大于等于                  |
| BETWEEN        | 存在与指定范围            |
| IN             | 存在于指定集合            |
| IS NULL        | 为 NULL                   |
| IS NOT NULL    | 不为 NULL                 |
| LIKE           | 通配符匹配                |
| REGEXP 或RLIKE | 正则表达式匹配            |

`<> `可能会在未来版本中淘汰，尽量使用`!=`


例：

```
Select * from user where age between 20 and 22;
Select * from user where score in (99.0, 100.0);	//99到100分的同学
select * from user where score is not NULL;   		//未约束则可能为NULL
```

通配符`LIKE`

```
select * from user where name like 'zhang%'     
```

'zhang_'      _表示匹配一个字符  zhangx

%匹配多个字符  zhangyao



> 能不能用到索引？
>
> 数据量大时不能每次都整表索引，效率较低，
>
> 一般通配符加在中间或末尾能用到索引，通配符在开头用不到索引。
>



### 2.3 MySQL完整性约束

**主键约束** primary key

**自增键约束** auto_increment 

**唯一键约束** Unique

**非空约束** not null

**默认值约束** Default

**外键约束** foreign key



#### 2.3.1 主键&自增键

```
CREATE TABLE user(
Id INT UNSIGNED PRIMARY KEY AUTO_INCREAMENT COMMENT '用户的主键(对字段说明）'
```

`PRIMARY KEY`：定义为**主键**（主键约束：不能取空值，不能重复，一个表只有一个），顺带写成**自增约束**`AUTO_INCREAMENT`（从1，2，3……自增，）



#### 2.1.2 唯一键&非空键

**唯一键**：不能重复，可以取空值，一个表可以取多个

```
nickname VARCHAR(50) UNIQUE NOT NULL COMMENT '用户的昵称'
```

 `COMMENT`：对字段进行说明，不能超过五十个字符 



#### 2.2.2 默认键

```
Age TINYINT UNSIGNED NOT NULL DEFAULT 18,
Sex NMUM('male', 'female') );
```

 年龄可以重复，所以不能用唯一键约束



完整的表定义：

```
CREATE TABLE user(
id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT COMMENT '用户的主键',
nickname VARCHAR(50) UNIQUE NOT NULL COMMENT '用户的昵称',
age TINYINT UNSIGNED NOT NULL DEFAULT 18,
sex ENUM('male', 'female'));
```

要创建此表，先创建一个数据库：

```
mysql> create database test;
Query OK, 1 row affected (0.03 sec)
```

切换到test：

```
mysql> use test;
Database changed
```

创建表：

```
mysql> CREATE TABLE user(
    -> id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT COMMENT '用户的主键',
    -> nickname VARCHAR(50) UNIQUE NOT NULL COMMENT '用户的昵称',
    -> age TINYINT UNSIGNED NOT NULL DEFAULT 18,
    -> sex ENUM('male', 'female'));
Query OK, 0 rows affected (0.15 sec)
```

描述表：

```
mysql> desc user;
+----------+-----------------------+------+-----+---------+----------------+
| Field    | Type                  | Null | Key | Default | Extra          |
+----------+-----------------------+------+-----+---------+----------------+
| id       | int unsigned          | NO   | PRI | NULL    | auto_increment |
| nickname | varchar(50)           | NO   | UNI | NULL    |                |
| age      | tinyint unsigned      | NO   |     | 18      |                |
| sex      | enum('male','female') | YES  |     | NULL    |                |
+----------+-----------------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)
```

此处desc是describe的缩写，用法： desc 表名/查询语句 

还有User/G 星号形式，信息展示更加详细：

```
mysql> desc user\G
*************************** 1. row ***************************
  Field: id
   Type: int unsigned
   Null: NO
    Key: PRI
Default: NULL
  Extra: auto_increment
*************************** 2. row ***************************
  Field: nickname
   Type: varchar(50)
   Null: NO
    Key: UNI
Default: NULL
  Extra:
*************************** 3. row ***************************
  Field: age
   Type: tinyint unsigned
   Null: NO
    Key:
Default: 18
  Extra:
*************************** 4. row ***************************
  Field: sex
   Type: enum('male','female')
   Null: YES
    Key:
Default: NULL
  Extra:
4 rows in set (0.00 sec)
```



#### 2.2.3 外键

有两张表——

```
学生信息表                  父表

张三 XX XX XX XX
```

 

```
考试信息表                  子表

张三id XX XX XX XX
```

很明显，这两张表数据有关联。

**外键**使多张表字段产生关联，子表id字段关联父表字段。

若张三退学，原始信息表删去，其他表里变无用，要提醒使用者删除。



> Q：为什么现在后台开发中，外键、存储函数、存储过程、触发器等基本不用
>
> A：因为存储层最先遇到瓶颈，所以限制逻辑代码逻辑由mysql本身控制，表间关联关系都交给服务层的业务代码实现，不要给存储层额外的压力。

