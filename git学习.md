### 介绍

git是分布式版本控制系统

集中式与分布式：集中式有一个中央服务器，需要联网进行操作。分布式，每个人都有一个版本库

#### 1. 安装git

- 下载git->安装完成后找到git bash，打开是一个命令行(说明安装成功)

- 在命令行输入以下


~~~
引号内部填自己信息
$ git config --global user.name "Your Name" 
$ git config --global user.email "email@example.com"
~~~

#### 2. 创建版本库

版本库又名仓库，英文名`repository`

### 使用

git有三个区，工作区，暂存区，版本库。工作区add之后就进入了暂存区，暂存区的文件commit之后进入版本库

#### 1. 添加  

**注：**以下文件名都带后缀

~~~
git add "文件名"
~~~

#### 2. 提交

注意：提交是将暂存区的文件都提交到版本库里

~~~
git commit -m "操作名称"
~~~

#### 3. 查看状态

~~~
git status
~~~

#### 4. 查看文件内容

~~~
cat "文件名"
~~~

#### 5. 查看git日志

~~~
git log 
~~~

如：commit后接的就是版本号，随机生成的

~~~
commit 980993de744a8886692ed79fc7f4cdd00ec15959 (HEAD -> master)
Author: zouyou <>
Date:   Sat Apr 11 14:35:04 2020 +0800

    update commit

commit ea799348f2b1ccc7d046f8bd61c6b193b79bdc18
Author: zouyou <>
Date:   Sat Apr 11 14:33:07 2020 +0800

    git tracks changes

~~~

**- 回退版本**：

1. 使用HEAD

~~~
git reset --hard HEAD^   HEAD^:上个版本  HEAD^^：上上版本
~~~

2. 使用版本号，只需要写前几个数就行

~~~
git reset --hard ea799348f 
~~~

如果忘记了版本号，可以使用reflog查看历史的变化，不管有没有回退

~~~
git reflog
~~~

#### 6. 查看文件变化

~~~
git diff
~~~

#### 7. 撤销修改

1. 撤销工作区的修改，相当于直接操作文件，将改变撤销。

~~~
git restore 文件名
~~~

2. 撤销暂存区的提交，退回到工作区，但是文件还是修改过后的，要想文件撤销修改，重复1步骤

~~~
git resore --staged 文件名
~~~

#### 8. 删除文件

1. 要同时删除工作区以及版本库，删除工作区可以手动删除等。。以下是删除版本库

~~~
git rm 文件名
~~~

2. 误删工作区文件，但是已经上传到版本库了，可以通过版本库恢复

~~~
git checkout 文件名
~~~

#### 9. 远程仓库：github

1. 在github上创建一个仓库，记住ssh码或者https地址
2. 输入以下，创建远程连接，会有输入账号密码

~~~
$ git remote add origin (ssh码)/(hhtps)
~~~

3. 将文件上传到github

~~~
$ git push -u origin master
~~~

**注：**由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

上传完成之后，只要本地进行了commit，就可以通过以下命令

~~~
git push origin master //这里与上面是差不多一样的语法
~~~

**总结：**要关联一个远程库，首先在远程创建好一个库，记住SSH码，再进行连接 ` git remote add origin ssh码`

上传：第一次上传时`git push origin -u master`，之后就不用加`-u`了 `git push origin master` 

**这些命令里面，origin其实就是远程仓库的名字，通常命名为origin**

3. 从远程仓库克隆到本地

首先在github上找到一个仓库再复制其ssh码，在git bash上输入命令行

~~~
git clone ssh码
~~~

注意：在哪个文件夹打开的git bash就克隆到哪个文件夹下面。

#### 10. 分支管理

##### 1. 分支介绍

分支可以实现类似于开发版系统，完成之后再推送到主干，就是稳定系统。如下，两个分支合并到主干

