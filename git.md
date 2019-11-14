# git指令学习

#### 介绍
git一些操作指令和介绍

#### 软件架构
git 学习. md文件


# 配置

一般在新的系统上，我们都需要先配置下自己的Git工作环境。配置工作只需一次，以后升级时还会沿用现在的配置。当然，如果需要，你随时可以用相同的命令修改已有的配置

## 【用户信息】
个人的用户名称和电子邮件地址
```
$ git config --global user.name "lff"
$ git config --global user.email "888888@qq.com"
```

## 【配置级别】

### git共有三个配置级别

- 　　--local【默认，高优先级】：只影响本仓库，文件为.git/config
- 　　--global【中优先级】：影响到所有当前用户的git仓库，文件为~/.gitconfig
- 　　--system【低优先级】：影响到全系统的git仓库，文件为/etc/gitconfig

## 【配置文本编辑器】

　　Git需要输入一些额外消息的时候，会自动调用一个外部文本编辑器。默认会使用操作系统指定的默认编辑器。如果有其他偏好，比如 EmEditor 的话，可以重新设置

```
$ git config --global core.editor D:/soft/EmEditor/EmEditor.exe
```

## 【配置别名】

　　Git并不会推断你输入的几个字符将会是哪条命令，不过如果想偷懒，少敲几个命令的字符，可以用 git config 为命令设置别名　　

- $ git config --global alias.co checkout
- $ git config --global alias.br branch
- $ git config --global alias.ci commit
- $ git config --global alias.st status

　　现在，如果要输入git commit只需键入git ci即可

　　使用这种技术还可以创造出新的命令，比方说取消暂存文件时的输入比较繁琐，可以自己设置一下

```
$ git config --global alias.unstage 'reset HEAD --'
```
　　这样一来，下面的两条命令完全等同

```
$ git unstage fileA
$ git reset HEAD fileA
```


## 【查看配置信息】

```
git config --list
```

## 【获取帮助】

```
 git help
```

## 学习 config 命令

```
$ git help config
``


# 取得仓库
　　有两种取得Git项目仓库的方法。第一种是在现存的目录下，通过导入所有文件来创建新的Git仓库。第二种是从已有的Git仓库克隆出一个新的镜像仓库来

## 【初始化新仓库】

　　要对现有的某个项目开始用Git管理，只需到此项目所在的目录，执行：

```
$ git init (路径/name)
```
　　初始化后，在当前目录下会出现一个名为.git的目录，所有Git需要的数据和资源都存放在这个目录中。

## 克隆仓库

```
$ git clone <repo> <directory>
```
### 克隆分支
```
git clone -b <branch> <repo>
git clone  <repo> -b <branch>
```
 -b <branch> 指定的分支名字

## 跟踪文件

```
$ git add 文件名  // 文件名
$ git add . // 所有文件
```

## 提交到仓库

```
$ git commit -m 'wrote a file'
```
-m后面输入的是本次提交的说明

## 检查当前文件状态

```
$ git status
$ git diff
$ git diff--cached
```
## 查看变化

```
$ git diff // 查看尚未暂存的文件更新了哪些部分
$ git diff--cached // 已经暂存起来的文件和上次提交时的快照之间的差异
```

## 移除文件

```
git rm a.txt
git rm -f a.txt  // 该文件就不再纳入版本管理了,强制删除
git rm --cached a.txt // 从暂存区域移除)，但仍然希望保留在当前工作目录中
```


以下代码会递归删除当前目录及其子目录中所有 ~ 结尾的文件

```
$ git rm \*~
```
　　以下代码会删除所有被跟踪，但在工作目录被删除的文件

```
$ git rm $(git ls-files --deleted)
```

## 移动文件

```
$ git mv file_from file_to // 在Git中对文件改名，可以这么做
```

## 查看提交历史

```
git clone <repo> // 退出：英文状态下按Q
```
不用任何参数的话，git log会按提交时间列出所有的更新，最近的更新排在最上面

### git log有许多选项，下表列出了一些常用的选项及其释义
```
选项 　　　　　　　　说明
-p    　　　　　　 按补丁格式显示每个更新之间的差异
--word-diff       按 word diff 格式显示差异
--stat    　　　   显示每次更新的文件修改统计信息
--shortstat       只显示 --stat 中最后的行数修改添加移除统计
--name-only       仅在提交信息后显示已修改的文件清单
--name-status     显示新增、修改、删除的文件清单
--abbrev-commit   仅显示 SHA-1 的前几个字符，而非所有的 40 个字符
--relative-date   使用较短的相对时间显示(比如，“2 weeks ago”)
--graph    　　　　显示 ASCII 图形表示的分支合并历史
--pretty    　　　 使用其他格式显示历史提交信息可用的选项包括oneline，short，full，fuller 和format(后跟指定格式)
--oneline        `--pretty=oneline --abbrev-commit` 的简化用法

