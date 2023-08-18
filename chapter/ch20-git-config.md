# config

> `git`的配置
>

```bash
git config [<file-option>] [--type=<type>] [--fixed-value] [--show-origin] [--show-scope] [-z|--null] <name> [<value> [<value-pattern>]]
git config [<file-option>] [--type=<type>] --add <name> <value>
git config [<file-option>] [--type=<type>] [--fixed-value] --replace-all <name> <value> [<value-pattern>]
git config [<file-option>] [--type=<type>] [--show-origin] [--show-scope] [-z|--null] [--fixed-value] --get <name> [<value-pattern>]
git config [<file-option>] [--type=<type>] [--show-origin] [--show-scope] [-z|--null] [--fixed-value] --get-all <name> [<value-pattern>]
git config [<file-option>] [--type=<type>] [--show-origin] [--show-scope] [-z|--null] [--fixed-value] [--name-only] --get-regexp <name-regex> [<value-pattern>]
git config [<file-option>] [--type=<type>] [-z|--null] --get-urlmatch <name> <URL>
git config [<file-option>] [--fixed-value] --unset <name> [<value-pattern>]
git config [<file-option>] [--fixed-value] --unset-all <name> [<value-pattern>]
git config [<file-option>] --rename-section <old-name> <new-name>
git config [<file-option>] --remove-section <name>
git config [<file-option>] [--show-origin] [--show-scope] [-z|--null] [--name-only] -l | --list
git config [<file-option>] --get-color <name> [<default>]
git config [<file-option>] --get-colorbool <name> [<stdout-is-tty>]
git config [<file-option>] -e | --edit
```

| 选项 | 说明 | 示例 |
| --- | --- | --- |

一个非常好用的 `git alias`
来源：https://zhuanlan.zhihu.com/p/140767014

```
[alias]
        aliases = config --get-regexp alias
        last = log -1 HEAD
        amend = commit --amend --reuse-message=HEAD
        update = fetch --all --prune
        purge = !bash -c \"git branch -r | awk '{print \\$1}' | grep -E -v -f /dev/fd/0 <(git branch -vv | grep origin) | awk '{print \\$1}' | xargs -r git branch -D\"
        graph = log --graph --all --pretty=format:'%Cred%h%Creset - %s %Cgreen(%cr) %C(bold blue)%an%Creset %C(yellow)%d%Creset'
        uncommit = reset --soft HEAD~1
        unstage = reset HEAD --
        stat = diff --stat
[help]
        autocorrect = 1
```