![learn-branches](https://www.liaoxuefeng.com/files/attachments/919021987875136/0)

在git中，`master`分支是主干，一开始`master`指向这根主线，`head`指向`master`，所以`head`是充当一个指向当前点的指针，可以指向主干，也可以指向分支。

![git-br-initial](https://www.liaoxuefeng.com/files/attachments/919022325462368/0)

查看分支，显示所有分支，当前分支前会有*

~~~
git branch
~~~

##### 2. 分支创建

创建一个分支`dev`并切换到此分支 `-b`的作用是创建并切换

~~~
git checkout -b dev
等价于
git branch dev  //创建分支dev
git checout dev // 切换到分支dev
~~~

**注意：**每一个分支的工作区，暂存区，版本库都是独立的，切换分支之后，都会不一样。

**Git鼓励大量使用分支：**

查看分支：`git branch`

创建分支：`git branch `

切换分支：`git checkout `或者`git switch `

创建+切换分支：`git checkout -b `或者`git switch -c `

合并某分支到当前分支：`git merge `

删除分支：`git branch -d `

查看分支图：`git log --graph`

-- **文件冲突**

![git-br-feature1](https://www.liaoxuefeng.com/files/attachments/919023000423040/0)

出现这种情况，两个分支无法merge，必须手动解决。

~~~
$ git merge feature1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.
~~~

`git status`也可以显示冲突文件，在冲突文件里打开可以看到标记。

Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容

##### 3. bug分支

当正在分支dev上进行一个工作时，突然要修复一个bug（如在主干上），所以需要先将dev正在进行的工作隐藏一下，先去把bug修复。Git还提供了一个`stash`功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：

~~~
git stash //可以将在暂存区的文件(还未提交)隐藏，使用status也看不到
~~~

可以查询stash里隐藏的东西

~~~
git stash  //=>例如：stash@{0}: WIP on dev: f52c633 add merge
~~~

修复完master的bug之后，恢复dev的现场：

~~~
git stash aplly //对现场进行恢复，此时stash里还有，需要进一步
git stash drop //对stash里的东西删除
同时还可以从stash里一步步恢复：git stash apply stash@{0}
等价于一句话
git stash pop
~~~

注：由于dev本来就是master的分支，那么dev也可能存在主干刚刚修复的bug，所以git有个功能可以实现bug的修复复制。由此可以推出，可以在分支解决bug在主干复制即可

~~~
git cherry-pick <版本号>
这里的版本好就是刚刚在主干修复bug后commit之后的版本号
~~~

开发一个新feature，最好新建一个分支，类似于bug分支；

如果要丢弃一个没有被合并过的分支，可以通过`git branch -D `强行删除。

##### 4. 远程合作

要查看远程库的信息，用

~~~
git remote //通常远程库是origin
~~~

也可以用`git remote -v`，可以返回抓取和推送的地址，如下

~~~
origin  https://github.com/zy116/first-blog.git (fetch)
origin  https://github.com/zy116/first-blog.git (push)
~~~

-- 推送分支

~~~
git push origin dev //推送分支
git push origin master //推送主干
~~~

但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？

- `master`分支是主分支，因此要时刻与远程同步；
- `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
- bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
- feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！

-- 抓取分支

通常都会在`master`和`dev`分支分别推送各自的更改，当一个人把自己的分支都推送上去之后，另一个人克隆下来的只能看到master分支，如果要在`dev`分支上开发，必须建立一个远程分支到本地

~~~
git switch -c dev origin/dev
~~~

当另一个人推送上了一个东西后，你也要推送，此时就会发生矛盾。另一个人的最新提交和你试图推送的提交有冲突。

此时会提示你进行`git pull`操作，但是会提示错误。

需要指定本地`dev`分支与远程`origin/dev`分支的链接，设置`dev`和`origin/dev`的链接

~~~
 git branch --set-upstream-to=origin dev
~~~

再进行pull

~~~
git pull
~~~

这时候pull成功，会在冲突文件里标注，需要手动解决

因此，多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin <branch>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin `推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to  origin/`。

**小结**：

- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。



---



**感谢廖雪峰大佬的教程，文中有一些都是直接copy过来的。**

[git教程](https://www.liaoxuefeng.com/wiki/896043488029600)