选项    　　　　　　　　  说明
-(n)    　　　　　　　　 仅显示最近的 n 条提交
--since, --after      仅显示指定时间之后的提交
--until, --before     仅显示指定时间之前的提交
--author    　　　　　　仅显示指定作者相关的提交
--committer    　　　　仅显示指定提交者相关的提交
```

```
git clone -p -2 // -p选项展开显示每次提交的内容差异，用-2则仅显示最近的两次更新
git clone -U1 --word-diff // 单词层面的对比  上下文(context)行数从默认的3行，减为1行，那么可以使用-U1选项

$ git log --pretty=oneline 简单用法
$ git log --since=2.weeks // 按照时间作限制的选项，比如--since和--until
```
## 使用图形化工具查阅提交历史

```
gitk // 图形化工具
```

## 撤销操作

### 修改最后一次提交

有时候我们提交完了才发现漏掉了几个文件没有加，或者提交信息写错了。想要撤消刚才的提交操作，可以使用--amend选项重新提交：

```
$ git commit --amend
```

此命令将使用当前的暂存区域快照提交如果刚才提交完没有作任何改动，直接运行此命令的话，相当于有机会重新编辑提交说明，但将要提交的文件快照和之前的一样
    如果刚才提交时忘了暂存某些修改，可以先补上暂存操作，然后再运行 --amend 提交：

```
$ git commit -m 'initial commit'
$ git add new_file
$ git commit --amend
```
　　上面的三条命令最终只是产生一个提交，第二个提交命令修正了第一个的提交内容

### git 放弃本地修改


**未使用 git add 跟踪缓存代码时**
 ```
$ git checkout -- filepathname // 放弃单个文件修改
$ git checkout . // 放弃所有文件修改

(刚新建的文件还没已有加入到 git 的管理系统中，自己手动删除就好了)
```

**使用 git add 跟踪缓存代码时**
 ```
$ git reset HEAD filepathname 
$ git checkout -- filepathname 

(此命令用来清除 git  对于文件修改的缓存，相当于撤销 git add 命令所在的工作。在使用本命令后，本地的修改并不会消失，而是回到了如（一）所示的状态。继续用（一）中的操作，就可以放弃本地的修改。)
```
**用 git commit提交了代码**

```
$ git reset --hard HEAD^ // 回退上一次commit 状态

(此命令可以用来回退到任意版本：git reset --hard  commitid 
你可以使用 git log 命令来查看git的提交历史。git log 的输出如下,之一这里可以看到第一行就是 commitid：
commit cf0d692e982d8e372a07aaa6901c395eec73e356 (HEAD -> master)
Author: toyflivver <2440659688@qq.com>
Date: Thu Sep 28 14:07:14 2017 +0800
可以看出现在的状态在 commitid 为 cf0d692e982d8e372a07aaa6901c395eec73e356 的提交上（有 HEAD -> master 标记）。
如果在此之间有其他人提交过代码，必须执行一次
git pull  拉取最新)
```

###  【总结】

　　当文件被提交后(git commit)，就无法撤销了，只能使用--amend命令来修改提交说明，或增加要提交的文件

　　当文件被提交前，如果想恢复文件内容，如果文件处于暂存区(stage)，则需要先使用git reset HEAD <file>的方式取消暂存，然后再使用git checkout -- <file>的方式来恢复文件内容


## 版本切换
```
$ git log // 从近到远查看提交日志
$ git reset --hard HEAD^ // 回退到上一个版本，^^两个箭头就表示上上个版本，依次类推
$ git reset --hard 3628164 // 回退到指定版本号
$ git reflog // 查看最近几次提交记录的版本号

