
# fetch 获取

> 从另一个存储库下载对象和引用
>

```bash
usage: git fetch [<options>] [<repository> [<refspec>...]]
   or: git fetch [<options>] <group>
   or: git fetch --multiple [<options>] [(<repository> | <group>)...]     
   or: git fetch --all [<options>]
```

| 选项 | 说明 | 示例 |
| :---: | --- | --- |
| --all | 获取所有的远端 |  |
| --atomic | 原子 (atomic) 交易更新获取 |  |
| -t,--tangs | 获取所有 tags 的远端 |  |

git fetch 的输出状态

```bash
<flag> <summary> <from> -> <to> (<reason>)
```

flag:指示引用状态的单个字符

| 符号 | 说明 |
| :---: | --- |
| \<space\> | 成功快速推送 |
| + | 成功强制更新获取 |
| - | 成功修剪 (prune) 引用 |
| t | 成功更新 tag |
| * | 成功推送新引用 |
| ！ | 引用被拒绝或者失败 |
| = | 引用已为最新不需要更新 |

* 更新远程跟踪分支：

```bash
$ git fetch origin

# 上述命令从远程 refs/heads/ 命名空间复制所有分支并将它们存储到本地 refs/remotes/origin/ 命名空间，除非 branch.<name>.fetch 选项用于指定非默认 refspec。
```

* 明确使用指定仓库：

```bash
$ git fetch origin +seen:seen maint:tmp

# 本地仓库分别根据 seen 和 maint 更新 seen 和 tmp
```

* 查看远程分支，无需在本地存储库中配置远程：

```bash
git fetch git://git.kernel.org/pub/scm/git/git.git maint
git log FETCH_HEAD
```

```bash
# 上面一条命令等同于下面两条命令   
git fetch origin  # 将代码拉取到版本区
git merge origin/<branch>  # 将版本区的代码放到工作区（索引区？）
```
