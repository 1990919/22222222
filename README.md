cd    进入目录
cd .. 进入父级目录
dir   当前目录文件列表 
ls    当前目录文件列表 
mkdir 创建文件夹
pwd   列出当前远端主机目录 
alt+enter 全屏
cd desktop进入桌面
reset 清屏
clear 清屏
cls   cmd清屏
touch 1.txt 创建文件
touch .gitignore 

$ git reset（回退add操作）
http://blog.csdn.net/yaoming168/article/details/38777763


```
<html>
11111111111111111
</html>
```

```
<d>
11111111111111111
</d>
```

#创建账户#创建账户#创建账户
```
$ git config --global user.email "you@example.com"
$ git config --global user.name "Your Name"
$ git config --list   查看已设配置
$ git config --get-all user.name  获得当前所有用户
```

查看文件内容
$ cat 1.txt

查看仓库状态,提示哪些文件被修改,但还没有提交
$ git status

查看修改细节, 按Q键退出
$ git diff
$ git diff HEAD -- readme.txt
此时add修改的文件后，再次git status查看仓库状态,会提示我们,将要被提交的修改包括这个文件，下一步，就可以放心地提交了

#创建版本库
进入目录,把这个目录变成git管理仓库,最好是空目录
```
$ git init 
```

提交文件需要以下两步
2.把一个文件放到Git仓库,可以多次add,可以一次添加多个，空格相隔
```
$ git add readme.txt 
$ git add file1.txt
$ git add file2.txt file3.txt
```

3.把文件提交到仓库,提交成功后,会提示 “1 file changed, 2 insertions(+)” 一个文件改动，插入两行
```
$ git commit -m "commit a readme file"  
```

#版本回退
每次commit都会有一个快照,一旦有需要,就可以从任意一个commit恢复

在Git中，用HEAD表示当前版本，，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
```
$ git reset --hard HEAD   回退到最新版本
$ git reset --hard HEAD^  上一个版本
```
还可根据版本id，执行 git rest --hard id

```
$ git log 查看提交日志
$ git log --pretty=oneline 精简日志 ，提交版本记录
```
类似一长串的码是commit id ：36fa5fb0615d7a424b8727ea68632ffe7dfbd3e7
e0c0cd85504533492bd00f7dba3c8478bfcf7496 3
6052f96ac0f4e260349da621d6d9331f7223d164 3
52fab1968e765efa5612efd9fd3019542881b41f all
34d488374a26cd99134a96b5bc20f3ac3b81eee0 rename
0486662d502127afb90ca45d5066eb05db9a1312 commit file2
6b77aba41331e7cf716a1e9215ce85beb02df3e9 commit file
38c6eb9ee2d3e010d94f1c2e91f939ddb296240b Upload Index.html
36fa5fb0615d7a424b8727ea68632ffe7dfbd3e7 new file
78aa8fe186c79e677a5646a6c40e9ce9c346f3bf Initial commit

查看当前版本
在Git中,用HEAD表示当前版本,上一个版本就是HEAD^,
上上一个版本就是HEAD^^,
当然往上100个版本写100个^比较容易数不过来，
所以写成HEAD~100
$ git reset --hard HEAD^  回退到上一个版本

此时使用git log 查看版本列表,发现最新版本消失了
如果窗口没有关闭,可以从上面找到之前版本的commit id，再次返回新版本
$ git reset --hard e0c0cd  版本号可以不用写全,能区别其他版本就行

如果窗口关了,找不到commit id
$ git reflog  查看命令记录
238f894 HEAD@{0}: reset: moving to head^
286c6a5 HEAD@{1}: reset: moving to 286c6a511279d72a0e270b385c0791c91db0390c
238f894 HEAD@{2}: reset: moving to head^
286c6a5 HEAD@{3}: commit: v.4
238f894 HEAD@{4}: commit: v.3
d0dbf2c HEAD@{5}: commit: v.2
d4ce964 HEAD@{6}: commit (initial): v.1

