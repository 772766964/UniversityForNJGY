# Git

### Git 第一次创建项目

+ git init
+ git add .
+ git commit -m "备注"
+ git remote add origin SSH地址
+ git push -u origin master

### 多人合作

+ git checkout -b 分支名   创建分支,如果已经有分支，直接 git  checkout 分支名
+  git add .
+  git commit -m "备注"
+  git push origin 分支名 -u

`（注意：git push origin dev -u 这行命令，由于是第一次推送到远程dev分支，所以加上-u让本地和远程的dev分支关联起来，否则后面在推送时会提示未关联远程项目，造成不必要的麻烦。这次加上-u关联起来后，后面就不用加-u 了，直接使用git push origin dev推送就行）`

`而看master分支却没有我们的项目，我们的分支内容不能在master上显示`

#### 合并分支
`这里我们需要先切换到master分支`
+ git checkout master
+ git merge                  之前那个分支名
+ git push origin master     最后推送上去

`如果遇到问题就是用以下语句`

```java
git pull --rebase origin master
git push -u origin master
```

	git checkout 分支名
`上传之后可以回到原来的分支，如果发现自己分支不是最新的则以下操作`

```java
git pull
git checkout 自己分支名
git merge master        //这里将主分支合并到自己分支，确保最新的代码
```


组员Git提交之后如何操作?  
`Git 组员上传代码之后肯定会上传到master，那么我们要先进入master分支pull下来`
``` java
git checkout master
git pull
git checkout 分支名
git merge master
```

---


### Git 分支 - 分支管理
```java
	 	 git branch 查看该项目的分支列表
	 	 git branch -v  查看该分支最后一次提交
	 	 git checkout 分支名   切换分支
	 	 git checkout -b 分支名  创建分支

# 在IDEA中用git提交代码时的detached HEAD问题

上次在修改项目的时候,回退到之前的版本,导致git中产生了一个新的分支,然后在提交的时候都提交到了那个新的分支中去了,所以出现了这个detached HEAD的问题

经过一番网上查资料,也解决了问题

现在mark下来

1.首先在自己的代码的目录下打开git bash

2.然后通过 git branch ,查看当前项目中的所有分支

3.先查看自己的当前分支的提交状态 git status

4.如果发现了别的分支 , 记录下那个版本号(比如我当时需要提交的分支是master,可是新创建的分支为head),记下最新提交的版本号

5.然后创建一个临时分支

$git branch temp + 上面记录下的版本号

6.然后切换到你需要提交到的分支

$git checkout master

7.将之前新增加的临时分支与你要提交的分支合并

$git merge temp

这个时候已经将临时分支的内容合并好了

8.删除临时创建的分支

$git branch -d temp

最后回去检查一下代码,就会发现解决了问题

## git rebasing , git merge 的区别

git rebase 和 git merge 一样都是用于从一个分支获取并且合并到当前分支，但是他们采取不同的工作方式，以下面的一个工作场景说明其区别

场景： 
![这里写图片描述](https://upload-images.jianshu.io/upload_images/305877-5dece524b7130343.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如图所示：你在一个feature分支进行新特性的开发，与此同时，master 分支的也有新的提交。

### merge

`git checkout feature `

`git merge master`

或者 `git merge master feature`

那么此时在feature上git 自动会产生一个新的commit(merge commit) 
look like this： 
![这里写图片描述](https://upload-images.jianshu.io/upload_images/305877-c4ddfcf679821e2f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

​``` marge 特点：自动创建一个新的commit 
如果合并的时候遇到冲突，仅需要修改后重新commit 
优点：记录了真实的commit情况，包括每个分支的详情 
缺点：因为每次merge会自动产生一个merge commit，所以在使用一些git 的GUI tools，特别是commit比较频繁时，看到分支很杂乱。
```

rebase

本质是变基 变基 变基 
变基是什么? 找公共祖先

执行以下命令：

`git checkout feature`

` git rebase master`

look like this: 
![这里写图片描述](https://upload-images.jianshu.io/upload_images/305877-467ba180733adca1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

``` rebase 特点：会合并之前的commit历史 
优点：得到更简洁的项目历史，去掉了merge commit 
缺点：如果合并出现代码问题不容易定位，因为re-write了history
```

合并时如果出现冲突需要按照如下步骤解决

修改冲突部分

```
git add
git rebase --cotinue
```

- 1
- 2

（如果第三步无效可以执行 `git rebase --skip`） 
不要在git add 之后习惯性的执行 git commit命令

The Golden Rule of Rebasing rebase的黄金法则

 never use it on public branches(不要在公共分支上使用)

比如说如下场景：如图所示 
![这里写图片描述](https://upload-images.jianshu.io/upload_images/305877-8845daa6b5fd004e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果你rebase master 到你的feature分支：

rebase 将所有master的commit移动到你的feature 的顶端。问题是：其他人还在original master上开发，由于你使用了rebase移动了master，git 会认为你的主分支的历史与其他人的有分歧，会产生冲突。

所以在执行git rebase 之前 问问自己，

会有其他人看这个分支么？

 if YES 不要采用这种带有破坏性的修改commit 历史的rebase命令 
 if NO ok，随你便，可以使用rebase 
 Summary 总结

如果你想要一个干净的，没有merge commit的线性历史树，那么你应该选择git rebase 
如果你想保留完整的历史记录，并且想要避免重写commit history的风险，你应该选择使用git merge


————————————————

创建分支： $ git branch mybranch

切换分支： $ git checkout mybranch

创建并切换分支： $ git checkout -b mybranch



对最近一次commit的进行修改：git commit -a –amend

commit之后，如果想撤销最近一次提交(即退回到上一次版本)并本地保留代码：git reset HEAD^



查看所有本地分支：git branch -a

只查看远程分支：git branch -r

查看远程连接地址：git remote show origin

查看本地分支对应的远程分支地址：git branch -vv

此时我们可以看到那些远程仓库已经不存在的分支，根据提示，使用 `git remote prune origin` 命令即可删除远程仓库不存在的分支



合并分支：`git checkout feature； git merge master 或者 git merge master feature`

删除分支： $ git branch -d mybranch

强制删除分支： $ git branch -D mybranch

列出所有分支： $ git branch

查看各个分支最后一次提交： $ git branch -v

查看哪些分支合并入当前分支： $ git branch –merged

查看哪些分支未合并入当前分支： $ git branch –no-merged

```awk
//远程仓库已删除分支，本地git branch -a还会有缓存分支信息，使用：
git remote prune origin

