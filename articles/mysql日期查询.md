title: mysql日期查询
author: 骑马揍比尔
tags:
  - MySQL
categories:
  - MySQL
date: 2019-03-28 15:49:00
---

## 查询当前时间之前5分钟内的数据
```sql
select * from 数据表名 where 字段名 between date_add(now(), interval - 5 minute) and now();
```
> 字段名是字符串格式，也是可以的。

<!--more-->


## 今天
```sql
select * from 表名 where to_days(时间字段名) = to_days(now());
```
## 昨天
```sql
SELECT * FROM 表名 WHERE TO_DAYS( NOW( ) ) - TO_DAYS( 时间字段名) <= 1
```

## 近7天
```sql
SELECT * FROM 表名 where DATE_SUB(CURDATE(), INTERVAL 7 DAY) <= date(时间字段名)
```
## 近30天
```sql
SELECT * FROM 表名 where DATE_SUB(CURDATE(), INTERVAL 30 DAY) <= date(时间字段名)
```
## 本月
```sql
SELECT * FROM 表名 WHERE DATE_FORMAT( 时间字段名, '%Y%m' ) = DATE_FORMAT( CURDATE( ) , '%Y%m' )
```
## 上一月
```sql
SELECT * FROM 表名 WHERE PERIOD_DIFF( date_format( now( ) , '%Y%m' ) , date_format( 时间字段名, '%Y%m' ) ) =1
```
## 查询本季度数据
```sql
select * from `ht_invoice_information` where QUARTER(create_date)=QUARTER(now());
```
## 查询上季度数据
```sql
select * from `ht_invoice_information` where QUARTER(create_date)=QUARTER(DATE_SUB(now(),interval 1 QUARTER));
```
## 查询本年数据
```sql
select * from `ht_invoice_information` where YEAR(create_date)=YEAR(NOW());
```
## 查询上年数据
```sql
select * from `ht_invoice_information` where year(create_date)=year(date_sub(now(),interval 1 year));
```
## 查询当前这周的数据
```sql
SELECT name,submittime FROM enterprise WHERE YEARWEEK(date_format(submittime,'%Y-%m-%d')) = YEARWEEK(now());
```
## 查询上周的数据
```sql
SELECT name,submittime FROM enterprise WHERE YEARWEEK(date_format(submittime,'%Y-%m-%d')) = YEARWEEK(now())-1;
```
## 查询上个月的数据
```sql
select name,submittime from enterprise where date_format(submittime,'%Y-%m')=date_format(DATE_SUB(curdate(), INTERVAL 1 MONTH),'%Y-%m')
```
```sql
select * from user where DATE_FORMAT(pudate,'%Y%m') = DATE_FORMAT(CURDATE(),'%Y%m') ; 
```
```sql
select * from user where WEEKOFYEAR(FROM_UNIXTIME(pudate,'%y-%m-%d')) = WEEKOFYEAR(now()) 
```
```sql
select * from user where MONTH(FROM_UNIXTIME(pudate,'%y-%m-%d')) = MONTH(now()) 
```
```sql
select * from user where YEAR(FROM_UNIXTIME(pudate,'%y-%m-%d')) = YEAR(now()) and MONTH(FROM_UNIXTIME(pudate,'%y-%m-%d')) = MONTH(now()) 
```
```sql
select * from user where pudate between  上月最后一天  and 下月第一天 
```
 
## 查询当前月份的数据

```sql
select name,submittime from enterprise where date_format(submittime,'%Y-%m')=date_format(now(),'%Y-%m');
```


## 查询距离当前现在6个月的数据

```sql
select name,submittime from enterprise where submittime between date_sub(now(),interval 6 month) and now();
```

## 求2个时间的时间差值

### 参数：

|名称|值|
|---|--|
|秒|SECOND|
|分|MINUTE|
|时|HOUR|
|天|DAY|
|月|MONTH|
|年|YEAR|


### 1.时间差
```sql
select times,TIMESTAMPDIFF(YEAR,now(),times) as years from user 
```

当now()为2018-01-22 16:02:04时间，times为 2016-08-22 16:02:04
 
查出的结果集为 
```shell
------------------------------------------------
     times                          years
------------------------------------------------
 2018-01-22 16:02:04                  -2
------------------------------------------------
```
 
可以看出年份相差-2年
 
其中YEAR可以换成月份，秒 ,天


### 2.求绝对值

在以上查询中加入ABS()函数求绝对值
```sql
select times,ABS(TIMESTAMPDIFF(YEAR,now(),times)) as years from user 
```
 
 
当now()为2018-01-22 16:02:04时间，times为 2016-08-22 16:02:04
 
查出的结果集为
```shell
------------------------------------------------
     times                          years
------------------------------------------------
 2018-01-22 16:02:04                 2
------------------------------------------------
```
可以看出年份相差2年

[原文传送门1](https://blog.csdn.net/m0_37754003/article/details/82683623)

[原文传送门2](https://blog.csdn.net/qq_42152399/article/details/81358593)

[原文传送门3](https://blog.csdn.net/li1325169021/article/details/82021513)

[原文传送门4](https://www.cnblogs.com/dengyg200891/p/5966280.html)