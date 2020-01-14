---
title: Git-Notes
date: 2019-12-27 17:23:29
tags:
---

# 新建代码库

```bash
# 在当前目录新建一个Git代码库
$ git init


# 下载一个项目和它的整个代码历史
$ git clone [url]


# 显示所有远程仓库
$ git remote -v
```

# 配置

```bash
# 配置文件增加一个新的远程仓库，并命名
$ git remote add [shortname] [url]


# 配置文件删除一个远程仓库
$ git remote rm [shortname]


# 显示当前的Git配置
$ git config --list


# 编辑Git配置文件
$ git config -e [--global]


# 设置提交代码时的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```

# 增加/删除文件

```bash
# 添加所有文件到暂存区
$ git add .


# 不删除工作空间改动代码，撤销commit，并且撤销git add . 
$ git reset --mixed 

# 不删除工作空间改动代码，撤销commit，不撤销git add . 
$ git reset --soft

# 删除工作空间改动代码，撤销commit，撤销git add . (重置暂存区与工作区，与上一次commit保持一致)
$ git reset --hard
```

# 代码提交

```bash
# 提交暂存区到仓库区
$ git commit -m [message]
```

# 分支

```bash
# 列出所有本地分支
$ git branch


# 列出所有远程分支
$ git branch -r


# 列出所有本地分支和远程分支
$ git branch -a

# 将当前分支重命名
$ git branch -m [name]


# 新建一个分支，但依然停留在当前分支
$ git branch [branch-name]


# 新建一个分支，并切换到该分支
$ git checkout -b [branch]
# 新的git switch命令
$ git switch -c [branch-name]


# 切换到指定分支，并更新工作区
$ git checkout [branch-name]
$ git switch [branch-name]


# 切换到上一个分支
$ git checkout -


# 合并指定分支到当前分支
$ git merge [branch]


# 删除分支
$ git branch -d [branch-name]


# 删除远程分支
$ git push origin --delete [branch-name]
```

# 查看信息

```bash
# 显示有变更的文件
$ git status


# 显示commit历史，以及每次commit发生变更的文件
$ git log --stat
```

# 远程同步

[remote]是远程服务仓库名字 , 未设置默认是 origin

[branch]是本地分支名字

```bash
# 上传本地指定分支到远程仓库
$ git push [remote] [branch]


# 强行推送当前分支到远程仓库，即使有冲突
$ git push [remote] --force


# 推送所有分支到远程仓库
$ git push [remote] --all
```

# 问题记录

## 删除 GitHub 中的所有提交历史记录

```bash
# 1.创建orphan分支,名为latest_branch
$ git checkout --orphan latest_branch
# 2.添加所有文件
$ git add -A
# 3.提交更改
$ git commit -am "commit message"
# 4.删除分支
$ git branch -D master
# 5.将当前分支重命名
$ git branch -m master
# 6.最后，强制更新存储库
$ git push -f origin master
```

## 删除暂存区或版本库中的文件

```bash
# 撤销错误添加到暂存区里的文件
$ git rm --cache 文件名

# 删除暂存区和工作区的文件
$ git rm -f 文件名


# 删除错误提交的commit

#仅仅只是撤销已提交的版本库，不会修改暂存区和工作区
$ git reset --soft 版本库ID

# 仅仅只是撤销已提交的版本库和暂存区，不会修改工作区
$ git reset --mixed 版本库ID

# 彻底将工作区、暂存区和版本库记录恢复到指定的版本库
$ git reset --hard 版本库ID

#版本库I可以通过以下命令获取
$ git log
```



## 拒绝合并无关历史

```bash
$ git pull origin master
# fatal: refusing to merge unrelated histories  *// 拒绝合并无关历史*

# 拉取时使用以下命令：
$ git pull origin master --allow-unrelated-histories
```

## 本地更改将被合并覆盖

```bash
# Your local changes to the following files would be overwritten by merge *// 本地更改将被合并覆盖*

#方法1：保留本地修改的代码，并把git服务器上的代码pull到本地
$ git stash
$ git pull origin master
$ git stash pop

# 方法2、完全覆盖本地代码，只保留服务器端代码，则直接回退到上一个版本，再进行pull：
$ git reset --hard
$ git pull origin master
```

