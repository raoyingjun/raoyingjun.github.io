---
title: linux 添加用户命令提示符显示不正确
date: 2023-12-25 14:54:54
tags: linux
categories: linux
---

### 起因

在 linux 使用 `useradd` 添加用户的时候，命令提示符显示不正确，如下所示：

```bash
# 创建用户并添加到自动创建其家目录
root@ubuntu:~# useradd -m test

# 切换到 test 用户
root@ubuntu:~# su - test

# 注意看下面一行，命令提示符只显示了一个 $ 符号，有问题
$
```

### 问题排除与解决

经排查是使用 `useradd` 创建用户时其默认指定的 shell 不正确导致。查询 `/etc/default/useradd` 文件也就是 `useradd` 的默认配置，可发现：

```bash
# /etc/default/useradd
# 部分略，仅展示与本文相关部分

# 默认使用的 shell 为 /bin/sh ，不正确
SHELL=/bin/sh

# 进行修改，默认的 shell 应使用 
SHELL=/bin/bash
```

接着再进行尝试，发现命令提示符显示正常了，如下：

```bash
# 切换到 test 用户
root@ubuntu:~# su - test

# 注意看下面一行，命令提示符显示正确
test@ubuntu:~$ 
```

至此，问题解决。