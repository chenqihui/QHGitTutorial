# Git 辅导

想写篇 Git 来让产品和设计使用 git 管理他们的产品文档与设计图。然后将想法说出来，有人觉得没必要。产品和设计其实只需要类似 SVN 这种以文件来同步即可，而 Git 的操作会比较复杂。  
可是回想之前使用 SVN 其实也是很难用，多人提交时出现的等待，切分支，上传文件的各种慢。那回到该篇博文，将青铜部分就算入门，以单个人的维护的操作为主（这样可以避免一些比较复杂的情况）进行演示，并结合操作的截图进行说明，

## 环境

Git 环境配置 & 客户端的安装，不管是什么段位都需要了解 & 操作。

### 安装

通过此 [《安装 Git》](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git) 来安装 Git，注意不同平台的相应安装链接。主要会以 GitHub 此客户端为主介绍。 

### 配置

配置是必要且固定的操作（在第一次安装 Git 之后），只需按下面步骤一步步执行就可以了。

#### 用户信息

Windows 的在运行或者文件地址栏输入 cmd 或者 Mac 用户在程序列表中的打开终端，输入

~~~
git config --global user.name "yyyy（自己的名字）"
git config --global user.email "yyyy@xxx.com（自己的邮箱）"
~~~

这些信息将会在后续的 Git 提交的里显示，用户查看提交的用户

#### SSH

依然是在上述开打的终端中，依次输入

~~~
cd ~

ssh-keygen -t rsa -C  'yyyy@xxx.com（自己的邮箱）'

cd ~/.ssh
cat id_rsa.pub
~~~

这一步之后会显示一段字符内容，这就是上面操作生成的秘钥 & 公钥中的公钥内容，将内容复制后在Git 服务的网站上找到个人设置 SSH 处粘贴设置即可（只需保护好秘钥即可）。

好了，这就完成整个 Git 的安装 & 配置，终于搭起了 Git 环境。

## 青铜

接下来，进入 Git 的学习。

### 聊聊 Git

首先简单的聊聊 Git，Git 的详细介绍可以在参考中查看到。而现在只需有个初步印象，就是知道 Git 可以帮管理及同步文件的工具。什么版本控制，什么分布式等等都可以暂时忽略。

然后有几个名词需要记住，后面会经常用到，Git 管理的项目称为仓库 Repository。目前使用的 Git服务器 主要是 GitHub 或者 公司自搭建的 GitLab。GitHub、Git GUI 都是 Git 的客户端软件，后面的界面操作 & 截图会以 GitHub 为主。

### 仓库（Repository）

首先，在 GitHub 或者 GitLab 的服务网站上创建一个 仓库

[New Repository] 可能网站的按钮位置不同

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/1.png)

然后输入项目的名称，项目为 public 即可。确定之后会有如下说明，可以先忽略。

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/2.png)

这样其实一个仓库就已经创建完成（先有个记忆，这是一个远程仓库），接下来看看如何使用

一般使用 Git 都会使用命令，链接的教程也以命令为主，那如何让大众接受呢？本部分以 GitHub 客户端 的截图为主，windows 下还有 Git GUI。但还是会结合 Git 命令，即会有绑定。对应的功能其实就是执行对应的命令，后续段位介绍。

### 基础操作

这里的 Git 基础操作其实是为了完成简单的操作

#### clone

clone 也就是复制、克隆。将前面创建的仓库给同步到本地

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/3.png)

可以在 Git 服务器上创建仓库后的页面看到如下地址：

~~~
SSH：git@github.com:chenqihui/QHGitTutorial.git
HTTPS：https://github.com/chenqihui/QHGitTutorial.git
~~~

找到 客户端 上 [Clone Repository] 相应的按钮，点击后选择 URL ，输入上面地址其中一个即可，还有保存本地的文件夹地址路径，确定后就能在设置的保存地址上看到仓库的文件夹了，这里就是将要保存的文件的地方。

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/4.png)

由于是新仓库，即什么都没有，无需先再更新（其实 clone 的时候已经是包括更新了，也就是后面的 pull 操作）

#### add

先在文本编辑器新建一个文本并写上随意的文字后，保存到 clone 提到的文件夹里面。回到 Git客户端 会发现在列表处多了添加的文件，并且前面是有 勾选 功能。勾选上意思就是该文件的修改将被后续提交。对于此次的新文件，它也相当于 add，将文件添加到 Git 跟踪上，后面删除文件也会有对应的红色状态。add 只会出现在文件第一次加入的时候

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/5.png)

