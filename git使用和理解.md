# Git的使用和理解

## Git 初探

Git是目前世界上最先进的分布式版本控制系统，每次的增删查都有着记录。。使用Git，每次提交或保存项目状态时，Git基本上都会记录当时所有文件的外观，并存储对该快照的引用。为了提高效率，如果文件没有改变，Git不会再次存储文件，只是指向它已存储的上一个相同文件的链接。Git认为它的数据更像是一个快照流，会将数据作为项目的快照存储一段时间。可以有效、高速地处理从很小到非常大的项目版本管理。 

Git诞生于Linux的创始人，Linus使用C写了一个分布式版本控制系统。

Workspace：工作区
Index / Stage：暂存区
Repository：仓库区（或本地仓库）
Remote：远程仓库

### Git和SVN区别
SVN是集中式版本控制系统，版本库是集中放在中央服务器的，而干活的时候，用的都是自己的电脑，所以首先要从中央服务器哪里得到最新的版本，然后干活，干完后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，如果在局域网还可以，带宽够大，速度够快，如果在互联网下，如果网速慢的话，就纳闷了。

Git是分布式版本控制系统，那么它就没有中央服务器的，每个人的电脑就是一个完整的版本库，这样，工作的时候就不需要联网了，因为版本都是在自己的电脑上。既然每个人的电脑都有一个完整的版本库，那多个人如何协作呢？比如说自己在电脑上改了文件A，其他人也在电脑上改了文件A，这时，你们两之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

分布式版本控制系统安全性高，以及强大的分支管理。

### git 安装

Linux/Mac/windows git查看是否安装	
```
sudo apt-get install git
```

### git 初始化
因为Git是分布式版本控制系统，所以需要填写用户名和邮箱作为一个标识。
```
 git config --global user.name "Bioplanet"
 git config --global user.email "Bioplanet520@outlook.com"
 #查看系统设置
 git config --list
```

### 创建版本库
什么是版本库，又名仓库，英文名repository,可以理解成目录，这个目录里所有的文件都可以被Git管理起来，每个文件的修改，删除都会追踪还原。

```
#first step
mkdir gitTest
cd gitTest
pwd

#second step
git init
```
注意点：千万不要使用windows自带的笔记本来写任何文本文件，Microsoft开发的记事本在每个文件的开头添加了0xefbbbf（十六进制）的字符

### 举个例子介绍git add 和gti commit

1. 先创建一个txt的文本文档
2. 用命令git add 告诉Git，把文件添加仓库；
3. 用命令git commit -m "message" 告诉Git，把文件提交到仓库；-m 是用来填写你提交过程中加入的信息的。
```
$ git commit -m "message"
[master (root-commit) 9405497] message
 1 file changed, 2 insertions(+)
 create mode 100644 Git
git commit可以提交多个git add 的文件
```

*总结*  
git init  
git add  
git commit -m  

## git 时空穿梭
当文件被修改后，可以使用**git status**查看文件的状态
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   Git

no changes added to commit (use "git add" and/or "git commit -a")
```
但是无法看清修改了什么内容，如果要看修改了什么内容，需要使用**git diff** 命令来查看

```
git diff Git

diff --git a/Git b/Git
index d8036c1..936d069 100644
--- a/Git
+++ b/Git
@@ -1,2 +1,4 @@
 Git is a version control system.
-Git is free software.
\ No newline at end of file
+Git is free software.
+
+Git is not good.
\ No newline at end of file
```
再进行完git add之后，可以使用git status查看后面的状态，如果没有问题之后，就可以使用git commit进行提交。

### 版本回退
实际工作中，人脑无法记录全部的信息，需要在Git中使用**git log** 来查看。
```
$ git log
commit 85d264046a4501b027edf4c5fedc03a23a084d11 (HEAD -> master)
Author: QiaoWu <18235446416@139.com>
Date:   Mon Jul 3 16:28:44 2023 +0800

    changed

commit 94054979577b9ffc83cf771ccdc1973015c32e13
Author: QiaoWu <18235446416@139.com>
Date:   Mon Jul 3 16:04:28 2023 +0800

    message
```
1. 首先在git中，是<u>HEAD</u>表示当前的版本，上个版本就是<u>HEAD^</u>,上上个版本就是<u>HEAD^^</u>,如果要回到上个版本就要使用**add distributed** ,使用**git reset**命令。
```
git reset --hard  HEAD^

git log

git log --oneline --graph

#发现文件被修改了，之前的git log也不在了

