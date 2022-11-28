
# remote 远端

> 管理设置已跟踪 (tracked) 的仓库
>

```bash
usage: git remote [-v | --verbose]
   or: git remote add [-t <branch>] [-m <master>] [-f] [--tags | --no-tags] [--mirror=<fetch|push>] <name> <url>
   or: git remote rename <old> <new>
   or: git remote remove <name>
   or: git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
   or: git remote [-v | --verbose] show [-n] <name>
   or: git remote prune [-n | --dry-run] <name>
   or: git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)...]
   or: git remote set-branches [--add] <name> <branch>...
   or: git remote get-url [--push] [--all] <name>
   or: git remote set-url [--push] <name> <newurl> [<oldurl>]
   or: git remote set-url --add <name> <newurl>
   or: git remote set-url --delete <name> <url>
```

| 选项 | 说明 | 示例 |
| :---: | --- | --- |
| add | 添加远端仓库 | git remote add origin \<url\> |
| rename | 远端仓库重命名 | git remote rename dev feature <font color=green> # 重命名 dev 为 feature  </font> | |
| remove | 移除远端仓库 | git remote remove bug <font color=green> # 删除 bug </font> ||
| set-head | 设置或删除 (-d) 默认的远端分支 | |
| set-url | 更改远程的链接 (URL) |  |
| show | 显示关于远端的信息 | git remote show origin  <font color=green># 查看指定源的全部信息 </font> |
| update | 更新远端 |  |

* Add a new remote, fetch, and check out a branch from it

```bash
$ git remote
origin
$ git branch -r
  origin/HEAD -> origin/master
  origin/master
$ git remote add staging git://git.kernel.org/.../gregkstaging.git
$ git remote
origin
staging
$ git fetch staging
...
From git://git.kernel.org/pub/scm/linux/kernel/gigregkh/staging
  * [new branch]      master     -> staging/master
  * [new branch]      staging-linus -> staginstaging-linus
 * [new branch]      staging-next -> staging/staging-next
$ git branch -r
  origin/HEAD -> origin/master
  origin/master
  staging/master
  staging/staging-linus
  staging/staging-next
$ git switch -c staging staging/master
...

```

* Imitate git clone but track only selected branches

```bash
mkdir project.git
cd project.git
git init
git remote add -f -t master -m master origin git:example.com/git.git/
git merge origin
```

```bash
git remote add origin git@github.com:JSLite/test.git #添加源 
# 默认添加在本地配置文件中(--local),即：<项目>/.git/config

# 推送3个 git
git remote add origin https://github.com/JSLite/JSLite.git  
git remote set-url --add origin https://gitlab.com/wang/JSLite.js.git  
git remote set-url --add origin https://oschina.net/wang/JSLite.js.git  

# 删除 git 的 remote 地址
git remote set-url --delete origin https://oschina.net/wang/JSLite.js.git
```

> git 是一个分布式代码管理工具，所以可以支持多个仓库，在 git 里，服务器上的仓库在本地称之为 remote。个人开发时，多源用的可能不多，但多源其实非常有用。  
>

```shell
git remote add origin1 git@github.com:yanhaijing/data.js.git  
git remote    # 显示全部源  
git remote -v # 显示全部源+详细信息   
```