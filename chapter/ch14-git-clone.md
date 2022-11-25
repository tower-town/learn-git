
# clone 克隆

> 将存储库克隆到新目录中
>

```bash
usage: git clone [<options>] [--] <repo> [<dir>]

git clone [--template=<template_directory>]
   [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
   [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
   [--dissociate] [--separate-git-dir <git dir>]
   [--depth <depth>] [--[no-]single-branch] [--no-tags]
   [--recurse-submodules[=<pathspec>]] [--[no-]shallow-submodules]
   [--[no-]remote-submodules] [--jobs <n>] [--sparse] [--[no-]reject-shallow]
   [--filter=<filter>] [--] <repository>
   [<directory>]
```

| 选项 | 说明 |
| :---: | --- |
| -l,--local | 从本地(local)仓库克隆 |
| -s,--share | 从本地分享(share)仓库中克隆 |
| -r,--reference | 从本地引用(reference)中克隆 |
| --bare | 创建一个空仓库 |
---
`git clone --local`时，注意：此操作可以与对源存储库为硬链接的并发修改竞争，类似于在修改 src 时运行 cp -r src dst.

`git clone --share`时，注意：此时共享仓库使用软连接，删改时可能会发生为引用或`dangling`.若要`---share`仓库，同时能够使彼此不产生依赖，建议使用`git repack -a`命令重新打包仓库.

`git clone --refernce`类似`git clone --share`

* Clone from upstream:

```bash
git clone git://git.kernel.org/pub/scm/.../linux.gimy-linux
cd my-linux
make
```

* Make a local clone that borrows from the currendirectory, without checking things out:

```bash
git clone -l -s -n . ../copy
cd ../copy
git show-branch

```

* Clone from upstream while borrowing from an exist in local directory:

```bash
$ git clone --reference /git/linux.git \
  git://git.kernel.org/pub/scm/.../linux.git \
  my-linux
$ cd my-linux
```

* Create a bare repository to publish your changes to thpublic:

```bash
git clone --bare -l /home/proj/.git /pub/scm/proj.git
```

```bash
git clone git://github.com/JSLite/JSLite.js.git
git clone git://github.com/JSLite/JSLite.js.git mypro #克隆到自定义文件夹  
git clone [user@]example.com:path/to/repo.git/ #SSH协议还有另一种写法。 
```

`git clone`支持多种协议，除了HTTP(s)以外，还支持SSH、Git、本地文件协议等，下面是一些例子。`git clone <版本库的网址> <本地目录名>`  

```bash
git clone http[s]://example.com/path/to/repo.git/
git clone ssh://example.com/path/to/repo.git/
git clone git://example.com/path/to/repo.git/
git clone /opt/git/project.git 
git clone file:///opt/git/project.git
git clone ftp[s]://example.com/path/to/repo.git/
git clone rsync://example.com/path/to/repo.git/
```

```bash
# 查看远程仓库状态
git status
git branch # 注意其可能不显示分支但实际上存在分支
# git switch <branch> # 或者 git checkout <branch>
# git status 
```
