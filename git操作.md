转自Git教程 - 廖雪峰的官方网站  https://www.liaoxuefeng.com/wiki/896043488029600

------

# 1、准备

##### 准备工具：notepad++,git安装包

##### 安装notepad++,git

- ###### 打开git bash

- ###### cd 命令进入到操作目录

  

  [^pwd]: 显示当前目录
  [^ls]: 显示当前目录内文件
  [^-ah]: 显示当前目录内所有文件（包括隐藏文件）




# 2、初步操作

### 全局配置：

- 设置用户名和邮箱

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

[^reset]: 清屏

1. 初始化一个Git仓库，使用git init命令：

```
git init
```

2. 添加文件到Git仓库，分两步：

```
git add <file>
```

> 注意，可反复多次使用，添加多个文件；

3. 使用以下命令提交到git仓库暂存区

```
git commit -m <message>
```



# 3、修改查看

-  修改后使用以下命令查看当前状态

```
git status 
```

- 使用以下命令可以查看修改内容

```
gif diff
```

- 
  修改后重新提交步聚：

```
git add 修改的文件名
git commit 修改的文件名
```



# 4、版本跳转

查看修改日志git log 
如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数：
git log --pretty=oneline
命令行中一大串类似1094adb...的是commit id（版本号），是一个SHA1计算出来的一个非常大的数字，用十六进制表示

版本回退：
HEAD指向的版本就是当前版本，
HEAD^就是上一个版本，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
回退上一个版本：
`$ git reset --hard HEAD^`

Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。

穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

# 5、工作区与暂存区

工作区（Working Directory）就是我们操作的目录
版本库（Repository）
工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
暂存区（stage）：
Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，
还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，
第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支master。
git commit就是往master分支上提交更改。

# 6、修改文件

每次修改，如果不用git add到暂存区，那就不会加入到commit中。
第一次修改 -> git add -> 第二次修改 -> git add -> git commit

# 7、回退上一个版本

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考
版本回退一节，不过前提是没有推送到远程库。

# 8、删除以及恢复

命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，
你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。
恢复操作：
$ git checkout -- 文件名

# 9、连接远程仓库

要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

```
git remote add origin https://github.com/prcool/git.git(仓库地址)
```

###  git push origin与git push -u origin master的区别

`$ git push origin`

上面命令表示，将当前分支推送到origin主机的对应分支。

如果当前分支只有一个追踪分支，那么主机名都可以省略。

`$ git push` 如果当前分支与多个主机存在追踪关系，那么这个时候-u选项会指定一个默认主机，这样后面就可以不加任何参数使用git push。

`$ git push -u origin master` 上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。

不带任何参数的git push，默认只推送当前分支，这叫做simple方式。此外，还有一种matching方式，会推送所有有对应的远程分支的本地分支。Git 2.0版本之前，默认采用matching方法，现在改为默认采用simple方式。



## 生成ssh公钥

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

```
ssh-keygen -t rsa -C "463852090@qq.com"
```

```
ssh-keygen -t rsa -C "463852090@qq.com"
```


在继续阅读后续内容前，请自行注册GitHub账号。由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

$ ssh-keygen -t rsa -C "youremail@example.com"
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容。
点“Add Key”，你就应该看到已经添加的Key：

第3步：新建仓库
在github中新建仓库
第4步：远程连接
`git remote add origin git@github.com:github用户名/仓库名.git`
`git remote add origin git@github.com:prcool/test.git`
`git remote add origin git@github.com:prcool/prcool.git`

git remote add origin  git@gitee.com:prcool/pro-heima.git

若为gitee码云，`git remote add origin git@gitee.com:prcool/prcool.git`

修改ssh存放地址：
/d/front end engineering/git/ssh/id_rsa
复制公钥
clip < ~/.ssh/id_rsa.pub

命令流程：
新建公钥：
ssh-keygen -t rsa -C "463852090@qq.com"
新建仓库，
远程连接：
git remote add origin git@github.com:github用户名/仓库名.git
git push -u origin master

### **命令流程：**

```
echo "# prcool" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/prcool/prcool.git
git push -u origin master
```

SSH警告
当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
这个警告只会出现一次，后面的操作就不会有任何警告了。

要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；

关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！

# 10、克隆

git clone git@github.com:prcool/test.git

