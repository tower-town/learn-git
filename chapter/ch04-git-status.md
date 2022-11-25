
# status 获取状态

> 显示仓库的工作目录的状态

```bash
git status [<options>…​] [--] [<pathspec>…​]
```

| 选项 | 说明 |
| :--: | --- |
|  -b | 显示<branch>的跟踪(tracking)信息 |
| -s | 显示简短状态信息 |
| --long | 显示详细状态信息（默认） |

显示简短状态信息的全称，即：`git status -b`

```bash
' ' = unmodified（未修改）

M = modified （已修改）

T = file type changed (文件类型改变)

A = added （添加）

D = deleted （被删除）

R = renamed （重命名）

C = copied (if config option status.renames is set to "copies")

U = updated but unmerged （更新但未合并）
```

```bash
# git status -h
git status #获取状态  #解决git status不能显示中文 -> 问题
# 红色：新增文件/修改的文件 -> git add <file>
# 绿色：git 管理的文件 -> git commit -m '<message>'
# 生成版本
```

* git 的区域划分

  > <font color=blue>工作区（work directory）</font>：跟踪tracked、<font color=red>新增</font>    <font color=green># 跟踪(tracked) -(自动)-> 新增</font>
  >
  > <font color=blue>暂存区(stage area)</font>：     <font color=green># <font color=blue>工作区</font>:<font color=red>新增</font> --(add )–> <font color=green>暂存区</font></font>
  >
  ><font color=blue>版本区(repository)</font>：     <font color=green># <font color=green>暂存区</font> --(commit )–> <font color=green>版本区</font></font>

## 解决git status不能显示中文

现象：:`git status`查看有改动但未提交的文件时总只显示数字串，显示不出中文文件名，非常不方便。如下图：

原因：在默认设置下，中文文件名在工作区状态输出，中文名不能正确显示，而是显示为[八进制](https://www.zhihu.com/search?q=八进制&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A133706032})的字符编码。

解决办法：

将git配置文件 `core.quotepath`项设置为`false`。`quotepath`表示引用路径，加上`--global`表示全局配置

`git bash`终端输入命令：

```text
git config --global core.quotepath false
```
