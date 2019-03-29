---
layout:     post
date:       2019-01-16
title:      NodeJS操作MySQL取出来的datatime与实际差8小时
categories: 
    - MySQL
tags:
    - MySQL
    - Node
---

nodejs操作mysql取出来的datatime与实际差8小时。

<!--more-->


MySQL中执行

```
SELECT NOW();
```
打印出来的结果是

```
2019-01-16 11:05:40
```
Node中执行

```javascript
db.query(`SELECT NOW() as tm`, (err, ret)=>{
  const tm = ret[0].tm;
  console.log(ret[0].tm);
})
```
结果为
2019-01-16T03:05:40.000Z

相差了8个小时。
其实用moment插件转换一下，是正常的
npm i moment --save


```javascript
const moment = require('moment');
db.query(`select now() as tm`, (err, ret)=>{
  const tm = ret[0].tm;
  console.log(moment(tm).format('YYYY-MM-DD hh:mm:ss'))
})
```
结果为

```
2019-01-16 11:05:40
```

原因是
数据库里的时区，发现是中国标准时CST
而node中mysql默认使用的是UTC通用标准时(协调世界时，又称世界统一时间、世界标准时间、国际协调时间)

解决方案：
1.将数据库的时区改成UTC
查看当前数据库时区

```
show variables like '%time_zone%'
```


```
system_time_zone:CST
time_zone:SYSTEM
```

 下面有两种修改方法，第一个是临时修改，第二个是永久修改
 (1).临时修改用sql命令
 
```
# 设置全局时区 mysql> set global time_zone = '+8:00';
Query OK, 0 rows affected (0.00 sec) 
# 设置时区为东八区 mysql> set time_zone = '+8:00'; 
Query OK, 0 rows affected (0.00 sec) 
# 刷新权限使设置立即生效 mysql> flush privileges; 
Query OK, 0 rows affected (0.00 sec)
```

```

mysql> show variables like '%time_zone%';
 +------------------+--------+
 | Variable_name | Value |
 +------------------+--------+
 | system_time_zone | EST |
 | time_zone | +08:00 | 
 +------------------+--------+
 2 rows in set (0.00 sec)
```
(2).永久修改，修改my.cnf配置文件
打开编辑my.cnf文件
```
vi /etc/mysql/my.cnf
```
在mysqld下边的配置中添加一行

```
default-time_zone = '+8:00'
```
重启mysql 服务

```
service mysql restart
```
2.在连接mysql的配置文件中添加一条，timezone:"08:00"，如下

```javascript
var pool = mysql.createPool({
    host: 'localhost',
    user: 'root',
    password: '123',
    database: 'test',
    timezone:"08:00"
});
```
然后，Node中执行

```javascript
db.query(`SELECT NOW() as tm`, (err, ret)=>{
  const tm = ret[0].tm;
  console.log(ret[0].tm);
})
```
结果为

```
2019-01-16 11:05:40
```