git clone git@gitee.com:prcool/pr-heima.git克隆后会在本地工作区目录，新建一个文件夹，即为远程克隆的文件

如果有多个人协作开发，那么每个人各自从远程克隆一份就可以了。

你也许还注意到，GitHub给出的地址不止一个，还可以用https://github.com/michaelliao/gitskills.git这样的地址。实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。

使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。

小结
要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。

Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

# 11、分支

创建分支git branch 分支名
切换到分支 git checkout 分支名
创建并切换到分支 git branch -b 分支名
例：git checkout -b dev

查看当前分支：git branch
git branch命令会列出所有分支，当前分支前面会标一个*号。
切换回主分支： git checkout master

把分支的工作成果合并到master分支上：
git merge 分支名

git merge命令用于合并指定分支到当前分支。
合并完后可以删除分支：
git branch -d 分支名 

Git鼓励大量使用分支：

查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>

12、解决分支合并的冲突conflict

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

用git log --graph命令可以看到分支合并图。



分支策略
在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
Git分支十分强大，在团队开发中应该充分应用。

合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，
能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并

查看分支历史：
$ git log --graph --pretty=oneline --abbrev-commit


git 在pull或者合并分支的时候有时会遇到这个界面。可以不管(直接下面3,4步)，如果要输入解释的话就需要:

1.按键盘字母 i 进入insert模式

2.修改最上面那行黄色合并信息,可以不修改

3.按键盘左上角"Esc"

4.输入":wq",注意是冒号+wq,按回车键即可

# 13、bug分支

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。

首先，假如我的工作区是dev分支，现在发现master上有bug:
先在自己的工作区dev上使用命令git stash
git stash
可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：
用git status查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。
首先确定要在哪个分支上修复bug，假定需要在master分支上修复，就从master创建临时分支：
git checkout master
 git checkout -b issue-101
 修复bug，修复完后，然后提交：
 $ git add readme.txt 
$ git commit -m "fix bug 101"
修复完成后，切换到master分支，并完成合并，最后删除issue-101分支：
git checkout master
 git merge --no-ff -m "merged bug fix 101" issue-101
 现在，是时候接着回到dev分支干活了！
  git checkout dev
   git status
  工作区是干净的，刚才的工作现场存到哪去了？用git stash list命令看看：
git stash list
工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：

一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

另一种方式是用git stash pop，恢复的同时把stash内容也删了：
再用git stash list查看，就看不到任何stash内容了：
$ git stash list
你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令：

$ git stash apply stash@{0}

# 14、强行删除

开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

# 15、多人协作




要查看远程库的信息，用git remote：
$ git remote
用git remote -v显示更详细的信息：如果没有推送权限，就看不到push的地址。

推送分支：
就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：
$ git push origin master
如果要推送其他分支，比如dev，就改成：
$ git push origin dev

master分支是主分支，因此要时刻与远程同步；

dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。


因此，多人协作的工作模式通常是这样：

首先，可以试图用git push origin <branch-name>推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！

如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，
用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。


小结
查看远程库信息，使用git remote -v；

本地新建的分支如果不推送到远程，对其他人就是不可见的；

从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；

在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；

从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

注意：
git pull 失败 ,提示：fatal: refusing to merge unrelated histories

其实这个问题是因为 两个 根本不相干的 git 库， 一个是本地库， 一个是远端库， 然后本地要去推送到远端， 远端觉得这个本地库跟自己不相干， 所以告知无法合并

具体的方法， 一个种方法： 是 从远端库拉下来代码 ， 本地要加入的代码放到远端库下载到本地的库， 然后提交上去 ， 因为这样的话， 你基于的库就是远端的库， 这是一次update了

第二种方法：
使用这个强制的方法

git pull origin master --allow-unrelated-histories

后面加上 --allow-unrelated-histories ， 把两段不相干的 分支进行强行合并

后面再push就可以了 git push gitlab master:init
gitlab是别名 ， 使用

Java代码
git remote add gitlab ssh://xzh@192.168.1.91:50022/opt/gitrepo/withholdings/WithholdingTransaction

master是本地的branch名字
init是远端要推送的branch名字

本地必须要先add ，commit完了 才能推上去

关于这个问题，可以参考http://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories。

在进行git pull 时，添加一个可选项

