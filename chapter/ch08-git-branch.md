# branch 分支

> 列出、创建或删除分支，注意区别`git submodule`命令!!
>
```bash
usage: git branch [<options>] [-r | -a] [--merged] [--no-merged]
   or: git branch [<options>] [-l] [-f] <branch-name> [<start-point>]
   or: git branch [<options>] [-r] (-d | -D) <branch-name>...
   or: git branch [<options>] (-m | -M) [<old-branch>] <new-branch>
   or: git branch [<options>] (-c | -C) [<old-branch>] <new-branch>
   or: git branch [<options>] [-r | -a] [--points-at]
   or: git branch [<options>] [-r | -a] [--format]
```

| 选项 | 说明 | 示例 |
| :---: | --- | ---- |
| -a,--all | 显示所有 (all) 分支 (默认) | git branch -all<font color=green># 默认 (即 git branch) 只显示本地分支 (绿色) </font> |
| -l \<pattern\> | 列出 (list) 指定的分支 (默认为本地分支) |  git branch --list  m* <font color=green> # 列出 m 开头的分支 </font> |
| \<branch\> | 在主干上新建分支 |  \<matser\> git branch  todo <font color=green> # 在 master 上创建 todo 分支 </font> |
| -r | 列出远程 (remotes) 分支（红色） | git branch -r -l o* <font color=green> # 列出远程以 o 开头的分支 </font> |
| -d/-D | 删除/强制删除(delete)分支 | git branch -d todo <font color=green> # 删除 todo 分支 |
| -m/-M | 移动/强制移动(move)分支 | git branch -m dev feature <font color=green> # 将 dev 命名为 feature 分支 |
| -c/-C | 复制/强制拷贝(copy)分支 | git branch -c dev release <font color=green> # 拷贝 dev 为 release 分支 |

```bash
git branch # 查看分支
git branch <branch> # 创建分支
git status # 查看状态，注意区别与原来的主干master

working ...
git add .
git commit -m "<message>"
```

```shell
git branch -v   # 查看各个分支最后一个提交对象的信息   
git branch --merge      # 查看已经合并到当前分支的分支   
git branch --no-merge   # 查看为合并到当前分支的分支
git branch --create-reflog # 创建新的 reflog
```

```shell
git branch --set-upstream dev origin/dev     # 将本地dev分支与远程dev分支之间建立链接  
git branch --set-upstream master origin/next # 手动建立追踪关系  
```

```bash
git push origin :branchName  # 删除远程分支  
git push origin --delete new # 删除远程分支new   
git remote prune origin # 远程删除了，本地还能看到远程存在，这条命令删除远程不存在的分支
```