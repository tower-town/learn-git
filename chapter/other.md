
## **问题**

###### 解决 git bash 终端显示中文乱码

要注意的是，这样设置后，你的`git bash`终端也要设置成中文和`utf-8`编码，才能正确显示中文。

在`git bash`的界面中右击空白处，弹出菜单，选择`选项->文本->本地Locale`，设置为`zh_CN`，而字符集选框选为`UTF-8`。

英文显示则是：
`Options->Text->Locale`改为`zh_CN`，`Character set`改为`UTF-8`

###### 通过修改配置文件来解决中文乱码

如果你的 git bash 终端没有菜单选项显示，还可以通过直接修改配置文件的方式来解决中文乱码问题。

进入 git 的安装目录

编辑`etc\gitconfig`文件，也有些 windows 系统是存放在`%homepath%\.gitconfig`路径或`安装盘符:ProgramFiles\Git\mingw64\etc\gitconfig`，在文件末尾增加以下内容：

```text
[gui]  
    encoding = utf-8  
    # 代码库统一使用utf-8  
[i18n]  
    commitencoding = utf-8  
    # log编码  
[svn]  
    pathnameencoding = utf-8  
    # 支持中文路径  
[core]
    quotepath = false 
    # status引用路径不再是八进制（反过来说就是允许显示中文了）
```

编辑`etc\git-completion.bash`文件，在文件末尾增加以下内容：

```text
# 让 ls 命令能够正常显示中文
alias ls='ls --show-control-chars --color=auto' 
```

编辑`.\etc\inputrc`文件，修改`output-meta`和`convert-meta`

属性值：

```text
set output-meta on  # bash 可以正常输入中文  
set convert-meta off  
```

编辑`.\etc\profile`文件，在文件末尾添加如下内容：

```text
export LESSHARESET=utf-8
```

## 报错问题解决

**1. `git fatal: protocol error: bad line length character: No s`**

解决办法：更换 remote 地址为 `http/https` 的  

**2. `The requested URL returned error: 403 Forbidden while accessing`**

解决 github push 错误的办法：

```shell
#vim 编辑器打开 当前项目中的config文件
vim .git/config

#修改
[remote "origin"]  
    url = https://github.com/jaywcjlove/example.git  

#为下面代码
[remote "origin"]  
    url = https://jaywcjlove@github.com/jaywcjlove/example.git  
```

**3. git status 显示中文问题**

在查看状态的时候 git status 如果是中文就显示下面的情况

```shell
\344\272\247\345\223\201\351\234\200\346\261\202
```

解决这个问题方法是：

```shell
git config --global core.quotepath false
```

## 配置

首先是配置帐号信息 `ssh -T git@github.com` 测试。

```bash
git config --help # 获取帮助信息，查看修改个人信息的参数
```

### 配置的个人信息

* 项目配置文件：<项目>/.git/config

```bash
git config --local user.name "your name"          
git config --local user.email "you@exmaple.com"  
git config --list         # 查看配置的信息  
```

* 全局配置文件：~/.gitconfig

```shell
git config --global user.name "your name"           # 修改全局名字
git config --global user.email "you@exmaple.com"  # 修改全局邮箱
```

* 系统配置文件：/etc/.gitconfig

```bash
# 注意：需要root/管理员权限
git config --system user.name "your name"          
git config --system user.email "you@exmaple.com"  
```

### 配置自动换行

自动转换坑太大，提交到 git 是自动将换行符转换为 lf

```shell
git config --global core.autocrlf input
```

### 配置 SSH

#### 创建 SSH 密钥

这个密钥用来跟 github 通信，在本地终端里生成然后上传到 github

```shell
ssh-keygen -t rsa -C 'wowohoo@qq.com' # 生成密钥  
ssh-keygen -t rsa -C "wowohoo@qq.com" -f ~/.ssh/ww_rsa # 指定生成目录文件名字
ssh -T git@github.com # 测试是否成功  
```

#### 多账号 ssh 配置

**1.生成指定名字的密钥**

`ssh-keygen -t rsa -C "邮箱地址" -f ~/.ssh/jslite_rsa`  
会生成 `jslite_rsa` 和 `jslite_rsa.pub` 这两个文件  

**2.密钥复制到托管平台上**

`vim ~/.ssh/jslite_rsa.pub`
打开公钥文件 `jslite_rsa.pub` ，并把内容复制至代码托管平台上

