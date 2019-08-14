---
title: 成为 PinCAP 的 contribute
date: 2019-08-12 00:00:00
categories:
- GitHub 学习
tags:
- 笔记
typora-root-url: ../../WalterWJ.github.io
---
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

<!-- **格式参考：**[PingCAP 中文技术文档风格指南](https://docs.google.com/document/d/1b6ZhZD33OoM8AacpKksGGSuxJWReLkNnSt8eSc1kTXc/edit) -->

* 先 fork 相关项目
* 配置将官方项目的 commit 提交记录同步到自己 fork 的项目中
* 如果想给官网项目提交 pr，成为 Contribute:
  - 先在自己 fork 的项目中，切一个分支
  - 在分支中修改完成之后，pull 一下官方项目，查看是否有冲突
  - 当没有冲突的时候，提交修改到自己 fork 的项目中新切的分支中
  - 提交到自己的 fork 项目中之后，登录 GitHub 网站，点击 `New pull request` 按钮将自己修改的 pr 推到官方
  - Assignees 相关同学，进行审核，等待通过即可

**注意项：**

* 修改文档完成，上推代码要切新分支
* 上推之前，commit 之后，推荐先进行 pull 官方代码，进行冲突检查

# 操作

* fork 相关项目到自己的 GitHub 中

![](/assets/images/PostsImages/Become-Contribute-template/pr-01.png)

* git clone 项目到本地

```shell
git clone https://github.com/WalterWj/docs-cn.git
```

* 配置将官方项目的 commit 提交记录同步到自己 fork 的项目中

```shell
# 查看列举本地 master 分支的个人远程仓库
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git remote -v
origin  https://github.com/WalterWj/docs-cn.git (fetch)
origin  https://github.com/WalterWj/docs-cn.git (push)

# 本地分支关联官方源远程仓库，使用远程仓库的地址，并设置一个别名
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git remote add followPingCAP-DOCS https://github.com/pingcap/docs-cn.git
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git remote -v
followPingCAP-DOCS      https://github.com/pingcap/docs-cn.git (fetch)
followPingCAP-DOCS      https://github.com/pingcap/docs-cn.git (push)
origin  https://github.com/WalterWj/docs-cn.git (fetch)
origin  https://github.com/WalterWj/docs-cn.git (push)

# 将源远程仓库项目 pull 到本地 master 分支
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git pull followPingCAP-DOCS master // down 到本地
# wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git add .
# wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git commit -m 'master' // 需要先将修改 commit 到本地
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git status // 查看状态
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git push origin // 推到自己的 GitHub 中
```

**这样就能保持自己 fork 的项目和官方保持一致**

* 切分支/修改文档/上推到本地

```shell
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git checkout -b 'WalterWJ'
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git branch
* WalterWJ
  master

# 然后修改想修改文档的内容

wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git status // 查看修改的文件
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git add v3.0/reference/tispark.md
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git commit -s -m 'update tispark faq'
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git pull followPingCAP-DOCS master // 拉取官方最新 commit，确认没有冲突，可不做
wangjun@wangjundeMacBook-Pro:~/PycharmProjects/docs-cn$ git push origin WalterWJ // 上推到自己 fork 的项目中
```

**这样我们修改内容就会同步到自己 fork 的项目中去**

* 登录自己的 GitHub，将自己的修改推到官方

**推送按钮**

![](/assets/images/PostsImages/Become-Contribute-template/pr-02.png)

**推送**

![](/assets/images/PostsImages/Become-Contribute-template/pr-03.png)

**选择帮忙 review 的人,并且 at 相关人员**

![](/assets/images/PostsImages/Become-Contribute-template/pr-04.png)

**review 完成之后，点击 `Merge pull request` 进行 merge**

![](/assets/images/PostsImages/Become-Contribute-template/pr-05.png)

**合并完成之后，删除 GitHub 上自己创建的分支，本地可以本地删除也可以不做处理**

![](/assets/images/PostsImages/Become-Contribute-template/pr-07.png)

**完成**

![](/assets/images/PostsImages/Become-Contribute-template/pr-06.png)