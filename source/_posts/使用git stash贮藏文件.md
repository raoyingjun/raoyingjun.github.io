---
title: 使用 git stash 贮藏文件
date: 2021-11-19 14:53:46
tags: git
categories: git
---

##### 前景引入

当你使用 Git 作为版本控制工具，当你正在开发 A
功能，已经开发了一定的进度，此时来了一个紧急BUG，而你应该不会想commit未开发完成的代码，也不太可能会选择回滚自己已经完成了部分的代码。不知道该怎么把A功能先暂时搁置在一边，待修复完该 BUG，再回来继续 A
功能的开发。接下来，我们来使用 `git stash`
解决这个问题

##### 概念介绍

利用 `git stash` 可以将工作区的代码，暂存在一个堆栈（Stack）中，每次暂存将会对应产生一个暂存记录。stash可以译为“藏匿、隐藏、存放、贮藏”。

> 堆栈（Stack）是一种数据结构，其中的数据满足后进先出，也可以说成是先进后出

##### 相关命令

* 将当前工作区的更改进行贮藏

    ```bash
    git stash save -u "备注信息"
    ```


* 查看堆栈中所有的贮藏记录

    ```bash
    git stash list
    ```


* 删除所有的贮藏记录

    ```bash
    git stash clear
    ```


* 将最近一次贮藏记录应用到工作区（贮藏记录仍会被保留）

    ```bash
    git stash apply
    ```


* 将指定的贮藏记录应用到工作区（贮藏记录仍会被保留）

    ```bash
    git stash apply [stash]
    ```

`stash`为要被应用到工作区的对应的贮藏，例如 “stash@{0}”

* 将最近一次贮藏记录应用到工作区（贮藏记录同时会被删除）

    ```bash
    git stash pop
    ```


* 将指定的贮藏记录应用到工作区（贮藏记录同时会被删除）

    ```bash
    git stash pop [stash]
    ```

  `stash`为要被应用到工作区的对应的贮藏记录，例如 “stash@{0}”


* 将最近一次的贮藏记录删除

    ```bash
    git stash drop
    ```


* 将指定的的贮藏记录删除

    ```bash
    git stash drop [stash]
    ```

`stash`为要被删除的贮藏记录，例如 “stash@{0}”

* 删除所有的贮藏记录

    ```bash
    git stash clear
    ```

##### 注意事项

`git stash` 不会暂存被 `.gitignore` 忽略的文件或文件夹

