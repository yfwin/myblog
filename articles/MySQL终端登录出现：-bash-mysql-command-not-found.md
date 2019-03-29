title: 'MySQL终端登录出现：-bash: mysql: command not found'
author: 骑马揍比尔
tags:
  - MySQL
categories:
  - MySQL
date: 2019-01-21 10:46:00
---
## 问题
用终端登录mysql时，报错：-bash: mysql: command not found

```
mac$ mysql -u root -p
-bash: mysql: command not found
```
<!--more-->


## 解决方案：
 **查询mysql安装路径**
mac：

```
mdfind -name mysql
```

linux:


```
whereis mysql
```
 **假设安装路径为：/usr/local/mysql，进入mysql 安装文件夹，执行：**

```
vim ~/.bash_profile
```
**按“i”键，进入编辑模式，添加：**

```
export PATH=$PATH:/usr/local/mysql/bin
```
**ESC->:wq->回车
执行**：

```
source ~/.bash_profile；
```
**over；**