git reset --hard 26c08f23 
#又恢复到了最新的版本
```

<u>HEAD</u>相当于指针，指向不同版本的方向。**git reset --hard** 忘记或者找不到commit id后，或者退出关机之后，可以使用**git reflog**来记录每次一命令。
```
git reflog

26c08f2 (HEAD -> master) HEAD@{0}: reset: moving to 26c08f23
b604ceb HEAD@{1}: reset: moving to HEAD^
26c08f2 (HEAD -> master) HEAD@{2}: commit: append GPL
b604ceb HEAD@{3}: commit: add distributed
11a0817 HEAD@{4}: commit: wrote a readme file
01b07cf HEAD@{5}: commit: wrote a readme file
85d2640 HEAD@{6}: commit: changed
9405497 HEAD@{7}: commit (initial): message

```
### 工作区或暂存区
1. 工作区(working directory)
文件所在的文件夹

2. 版本库(Repository)
工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

需要提交的文件修改通放到暂存区，然后一次性提交暂存区所有的修改。
```
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Lisence.txt

nothing added to commit but untracked files present (use "git add" to track)

```

### 管理修改而不是管理文件
Git 跟踪并管理的是修改，而不是文件。
修改后Git add 第一次然后 Git commit，再进行修改文件，使用Git status查看状态，发现并没有提交第二次修改。Git commit只负责提交暂存区的修改。

使用**git diff** 查看文件版本状态

### 撤销修改

每个人都会写错文本，但是写错了之后怎么修改呢？
修改后 使用**git status** 查看状态
```
git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")

```
注意到可以使用**git restore**<file> 去撤销修改内容。
也可以使用**git checkout** -- <file> --很重要！！去撤销内容，一个作用是撤销还没放到暂存区的内容；一个是回到git commit或git add的状态。

当已经讲内容git add之后，使用git reset HEAD <file> 可以撤销掉暂存区的内容，git reset 既可以回退版本，也可以将暂存区的修改退回到工作区，使用HEAD就是最新的commit版本。

### 删除文件
当删除一个文件后，使用git statsu查看状态
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    test.txt

no changes added to commit (use "git add" and/or "git commit -a")

```

删除后你需要将状态commit上去，如果是直接删除的文件，没有使用add 添加到暂存区，你是无法commit的。 你需要使用git add <file>，然后git commit。

也可以使用git rm <file>处理，然后使用git commit进行提交

如果删除错误的情况下，可以使用git checkout -- test.txt进行恢复，check out是用版本库里的版本替换工作区的版本，无论工作区修改还是删除，都可以一键还原，注意！！是版本库的文件。

*总结*
git status  
git diff <file>  
git log --oneline  
git reset --hard HEAD^  
git reset --hard commit号  
git reflog  
git checkout -- <file>  
git restore  
git rm  

## 远程仓库

Github网站，最好用的Git远程库
Github 添加公钥 sra public

学会使用Github，首先要注册自己的账号，由于本地Github仓库和远程的仓库之间需要SSH加密，所以要设置公钥解密。
1. 创建SSH key，在windows系统，公钥是在/C/用户/名称/.ssh
在git bash中或者在shell中输入
```
ssh-keygen -t rsa -C "youremail@example.com"
```

2. 一定注意使用的是公钥，id_rsa.pub，私钥不要泄露出去，登陆Github，打开账户设定，在SSH Key界面，点击Add SSH key，然后添加任意Title，在key文本框中粘贴id_rsa.pub文件中的内容

可以添加多个key，能够多台电脑推送
Github是免费托管的Git仓库，任何二五年都可以看到。

### 添加远程仓库
要想远程仓库能够同步本地仓库，需要在Github上添加一个运程仓库。

自行在Github上摸索，一般是create a new repo;填写基础信息;使用命令进行远程仓库和本地仓库的关联。

```
git remote add origin git@github.com:michaelliao/learngit.git
```
这个关联之后，必须有公钥才能进行传输。
origin是远程仓库的名称，是Git的默认叫法

关联之后，下一步就是推送
```
git push -u origin master

#下面是提示信息
Counting objects: 20, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (15/15), done.
Writing objects: 100% (20/20), 1.64 KiB | 560.00 KiB/s, done.
Total 20 (delta 5), reused 0 (delta 0)
remote: Resolving deltas: 100% (5/5), done.
To github.com:michaelliao/learngit.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```
由于远程库是空的，第一次推送就要加上参数-u，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

### 从远程库克隆
之前是先有本地库，然后再有远程库，关联起来。

最好的方式是先创建远程库，然后从远程库克隆。
1. 还是按照之前的方式构建远程库，最好是点击README add。这样就会创建README.md文件

2. 使用**git clone**
