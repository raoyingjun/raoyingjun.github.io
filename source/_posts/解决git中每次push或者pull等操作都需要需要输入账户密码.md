---
title: 解决git中每次push或者pull等操作都需要需要输入账户密码
date: 2021-10-26 20:19:46
tags: git
categories: git
---

#### 前景引入

使用git时，如果每次push推送、pull拉取等操作都需要输入账户密码来验证账户才允许推送，非常繁琐。问题的表现像下面这样：

```bash
C:\adir\bsubdir\cproject>git push origin
Username for 'https://github.com': XXXX
Password for 'https://raoyingjun@foxmail.com@github.com': XXXX
```

#### 为什么每次都需要登录

如果你是下面这种方式clone项目的，则每次都需要进行登录：

```bash
git clone https://github.com/xxx/xxxxxx.git
```

原因如下：
> 如果你使用的是 SSH 方式连接远端（remote），这样就可以在不输入用户名和密码的情况下安全地传输数据。 然而，这对 HTTP 协议来说是不可能的，每一个连接都是需要用户名和密码的。
> 当在使用双重认证的情况下会更麻烦，因为你需要输入一个随机生成并且毫无规律的 token 作为密码。

注意，这个token指的是git的
[Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

#### 如何解决

使用下面的命令即可解决

```bash
git config --global credential.helper store
```

其中参数 store 的含义是什么？

> “store” 模式会将凭证用明文的形式存放在磁盘中，并且永不过期。 这意味着除非你修改了你在 Git 服务器上的密码，否则你永远不需要再次输入你的凭证信息。 这种方式的缺点是你的密码是用明文的方式存放在你的 home
> 目录下。当然，除了参数store还有其他的参数可选

当然，也可用通过
[设置SSH免密登录](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
的方式登录

以上参考自
[git中文使用文档](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%87%AD%E8%AF%81%E5%AD%98%E5%82%A8)
