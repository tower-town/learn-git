
# 工作提要

>一般的工作流：master –> v1 —> v2 ….
>
>​                       | 分支：dev(开发版) —> V1.1 —> V1.2 …|合并到（master）V2
>
>即一般工作环境会出现至少两个分支：master、development，master 即主分支存在正式版/稳定版，development(dev) 存放开发版本，开发版成熟则合并至 master 中，然后在分支 dev 依次发展

# 线上连接

> github/gitee（网站提供仓库）/gitlab(工具提供生成私有仓库)
>
> ps:[github 的高级搜索](https://www.cnblogs.com/catluo/p/11728554.html)，[github 官方 api 帮助文档](https://docs.github.com/cn/rest):[知乎解析 GitHub 的 api](https://zhuanlan.zhihu.com/p/152164873)
>
> pss:[powershell core 自动更新](https://blog.lingyf.com/powershell-script-automatically-update-powershell-core/)

* 注册账号

* 创建仓库

* 本地代码推送

```bash
 # 新仓库
echo '# <repository>' >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin <url>
git push -u origin master
               
# 已存在的仓库
git remote add origin <url> # 使远程 <url> 成为 变量 origin
git push -u origin master # 推送master分支到远端,并设置为push默认
# git push origin dev # 推送dev分支到远端
```
