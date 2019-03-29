
---
layout:     post
date:       2019-01-16
title:      Ubuntu系统快速安装nodeJS
categories: 
    - Node
tags:
    - Ubuntu
    - Node
---
 


第一步，去 nodejs 官网 https://nodejs.org 看最新的版本号，求稳的话建议选LTS版。
第二步，添加源后安装
重点来了，nodejs 的每个大版本号都有相对应的源，比如这里的 9.x.x版本的源是https://deb.nodesource.com/setup_9.x。

所以在终端执行： 
```
curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
```

<!--more-->

稍等片刻，源已经添加完毕，再执行： 
```
sudo apt-get install -y nodejs
```
等待安装完成。

顺带一提，如果你要安装8.x.x 的版本，只需要修改添加源地址中的数字即可，比如： 
```
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
```

最后验证一下，执行：“nodejs -v” 即可出现刚才安装的版本号。