在某些情况下，比如说因为某些原因，我从2.0版本回退到了1.0版本，这个操作可以通过git reset --hard HEAD^命令实现，但是这时我又想回到2.0版本怎么办呢？这时候去查看git log命令，发现最新的版本是1.0，git log查看的是提交历史，似乎是没有什么办法回到2.0版本了。答案是 git reflog命令，该命令可以查看命令历史，可以通过找到2.0的版本号，再通过git reset --hard回到2.0版本。
```
## 使用远程仓库

### 查看当前的远程库

```
git remote // 也可以加上 -v 选项(v为--verbose的简写，中文意思是冗长的)，显示对应的克隆地址：
git remote -v
```

### 添加远程仓库

```
$ git remote add [shortname] [SSH地址]
$ git remote add origin [SSH地址]
```

### 删除远程仓库关联

```
git remote rm [shortname]
```

### 从远程仓库抓取数据

```
$ git fetch [remote-name]
```
　　此命令会到远程仓库中拉取所有你本地仓库中还没有的数据。运行完成后，你就可以在本地访问该远程仓库中的所有分支，将其中某个分支合并到本地，或者只是取出某个分支，一探究竟
　　如果克隆了一个仓库，此命令会自动将远程仓库归于origin名下。所以，git fetch origin会抓取从你上次克隆以来别人上传到此远程仓库中的所有更新(或是上次fetch以来别人提交的更新)。有一点很重要，**fetch命令只是将远端的数据拉到本地仓库**，并不自动合并到当前工作分支，只有当你确实准备好了，才能手工合并
　　如果设置了某个分支用于跟踪某个远端仓库的分支，可以使用git pull命令自动抓取数据下来，然后将远端分支自动合并到本地仓库中当前分支。在日常工作中我们经常这么用，既快且好。实际上，默认情况下git clone命令本质上就是自动创建了本地的master分支用于跟踪远程仓库中的master分支(假设远程仓库确实有master分支)。所以一般我们运行git pull，目的都是要从原始克隆的远端仓库中抓取数据后，合并到工作目录中的当前分支

### 推送数据到远程仓库

```
git push [remote-name] [branch-name]
```
*克隆操作会自动使用默认的master和origin名字*

### 查看远程仓库信息

```
git remote show [remote-name]
```

### 远程仓库的删除和重命名
```
$ git remote rename pb paul
$ git remote rm paul
```

## 忽略某些文件

.gitignore的文件，列出要忽略的文件模式

```
# 此为注释 – 将被 Git 忽略
# 忽略所有 .a 结尾的文件
*.a
# 但 lib.a 除外
!lib.a
# 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
/TODO
# 忽略 build/ 目录下的所有文件
build/
# 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
doc/*.txt
# ignore all .txt files in the doc/ directory
doc/**/*.txt
```

# 分支
　　Git中的分支，其实本质上仅仅是个指向commit对象的可变指针。Git会使用master作为分支的默认名字。在若干次提交后，其实已经有了一个指向最后一次提交对象的master分支，它在每次提交的时候都会自动向前移动

## 查看分支
```
$ git branch
$ git branch -v // 查看各个分支最后一个提交对象的信息
$ git branch --merged // 查看已合并的分支
$ git branch --no-merged // 查看尚未合并的分支
$ git branch -r // 查看远程分支
$  git branch -a // 查看所有分支（远程和本地）
```

## 创建分支
```
$ git branch dev // 新建 testing 分支
$ git checkout dev // 切换到 testing 分支
$ git checkout -b dev // 新建 iss53 分支并切换过来
```

## 删除分支

```
git branch -d dev // 删除本地分支 dev
git branch -D dev // 强制删除本地分支 dev
```

## 合并分支
```
git merge dev // 合并分支dev到当前分支 git merge --no-ff -m "merged bug fix 101" dev
git rebase master // git rebase [主分支] [特性分支] 当前分支衍合到master
```
## 保存现场
```
git stash
git stash apply // 恢复，但是恢复后，stash内容并不删除
git stash apply stash@{0} // 恢复到指定的stash
git stash drop // 删除
git stash pop // 恢复的同时把stash内容也删了
git stash list // 查看
```

## 新建的本地分支push到远程服务器
```
 git push origin 本地名字:外地名字
