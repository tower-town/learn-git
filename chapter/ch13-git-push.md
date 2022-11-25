
# push 推送

> 更新远程引用以及关联的对象
>

```bash
usage: git push [<options>] [<repository> [<refspec>...]]

git push [--all | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>]
    [--repo=<repository>] [-f | --force] [-d | --delete] [--prune] [-v | --verbose]
    [-u | --set-upstream] [-o <string> | --push-option=<string>]
    [--[no-]signed|--signed=(true|false|if-asked)]
    [--force-with-lease[=<refname>[:<expect>]] [--force-if-includes]]
    [--no-verify] [<repository> [<refspec>…]]
```

> ps: \<repository\>:远程仓库的目的地 ； \<refspec\>:repositoty
specify 指定的仓库
>

| 选项 | 说明 | 示例 |
| :---: | --- | --- |
| --all | 推送所有分支到远端仓库 | git push --all origin master |
| --prune | 删除没有本地副本的远程分支 |  |
| -d | 所有列出的引用都从远程存储库中删除(delete) |  |
| --tag | 除了明确列出的仓库之外，refs/tags 下的所有 refs 都会被推送 |  |
| -f | 强制(force)推送更新并覆盖原有的仓库，非必要不建议使用 | git push --force origin master  <font color=green># 强制推送master，建议使用 git push origin +master <font> |
| -u | 设置默认上传(set-upstream)分支 | git push -u origin master <font color=green># 设置默认上传(tracked)分支为master <font> |

远端的配置地址的格式：

* $GIT_DIR/config

```bash
 [remote "<name>"]
  url = <url>
  pushurl = <pushurl>
  push = <refspec>
  fetch = <refspec>
```

* $GIT_DIR/remotes

```bash
  URL: one of the above URL format
 Push: <refspec>
 Pull: <refspec>
```

* $GIT_DIR/branches

```bash
<url>#<head>
```

> \<url\> is required; #\<head\> is optional.
>

```bash
git push origin <branch>  
```

git pull的输出状态

```bash
<flag> <summary> <from> -> <to> (<reason>)
```

flag:指示引用状态的单个字符

| 符号 | 说明 |
| :---: | --- |
| \<space\> | 成功快速推送 |
| + | 成功强制更新 |
| - | 成功删除引用 |
| * | 成功推送新引用 |
| ！ | 引用被拒绝或者失败 |
| = | 引用已为最新不需要更新 |

```bash
git push # 推送当前分支到远端

git push origin HEAD # 一种将当前分支推送到远端上相同名称的便捷方法

git push origin HEAD:master # 将当前分支推送到源存储库中的远程 ref 匹配 master。这种形式方便推送当前分支，无需考虑其本地名称。

git push origin master:refs/heads/experimental # 通过复制 master 分支，以在远端创建 experimental 分支

git push origin +dev:master # ...
```

```shell
git reset --hard HEAD~1 # 撤销一条记录   
git push -f origin HEAD:master # 同步到远程仓库  
```