#### commit

可以留意下勾选与不勾选时，[Commit to master] 的按钮状态。其实按钮跟踪的是文件的改变，新增、删除、修改都算改变。而第一次 add 的时候，取消全部相当没有改变。接着就是 commit（提交）了，最好在输入栏里添加 commit 信息，即提交的内容，方便查看该提交的内容。接着可以在历史列表里面看到本次提交。可以再对文本内容进行修改就会看到不需要勾选，接着再提交一次看看历史列表。

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/6.png)

#### push

然后回到提交页面，此两处会有 [Publish branch] ，其实就是 push，推送到创建的仓库。在点击前，可以先看看页面下依然什么都没有。好了，点击看看，OK之后再次刷新仓库页面看看，是否多了新增的文件。

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/7.png)

到这里就算了解日常推送内容到远程仓库。

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/8.png)

#### fetch

学会本地数据的推送之后，让我们完成另一半来，就是更新数据。因为我们使用 Git，由于模拟的最简单的操作，也需要满足一个在多台电脑终端的更新。因此，试试再新的文件夹位置 clone 一份新代码下来修改再push 或者直接在网站编辑后 commit（这里由于已经是在远程了，所以可以不用 push），操作完之后，可以在网站上看到新的数据。

而回到前面客户端的历史列表是没有此部分。

然后先找到 [Fetch（抓取）] 的按钮，点击后一般会有显示远程有几个 commit 的更新，这里简单说下 fetch 其实就是将 Git 的修改记录进行更新，但不更新真实文件，即它会更新提交记录的情况，更新文件需要用户再操作

#### pull

pull 拉取就是再次操作，点击它之后本地仓库就将更新的文件也同步下来，我们也可以在文件中看到其他地方修改后提交的数据，且历史里面也会有其 commit 记录。而有些客户端是可以直接点击 pull，不需要先 fetch。实际上 pull 是 fetch 和 merge 。所以直接 pull 也可以。

好了，这就完成了 Git 的日常操作，这里需要强调下，上面都是基于一个人操作下，每次有数据修改时候都得 commit & push，切换另一台时再 pull，然后才修改。

#### merge

只是上面的流程操作还不够，前面说到 pull = fetch + merge。

先说下场景，假如你在公司修改了文件，没有 commit 或者 没有 push，此时回到家里 pull 就不可能有公司修改的。然后你继续修改。这里你只是修改其他部分，也就是公司的修改你还是需要的。你继续在家中 commit & push 修改的其他部分。然后回到公司 commit（如果没有），在 push 后会提示需要先 fetch 或者 pull，其实意思就是需要先更新最新数据才能 push，此时最后都是要先 pull 才能 push。

这里强调是 远程仓库还没有对应的更新数据。

此时的 pull 会产生 merge 操作

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/10.png)

#### conflict

冲突就是 merge 时修改的是同个文件时最常出现的情况，客户端会提示你冲突的文件，此时用编辑工具打开，看到如下的

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/12.png)

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/11.png)

~~~
<<<<<<< HEAD
remote Update2
=======
remote Update3
>>>>>>> 888cdf6916a800e1680c4609383caa1afc0c366c
~~~

它告诉你这两端由于 merge 出现冲突，需要自行解决，只需要看看是否保留或者删除其中一个即可，如都保留

~~~
remote Update2
remote Update3
~~~

修改之后会发现没有 conflict 了，而其他的客户端可能需要需要自己点击<已解决冲突>。总之解决之后就可以继续 commit & push 了。merge 会产生一个新的 commit 来记录此次操作。

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/13.png)

其实上面的情况很正常，不过 conflict 也可以避免，就是不在未 push & pull 下修改同一个文件即可。而按正常流程 commit & push，一个人操作的会理论上不太会遇到。而像我们开发其实大部分 merge 都不一定有出现 conflict。

#### reset

好了再补充一点，如果回到家里，记得修改的部分，想不要公司的修改。两种情况，一是未 commit，那么直接 Discharge 或者还原文件即可。而第二种是已经 commit，只是未 push，那就需要撤销本次 commit。在历史列表或者提交记录里面大部分可以出发 [Revert this commit]，点击后会多次新的 commit ，但是会修改回来。当然还有其他操作，不过需要结合命令 checkout，这不在本次教学里面