```
 ## 删除远程分支
 ```
 git push origin :分支
```

## 关联

```
git push --set-upstream origin dev // 分支dev关联 master
```

#  理论
git commit -m用于提交暂存区的文件，git commit -am用于提交跟踪过的文件

　　***[注意]git commit -am可以写成git commit -a -m，但不能写成git commit -m -a***

　　定义中出现了暂存区、跟踪过的文件等术语，如果要理解它们，就需要了解Git的文件状态变化周期

首次创建的新文件（此时出去未跟踪）需要通过 git add 命令进行跟踪；
内容变化时，
直接使用 *git commit -am* 进行提交（文件已被跟踪）
或者使用 *git add 和 git commit -m* 进行提交

## 总结
　　**这两个命令的区别的关键就是git add命令**

　　git add命令是个多功能命令，根据目标文件的状态不同，此命令的效果也不同：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等

　　我们需要用git add命令来跟踪新文件，但如果使用git commit -am可以省略使用git add命令将已跟踪文件放到暂存区的功能



# ssh 查看公钥，生成公钥
## 何谓公钥
1. 很多服务器都是需要认证的，ssh认证是其中的一种。在客户端生成公钥，把生成的公钥添加到服务器，你以后连接服务器就不用每次都输入用户名和密码了。
2. 很多git服务器都是用ssh认证方式，你需要把你生成的公钥发送给代码仓库管理员，让他给你添加到服务器上，你就可以通过ssh自由地拉取和提交代码了。

## 查看 ssh 公钥
1. 打开你的 git bash 窗口
2. 进入 .ssh 目录：cd ~/.ssh
3. 输入ls指令，找到 .pub后缀文件
4. 查看公钥：cat id_rsa.pub 或者 vim id_rsa.pub

*直接打开你用户（一般都是 C:\Users\Administrator\.ssh）下的 .ssh 文件夹，打开它里面的 .pub后最 文件*

## 生成公钥
1. 如果通过上面的方式找不到公钥，你就需要先生成公钥了：ssh-keygen（邮件地址换成自己的邮件地址）
```
$ ssh-keygen -t rsa -C "注册邮箱"
```
2. 接着会确认存放公钥的地址，默认就是上面说的路径，直接enter键确认
3. 接着会要求输入密码和确认密码，如果不想设置密码直接不输入内容 按enter键

*删除 rm -r .ssh/*

## 公钥添加到服务器
1. 接下来，登陆GitHub，打开“Settings”，“SSH Keys”页面
2. 然后，点“New SSH Key”，填上任意Title，在Key文本框里粘贴.pub后缀文件的内容
3. 点击"Add SSH key"按钮后，添加成功。

> 为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送
　　当然，GitHub允许你添加多个Key。假定你有若干电脑，一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了
　　在GitHub上托管的Git仓库，任何人都可以看到，但是只有你自己才能修改。所以，不要把敏感信息放进去

## 添加远程库
1. 点击右上角'+'号弹出的'New repository'
2. 输入仓库名称Repository name为'test'，仓库介绍Description为'test'，点击'Create repository'按钮，即可添加成功

> 添加成功后，在GitHub上的这个'xx'仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库


 ssh -T git@github.com  测试公匙



# 配置
## $ git config  Git 相关配置

```
$ git config --global user.name "match"
$ git config --global user.email "121631835@qq.com"
$ git config --global core.editor D:/soft/EmEditor/EmEditor.exe
$ git config --global alias.co checkout

