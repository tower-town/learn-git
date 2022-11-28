# reset 回滚/重置

> 重置 HEAD 到指定状态
>
>PS: HEAD 是对存储库中某个头的引用，除非使用分离的 HEAD，在这种情况下，它直接引用任意提交。--> [git 名词库](https://git-scm.com/docs/gitglossary)
>

```bash
git reset [-q] [<tree-ish>] [--] <pathspec>..
git reset [-q] [--pathspec-from-file=<file> [--pathspec-file-nul]] [<tree-ish>]
git reset (--patch | -p) [<tree-ish>] [--] [<pathspec>…]
git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]
```

在前三种形式中，将条目从 \<tree-ish\> 复制到索引。在最后一种形式中，将当前分支头（HEAD）设置为 \<commit\>,\<tree-ish\>/\<commit\> 在所有形式中默认为 HEAD.

```bash
git reset [<mode>] [<commit>] 
```

| 模式选项 | 说明 | 示例 |
| :------: | ----- | ------ |
| --soft \<hash\> | 保留工作区的修改和索引，但撤回提交 | git reset --soft b8d8ad2 <font color=green># \<hash\>可在 git log 或者 git reflog</font>|
| --mixed \<hash\>| 重置索引但不改变工作区，即保留修改的文件，但不标记提交（默认） | git reset HEAD 或者 git reset --mixed HEAD <font color=green> # 重置提交 </font>|
| --hard \<hash\> | 重置索引和工作树，即将自提交以来的所有更改都丢弃 | git reset --hard HEAD~3 <font color=green> # 回滚至最近第三个提交之前 </font> |
| -- \<file\> | 撤销文件更改 | git reset -- frotz.c |

---------

最近的三个提交为 HEAD,HEAD^,HEAD~2

通过存储暂存区 stash，在删除暂存区的方法放弃本地修改。

```shell
git stash && git stash drop 
```

> **索引 (Index)**是您建议的下一次提交，这个概念称为 Git 的**“暂存区”(stage area)**
>
> <https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified>

|                             | HEAD | Index<br />/stage area | Workdir | WD Safe? |
| --------------------------- | ---- | :--------------------: | ------- | -------- |
| **Commit Level**            |      |                        |         |          |
| `reset --soft [commit]`     | REF  |           NO           | NO      | YES      |
| `reset [commit]`            | REF  |          YES           | NO      | YES      |
| `reset --hard [commit]`     | REF  |          YES           | YES     | **NO**   |
| `checkout <commit>`         | HEAD |          YES           | YES     | YES      |
| **File Level**              |      |                        |         |          |
| `reset [commit] <paths>`    | NO   |          YES           | NO      | YES      |
| `checkout [commit] <paths>` | NO   |          YES           | YES     | **NO**   |

* 撤销添加

```bash
edit                                     # (1)
git add frotz.c filfre.c
mailx                                    # (2)
git reset                                # (3)
git pull git://info.example.com/ nitfol  # (4)

```

* 撤销一个提交并重做

>这通常是在你记得你刚提交的内容不完整，或者你的提交信息拼错了，或者两者都是
>

```bash
git commit ...
git reset --soft HEAD^      # (1)
edit                        # (2)
git commit -a -c ORIG_HEAD  # (3)
```

* 撤销一个提交，使其成为一个主题分支

>你已经做了一些提交，但意识到它们在 "master "分支中还不成熟。你想在一个主题分支中继续完善它们，所以在当前的`HEAD`之外创建了`topic/wip`分支
>

```bash
git branch topic/wip          # (1)
git reset --hard HEAD~3       # (2)
git switch topic/wip          # (3)
```

* 永久撤销提交

```bash
git commit ...
git reset --hard HEAD~3 # (1)
```

* 撤销合并或撤销拉取

```bash
git pull
git reset --merge ORIG_HEAD 
```

* 打断工作流

> 假设您在进行大的更改时，被紧急修复 bug 的请求打断了。您的工作树中的文件还没有提交任何状态，但是您需要转到另一个分支以快速修复 bug
>

```bash
git switch feature  ;# you were working in "feature" branch and
work work work      ;# got interrupted
git commit -a -m "snapshot WIP"                 # (1)
git switch master
fix fix fix
git commit ;# commit with real log
git switch feature
git reset --soft HEAD^ ;# go back to WIP state  # (2)
git reset                                       # (3)
```

* 重置单个文件索引

```bash
git reset -- frotz.c                      # (1)
git commit -m "Commit files in index"     # (2)
git add frotz.c                           # (3)
```

* 保留工作树中的更改，同时丢弃一些先前的提交

```bash
git tag start
git switch -c branch1
edit
git commit ...                            # (1)
edit
git switch -c branch2                     # (2)
git reset --keep start                    # (3)
```

* 将提交拆分为一系列提交

```bash
$ git reset -N HEAD^                        # (1)
$ git add -p                                # (2)
$ git diff --cached                         # (3)
$ git commit -c HEAD@{1}                    # (4)
...                                         # (5)
$ git add ...                               # (6)
$ git diff --cached                         # (7)
$ git commit ...                            # (8)
```

```shell
git reset --hard FETCH_HEAD # FETCH_HEAD表示上一次成功git pull之后形成的commit点。然后git pull
```