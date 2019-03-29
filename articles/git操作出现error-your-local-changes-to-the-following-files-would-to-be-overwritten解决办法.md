title: >-
  git操作出现error:your local changes to the following files would to be
  overwritten解决办法
author: 骑马揍比尔
tags:
  - git
categories:
  - git
date: 2019-01-29 15:52:00
---
git 在上传的时候出现了如下错误

```
error: Your local changes to the following files would be overwritten by merge:
        package-lock.json
        package.json
Please, commit your changes or stash them before you can merge.
Aborting

```

<!--more-->

先查看一下跟踪的文件的状态
```
git status
```

结果如下：

```
On branch master
Your branch is behind 'origin/master' by 2 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   package-lock.json
        modified:   package.json

no changes added to commit (use "git add" and/or "git commit -a")

```
切换到主分支

```
git checkout master
```

接下来我们推送到远程服务器的分支

```
git push -u origin master
```

原文传送门：[传送门](https://blog.csdn.net/qq_21004057/article/details/52928211)




