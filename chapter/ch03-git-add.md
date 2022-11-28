# add 添加

> 将内容添加到索引 (索引 (index)：工作树的储存版本)
>
> PS: [git 的名词库](https://git-scm.com/docs/gitglossary)

```bash
git add [<options>] [--] <pathspec>...
```

| 选项 | 说明 |
| :---: | --- |
| -A，--all <path>| 添加当前目录下的全部文件（除了.gitignore 设置的文件） |
| -u/--update <path>|更新<指定路径下>tracked 的文件|

```bash
git add <file> # .或*代表全部添加 (包括tracked 和 untrack 的文件)       
git add -u <path>   # 更新<指定路径下>tracked的文件
# git reset head # 在commit之前撤销git add操作    
```

# .gitignore 文件

> [.gitignore 文件](https://git-scm.com/docs/gitignore)：git 忽略管理的文件
>
> 一些常用的 .gitignore 的规则：<https://github.com/github/gitignore/>
>
> [配置全局忽略文件](https://blog.csdn.net/Leonxx/article/details/86294617)
>
> | 模式 | 描述   | 例子 |
>  | :--: | ------ | --- |
> |  ！  | 非     | !a.h  <font color=green># 忽略非 a.h 文件，即管理 a.h 文件</font> |
> |  *  | 通配符 | *.py <font color=green># 忽略所有以 .py 结尾的文件</font> |
> | [...]  | 集合 | [a-z].py <font color=green># 忽略一个字母 a-z 和以 .py 结尾的文件</font> |
> | a\|b  | a 或 b | [a|b].rs <font color=green># 忽略 a.rs 或者 b.rs 的文件</font> |

```bash
# echo "temp" >> ./.gitignore # temp文件
# echo "temp/" >> ./.gitigonre # temp文件夹

git check-ignore temp
```