//删除本地分支
git branch -d/-D <分支

//删除远程分支
git push origin --delete <分支

//新建tag并推送
git tag -a <版本 -m ""
git push origin 

//查看git提交版本
git log

//回退版本
git reset --hard <版本号

//强推
git push -f

## 在本地新建一个temp分支，并将远程origin仓库的master分支代码下载到本地temp分支；
$ git fetch origin master:temp

## 比较本地代码与刚刚从远程下载下来的代码的区别；
$ git diff temp

## 合并temp分支到本地的master分支;
$ git merge temp

## 如果不想保留temp分支，删除;
$ git branch -d temp

*****************************************************************
//已有本地分支创建关联
git branch --set-upstream-to origin/远程分支名  本地分支名

##拉取指定远程分支
git checkout -b 本地分支名 origin/远程分支名

//常用基础    
git branch -a 
git branch <分支
git checkout 
git checkout -b <分支
git merge <分支
git push
git pull
```

拉下某个远程分支：git pull origin develop

更新远程库到本地： $ git fetch origin

推送分支： $ git push origin mybranch

取远程分支合并到本地： $ git merge origin/mybranch

取远程分支并分化一个新分支： $ git checkout -b mybranch origin/mybranch

删除远程分支：$ git push origin :mybranch

回滚，撤销本次修改，回到上个版本：**git checkout .**  

暂存区：git stash

回滚暂存区代码：git stash pop

查看最新的x个版本信息：git log -x

回滚到指定版本号(xxx为版本号):git reset --hard xxx

回退之后直接push会失败：git push -f

放弃修改，回到修改前版本：git reset --hard origin/$branch







# [git删除本地分支和删除远程分支](https://www.cnblogs.com/liyong888/p/9822410.html)

## 引言：

　　**注：**本人一直都是用的git bash窗口完成日常的开发工作。

　　事情是这样的，切换分支的时候命令打错了，git checkout 后面没有跟分支名，结果git status，很多delete的文件，直接冒冷汗，git add ,commit 之后发现本地与远程确实是删除了很多文件，我本地没有修改的代码，于是选择直接删除本地的分支，然后重新从远程拉分支。

## 具体操作：

　　我现在在dev20181018分支上，想删除dev20181018分支

　　1 先切换到别的分支: git checkout dev20180927

　　2 删除本地分支： git branch -d dev20181018

　　3 如果删除不了可以强制删除，git branch -D dev20181018

　　4 有必要的情况下，删除远程分支**(慎用)**：git push origin --delete dev20181018

　　5 在从公用的仓库fetch代码：git fetch origin dev20181018:dev20181018

　　6 然后切换分支即可：git checkout dev20181018

　　注：上述操作是删除个人本地和个人远程分支，如果只删除个人本地，请忽略第4步









