
# pull 拉取

> 从另一个存储库或本地分支获取并集成
>

```bash
usage: git pull [<options>] [<repository> [<refspec>...]]
```

```text
   A---B---C master on origin
  /
    D---E---F---G master
 ^
 origin/master in your repository
```

`git pull之后`

```text
   A---B---C origin/master
  /           \
    D---E---F---G---H master
```

| 选项 | 说明 | 示例 |
| :---: | --- | --- |
| --commit | 执行合并与提交 |  |
| --all | 获取所有远端 | git pull --all <font color=green># 获取远程所有内容包括 tag </font> |
| -p,--prune | 在获取之前，修剪 (prune) 远程上不再存在的任何远程跟踪引用 |  |
| -t,--tags | 获取 tags 远端 |  |

* 更新您从中克隆的存储库的远程跟踪分支，然后将其中一个合并到您的当前分支中：

```bash
git pull
git pull origin
```

* 合并到当前分支到`next`远程分支

```bash
$ git pull origin next # 远程分支是与当前分支合并 

# 上面一条命令等同于下面两条命令   
git fetch origin  
git merge origin/next  
```

```bash
git pull origin <branch> # 从远端拉取代码到工作区
```

只能拉取 `origin`里的一个 url 地址，这个 fetch-urll  
默认为你添加的到 `origin`的第一个地址  

```shell
git pull origin master   

git pull origin next:master # 取回origin主机的next分支，与本地的master分支合并  
```

如果远程主机删除了某个分支，默认情况下，git pull 不会在拉取远程分支的时候，删除对应的本地分支。这是为了防止，由于其他人操作了远程主机，导致 git pull 不知不觉删除了本地分支。  
但是，你可以改变这个行为，加上参数 -p 就会在本地删除远程已经删除的分支。  

```shell
$ git pull -p
# 等同于下面的命令
$ git fetch --prune origin 
$ git fetch -p
```