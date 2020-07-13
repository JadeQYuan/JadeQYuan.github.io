---
title: git常用命令
date: 2020-04-05 09:28:55
categories:
  - Tools
tags:
  - How
  - null
description: git常用命令
---

- 添加远程仓库
```shell
git remote add <远程仓库名称，一般默认为origin> <url>
```

- 删除远程仓库
```shell
git remote remove <远程仓库名称>
```

- 更新/设置远程仓库地址
```shell
git remote set-url <远程仓库名称> <url>
```

- 添加远程仓库地址
```shell
git remote set-url --add <远程仓库名称> <url>
```

- 设置用户名
```shell
git --global user.name "Your Name"
```

- 设置邮箱
```shell
git --global user.email "you@example.com"
```

- 全局设置用户名
```shell
git config --global user.name "Your Name"
```

- 全局设置邮箱
```shell
git config --global user.email "you@example.com"
```

- 其他命令
```shell
git init ...
git add ...
git commit -m "..."
git status
git diff 文件名
git log 
git reset --hard HEAD^ / 版本号
git reflog 
git checkout -- 文件名
git checkout 分支名
git remote add origin 远程仓库路径
git push -u origin master
git push origin master
git clone
git checkout -b 分支名 = git branch 分支名 + git checkout 分支名 （创建并切换分支）
git merge 分支名
git branch -d
git merge -no-ff -m
git stash
git stash list
git stash apply
git stash drop
git stash pop
git remote
git remote -v
git checkout -b 分支名 origin/分支名
git pull
git branch --set-upstream 分支名 origin/分支名



git init <repo>
git add <file> [ <file> ... ]
git commit -m <message>
git status
git diff <file>
git log [--pretty=oneline] （提交历史）
git reset --hard HEAD^ / HEAD~<num> / <commit id>
git reflog （命令历史）
git diff -- HEAD <file>
git checkout -- <file>
git rm <file>
git remote add origin <URL>
git push -u orgin <branch>
git clone <URL>
git checkout -b <branch> = git branch <branch> + git checkout <branch> = git switch - c <branch>
git branch
git checkout <branch>
git merge <branch>
git branch -d <branch>
git switch <branch>
git log --graph
git merge --no-ff [-m <message>] <branch>
git stash
git stash list
git stash apply
git stash drop
git stash pop
git stash apply stash@{<num>}
git cherry-pick <commit id>
git branch -D <branch>
git remote
git remote -v
git checkout -b <branch> origin/<branch>
git pull
git branch --set-upstream <branch> origin/<branch>
git rebase
git tag <tag>
git tag
git tag <tag> <commit id>
```

<p style="text-align: center"><strong>END</strong></p>
