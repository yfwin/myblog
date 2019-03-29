title: MySQL常用SQL
author: 骑马揍比尔
tags:
  - MySQL
  - SQL
categories:
  - MySQL
date: 2019-01-21 09:42:00
---
![upload successful](/images/qmzbe-8.png)

## 终端登陆系统
```
[root@host]# mysql -u root -p   
Enter password:******  # 登录后进入终端
```
## 创建数据库
```
CREATE DATABASE 数据库名;
```

<!--more-->

## 查看数据库
### 1.查看所有数据库
```
SHOW DATABASES;
```
### 模糊查询 

```
show databases like 't%';
```
## 删除数据库
```
drop database <数据库名>;
```
**执行以上删除数据库命令后，会出现一个提示框，来确认是否真的删除数据库：**

> Dropping the database is potentially a very bad thing to do.
> Any data stored in the database will be destroyed.
> Do you really want to drop the 'RUNOOB' database [y/N] y
> Database "RUNOOB" dropped
## 选择数据库
### 1.在登陆后选择
```
use 数据库名;
```
### 2.在登陆时选择

```
shell> mysql -h host -u user -p 数据库名
Enter password: ********
```

## 常用SQL

### order by 排序

#### 1.单字段降序：
```sql
select * from table order by id desc;
```
#### 2.单字段升序：
```sql
select * from table order by id asc;
```
#### 3.多字段排序：

```sql
select * from table order by id desc,name desc;
```

> 多字字段排序只需要添加多个排序条件，并且每个排序的条件之前用逗号分开。

order by id desc,name desc; 表示先按照id降序排序，再按照name降序排序。

同理：

order by id desc,name asc; 表示先按照id降序排序，再按照name升序排序。