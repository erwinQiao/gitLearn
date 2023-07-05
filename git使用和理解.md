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

Git下载官网 https://git-scm.com/downloads
```
sudo apt-get install git
```
git windows安装好之后，在文件中点右键就会出现Git bash here和Git GUI here，先选择Git bash here，使用命令行进行操作。

### git 初始化
因为Git是分布式版本控制系统，所以需要填写用户名和邮箱作为一个标识。
```
 git config --global user.name "QiaoWu"
 git config --global user.email "18235446416@139.com"
 
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

1.先创建一个gitTest.txt的文本文档

txt中内容写的如下
```
Git is a version control system.
Git is free software.
```

2.用命令git add 告诉Git，把文件添加仓库；
```
git add gitTest.txt
```
3.用命令**git commit -m "message"** 告诉Git，把文件提交到仓库；-m 是用来填写你提交过程中加入的信息的。

```
git commit -m "wrote a readme file"

#显示信息
[master (root-commit) 9405497] message
 1 file changed, 2 insertions(+)
 create mode 100644 Git

#git commit可以提交多个git add 的文件
```

*总结*  
git init  
git add  
git commit -m  

## git 时空穿梭
当文件被修改后，可以使用**git status**查看文件的状态
Git is a distributed version control system.
Git is free software.
```
git status

#显示信息
#前面第一部分是远端仓库的提示信息，暂时不用看
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)

#这一部分是主要的变化
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitTest.txt

no changes added to commit (use "git add" and/or "git commit -a")

```
但是无法看清修改了什么内容，如果要看修改了什么内容，需要使用**git diff** 命令来查看

```
git diff gitTest.txt

diff --git a/gitTest.txt b/gitTest.txt
index d8036c1..013b5bc 100644
--- a/gitTest.txt
+++ b/gitTest.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
\ No newline at end of file
```

再进行完**git add**之后，可以使用**git status**查看后面的状态，如果没有问题之后，就可以使用**git commit  -m "add distributed"**进行提交。

### 版本回退
实际工作中，人脑无法记录全部的信息，需要在Git中使用**git log** 来查看。
```
git log 

commit 91d786a30acb5c0e615fef0cacc9707b2c516913 (HEAD -> master, origin/master)
Author: QiaoWu <18235446416@139.com>
Date:   Wed Jul 5 11:01:42 2023 +0800

    add distributed

commit e673bbbaa063900f47f47390cef43641c4a0e85e
Author: QiaoWu <18235446416@139.com>
Date:   Wed Jul 5 10:54:52 2023 +0800

    wrote a readme file

commit 36732e2c80e515590d47838438198e85545c6820
Author: QiaoWu <18235446416@139.com>
Date:   Wed Jul 5 10:47:30 2023 +0800

    gitTest.text

```
1.首先在git中，是<u>HEAD</u>表示当前的版本，上个版本就是<u>HEAD^</u>,上上个版本就是<u>HEAD^^</u>,如果要回到上个版本就要使用 ,**git reset**命令。通过查看commit的信息内容，找到前面的索引码，复制几位就可以了
```
git reset --hard  HEAD^

git log

git log --oneline --graph

#发现文件被修改了，之前的git log也不在了

git reset --hard e673bbbaa0 
#又恢复到了最新的版本
```

<u>HEAD</u>相当于指针，指向不同版本的方向。**git reset --hard** 忘记或者找不到commit id后，或者退出关机之后，可以使用**git reflog**来记录每次一命令。
```
git reflog

26c08f2 (HEAD -> master) HEAD@91d786a HEAD@{0}: commit: add distributed
e673bbb HEAD@{1}: commit: wrote a readme file
36732e2 HEAD@{2}: commit: gitTest.text

```
### 工作区或暂存区
1.工作区(working directory)
文件所在的文件夹

2.版本库(Repository)
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

使用**git diff <file>** 查看文件版本状态

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
也可以使用**git checkout** -- \<file> --很重要！！去撤销内容，一个作用是撤销还没放到暂存区的内容；一个是回到git commit或git add的状态。

当已经讲内容git add之后，使用git reset HEAD \<file> 可以撤销掉暂存区的内容，git reset 既可以回退版本，也可以将暂存区的修改退回到工作区，使用HEAD就是最新的commit版本。

### 删除文件
当删除一个文件后，使用git statsu查看状态
```
git status

On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    test.txt

no changes added to commit (use "git add" and/or "git commit -a")

```

删除后你需要将状态commit上去，如果是直接删除的文件，没有使用add 添加到暂存区，你是无法commit的。 你需要使用**git add \<file>**，然后**git commit**。

也可以使用**git rm \<file>**处理，然后使用**git commit**进行提交

如果删除错误的情况下，可以使用**git checkout -- gitTest.txt**进行恢复，check out是用版本库里的版本替换工作区的版本，无论工作区修改还是删除，都可以一键还原，注意！！是版本库的文件。

*总结*
git status  
git diff \<file>  
git log --oneline  
git reset --hard HEAD^  
git reset --hard commit号  
git reflog  
git checkout -- \<file>  
git restore  
git rm  

## 远程仓库

Github网站，最好用的Git远程库
Github 添加公钥 sra public

学会使用Github，首先要注册自己的账号，由于本地Github仓库和远程的仓库之间需要SSH加密，所以要设置公钥解密。

1.创建SSH key，在windows系统，公钥是在/C/用户/名称/.ssh
在git bash中或者在shell中输入
```
ssh-keygen -t rsa -C "youremail@example.com"
```

2.一定注意使用的是公钥，id_rsa.pub，私钥不要泄露出去，登陆Github，打开账户设定，在SSH Key界面，点击Add SSH key，然后添加任意Title，在key文本框中粘贴id_rsa.pub文件中的内容

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
1.还是按照之前的方式构建远程库，最好是点击README add。这样就会创建README.md文件

2.使用**git clone**
```
git clone git@github.com:michaelliao/gitskills.git

