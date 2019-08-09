# 作用
  帮助想成为 PingCAP 的 contribute 的人

# Git 用法

| 命令                                                                                             | 含义                                 |
| ------------------------------------------------------------------------------------------------ | ------------------------------------ |
| git clone [url]                                                                                  | 下载一个项目和它的整个代码历史       |
| git config --list                                                                                | 显示当前的Git配置                    |
| git config -e [--global]                                                                         | 编辑Git配置文件                      |
| git config [--global] user.name "[name]" <br> git config [--global] user.email "[email address]" | 设置提交代码时的用户信息             |
| git add/rm                                                                                       | 添加/删除修改文件                    |
| git commit -m [message]                                                                          | 提交暂存区到仓库区                   |
| git branch                                                                                       | 列出所有本地分支                     |
| git checkout -b [branch]                                                                         | 新建一个分支，并切换到该分支         |
| git tag [tag]                                                                                    | 新建一个tag在当前commit              |
| git status                                                                                       | 显示有变更的文件                     |
| git fetch [remote]                                                                               | 下载远程仓库的所有变动               |
| git remote -v                                                                                    | 显示所有远程仓库                     |
| git pull [remote] [branch]                                                                       | 取回远程仓库的变化，并与本地分支合并 |
| git push [remote] [branch]                                                                       | 上传本地指定分支到远程仓库           |
| git reset                                                                                        | 撤销                                 |

# 给 PingCAP 提交代码流程

**格式参考：**[PingCAP 中文技术文档风格指南](https://docs.google.com/document/d/1b6ZhZD33OoM8AacpKksGGSuxJWReLkNnSt8eSc1kTXc/edit)

* 先 fork 相关项目
* 将官方项目的 commit 提交记录同步到自己 fork 的项目中
* 如果想给官网项目提交 pr，成为 Contribute:
  - 先在自己 fork 的项目中，切一个分支
  - 在分支中修改完成之后，pull 一下官方项目，查看是否有冲突
  - 当没有冲突的时候，提交修改到自己 fork 的项目中新切的分支中
  - 提交到自己的 fork 项目中之后，登录 GitHub 网站，点击 `New pull request` 按钮将自己修改的 pr 推到官方
  - Assignees 相关同学，进行审核，等待通过即可

**注意项：**

* 1. 修改文档完成，上推代码要切新分支
* 2. 上推之前，commit 之后，推荐先进行 pull 官方代码，进行冲突检查

# 操作

* 拉取