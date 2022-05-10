---
title: git tag命令介绍和使用
date: 2022-05-10 11:45:52
tags: git
categories: git
---

### git tag 介绍和使用

git标签用来给分支打上标签。可以使用标签来做版本记号，指向当前最后一次的提交。

* 新建标签

  ```bash
  git tag <tagname>
  ```

  `tagname` 为要新建的标签名。同时指定 `-a` 和 `-m` 参数可以同时指定标签名和标签的描述信息，如下示例：

  ```bash
  git tag -a <tagname> -m <message>
  ```

  `tagname` 为要新建的标签名，`message` 为标签的描述信息。如果不指定描述信息，默认为最后一次 `commit` 提交的说明。


* 查看标签

  ```bash
  git tag
  ```

* 查看指定标签

  ```
  gt show <tagname>
  ```

  `tagname` 为要查看的标签信息以及对应的提交信息。


* 删除标签

  ```
  git tag -d <tagname>
  ```

  `tagname` 为删除的标签名


* 推送标签到远程仓库

  ```
  git push <remotehost> <tagname>
  ```

  `remotehost` 为远程仓库的地址或远程仓库的别名，`tagname` 为要推送到远程仓库的的标签名


* 推送全部**未推送过的**标签到远程仓库

  ```
  git push <remotehost> --tags
  ```

  `remotehost` 为远程仓库的地址或远程仓库的别名


* 删除远程仓库的标签

  ```
  git push <remotehost> :refs/tags/<tagname>
  ```

  `remotehost` 为远程仓库的地址或远程仓库的别名，`tagname` 为要删除的远程仓库的标签