#进程信息
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
Receiving objects: 100% (3/3), done.
```

注意信息：GitHub给出的地址不止一个，还可以用https://github.com/michaelliao/gitskills.git这样的地址。实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。

使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。

## 分支管理
现在到了Github 另外一个强大功能的介绍--分支管理。分支管理就像是平行宇宙，两个互不干扰，只有最后合并的时候才会并入一起。

创建分支后，master继续运行，你在dev分支上去写不干扰master，然后瞬间合并，是非常神奇的事情。

### 创建与合并分支

时间线就是一条分支，master分支是一条线，Git用master指向最新的提交，再用<u>HEAD</u>指向master，就能确定当前分支，以及当前分支的提交点。

当我们创建分支，例如 <u>dev</u>,就会创建一个新的指针，创建的时候是和master一样的位置，但是HEAD指向dev，文件是没有任何变化的。

在完成之后，合并的原理就是讲master指向dev当前的提交，就完成了合并，HEAD指向master，dev就可以删除，剩下master主线。

下面是基础的分支构建合并步骤
1.创建分支dev，然后切换HEAD到dev分支
```
git checkout -b dev

#提示信息
Switched to a new branch 'dev'
```
git checkout -b dev相当于命令的集合，是下面两条命令

```
git branch dev
git checkout dev
Switched to branch 'dev'
```

```
#用来查看分支信息
git branch

#*表示当前的分支
* dev
  master
```

切换好dev分支后，在gitTest.txt文档中加入Creating a new branch is quick.这句话，然后按照上面的步骤，add，commit。

```
git checkout master

Switched to branch 'master'
Your branch is up to date with 'origin/master'.

```
切换到master后发现没有新添加的文本，然后合并dev和master
```
git merge dev

#信息提示
Merge made by the 'ort' strategy.
 gitTest.txt | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)
```

删除分支
```
git branch -d dev
```
swtch命令
创建新的分支然后切换到新的用switch更加习惯
```
git switch -c dev
```
*总结*
git branch  
git checkout -b dev  
git switch -c dev  
git branch \<name>  
git checkout \<name>或者git switch \<name>
git branch -d \<name>  

### 解决冲突问题
冲突问题是git里面最麻烦的一个问题，往往只能通过修改文件来解决，无法使用命令来解决。

```
git switch -c feature1
```
在gitTset.txt文本中添加Creating a new branch is quick AND simple.然后add，commit -m "AND simple".

切换到master
```
git switch master
git checkout master
```
在gitTset.txt文本中添加Creating a new branch is quick & simple.然后add，commit -m "& simple".

```
git merge feature1

#错误信息
Auto-merging gitTest.txt
CONFLICT (content): Merge conflict in gitTest.txt
Automatic merge failed; fix conflicts and then commit the result.
```
在同时修改了文件之后，应为两个分支平行处理，导致HEAD无法合并，只能试图把各自修改的合并起来。
```
git status

#提示信息
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   gitTest.txt

no changes added to commit (use "git add" and/or "git commit -a")

```
提醒冲突，并且给了修改建议，下面是gitTest.txt的文本内容
```
Git is a distributed version control system.
Git is free software.

Creating a new branch is quick.
Creating a new branch is quick.
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======

Creating a new branch is quick AND simple.
>>>>>>> feature1

```
在修改文稿后Creating a new branch is quick and simple.再add,commit提交
相当于将文稿修改 然后在master中合并
```
git log --graph --oneline --abbrev-commit

#查看分支
*   72e4727 (HEAD -> master) conflict fixed!
|\
| * b1684f0 (feature1) AND simple
* | b9afced & simple

```

最后删除分支即可完成工作
```
git branch -d feature1
```

### 分支管理策略
为了防止Fast forward模式，在知县删除后看不到log，可以使用--no-ff参数进行合并。

实际上master是稳定的，干活都在dev上，dev是不稳定的，是用来发行测试版本的。分支管理的本质逻辑就是master下，dev，然后每个人在dev下再进行修改，尤其是在团队合作下。

### Bug分支
不管软件开发，还是文件处理中，Bug是常有的，开出分支来修复。

举例，当你接到一个修复代码101的bug任务，自然的你想创建一个分支issue-101来修复它，但是，当前dev上的工作还没有完成提交，工作一半没法提交，只能先搁置，怎么处理？

1.Git提供了stash功能

```
git stash
Saved working directory and index state WIP on dev: 0367d9b Merge branch 'dev'

git status
#显示是干净的工作区
```

2.首先要确定是哪个分支上修复Bug，你需要切换到分支创建临时分支，比如master上
```
git checkout  master
git switch -c issue-101

```

3.修改完成后，git add；git commit
```
git switch master
git merge --no-ff -m "merged bug fix 101" issue-101

Merge made by the 'ort' strategy.
 gitTest.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

```
4.最后删除分支issue-101

5.切换到dev分支，查看stash
```
git stash list

stash@{0}: WIP on dev: 0367d9b Merge branch 'dev'
```
恢复的方式两种一种是git stash apply,恢复后stash不删除，需要gitstash drop手动删除；一种是git stash pop，恢复的时候stash也删除了。
```
git stash pop

#提示内容
On branch dev
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitTest.txt

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (ee4c19bcd6ab6cc3c4c8c89600d268a8085cd13d)

```

git stash apply stash@{0} 用来恢复指定内容