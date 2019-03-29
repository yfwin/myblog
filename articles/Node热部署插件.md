title: Node热部署插件
author: 骑马揍比尔
tags:
  - Node
  - 热部署
categories:
  - Node
date: 2019-03-16 10:45:00
---
supervisor
首先需要使用 npm 安装 supervisor（这里需要注意一点，supervisor必须安装到全局）

```shell
$ npm install -g supervisor
```
Linux 或 Mac用户需要使用管理员权限

```shell
sudo npm install -g supervisor
```

<!--more-->

安装完成后就可以用supervisor启动服务了（假设你的Node.js程序主入口是app.js）

```shell
$ supervisor app.js
```
命令行窗口会显示启动成功信息，并开始代码监听，当代码被修改之后，运行的脚本会被终止，自动重新启动。

 

PS: express 4.x把用于项目启动的代码移到了./bin/www的文件，如需使用supervisor 启动express项目请使用下面的命令

```shell
supervisor bin/www
```
 
[原文传送门](https://www.cnblogs.com/aieceo/p/7905290.html)
 
对supervisor感兴趣的同学可以访问github地址了解更多详情：https://github.com/isaacs/node-supervisor