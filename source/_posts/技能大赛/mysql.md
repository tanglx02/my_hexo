---
title: mysql
categories:
  - 技能大赛
tags:
  - 技能大赛
abbrlink: 9520183a
date: 2021-05-09 23:09:36
top:
---

## 

## 创建数据库和表

1.安装数据库

`yum install mysql mysql-server mysql-devel -y`

`service mysqld start`	//启动服务

`mysqladmin –u root –p password "123456"`	//修改登录密码

`mysql –u root -p`	//登录用户

2.创建数据库

`create database www;`

3.选择数据库

`use www;`

4.创建表

`create table users (`

`ID int primary key auto_increment,`

`name varchar(10),`

`birthday datetime,`

`Password char(8) );`



- **not null** - 指示某列不能存储 NULL 值。
- **primary key** - NOT NULL 和 UNIQUE 的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。
- **default** - 规定没有给列赋值时的默认值。



## 插入用户

`insert into users values (“”,”web1”,””,””,password(‘6666’));`

`insert into users values (“”,”web2”,””,””,password(‘6666’));`



## 显示库和显示表

`show databases;` 	//显示库

`show tables;`	//显示表

`desc 表名`	//显示表结构

## 删除库和删除表

  `drop database 库名;`

  `drop table 表名；`

  `delete from 表名;`	//将表中记录清空：

## 备份

备份库

```sql
mysqldump -u root -p myDB > /1.sql
```

备份表

```
mysqldump -u root -p  myDB www > /root/2.sql
```