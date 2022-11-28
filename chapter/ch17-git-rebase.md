
# rebase 变为基类

> 在另一个基本提示之上重新应用提交
>

```bash
usage: git rebase [-i] [options] [--exec <cmd>] [--onto <newbase> | --keep-base] [<upstream> [<branch>]]
   or: git rebase [-i] [options] [--exec <cmd>] [--onto <newbase>] --root [<branch>]
   or: git rebase --continue | --abort | --skip | --edit-todo
```

| 选项 | 说明 | 示例 |
| --- | --- | --- |
|

```shell
git rebase master   # 将master分之上超前的提交，变基到当前分支  
git rebase --onto master 169a6  # 限制回滚范围，rebase当前分支从169a6以后的提交  
git rebase --interactive # 交互模式，修改commit   
git rebase --continue    # 处理完冲突继续合并   
git rebase --skip        # 跳过   
git rebase --abort       # 取消合并
```

```bash
# 1.合并多条commit为一条
git rebase -i HEAD~3 # 合并最近三条commit

# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit

# 将pick改为squash(融合),执行后，编写合并的commit
# 注意：最好不合并远端仓库的commit
```

```bash
# 2.分支commit合并到主干，从而去除分支commit
# 2.1 使用merge
git status
git switch <branch>
# working...
git add . ;git commit -m "<message>"
git switch <master>
# working...
git add . ;git commit -m "<message>"
git merge <branch>  # 使用merge
# 可能需要提交一条记录commit
git reflog

# 对比 ： git log --graph --pretty=format:%s

# 2.2 使用rebase
git status
git switch <branch>
# working...
git add . ;git commit -m "<message>"
git switch <master>
# working...
git add . ;git commit -m "<message>"
git checkout <branch>  # 开始使用rebase (1)
git rebase <master>    # 使用rebase (2)
git checkout <master>  # 使用rebase (3)
git merge <branch>     # 使用rebase (4)

# 对比 ： git log --graph --pretty=format:%s
```

```bash
# 3. 远程commit合并
git pull # 产生分支

# 使用rebase
git fetch origin <branch>
git rebase origin/<branch>
```

```bash
# 使用rebase时注意
# 在git rebase时发生冲突（conflict）
# solving...
# git add . 
# git rebase --continue
```

# Beyond compare 快速解决冲突

* 安装 Beyond compare

* 在 git 中配置

  ```bash
  git config --local merge.tool bc3
  git config --local mergetool.path "<install_path>"
  git config --local mergetool.keepBackup false
  ```

* 应用 beyond compare 解决冲突

  ```bash
  git mergetool
  ```
