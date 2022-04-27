## Git基本使用

> 写在前面
>
> 1. git允许你随时修改commit时的编辑器 
> 方法一是在git的config文件 core里手动添加工具(目录)
> 另一种方法就是直接在控制台里直接代码 
> git config --global core.editor "'工具目录'"进行设定
> 2. 你要至少commit成功(提交新内容)一次才能创建master分支
>
> 3. 使用commit -a 来强制提交没有文件添加变化的更改
>
> 





#### 直接从结构说起

和大多数管理软件一样 你要用 首先得创立一个project

这个project里包含了你将要配置的信息和将要接入的工作流程blabla



项目创建 How？

在当前文件路径 

**git init**

会创建一个隐藏的.git文件 一个包含工作区域的项目 就创建好了

git的作用范围有工作区、暂存区和版本库  这三个区域概念

工作区(workspace) 

>  顾名思义 你的本地代码的存放区域(当然 不包括.git里面)



暂存区(Index/stage)

> 一般存放在 **.git** 目录下的 index 文件（.git/index）中
>
> 存放你的单文件临时改动区域 毕竟你保存也不会同时保存所有东西 都是按队列执行的



版本库 工作区有一个隐藏目录 **.git**，这个不算工作区，而是 Git 的版本库。

>  版本库里包含了暂存区和资源库



资源库(Repository) 在你的.git项目文件下有个HEAD文件 里面的ref(引用)记录着“主分支”



#### 分支管理

主分支是来干什么的？

> 当执行提交操作（git commit）时，暂存区的目录树写到版本库（对象库）中，master 分支会做相应的更新。即 master 指向的目录树就是提交时暂存区的目录树。
>
> 
>
> 说白了就是stage 指向 库里的一个 桥梁
>
> 
>
> 另外
>
> git的分支必须指向一个commit，没有任何commit就没有任何分支
>
> 提交第一个commit后git自动创建master分支



在创立主分支之后的次级分支

```
git branch [branch]
git branch -d [branch] //删除
```



切换分支

```
git checkout [branch]
```

> 当你切换分支的时候，Git 会同步将改分支的工作目录跟着切换
>
> 所以无需多个目录储存工作代码



合并分支

```
git merge 
```

如果遇到 两个分支中存在同名文件 不同内容的时候 git会提示你遇到了合并冲突

> ```
> CONFLICT (content): Merge conflict in runoob.php
> ```
>
> 此时 git 会暂停对冲突文件的合并 需要自己手动git add 进分支里修改
>
> 对于比较不同 用git diff固然可以 但你又不是没有自己的编辑器(



****

仓库(remote) 也是代码最终同步的目标 其实就是你代码托管的服务器

这是流程的示意图



![img](https://www.runoob.com/wp-content/uploads/2015/02/git-command.jpg)



好的 那么远程的仓库 哪里整？

github(

> Q:SSH connect refused(22 port closed by ...)
>
> 只能在.ssh的.config将sshGitHub的端口强行拉到https ssh的443
>
> 而且在与github的远程仓库沟通时 不允许使用隧道服务器



#### 常用阶段解读

那么同步流程里总结也就是这三阶段 同时github上看到的也是这么三个状态

Untracked(未跟踪) 你在工作区里面添加了文件 但是未被加入到版本库里 通过git add可以变为staged属性

****

modified(已修改) 你已在工作目录上改动了文件 	比如经典**readme.md**

staged(暂存) 你已将工作区的新改动后的所有文件放入了暂存区域	

> git add 将工作区已修改的文件 添加进暂存区
>
> git status 查看当前暂存区的文件
>
> git diff 查看暂存区与工作区的不同



committed(已提交) 已将stage里面的新版本提交到git仓库				

本地 git commit(local) 		以及远程仓库push(github)

> git commit  -m(message) "str" 代表着提交消息(注释)

最后 git服务器同步

git push [alia] [branch]



然后 你去克隆别人的 或者把你自己的 拉到新工作环境下



我要从远程仓库里面拖到本地仓库 git fetch/clone

> git clone [url] [*fileurl] (可选)

我要从远程仓库直接拉到我工作区！

>  git pull [url]



#### 还原版本

```
git reset [--soft | --mixed | --hard] [HEAD]
```

> **--mixed** 为默认，可以不用带该参数，用于重置暂存区的文件与**上一次**的提交(commit)保持一致，工作区文件内容保持不变。
>
> **--soft** 参数用于回退到某个版本
>
> **--hard** 参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本，并删除之前的所有信息提交

实用性问题

****

**忽略文件**

你不可能每次都能在工作区里面都创建好你全部需要上传的东西

无可避免的会有你不想上传的东西 总而言之 

我们需要**黑名单**(.gitignore)

 

在主目录创立.gitgnore文件

既然有黑名单 那必然有类似正则的东西

git是linux环境 那理所当然的就用上了linux的通配符

```
理所当然 #为注释
* any/ ? 0-1/ [abcA-Z] etc..
*.txt 		#后缀排除
!lib.txt 	#但单个文件之外(白名单)
/lib		#只忽略该文件夹下的文件
lib/		#只忽略该文件夹里的文件夹
lib/*.txt	#只忽略该文件夹下的指定后缀(文件 文件夹嵌套 etc..)
默认全忽略当然就直接
```



#### 新环境迁移配置

SSH key重新引入

> ssh-keygen -t rsa -C "your@email.com"

会将在你user/username下 生成`.ssh`文件夹其中包含ssh的私钥与公钥

将`.pub`的公钥重新在GitHub上添加



并在当前Git环境下重新配置

> git config --global user.name "[name]"
>
> git config --global user.email "[email]"



最后在你的本地项目文件下

重新初始化git环境

> git init

并重新配置当前的git的远程仓库etc..

> git remote add [rep_name] [git_addr]



****

#### 排障

一般由于迁移新环境引起..



手上拿的是旧版本代码 然后自己改动了 想推进仓库里 报错

>  ! [rejected]        master -> master (non-fast-forward)
> error: failed to push some refs to 'github.com:kechuan/notepad.git'
> hint: Updates were rejected because a pushed branch tip is behind its remote
> hint: counterpart. Check out this branch and integrate the remote changes
> hint: (e.g. 'git pull ...') before pushing again.
> hint: See the 'Note about fast-forwards' in 'git push --help' for details.

其中 提示 

```
Check out this branch and integrate the remote changes
hint: (e.g. 'git pull ...') before pushing again.
```

建议你去先将所有的代码通过 git pull 完全整合在一起 再去push



但是你直接git pull难道不会直接覆盖你改动后的东西？



所以git pull 分支选项有

```
git pull --rebase [name] [fetch]
```

让你从仓库中只拖下来你本地欠缺的东西



如果你还有分支合并？	建议顺手

> git fetch



最后再

> git reabase --continue



当然你也可以直接强制这样操作

> git push -f [name] [fetch]

然后本地直接强制覆盖掉仓库(当然仓库方得允许你这样做)

