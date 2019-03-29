title: git教程
author: 骑马揍比尔
tags:
  - git
  - ''
categories:
  - git
  - ''
date: 2019-03-27 17:06:00
---
[原文传送门：仅仅为了自己查阅方便，如有侵权，我会删掉](https://mp.weixin.qq.com/s?__biz=MzU2NzczMzk5Nw==&mid=2247483753&idx=1&sn=a8d654a7f61833b976f65a9e93b4f56c&chksm=fc99faebcbee73fd8ef1b8bd777f064d90f5a8c5a628da6814065028264b174e09b1b3551176&scene=21#wechat_redirect)

[作者相关文章](https://juejin.im/post/5c9660c45188252d60192c5e)

**文末有总结，便于查阅**

第一件事，肯定就是先安装Git了  
官网下载Git比较麻烦，需要有梯子来帮助你，才能摸到它，这里直接给你一个Github上的镜像地址供你下载安装

> https://github.com/waylau/git-for-win

<!--more-->

  # <center>一、第一次使用Git</center>

---


安装好后，直接打开Git Bash，也就是Git 的控制台程序，就可以开始使用了

第一次使用Git，需要先配置自己的邮箱与名称

配置邮箱地址

```shell
git config --global user.email "NaoNao.@nao.com"
```

配置用户名

```shell
git config --global user.name "NaoNao"
```



配置完，Git不会给出任何提示，Linux的逻辑就是，没有提示就是最美的提示。

**注意**`git config`**命令的**`--global`**参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。**

要想查看是否配置成功，依然是使用上述命令，把引号以及引号内的内容去掉即可。

# <center>二、 拉取项目</center> 
---

配置好我们的个人信息后，自然也就需要拉取项目了

在磁盘中新建好存放项目的文件夹，进入文件夹点击鼠标右键，选择Git Bash即可

温馨提示：使用Git托管的项目，有两种地址，Https与SSH。  
使用Https地址拉取，验证一次密码后，以后每次拉取/推送的时候不再需要验证密码。  
使用SSH地址拉取的项目，每次拉取/推送的时候都需要密码验证。  
各位读者自己抉择。

我的项目地址是 https://github.com/AdolphKevin/NaoNao.git
```shell
git clone https://github.com/AdolphKevin/NaoNao.git
```

将你的项目地址替换掉我的项目地址即可

# <center># 三、 分支管理</center> 

---

说分支管理之前，在此做个**背景说明**：一般在项目开发中会有2个主分支（master与develop）  
master分支上的内容是发布在**生产环境**运行的内容  
develop分支是所有开发人员**开发完成**发布到测试环境的内容  
其它各种feature分支都是各位开发人员在开发时拉取使用的分支

此文，也沿用此方式，各位读者按照自己实际情况酌情判断

拉取下来后，我们要进行开发，肯定不能在master分支上开发，一般在项目上都会有各种分支

项目clone下来，首先就是查看分支了
```shell
git branch -r
```

加上-r是代表查看远程仓库的分支，要是查看本地分支，只需要把-r去掉即可，-r是remote的简写

查看远程分支，所有的分支名前均会带有origin/ 的前缀，这个前缀代表着远程分支，拉取远程分支，填写远程分支名时不需要带上origin/

接到开发任务，我们需要从远程仓库上将我们需要开发的分支拉取到本地
```shell
git fetch origin x(远程分支名):y(本地分支名)
```

使用上述代码，可以将远程分支拉取到本地，并创建本地分支

接着就是要将刚刚创建的本地分支与远程分支做关联了，做了关联之后，拉取更新与推送都不需要再指定分支名称
```shell
git branch --set-upstream-to=origin/x(远程分支名)  y(本地分支名)
```
其中，x是你本地分支对应的远程分支；y是你当前的本地分支。

做完关联后，咱们就需要切换分支，在特定的分支上去进行开发任务  
先查看本地分支，找到我们需要开发的分支
```shell
git branch
```
再切换到我们需要开发的分支上
```shell
git checkout y(分支名)
```
  
# <center>四、 内容推送</center>

---

我们在自己的分支上按照需求完成了开发任务，接着就是将我们开发的内容提交到远程仓库了

虽然咱们所在的分支，除了自己之外，按理说是没人会在自己这个分支上再进行开发，所以推送前拉取更新也不很必要

但是为了避免不必要的麻烦，提交之前还是先拉取一下最新的数据
```shell
git pull
```
获取了最新数据后，如果有别的同事动了咱们的分支，那肯定得先解决一下文件的冲突，若没有人动，那也就不用处理了

接着将我们添加/修改的文件提交到本地暂存区
```shell
git add xxx(文件名)
```
xxx代表着文件名。当然，开发时咱们基本上很少只修改/添加一个单独的文件，当修改或添加了很多文件时，让我们一个一个文件的add，能把人给累死

所以Git也给出了批量add的方法，简单粗暴
```shell
git add -A
```
-A是All的缩写，git add all 可以提交未跟踪、修改和删除文件。  
.git add . 可以提交未跟踪和修改文件，但是不处理删除文件。

提交到暂存区后完成后就是将改动内容全部提交
```shell
git commit -m "提交到暂存区"
```
引号内的文字，是此次提交内容的一个说明描述，以后看日志时也便于知道此次进行了什么内容的修改

提交完后就是将本次修改的内容推送至远程仓库
```shell
git push
```
好了，到这里push的时候，坑来了~~~

如果是自己一个人的项目，此时如何push都没问题，但问题就出在，咱们是多人开发的项目，咱们的分支是需要与主分支合并(merge)。

别的同事的任务完成了，早已推送到我们将要合并的develop分支上了

所以我们在push之前需要进行code merge ，将develop分支上的内容merge到我们当前的feature分支上

# <center>五、 代码合并</center>


---

此时我们在feature分支上已经将修改内容commit了  
需要将develop分支的内容合并到当前分支，先切换分支到develop上，再获取一次更新
```shell
git checkout developgit pull
```
这里切换到develop分支上获取更新时有个小坑，咱们暂且按照一切顺利来处理，后面再说一些常见的意外情况的处理。

获取完更新后，再切换到我们的feature分支上，将develop的内容合并到我们的feature分支上
```shell
git checkout feature
```
合并某分支到当前分支
```shell
git merge develop
```
  
# <center>六、解决冲突</center>
 
---

执行merge后，如果有冲突，控制台会将有冲突的文件名展示出来，我们按照文件名找到对应文件，将冲突给解决掉后。

打开文件我们可以看到冲突的内容，例如：

```shell
<<<<<<<HEAD

hello world feature

========

 hello world develop

>>>>>> develop
```


Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容

<<<<<<<与=======之间的内容为**当前分支**的内容

 =======与>>>>>>之间的内容为**develop分支**的内容（换句话说：就是需要**被合并的分支**内容）

将不需要保留的内容删除即可解决冲突

解决冲突后，我们再将当前的feature分支推送到远程仓库
```shell
git push
```
执行完本命令行后，即可将本地分支内容推送至远程仓库
# <center>七、获取更新时的意外情况</center> 
---

前面说从feature分支切换到develop分支拉取更新时，会有个小坑，因为有时候Git会报错

> **Git pull - Please move or remove them before you can merge**

这个错误是因为无论原始文件中.gitignore 文件的内容是什么，文件都被添加到远程存储库中。

由于文件存在于远程存储库中，因此git也必须将它们提取到本地工作树，因此会抱怨文件已经存在。

.gitignore 仅用于扫描新添加的文件，它与已添加的文件没有任何关系。

因此，解决方案是删除工作树中的文件并提取最新版本。或者长期解决方案是如果错误地添加了文件，则从存储库中删除文件。

这时我们在develop 分支上删除当前目录下没有被track过的文件和文件夹
```shell
git clean -d -f 
```
现在重新获取更新即可
# <center>八、开发到一半，却需要切换分支</center>  
---

软件开发中，Bug就像家常便饭一样。有了Bug就需要修复，在Git中，由于分支是如此的强大，所以，在实战中，每个Bug都是通过一个新的临时分支来修复，修复后，将Bug分支合并到develop与master两个分支上，然后将临时分支删除

**注意：将Bug分支合并到develop与master两个分支上，是在远程仓库完成。在本地，是需要将develop与master分支先获取最新，然后将这两分支分别合并在Bug分支上，解决冲突后直接推送Bug分支即可**

可我们在feature分支上开发功能开发到一半，leader突然跑来告诉我们，生产环境出现了一个Bug，需要咱们紧急修复，咱们兴致勃勃的使用`git checkout Bug`命令，打算切换到Bug分支上去修复Bug

结果……Git却告诉我们，无法切换过去，因为我们目前所在分支没有提交……

可我们若要完成开发任务再去修复Bug，可能需要好几个小时甚至几天时间才能完成，而Bug修复却是紧急任务，这该如何是好呢？

问题不大，不慌。此时我们可以将当前分支开发的工作状态储藏下来，待我们解决了Bug，再恢复我们现在的状态
```shell
git stash
```
执行完上述命令后，我们再来看看我们工作区是否干净  
```shell
git stash status
```
我们发现工作区非常干净，此时我们就可以顺利的执行`git checkout Bug`到Bug分支上去修改Bug了  

咱们现在将Bug也解决了，也推送了，现在又回到feature分支继续咱们之前的任务了，切换回feature分支后，之前修改的内容也没有恢复啊！说好的储藏了工作状态呢？

咱们就来看看所有储藏的工作
```shell
git stash list
```
使用上述命令，Git会将所有的储藏工作罗列出来，当我们想要恢复其中某一个储藏状态时，指定其名字就好了
```shell
git stash apply stash@{0}
```
上述的stash@{0} 是当前分支储藏的工作名，各位读者根据自己的`git stash list`中的内容，自行替换

切换后，确认完当前状态无误了，就可以将之前保存的储藏删除
```shell
git stash drop stash@{0}
```
觉得要执行两行命令比较麻烦？没关系，还有一次性解决问题的方法  
切换后并自动删除
```shell
git stash pop stash@{0}
```
不过我个人不大推荐这种方式，万一咱们恢复的储藏指定错了呢，要恢复起来还挺麻烦的。
# <center>九、版本回退</center> 
---

在开发时，总有需要回退到某个版本的时候，不然用版本控制系统干嘛？是吧

我们先来看看我们的历史版本
```shell
git log
```
现在控制台输出了最近三次提交的日志信息，友情提示一下，按键盘Q可退出，按回车可查看更多的日志

要是嫌弃输出的内容过于冗杂，可以让Git显示个简单版
```shell
git log --pretty=oneline
```
加上一个`--pretty=oneline`参数，就可以只看提交的ID了

现在我们可以根据当时commit时填写的描述信息，来判断哪一个ID是我们想要回退的版本

版本的回退，有两种常用的方式

回退到上一个版本
```shell
git reset --hard HEAD
```
根据commit的ID，回退到指定版本  
```shell
git reset --hard commit_id
```
commit_id这个版本号没必要写全，只需要写6位以上就差不多了，Git能自己找到它，若存在前6位重复ID，那再多加几位就好了

版本的回退也非常的简单吧，Git的命令行操作写到这儿，也进入尾声了。上述的命令基本可以满足日常的使用

  
# <center>十、写在最后</center>
---

Git命令行的操作，使用起来并不复杂，作为开发人员，会用就行了，使用Git的要领就是大量使用分支

总结一下本文牵扯到的git操作  
`git config --global user.name` 查看用户名或配置用户名

`git config --global user.email`查看email或配置email

`git clone`将远程仓库的项目克隆到本地

`git branch`查看分支

`git branch -r`查看远程分支

`git branch <name>`创建分支

`git fetch origin origin/remote_branch:your_branch`将远程分支下载到本地，并创建分支

`git branch --set-upstream-to=origin/remote_branch your_branch`将本地分支与远程分支做关联

`git pull`获取更新

`git clean -d -f`删除当前目录下没有被track过的文件和文件夹

`git merge <name>`将目标分支合并到当前分支

`git add`将内容添加到暂存区

`git commit`将添加的内容提交

`git push`将本地提交内容推送到远程仓库

`git checkout`切换分支

`git branch -d <name>`删除分支

`git stash`储藏当前分支所有内容

`git stash list`查看当前分支储藏列表

`git stash apply`恢复指定储藏内容

`git stash drop`删除指定储藏内容

`git stash pop`恢复并删除指定储藏内容

`git status`显示工作目录和暂存区的状态

`git log`显示commit的详细日志

`git log --pretty=oneline`只显示commit的ID与描述

`git reset --hard HEAD`回退到最近的一个版本

`git reset --hard commit_id`根据commit_id回退到指定版本


**END**