![](https://anakinpublicspace-1253727175.cos.ap-chengdu.myqcloud.com/blog/GitTutorial/14.png)

### 小结

本篇主要针对未接触过及只想通过 GUI 简单使用 Git 的小伙伴。只需要按步骤执行，如果遇到其他情况可先暂时忽略或者重新再来，只需要操作正常的单人流程即可。这样就能满足个人在公司和家里的文件（PPT、Excel 或 PS）的同步更新，有方便提供其他人 clone/checkout 查看（只有不允许他人修改更新即可）。

## 白银

说了上面，不知是否发现，为什么提交需要先 commit 再 push，而不能一步。而 更新 有 fetch 和 pull。这就是 Git 的根本了，Git 是分布式的，每个仓库，即远程仓库、本地仓库都是拥有完整的数据，commit 其实是提交本地仓库，而 push 则是推送到远程仓库，fetch 是让本地仓库与远程仓库的 Git 同步，pull 才是将文件同步更新。

接下来进入了解更多 Git，也就直接的命令操作。先回顾之前的基本操作，其对应执行的命令如下。

### 基础操作

~~~
# 本地创建仓库
git init

# clone
git clone [url]

# add
git add .
git add README
git rm README.md

# 查看当前工作区的修改
git status

# commit
git commit -m '【New】msg'

# push
git push [remote-name] [branch-name]

# log
git log

# fetch
git fetch [remote-name]

# pull
git pull [remote-name]

# merge
git merge

# reset
git reset --hard
git checkout -- [file]
~~~

### 其他

~~~
# 查看 Git 的配置情况
git config --lis
~~~


## 黄金

Git 除了前面的个人操作外，其实多人操作也很强。而多人操作的方式跟个人其实差不多。而其多分支的操作才是提现其价值，相比 SVN，真的不知快多少。当回看网站创建的仓库，会看到 branch 有 master，这就是分支，是 Git 为仓库创建的默认分支，而远程分支是 origin/master。这都是在执行命令时经常看到的。接下来我们可以自己新建、删除和操作分支

### branch

~~~
# 切换远程分支/创建
git checkout -b/-D a origin/a

# 查看本地分支
git branch

# 查看远程分支
git branch -r

# 查看当前分支所属
git branch -vv
~~~

* [Git-查看远程分支、本地分支、创建分支](https://www.cnblogs.com/yongdaimi/p/7600052.html)

### 多分支管理切换

#### 合并

merge

rebase

cherry-pick

#### 解决冲突

#### 暂存

git stash

* [git stash命令保存工作区和暂存区的改变](https://blog.csdn.net/qq_36078850/article/details/77278661)


<!--

### 铂金

#### 忽略

* [git取消文件跟踪](https://www.cnblogs.com/zhuchenglin/p/7128383.html)  
* [gitignore忽略规则总结](https://blog.csdn.net/qq_22494029/article/details/79537612)  

#### 排除 & 指定 checkout 目录

* [使用Sparse Checkout，排除跟踪Git仓库中指定的目录](https://www.jianshu.com/p/e82c89e187c5)  

### 星钻

#### 再探冲突

#### merge request

#### submodules

* [Git Submodule使用完整教程](https://www.cnblogs.com/lsgxeva/p/8540758.html)  
* [git clone 子模块](https://www.jianshu.com/p/945fa480744b)

### 皇冠

#### flow

#### 迁移关联的 Git 仓库

~~~shell
git remote #查看远程仓库名称：origin ； 
git remote get-url origin #查看远程仓库地址；
git remote set-url origin newPath
~~~

* [如何快速关联/ 修改 Git 远程仓库地址](https://blog.csdn.net/mlq8087/article/details/81360025)

### 王牌

#### 钩子

#### 搭个 Git 服务器
-->

## 参考

* [Git - Book](https://git-scm.com/book/zh/v2)
* [Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)

技巧补充

* [Git的奇技淫巧](https://github.com/521xueweihan/git-tips)
* ["Tracking Branches" And "Remote-Tracking Branches"](http://www.gitguys.com/topics/tracking-branches-and-remote-tracking-branches/)

在线练习

* [Learn Git Branching](https://learngitbranching.js.org/)