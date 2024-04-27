---
title: MySQL入门1——安装与配置
date: 2024-04-27 19:49:15
categories:
- MySQL
tags:
- DataBase
- 环境配置
---

<meta name="referrer" content="no-referrer" />

<!-- toc -->

## 1.安装与配置

### 1.1 Windows10

> 参考：[全网最简单的Mysql 8.3 安装及环境配置教程_mysql8.3安装教程-CSDN博客](https://blog.csdn.net/qq_53153755/article/details/136964335)

#### 1.1.1 Win10下 MySQL文件结构

配置文件

在`C:\ProgramData\MySQL\MySQL Server 8.3`目录下

注意`my.ini`（Linux是cnf）和`data`（存放数据库的地址，可在配置文件中更改），

`my.ini`中注意`[mysqld]`这一段中

**网络端口：**

```
# The TCP/IP Port the MySQL Server will listen on
port=3306
```

**数据目录：**

```
# Path to the database root
datadir=C:/ProgramData/MySQL/MySQL Server 8.3/Data
```

可在配置文件中进行参数调优。修改完配置要重启MySQL。

### 1.2 Linux（Ubuntu）

> 参考：[Ubuntu 安装和使用MySQL_ubuntu mysql-CSDN博客](https://blog.csdn.net/hwx865/article/details/90287715)

#### 1.2.1 MySQL数据库基本使用命令

启动MySQL数据库服务

```
sudo service mysql start
或
sudo systemctl start mysql.service
```

重启MySQL数据库服务

```
sudo service mysql restart
或
sudo systemctl restart mysql.service
```

停止MySQL数据库服务

```
sudo service mysql stop
或
sudo systemctl stop mysql.service
```

查看MySQL运行状态

```
sudo service mysql status
或
sudo systemctl status mysql.service
```

设置MySQL服务开机自启动

```
sudo service mysql enable
或
sudo systemctl enable mysql.service
```

停止MySQL服务开机自启动

```
sudo service mysql disable
或
sudo systemctl disable mysql.service
```

MySQL的配置文件

```
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```

使用命令查看mysql数据库自动设置的随机账户与密码

```
sudo cat /etc/mysql/debian.cnf
```

### 1.3 数据库文件结构简介

```
RDBMS：关系型数据库管理系统
  └──  RDB：关系型数据库
        └──  table：二位表（行：记录 列：字段/属性）
```

​       

### 1.4 关系型数据库表的设计

实体与实体之间的关系：一对一、一对多、多对多。

#### 1.4.1 一对一

#### 1.4.2 一对多

#### 1.4.3 多对多


