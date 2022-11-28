
# switch/checkout 切换分支或恢复工作树文件

> switch:切换到指定分支

```bash
usage: git switch [<options>] [<branch>]

git switch <branch> 
# eg
git switch dev   # 切换到 dev 分支

git switch -c <branch> # 创建(creat)并切换分支
# eg
git switch -c todo # 创建 todo 分支并切换到 todo 分支
```

> checkout:
>切换分支或恢复工作树文件
>

```bash
usage: git checkout [<options>] <branch>
   or: git checkout [<options>] [<branch>] -- <file>...
```

| 选项 | 说明 | 示例 |
| --- | --- | --- |
| -b/-B | 创建/强制创建新分支,并切换到该分支 | git branch -b dev <font color=green> # 创建 dev 分支并切换到 dev 分支 </font> |
...

```bash
git status # 查看状态
git switch <branch> # 切换分支
```

* 以下序列检出 master 分支，将 Makefile 恢复为两个修订版本，错误地删除 hello.c，并从索引中取回它。

```bash
git checkout master             #(1)
git checkout master~2 Makefile  #(2)
rm -f hello.c
git checkout hello.c            #(3)
```

* 在错误的分支中工作后，将使用以下方法切换到正确的分支：

```bash
# However, your "wrong" branch and correct mytopic branch may differ in files that you have modified locally, in which case the above checkout would fail like this:
$ git checkout mytopic
error: You have local changes to 'frotz'; not switching branches.

# You can give the -m flag to the command, which would try a three-way merge:
$ git checkout -m mytopic
# Auto-merging frotz
```

* 当使用 -m 选项切换分支期间发生合并冲突时，您会看到如下内容：

```bash
$ git checkout -m mytopic
Auto-merging frotz
ERROR: Merge conflict in frotz
fatal: merge program failed

#Edit and resolve the conflict and mark it resolved
git diff
edit frotz
git add frotz
```

```shell
git checkout -- file  # 取消对文件的修改（从暂存区——覆盖worktree file）  
git checkout branch|tag|commit -- file_name  # 从仓库取出file覆盖当前分支   
git checkout HEAD~1 [文件]  # 将会更新 working directory 去匹配某次 commit   
git checkout -- .          # 从暂存区取出文件覆盖工作区   
git checkout -b gh-pages  0c304c9  # 这个表示 从当前分支 commit 哈希值为 0c304c9 的节点，分一个新的分支gh-pages出来，并切换到 gh-pages   
```

```shell
# 如果有的修改以及加入暂存区的话
git reset --hard 
# 还原所有修改，不会删除新增的文件
git checkout . 
# 下面命令会删除新增的文件
git clean -xdf
```

```shell
# 这种方式新建的分支(gh-pages)是没有 commit 记录的
git checkout --orphan gh-pages
# 删除新建的gh-pages分支原本的内容，如果不删除，提交将作为当前分支的第一个commit
git rm -rf .
# 查看一下状态 有可能上面一条命令，没有删除还没有提交的的文件
git state 
```