git pull origin master --allow-unrelated-histories

# 16、rebase

小结
rebase操作可以把本地未push的分叉提交历史整理成直线；

rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

# 17、创建标签

小结
命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；

命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；

命令git tag可以查看所有标签。

在Git中打标签非常简单，首先，切换到需要打标签的分支上：

$ git branch
* dev
  master
$ git checkout master
Switched to branch 'master'
然后，敲命令git tag <name>就可以打一个新标签：

$ git tag v1.0
可以用命令git tag查看所有标签：

$ git tag
v1.0
默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？

方法是找到历史提交的commit id，然后打上就可以了：

比方说要对add merge这次提交打标签，它对应的commit id是f52c633，敲入命令：

$ git tag v0.9 f52c633
再用命令git tag查看标签：

$ git tag
v0.9
v1.0
注意，标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息：
$ git show v0.9
还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：

$ git tag -a v0.1 -m "version 0.1 released" 1094adb
用命令git show <tagname>可以看到说明文字：

$ git show v0.1

如果标签打错了，也可以删除：

$ git tag -d v0.1
因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

如果要推送某个标签到远程，使用命令git push origin <tagname>：
$ git push origin v1.0
或者，一次性推送全部尚未推送到远程的本地标签：

$ git push origin --tags
如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：

$ git tag -d v0.9
然后，从远程删除。删除命令也是push，但是格式如下：

$ git push origin :refs/tags/v0.9
要看看是否真的从远程库删除了标签，可以登陆GitHub查看。
小结
命令git push origin <tagname>可以推送一个本地标签；

命令git push origin --tags可以推送全部未推送过的本地标签；

命令git tag -d <tagname>可以删除一个本地标签；

命令git push origin :refs/tags/<tagname>可以删除一个远程标签。

# 18、使用github

小结
在GitHub上，可以任意Fork开源仓库；

自己拥有Fork后的仓库的读写权限；

可以推送pull request给官方仓库来贡献代码。

# 19、使用码云

先在码云上创建仓库

然后，我们在本地库上使用命令`git remote add`把它和Gitee的远程库关联：

```
git remote add origin git@gitee.com:liaoxuefeng/learngit.git
```

之后，就可以正常地用`git push`和`git pull`推送了！

如果在使用命令`git remote add`时报错：

```
git remote add origin git@gitee.com:liaoxuefeng/learngit.git
fatal: remote origin already exists.
```

这说明本地库已经关联了一个名叫`origin`的远程库，此时，可以先用`git remote -v`查看远程库信息：

```
git remote -v
origin	git@github.com:michaelliao/learngit.git (fetch)
origin	git@github.com:michaelliao/learngit.git (push)
```

可以看到，本地库已经关联了`origin`的远程库，并且，该远程库指向GitHub。

我们可以删除已有的GitHub远程库：

```
git remote rm origin
```

再关联Gitee的远程库（注意路径中需要填写正确的用户名）：

```
git remote add origin git@gitee.com:liaoxuefeng/learngit.git
```

此时，我们再查看远程库信息：

```
git remote -v
origin	git@gitee.com:liaoxuefeng/learngit.git (fetch)
origin	git@gitee.com:liaoxuefeng/learngit.git (push)
```

现在可以看到，origin已经被关联到Gitee的远程库了。通过`git push`命令就可以把本地库推送到Gitee上。

有的小伙伴又要问了，一个本地库能不能既关联GitHub，又关联Gitee呢？

答案是肯定的，因为git本身是分布式版本控制系统，可以同步到另外一个远程库，当然也可以同步到另外两个远程库。

使用多个远程库时，我们要注意，git给远程库起的默认名称是`origin`，如果有多个远程库，我们需要用不同的名称来标识不同的远程库。

仍然以`learngit`本地库为例，我们先删除已关联的名为`origin`的远程库：

```
git remote rm origin
```

然后，先关联GitHub的远程库：

```
git remote add github git@github.com:michaelliao/learngit.git
```

注意，远程库的名称叫`github`，不叫`origin`了。

接着，再关联Gitee的远程库：

```
git remote add gitee git@gitee.com:liaoxuefeng/learngit.git
```

同样注意，远程库的名称叫`gitee`，不叫`origin`。

现在，我们用`git remote -v`查看远程库信息，可以看到两个远程库：