$ git help <command>  获取帮助，也可以写成$ git <command> --help
$ git help config
```

# 基本操作
## 【初始化】
```
$ git init  初始化仓库
$ git init ~/git-server --bare  将当前的仓库初始化为一个裸仓库，裸仓库的意思是没有工作目录。中央服务器并不需要工作目录，它是一个被动的接收作用，如果有工作目录的话，反而会造成错乱
```
## 【增加】
```
$ git add <file> 跟踪新文件，或者把已跟踪的文件放到暂存区
$ git add .  批量跟踪所有工作目录下未被跟踪的文件
```
## 【删除】
```
$ git rm --cached <file> 仅从暂存区删除
$ git rm <file> 从暂存区和工作目录删除
$ git rm \*~　递归删除当前目录及其子目录中所有 ~ 结尾的文件
$ git rm $(git ls-files --deleted)  删除所有被跟踪，但在工作目录被删除的文件
```
## 【提交】
```
$ git commit  把文件提交到仓库，这种方式会启动文本编辑器以便输入本次提交的说明
$ git commit -m 'wrote a file'  -m参数后跟提交说明的方式，在一行命令中提交更新
$ git commit -am 'wrote a file'  把所有已经跟踪过的文件暂存起来一并提交
```

## 【查看】
```
　　$ git status  检查当前文件状态
　　$ git diff  查看工作目录与暂存区的差异
　　$ git diff --cached  查看暂存区与某次提交的差异，默认为HEAD
　　$ git diff id1 id2  查看两次提交之间的差异
　　$ git log  查看提交历史，git log有许多选项，下表列出了一些常用的选项及其释义
```
选项 　　　　　　　　说明
-p    　　　　　　  按补丁格式显示每个更新之间的差异
--word-diff       按 word diff 格式显示差异
--stat    　　　   显示每次更新的文件修改统计信息
--shortstat       只显示 --stat 中最后的行数修改添加移除统计
--name-only       仅在提交信息后显示已修改的文件清单
--name-status     显示新增、修改、删除的文件清单
--abbrev-commit   仅显示 SHA-1 的前几个字符，而非所有的 40 个字符
--relative-date   使用较短的相对时间显示(比如，“2 weeks ago”)
--graph    　　　　显示 ASCII 图形表示的分支合并历史
--pretty    　　　 使用其他格式显示历史提交信息可用的选项包括oneline，short，full，fuller 和format(后跟指定格式)
--oneline        `--pretty=oneline --abbrev-commit` 的简化用法

## 【撤销】
```
　　$ git commit --amend  修改最后一次提交，可以添加漏掉的文件，或者重写提交信息
　　$ git reset HEAD <file>  取消暂存
　　$ git checkout -- <file>  恢复文件内容
　　$ git checkout HEAD -- <file>  取消暂存，并恢复文件内容
```

# 分支操作
## 【查看】
```
　　$ git branch 列出所示分支，当前分支前面会标一个*号
　　$ git branch -v 查看各分支最后一个提交对象的信息
　　$ git branch -a 查看各分支情况，包括远程分支
　　$ git branch --merged 查看哪些分支被并入当前分支
　　$ git branch --no-merged 查看哪些分支没有被并入当前分支
　　$ git cat-file -t  <git对象> 查看Git对象的类型，主要的git对象包括tree、commit、parent和blob等
　　$ git cat-file -p  <git对象> 查看Git对象的内容
```

## 【新建】
```
　　$ git branch <branchName> 新建分支
```

## 【删除】
```
　　$ git branch -d <branchName> 删除分支
　　$ git branch -D <branchName> 强制删除分支，用于删除没有合并过的分支
```

## 【切换】
```
　　$ git checkout <branchName>  用于分支切换，将HEAD移动到目标分支，并将工作目录中的文件换成目标分支所指向的快照内容
　　$ git checkout -b <branchName> 创建新分支并将HEAD移动到该目标分支
　　$ git checkout -  将HEAD移动到上一分支
```

## 【合并】

```
　　$ git merge <branchName> 将目标分支合并到当前分支
　　$ git merge --no-ff -m "commit描述" <branchName> 合并分支，强制禁用Fast forward快进模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去
　　$ git log --graph 查看分支合并情况
```

【衍合(rebase)】
```
　　衍合是按照每行的修改次序重演一遍修改，而合并是把最终结果合在一起
　　$ git rebase master 把当前分支的改变移到master分支里重放一遍
　　$ git rebase --onto master server client 取出client分支，找出client分支和server分支的共同祖先之后的变化，然后把它们在master上重演一遍
```

## 【保存现场】
```
　　$ git stash 保存目录的工作目录和暂存区状态，并返回到干净的工作空间
　　$ git stash save "push to stash area" 保存目录的工作目录和暂存区状态，返回到干净的工作空间，并保存"push to stash area"信息
　　$ git stash list 查看stash栈中保存的记录列表
　　$ git stash apply stash@{0} 将stash栈中保存的stash@{0}内容重新恢复到工作目录中
　　$ git stash drop stash@{0} 删除stash栈中保存的stash@{0}内容
　　$ git stash pop 相当于apply和drop的合体，它将stash栈中最顶端的记录取出到工作目录中，这也意味着包含删除stash栈中对应内容的操作
```

# 版本切换
## 【回退】
```
　　$ git reset --mixed <commit> (默认)将当前分支回退到历史某个版本，提交的内容会复制到暂存区
　　$ git reset --hard <commit> 将当前分支回退到历史某个版本，提交的内容会复制到暂存区和工作目录
　　$ git reset --soft <commit> 将当前分支回退到历史某个版本，工作目录和暂存区不会在任何变化
```

## 【查看】
```
　　$ git reflog 按照之前经过的所有的commit路径按序来排列，用来记录每一次命令
```

# 远程操作
## 【查看】
```
　　$ git remote  查看当前配置有哪些远程仓库
　　$ git remote -v  (v为--verbose的简写，中文意思是冗长的)，显示远程仓库对应的克隆地址
　　$ git remote show origin  查看远程仓库origin详细信息
```

## 【关联】
## 【关联仓库地址】

当代码库远程迁移后，修改本地代码关联的远程地址
```
    git remote set-url origin 新仓库地址
