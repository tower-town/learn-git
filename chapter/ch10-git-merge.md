
# merge 合并分支

> 将两个或多个开发历史连接在一起
>

```bash
git merge [-n] [--stat] [--no-commit] [--squash] [--[no-]edit]
 [--no-verify] [-s <strategy>] [-X <strategy-option>] [-S[<keyid>]]
 [--[no-]allow-unrelated-histories]
 [--[no-]rerere-autoupdate] [-m <msg>] [-F <file>] [<commit>…​]
git merge (--continue | --abort | --quit)
```

| 选项 | 说明 | 示例 |
| --- | --- | --- |
| --abort | 中止当前的冲突解决过程，并尝试重建合并前的状态。 | (master)git merge dev ;git merge --abort <font color=green># 终止合并dev分支</font>|
| --continue | 继续当前的合并进程 | resolve conflict;git merge --continue <font color=green># 继续合并</font> |
| --squash(挤压) | 创建单个提交信息而非合并 |  |
| --commit | 若合并成功将执行一个提交（默认） |  |

* 在顶级当前分支之上合并分支修复和增强

```bash
git merge fixes enhancements
```

* 合并分支到当前分支中，使用`ours`的**合并策略(strategies)**

```bash
git merge -s ours <branch>
```

> merge的策略(strategies)
>
> **ort** :This is the default merge strategy when pulling or merging one branch. This strategy can only resolve two heads using a 3-way merge algorithm
>
>**ours**: This option forces conflicting hunks to be auto-resolved cleanly by favoring our version. Changes from the other tree that do not conflict with our side are reflected in the merge resul
>
>**theirs**:This is the opposite of `ours`; note that, unlike `ours`, there is no theirs merge strategy to confuse this merge option with.
>

* 合并分支不做提交说明

```bash
git merge --no--commmit <branch>
```

```bash
git status # 查看状态
git switch master
git merge <branch> # 在主分支中合并分支
# 注意：合并时可能会出现冲突，记得解决冲突
# working...
# git add .
# git commit -m "<message>"

# git branch -d <branch> #删除分支

git merge --squash test # 合并压缩，将test上的commit压缩为一条 
```
