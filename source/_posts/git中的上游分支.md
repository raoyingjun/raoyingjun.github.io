---
title: git中的上游分支
date: 2021-10-26 20:19:46
tags: git
---

### 预备知识

什么是`fork`？在github的某个仓库上通过`fork`按钮，`fork`一份项目到你的仓库，称其为`origin（源）`，并且还可以关联被`fork`的仓库，称其为`upstream（上游）`

### 概述

如果我们需要参与某个项目的开发或者对其进行改进，`fork`便是其中的一种的方式。我们将目标仓库`fork`一份到自己的仓库，然后在源仓库进行开发，通过向上游发起`pull request（合并请求）`，在通过上游的`review（评审）`
后，便可以将更改合并到上游

**记住，`fork`不同于`clone`。`clone`仅仅只是将目标仓库复制一份**

### 相关的常用命令

##### 添加上游远程仓库

```bash
git remote add [upstreamRepoName] [upstreamRepoAddress] 
```

`upstreamRepoName`：上游仓库的别名，一般为`upstream`

`upstreamRepoAddress`：上游仓库的地址

##### 获取上游最新的代码

```bash
git fetch [remoteName]
```

`remoteName`：上游远程仓库的别名，一般上游仓库的别名为`upstream`

##### 合并上游的分支到源分支

```bash
git merge [remoteName]/[branchName]
```

`remoteName`：上游远程仓库的别名，一般上游仓库的别名为`upstream`

`branchName`：上游分支的对应分支名

##### 推送到fork的源仓库

```bash
git push
```

`remoteName`：上游远程仓库的别名，一般上游仓库的别名为`upstream`

`branchName`：上游分支的对应分支名