**3.修改 config 文件**

`vim ~/.ssh/config`#修改 config 文件，如果没有创建建 `config`  

```shell
Host jslite.github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/jslite_rsa

Host work.github.com
  HostName github.com
  # Port 服务器open-ssh端口（默认：22,默认时一般不写此行）
  # PreferredAuthentications 配置登录时用什么权限认证 
  #                          publickey|password publickey|keyboard-interactive等
  User git
  IdentityFile ~/.ssh/work_rsa
```

* `Host` 这里是个别名可以随便命名
* `HostName` 一般是网站如：`git@ss.github.com:username/repo.git` 填写 `github.com`
* `User` 通常填写`git`
* `IdentityFile` 使用的公钥文件地址

**4.测试**

```shell
ssh -T git@jslite.github.com  # `@`后面跟上定义的Host  
ssh -T work.github.com        # 通过别名测试
ssh -i ~/公钥文件地址 Host别名  # 如 ssh -i ~/.ssh/work_rsa work.github.com
```

**5.使用**

```shell
# 原来的写法
git clone git@github.com:<jslite的用户名>/learngit.git
# 现在的写法
git clone git@jslite.github.com:<jslite的用户名>/learngit.git
git clone git@work.github.com:<work的用户名>/learngit.git
```

**6.注意**

如果你修改了 id_rsa 的名字，你需要将 ssh key 添加到 SSH agent 中，如：

```shell
ssh-add ~/.ssh/jslite_rsa
ssh-add -l  # 查看所有的key
ssh-add -D  # 删除所有的key
ssh-add -d  ~/.ssh/jslite_rsa # 删除指定的key
```

### 免密码登录

* https 协议下提交代码免密码

```shell
git clone https://github.com/username/rep.git
```

通过上面方式克隆可能需要密码，解决办法：进入当前克隆的项目 `vi rep/.git/config` 编辑 `config`, 按照下面方式修改，你就可以提交代码不用输入密码了。

```shell
[core]
 repositoryformatversion = 0
 filemode = true
 bare = false
 logallrefupdates = true
 ignorecase = true
 precomposeunicode = true
[remote "origin"]
- url = https://github.com/username/rep.git
+ url = https://用户名:密码@github.com/username/rep.git
 fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
 remote = origin
 merge = refs/heads/master
```

* SSH 免密登录

```bash
# 1.生成公钥和私钥(默认在 ~/.ssh/)
ssh-keygen -r rsa
# 公钥：id_rsa.pub ，私钥： id_rsa

# 2. 拷贝公钥内容，并设置到GitHub：settings --> "SSH and GPG key" --> key

# 3.在git本地配置ssh地址
git remote add origin <SSH_url>

# 4.以后使用
git push origin <branch>
```

* git 自动管理凭证

* 登录远程服务器

```shell
ssh-keygen -t rsa -P '' -f ~/.ssh/aliyunserver.key
ssh-copy-id -i ~/.ssh/aliyunserver.key.pub root@192.168.182.112 # 这里需要输入密码一次
```

编辑 `~/.ssh/config`

```shell
Host aliyun1
  HostName 192.168.182.112
  User root
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/aliyunserver.key
```

上面配置完了，可以通过命令登录，不需要输入 IP 地址和密码 `ssh aliyun1`

### 合并多个 commit

```shell
# 这个命令，将最近4个commit合并为1个，HEAD代表当前版本。
# 将进入VIM界面，你可以修改提交信息。
git rebase -i HEAD~4 
# 可以看到其中分为两个部分，上方未注释的部分是填写要执行的指令，
# 而下方注释的部分则是指令的提示说明。指令部分中由前方的命令名称、commit hash 和 commit message 组成
# 当前我们只要知道 pick 和 squash 这两个命令即可。
# --> pick 的意思是要会执行这个 commit
# --> squash 的意思是这个 commit 会被合并到前一个commit

# 我们将 需要保留的 这个 commit 前方的命令改成 squash 或 s，然后输入:wq以保存并退出
# 这是我们会看到 commit message 的编辑界面

# 其中, 非注释部分就是两次的 commit message, 你要做的就是将这两个修改成新的 commit message。
# 
# 输入wq保存并推出, 再次输入git log查看 commit 历史信息，你会发现这两个 commit 已经合并了。
# 将修改强制推送到前端
git push -f origin master
```

