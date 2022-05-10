---
title: fatal refusing to merge unrelated histories
date: 2022-05-09 10:05:58
tags: git
categories: git
---

### git 合并代码提示 fatal: refusing to merge unrelated histories

合并代码中出现错误 fatal: refusing to merge unrelated histories 原因是本地仓库和远程仓库实际上是两个独立不相关联的仓库。如果是本地基于 git clone 远程 github
仓库则不会产生该问题

### 解决办法

使用 –allow-unrelated-histories 将两个不相关联的git仓库合并到一起，命令如下：

```bash
git pull [remote] [branch] –allow-unrelated-histories
```

示例如下

```bash
git pull origin master –allow-unrelated-histories
```

### 参数介绍

–allow-unrelated-histories 表示允许合并两个不相关联的仓库