　　$ git remote add [shortname] [url]  添加一个新的远程仓库，可指定一个名字，以便引用，一般为origin
　　$ git remote rename pb paul  将远程库的名称从pb改为paul
　　$ git remote rm [shortname]  取消对该远程库的关联
```

## 【获取】
```
　　$ git clone <address> Git会自动将此远程仓库命名为origin，并下载其中所有的数据，建立一个指向它的master分支的指针，在本地命名为origin/master
　　$ git fetch origin 同步远程服务器origin上master分支的数据到本地的master分支
　　$ git fetch origin <branchName> 获取远程服务器origin上<branchName>分支的数据到本地的<branchName>分支
　　$ git merge origin/master 使用fetch命令，只是将origin的数据下载到了本地，但本地的工作目录只有使用merge合并，才能更新为最新的内容
　　$ git pull origin <branchName> 相当于fetch和merge命令的合体

## 【跟踪远程分支】
　　$ git checkout -b serverfix origin/serverfix 把远程分支serverfix的内容合并到当前分支serverfix。这会切换到新建的serverfix本地分支，其内容同远程分支origin/serverfix一致，这样就可以在里面继续开发了
　　$ git checkout --track origin/serverfix 用--track选项简化$ git checkout -b serverfix origin/serverfix命令
　　$ git checkout -b a1 origin/a2 把远程分支a2的内容合并到当前分支a1