#工作区和暂存区
工作区：就是你在电脑里能看到的目录，比如某个文件夹就是一个工作区.
工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
![输入图片说明](http://git.oschina.net/uploads/images/2016/0921/143558_1d69ed93_1009329.png "在这里输入图片标题")

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

每次修改后都要添加到暂存区,否则提交后的不是最新内容

#撤销修改
1.$ git checkout -- readme.txt,把readme.txt文件在工作区的修改全部撤销
这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态

总之，就是让这个文件回到最近一次git commit或git add时的状态。


2.$ git reset HEAD readme.txt 把暂存区的修改撤销掉（unstage），重新放回工作区

git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。

3.如果已经提交了，就回退版本


#删除文件
1.确实要从版本库中删除该文件
$ git rm 1.txt
rm 1.txt
$ git commit -m "delete"

2.另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：
$ git checkout -- 1.txt
git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”,但只是最近一次的commit


#远程仓库

1.创建SSH Key, 会在用户主目录下，生成.ssh目录,目录下有id_rsa和id_rsa.pub这两个文件,id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
$ ssh-keygen -t rsa -C "youremail@example.com"

2.添加远程仓库,实现两个仓库同步
在git上手动创建一个空仓库, 然后进行关联 , SSH Key公钥必须在账户列表中。 
远程库的名字默认是origin
$ git remote add origin git@github.com:用户名/xxxxxxxxxxxxxx.git

3.推送到远程仓库,实际上是把当前分支master推送到远程。
$ git push -u origin master
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

$ git push origin master

#SSH警告

当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：arning: Permanently added 'github.com' (RSA) to the list of known hosts.


#从远程仓库克隆
假设一个新项目,建议：先建立远程库,再克隆到本地

$ git clone git@github.com:xxxxxxxxxx/xxxxxxxxxxxxxx.git

克隆后不要忘了cd 目录

Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。
使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。

#分支管理
每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

$ git branch 查看分支,列出所有分支，当前分支前面会标一个*号。

$ git branch dev 创建分支
$ git checkout dev 切换分支

$ git checkout -b dev 创建并切换到分支,相当于以上两步


在不同的分支上提交，工作区的内容不一样
![输入图片说明](http://git.oschina.net/uploads/images/2016/0922/114949_baeb1d62_1009329.png "在这里输入图片标题")
![输入图片说明](http://git.oschina.net/uploads/images/2016/0922/115014_99c316f0_1009329.png "在这里输入图片标题")

$ git merge dev 合并指定分支到当前分支
$ git branch -d dev 删除指定分支,不能删除当前分支

因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。


#解决分支冲突
![输入图片说明](http://git.oschina.net/uploads/images/2016/0922/133728_7ef359bd_1009329.png "在这里输入图片标题")

现在，master分支和feature1分支各自都分别有新的提交
这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突

```
$ git merge feature1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.
```
果然冲突了！Git告诉我们，readme.txt文件存在冲突，必须手动解决冲突后再提交。git status也可以告诉我们冲突的文件：

```
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:   1.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

此时, cat readme.txt,会提示具体冲突内容,Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容
```
12sa132c1x32z1c23x1z321c132
<<<<<<< HEAD
Creating a new branch is quick.
=======
22222222222
33333333
>>>>>>> fen
```

此时手动重新修改内容后,再add,commit
![输入图片说明](http://git.oschina.net/uploads/images/2016/0922/135542_5b24167d_1009329.png "在这里输入图片标题")

用带参数的git log也可以看到分支的合并情况：
```
$ git log --graph --pretty=oneline --abbrev-commit
*   f25bf20 too
|\
| * fe43376 update at fen
* | 3a1ab9b at master
|/
* 0cc405f update at dev
* e0337be add 1.txt
```

总结：当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
用git log --graph命令可以看到分支合并图。


#分支管理策略

正常合并,Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
```
$ git merge --no-ff -m "merge with no-ff" dev
```
因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。

#BUG 分支
有时候需要临时处理BUG,可是当前dev分支上,手头工作还没完成, Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：
```
$ git stash
Saved working directory and index state WIP on master: 1916672 merge with no-ff
HEAD is now at 1916672 merge with no-ff
```
此时git status查看工作区,是干净的,然后创建BUG分支,去修复BUG,完成后,切换回master合并提交,删除BUG分支.

查看“储藏”的工作现场
```
$ git stash list
stash@{0}: WIP on dev: 6224937 add merge
```

恢复工作现场

1.第一种方式 $ git stash apply 恢复后，stash内容并不删除，你需要用git stash drop来删除
2.第二种方式 $ git stash pop，恢复的同时把stash内容也删了

你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令：
```
$ git stash apply stash@{0}
```

 :angry:  但是stash  和 创建分支有什么区别
解决完master， 就会和dev冲突,还要合并


#Feature分支

添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。



如果要删除一个没有被合并过的分支，要强行删除，需要使用命令git branch -D <name>
```
$ git branch -D fenzhi1
Deleted branch fenzhi1(was 756d4af).
```


#远程仓库

当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。

要查看远程库的信息，用git remote：
```
$ git remote
origin
```

或者，用git remote -v显示更详细的信息：
```
$ git remote -v
origin  git@git.oschina.net:SUNCOM/Test.git (fetch)
origin  git@git.oschina.net:SUNCOM/Test.git (push)
```

推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：
```
$ git push origin master
```

如果要推送其他分支，比如dev，就改成：
```
$ git push origin dev
```

但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？

master分支是主分支，因此要时刻与远程同步；

dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。


#抓取分支
多人协作时，大家都会往master和dev分支上推送各自的修改。

git pull,先把最新代码抓取下来
 

#创建标签
```
$ git tag v1.0 默认标签是打在最新提交的commit上的
```

查看所有标签
```
$ git tag
v0.9
v1.0
v1.1
```

如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打,方法是找到历史提交的commit id，然后打上就可以了：
```
$ git tag v0.9 6224937edsadasc
```

注意，标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息：
```
$ git show v0.9
```

创建带有说明的标签，用-a指定标签名，-m指定说明文字：
```
$ git tag -a v0.1 -m "version 0.1 released" 3628164
```

删除标签
```
$ git tag -d v0.1
```
因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。


如果要推送某个标签到远程，使用命令git push origin <tagname>：
```
$ git push origin v1.0
```

一次性推送全部尚未推送到远程的本地标签：
```
$ git push origin --tags
```


如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除,再删除远程的：
```
$ git tag -d v0.9
$ git push origin :refs/tags/v0.9
```



#忽略特殊文件