```
git remote -v
gitee	git@gitee.com:liaoxuefeng/learngit.git (fetch)
gitee	git@gitee.com:liaoxuefeng/learngit.git (push)
github	git@github.com:michaelliao/learngit.git (fetch)
github	git@github.com:michaelliao/learngit.git (push)
```

如果要推送到GitHub，使用命令：

```
git push github master
```

如果要推送到Gitee，使用命令：

```
git push gitee master
```

这样一来，我们的本地库就可以同时与多个远程库互相同步：

使用多个远程库时，我们要注意，git给远程库起的默认名称是origin，如果有多个远程库，我们需要用不同的名称来标识不同的远程库。

仍然以learngit本地库为例，我们先删除已关联的名为origin的远程库：

git remote rm origin
然后，先关联GitHub的远程库：

git remote add github git@github.com:michaelliao/learngit.git
注意，远程库的名称叫github，不叫origin了。

接着，再关联码云的远程库：

git remote add gitee git@gitee.com:liaoxuefeng/learngit.git
同样注意，远程库的名称叫gitee，不叫origin。

现在，我们用git remote -v查看远程库信息，可以看到两个远程库：

git remote -v
gitee	git@gitee.com:liaoxuefeng/learngit.git (fetch)
gitee	git@gitee.com:liaoxuefeng/learngit.git (push)
github	git@github.com:michaelliao/learngit.git (fetch)
github	git@github.com:michaelliao/learngit.git (push)
如果要推送到GitHub，使用命令：

git push github master
如果要推送到码云，使用命令：

git push gitee master
这样一来，我们的本地库就可以同时与多个远程库互相同步

# 20、忽略特殊文件

忽略特殊文件
阅读: 508162
有些时候，你必须把某些文件放到Git工作目录中，但又不能提交它们，比如保存了数据库密码的配置文件啦，等等，每次git status都会显示Untracked files ...，有强迫症的童鞋心里肯定不爽。

好在Git考虑到了大家的感受，这个问题解决起来也很简单，在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：https://github.com/github/gitignore

忽略文件的原则是：

忽略操作系统自动生成的文件，比如缩略图等；
忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。
举个例子：

假设你在Windows下进行Python开发，Windows会自动在有图片的目录下生成隐藏的缩略图文件，如果有自定义目录，目录下就会有Desktop.ini文件，因此你需要忽略Windows自动生成的垃圾文件：

# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini
然后，继续忽略Python编译产生的.pyc、.pyo、dist等文件或目录：

# Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist
build
加上你自己定义的文件，最终得到一个完整的.gitignore文件，内容如下：

# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini

# Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist
build

# My configurations:
db.ini
deploy_key_rsa
最后一步就是把.gitignore也提交到Git，就完成了！当然检验.gitignore的标准是git status命令是不是说working directory clean。

使用Windows的童鞋注意了，如果你在资源管理器里新建一个.gitignore文件，它会非常弱智地提示你必须输入文件名，但是在文本编辑器里“保存”或者“另存为”就可以把文件保存为.gitignore了。

有些时候，你想添加一个文件到Git，但发现添加不了，原因是这个文件被.gitignore忽略了：

$ git add App.class
The following paths are ignored by one of your .gitignore files:
App.class
Use -f if you really want to add them.
如果你确实想添加该文件，可以用-f强制添加到Git：

$ git add -f App.class
或者你发现，可能是.gitignore写得有问题，需要找出来到底哪个规则写错了，可以用git check-ignore命令检查：

$ git check-ignore -v App.class
.gitignore:3:*.class	App.class
Git会告诉我们，.gitignore的第3行规则忽略了该文件，于是我们就可以知道应该修订哪个规则。

小结
忽略某些文件时，需要编写.gitignore；

.gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！

21、配置别名
配置别名
阅读: 254530
有没有经常敲错命令？比如git status？status这个单词真心不好记。

如果敲git st就表示git status那就简单多了，当然这种偷懒的办法我们是极力赞成的。

我们只需要敲一行命令，告诉Git，以后st就表示status：

$ git config --global alias.st status
好了，现在敲git st看看效果。

当然还有别的命令可以简写，很多人都用co表示checkout，ci表示commit，br表示branch：

$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch
以后提交就可以简写成：