## 【推送】
　　$ git push origin <branchName> 取出在本地的<branchName>分支，推送到远程仓库的<branchName>分支
　　$ git push origin serverfix:somebranch 取出在本地的serverfix分支，推送到远程仓库的somebranch分支
```

## 【删除】
```
　　$ git push origin :serverfix 在服务器上删除serverfix分支
```

# 标签管理
## 【新建】
```
　　$ git tag <tagname>  新建一个轻量级标签，默认为HEAD
　　$ git tag <tagname> <commit id>  为指定的commit ID新建一个轻量级标签
　　$ git tag -a <tagname> -m <标签信息>  新建一个带有标签信息的附注标签
```

## 【签名】
```
　　$ git tag -s <tagname> -m <标签信息>  新建一个GPG签名标签
　　$ git tag -v <tagname>  验证一个GPG签名标签
```

## 【查看】
```
　　$ git tag 查看所有标签
　　$ git show <tagname>  查看标签详细信息
```

## 【删除】
```
　　$ git tag -d <tagname>  删除本地标签
　　$ git push origin :refs/tags/<tagname>  删除远程标签
```

## 【推送】
```
　　$ git push origin <tagname>  推送标签到远端仓库
　　$ git push origin --tags  一次性推送全部尚未推送到远程的本地标签
```

# 解决冲突
## stash
```
$ git stash
$ git pull
$ git stash pop
```
接下来diff一下此文件看看自动合并的情况，并作出相应的修改。
git stash：备份当前的工作区，从最近一次提交中读取相关内容，让工作区保持和上一次提交的内容一致。同时，将工作区的内容保存到git栈中。
git pull: 从远程仓库拉取内容更新合并到本地。
git stash pop：从git栈中读取最近一次保存的内容，恢复工作区的相关内容。由于可能存在多个stash的内容，所以用栈来管理，pop会从最近一个stash中读取内容并恢复到工作区。

## git 放弃本地修改


**未使用 git add 跟踪缓存代码时**
 ```
$ git checkout -- filepathname // 放弃单个文件修改
$ git checkout . // 放弃所有文件修改

(刚新建的文件还没已有加入到 git 的管理系统中，自己手动删除就好了)
```

**使用 git add 跟踪缓存代码时**
 ```
$ git reset HEAD filepathname
$ git checkout -- filepathname

(此命令用来清除 git  对于文件修改的缓存，相当于撤销 git add 命令所在的工作。在使用本命令后，本地的修改并不会消失，而是回到了如（一）所示的状态。继续用（一）中的操作，就可以放弃本地的修改。)
```
**用 git commit提交了代码**

```
$ git reset --hard HEAD^ // 回退上一次commit 状态

(此命令可以用来回退到任意版本：git reset --hard  commitid 
你可以使用 git log 命令来查看git的提交历史。git log 的输出如下,之一这里可以看到第一行就是 commitid：
commit cf0d692e982d8e372a07aaa6901c395eec73e356 (HEAD -> master)
Author: toyflivver <2440659688@qq.com>
Date: Thu Sep 28 14:07:14 2017 +0800
可以看出现在的状态在 commitid 为 cf0d692e982d8e372a07aaa6901c395eec73e356 的提交上（有 HEAD -> master 标记）。
如果在此之间有其他人提交过代码，必须执行一次
git pull  拉取最新)
```


#  码云

报错Incorrect username or password ( access token )
使用码云将仓库clone到本地，报错信息如下：

D:\123>git clone https://gitee.com/ycyzharry/helloworld.git
Cloning into 'helloworld'...
remote: Incorrect username or password ( access token )
fatal: Authentication failed for 'https://gitee.com/ycyzharry/helloworld.git/'

后面继续clone时候以为会弹出登录窗口，结果直接提示用户名或密码错误。
解决办法：
打开电脑的控制面板–>用户账户–>凭据管理器
找到普通凭据git:https://gitee.com这一栏，选择编辑，填入正确的用户名和密码，最后点击保存即可。





