### 修改远程 Commit 记录

```shell
git commit --amend
# amend只能修改没有提交到线上的，最后一次commit记录
git rebase -i HEAD~3
# 表示要修改当前版本的倒数第三次状态
# 将要更改的记录行首单词 pick 改为 edit
pick 96dc3f9 doc: Update quick-start.md
pick f1cce8a test(Transition):Add transition test (#47)
pick 6293516 feat(Divider): Add Divider component.
# Rebase eeb03a4..6293516 onto eeb03a4 (3 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
```

保存并退出，会弹出下面提示

```shell
# You can amend the commit now, with
# 
#   git commit --amend
# 
# Once you are satisfied with your changes, run
# 
#   git rebase --continue

# 通过这条命令进入编辑页面更改commit，保存退出
git commit --amend
# 保存退出确认修改，继续执行 rebase, 
git rebase --continue
# 如果修改多条记录反复执行上面两条命令直到完成所有修改

# 最后，确保别人没有提交进行push，最好不要加 -f 强制推送
git push -f origin master
```

### 同步 fork 的上游仓库

[Github 教程同步 fork 教程](https://help.github.com/articles/syncing-a-fork/)，[在 Github 上同步一个分支 (fork)](http://www.miss77.net/549.html)  

**设置添加多个远程仓库地址。**

在同步之前，需要创建一个远程点指向上游仓库 (repo).如果你已经派生了一个原始仓库，可以按照如下方法做。

**同步更新仓库内容**

同步上游仓库到你的仓库需要执行两步：首先你需要从远程拉去，之后你需要合并你希望的分支到你的本地副本分支。从上游的存储库中提取分支以及各自的提交内容。 `master` 将被存储在本地分支机构 `upstream/master`

```shell
git fetch upstream
```

检查你的 fork's 本地 `master` 分支

```shell
git checkout master
# Switched to branch 'master'
```

合并来自 `upstream/master`的更改到本地 master  分支上。这使你的前 fork'ss `master` 分支与上游资源库同步，而不会丢失你本地修改。  

```shell
git merge upstream/master
# Updating a422352..5fdff0f
# Fast-forward
#  README                    |    9 -------
#  README.md                 |    7 ++++++
#  2 files changed, 7 insertions(+), 9 deletions(-)
#  delete mode 100644 README
#  create mode 100644 README.md
```

**2.命令行中运行代码**

OLD_EMAIL 原来的邮箱  
CORRECT_NAME 更正的名字  
CORRECT_EMAIL 更正的邮箱  

将下面代码复制放到命令行中执行

```shell
git filter-branch -f --env-filter '
OLD_EMAIL="wowohoo@qq.com"
CORRECT_NAME="小弟调调"
CORRECT_EMAIL="更正的邮箱@qq.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

执行过程

```shell
Rewrite 160d4df2689ff6df3820563bfd13b5f1fb9ba832 (479/508) (16 seconds passed, remaining 0 predicted)
Ref 'refs/heads/dev' was rewritten
Ref 'refs/heads/master' was rewritten
```

**3.同步到远程仓库**

同步到 push 远程 git 仓库

```shell
git push --force --tags origin 'refs/heads/*'
```

我还遇到了如下面错误，lab 默认给 master 分支加了保护，不允许强制覆盖。`Project(项目)`->`Setting`->`Repository` 菜单下面的`Protected branches`把 master 的保护去掉就可以了。修改完之后，建议把 master 的保护再加回来，毕竟强推不是件好事。

```shell
remote: GitLab: You are not allowed to force push code to a protected branch on this project.
```

当上面的 push 不上去的时候，先 `git pull` 确保最新代码

```shell
git pull  --allow-unrelated-histories
# 或者指定分枝
git pull origin master --allow-unrelated-histories
```

### 查看某个文件历史

```shell
git log --pretty=oneline 文件名  # 列出文件的所有改动历史  
git show c178bf49   # 某次的改动的修改记录  
git log -p c178bf49 # 某次的改动的修改记录  
git blame 文件名     # 显示文件的每一行是在那个版本最后修改。  
git whatchanged 文件名  # 显示某个文件的每个版本提交信息：提交日期，提交人员，版本号，提交备注（没有修改细节）  
```

### 打造自己的 git 命令

```shell
git config --global alias.st status
git config --global alias.br branch
git config --global alias.co checkout
git config --global alias.ci commit
```

配置好后再输入 git 命令的时候就不用再输入一大段了，例如我们要查看状态，只需：

```shell
git st
```

### 中文乱码的解决方案

```shell
git config --global core.quotepath false
```

## 本地

### rm

```shell
rm *&git rm *          # 移除文件  
git rm -f *            # 移除文件  
git rm --cached *      # 取消跟踪  
git mv file_from file_to  # 重命名跟踪文件  
git log   # 查看提交记录  
```

### revert

```shell
git revert HEAD   # 撤销前一次操作   
git revert HEAD~  # 撤销前前一次操作   
git revert commit # 撤销指定操作   
```

### diff

```shell
git diff file     # 查看指定文件的差异   
git diff --stat   # 查看简单的diff结果   
git diff  # 比较Worktree和Index之间的差异   
git diff --cached   # 比较Index和HEAD之间的差异   
git diff HEAD       # 比较Worktree和HEAD之间的差异   
git diff branch     # 比较Worktree和branch之间的差异   
git diff branch1 branch2  # 比较两次分支之间的差异   
git diff commit commit    # 比较两次提交之间的差异   
git diff master..test   # 上面这条命令只显示两个分支间的差异  
git diff master...test    # 你想找出‘master’,‘test’的共有 父分支和'test'分支之间的差异，你用3个‘.'来取代前面的两个'.'  
```

### stash

```shell
git stash # 将工作区现场（已跟踪文件）储藏起来，等以后恢复后继续工作。   
git stash list  # 查看保存的工作现场   
git stash apply # 恢复工作现场   
git stash drop  # 删除stash内容   
git stash pop   # 恢复的同时直接删除stash内容   
git stash apply stash@{0} # 恢复指定的工作现场，当你保存了不只一份工作现场时。   
```

### cherry-pick

```shell
git cherry-pick commit    # 拣选合并，将commit合并到当前分支   
git cherry-pick -n commit # 拣选多个提交，合并完后可以继续拣选下一个提交   
```

### 拉取

`git fetch -p` #拉取远程分支时，自动清理 远程分支已删除，本地还存在的对应同名分支。  

### 分支合并

```shell
git merge branchName      # 合并分支 - 将分支branchName和当前所在分支合并   
git merge origin/master   # 在本地分支上合并远程分支。   
git rebase origin/master  # 在本地分支上合并远程分支。   
git merge test            # 将test分支合并到当前分支   
```

## 远端

```shell
git fetch <远程主机名> <分支名>   # fetch取回所有分支（branch）的更新  
git fetch origin remotebranch[:localbranch]   #  从远端拉去分支[到本地指定分支]   
git merge origin/branch   # 合并远端上指定分支   
git pull origin remotebranch:localbranch  #  拉去远端分支到本地分支   
git push origin branch    # 将当前分支，推送到远端上指定分支   
git push origin localbranch:remotebranch  # 推送本地指定分支，到远端上指定分支   
git push origin :remotebranch   # 删除远端指定分支   
git checkout -b [--track] test origin/dev # 基于远端dev分支，新建本地test分支[同时设置跟踪]  
```

## submodule

克隆项目同时克隆 submodule

```shell
git clone https://github.com/jaywcjlove/handbook.git --depth=1 --recurse-submodules
```

克隆项目，之后再手动克隆 submodule 子项目

```shell
git submodule add --force '仓库地址' '路径'
# 其中，仓库地址是指子模块仓库地址，路径指将子模块放置在当前工程下的路径。
# 注意：路径不能以 / 结尾（会造成修改不生效）、不能是现有工程已有的目录（不能順利 Clone）
git submodule init # 初始化submodule
git submodule update # 更新submodule(必须在根目录执行命令)
git submodule update --init --recursive  # 下载的工程带有submodule
```

当使用`git clone`下来的工程中带有 submodule 时，初始的时候，submodule 的内容并不会自动下载下来的，此时，只需执行如下命令：

```shell
git submodule foreach git pull  # submodule 里有其他的 submodule 一次更新
git submodule foreach git pull origin master # submodule更新

git submodule foreach --recursive git submodule init
git submodule foreach --recursive git submodule update
```


## 删除文件

```shell
git rm -rf node_modules/
```

## 日志 log

## 重写历史

```shell
  
```