# git 的命令与流程

## 版本控制来源

* 文件拷贝
* 本地版本控制
* 集中式版本控制
* 分布式版本控制

## 特点

* Speed
* Simple design
* Strong support for non-linear development (thousands of parallel branches)
* Fully distributed
* Able to handle large projects like the Linux kernel efficiently (speed and data size)

## 语法

```shell
git [--version] [--help] [-C <path>] [-c name=value]
   [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
   [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
   [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
   <command> [<args>]
```

## 选项

```shell
add              将文件内容添加到索引
bisect           通过二进制查找引入错误的更改
branch           列出，创建或删除分支
checkout         检查分支或路径到工作树
clone            将存储库克隆到新目录中
commit           将更改记录到存储库
diff             显示提交，提交和工作树等之间的更改
fetch            从另一个存储库下载对象和引用
grep             打印匹配模式(pattern)的行
init             创建一个空的Git仓库或重新初始化一个现有的
log              显示提交日志
merge            加入两个或更多的开发历史
mv               移动或重命名文件，目录或符号链接
pull             从另一个存储库或本地分支获取并合并
push             更新远程引用以及相关对象
rebase           转发端口本地提交到更新的上游头
reset            将当前HEAD复位到指定状态
rm               从工作树和索引中删除文件
show             显示各种类型的对象
status           显示工作树状态
tag              创建，列出，删除或验证使用GPG签名的标签对象
```