$ git ci -m "bala bala bala..."
--global参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。

在撤销修改一节中，我们知道，命令git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区。既然是一个unstage操作，就可以配置一个unstage别名：

$ git config --global alias.unstage 'reset HEAD'
当你敲入命令：

$ git unstage test.py
实际上Git执行的是：

$ git reset HEAD test.py
配置一个git last，让其显示最后一次提交信息：

$ git config --global alias.last 'log -1'
这样，用git last就能显示最近一次的提交：

$ git last
commit adca45d317e6d8a4b23f9811c3d7b7f0f180bfe2
Merge: bd6ae48 291bea8
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Thu Aug 22 22:49:22 2013 +0800

    merge & fix hello.py
甚至还有人丧心病狂地把lg配置成了：

git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
来看看git lg的效果：

git-lg

为什么不早点告诉我？别激动，咱不是为了多记几个英文单词嘛！

配置文件
配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

配置文件放哪了？每个仓库的Git配置文件都放在.git/config文件中：

$ cat .git/config 
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = git@github.com:michaelliao/learngit.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
[alias]
    last = log -1
别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。

而当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中：

$ cat .gitconfig
[alias]
    co = checkout
    ci = commit
    br = branch
    st = status
[user]
    name = Your Name
    email = your@email.com
配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。

小结
给Git配置好别名，就可以输入命令时偷个懒。我们鼓励偷懒。

22、搭建git服务器
搭建Git服务器
阅读: 919546
在远程仓库一节中，我们讲了远程仓库实际上和本地仓库没啥不同，纯粹为了7x24小时开机并交换大家的修改。

GitHub就是一个免费托管开源代码的远程仓库。但是对于某些视源代码如生命的商业公司来说，既不想公开源代码，又舍不得给GitHub交保护费，那就只能自己搭建一台Git服务器作为私有仓库使用。

搭建Git服务器需要准备一台运行Linux的机器，强烈推荐用Ubuntu或Debian，这样，通过几条简单的apt命令就可以完成安装。

假设你已经有sudo权限的用户账号，下面，正式开始安装。

第一步，安装git：

$ sudo apt-get install git
第二步，创建一个git用户，用来运行git服务：

$ sudo adduser git
第三步，创建证书登录：

收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件，把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。

第四步，初始化Git仓库：

先选定一个目录作为Git仓库，假定是/srv/sample.git，在/srv目录下输入命令：

$ sudo git init --bare sample.git
Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾。然后，把owner改为git：

$ sudo chown -R git:git sample.git
第五步，禁用shell登录：

出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑/etc/passwd文件完成。找到类似下面的一行：

git:x:1001:1001:,,,:/home/git:/bin/bash
改为：

git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
这样，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出。

第六步，克隆远程仓库：

现在，可以通过git clone命令克隆远程仓库了，在各自的电脑上运行：

$ git clone git@server:/srv/sample.git
Cloning into 'sample'...
warning: You appear to have cloned an empty repository.
剩下的推送就简单了。

管理公钥
如果团队很小，把每个人的公钥收集起来放到服务器的/home/git/.ssh/authorized_keys文件里就是可行的。如果团队有几百号人，就没法这么玩了，这时，可以用Gitosis来管理公钥。

这里我们不介绍怎么玩Gitosis了，几百号人的团队基本都在500强了，相信找个高水平的Linux管理员问题不大。

管理权限
有很多不但视源代码如生命，而且视员工为窃贼的公司，会在版本控制系统里设置一套完善的权限控制，每个人是否有读写权限会精确到每个分支甚至每个目录下。因为Git是为Linux源代码托管而开发的，所以Git也继承了开源社区的精神，不支持权限控制。不过，因为Git支持钩子（hook），所以，可以在服务器端编写一系列脚本来控制提交等操作，达到权限控制的目的。Gitolite就是这个工具。

这里我们也不介绍Gitolite了，不要把有限的生命浪费到权限斗争中。

小结
搭建Git服务器非常简单，通常10分钟即可完成；

要方便管理公钥，用Gitosis；

要像SVN那样变态地控制权限，用Gitolite。

[^reset]: 

# 完整操作步骤

```cmd
echo "# git" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/prcool/git.git(仓库地址)
git push -u origin master
```

如果是gitee

请查看第19章节

