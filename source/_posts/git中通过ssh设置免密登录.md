---
title: git 中通过 ssh 设置免密登录
date: 2021-10-26 20:19:46
tags: git
categories: git
---

#### 前景引入

在使用 `git` 时，可以使用 `SSH` 避免了每次推送操作等都需要输入用户名和密码的繁琐。

#### 如何使用ssh设置免密登录

##### 注意事项

请先确认你是以下面这种方式 clone 项目的，则 ssh 免密登录才会生效：

```bash
git clone git@github.com:xxx/xxxxxx.git
```

##### 操作步骤

注意：以下命令如果无法在工作，请尝试在 `git bash` 终端环境下尝试

1. 使用以下命令生成 `SSH` 公钥和私钥

   ```bash
   ssh-keygen -t rsa -C email
   ```

   `email` 为github账户邮箱。命令执行后将会在在 `~/.ssh` 目录下生成公钥和私钥


2. 接着会提示你输入生成存储密钥（公钥和私钥）文件名 、输入密码、确
   认密码等。可直接输入回车省略跳过，默认生成私钥文件名为 `id_rsa` 以及公钥
   文件名为 `id_rsa.pub`


3. 执行以下命令确保 `ssh-agent` 正在运行

   ```bash
   eval `ssh-agent -s`
   ```

4. 使用下面命令将 `SSH` 私钥添加到 `ssh-agent`

   ```bash
   ssh-add ~/.ssh/privatekeyname
   ```

   其中 `privatekeyname` 为私钥文件的名称，也就是在步骤2生成的存储私钥的文件名


4. 进入github，将 `SSH` 公钥添加到github账户


5. 使用以下命令测试连接

   ```bash
   ssh -T git@github.com
   ```

   如果该命令返回结果的信息中包含 `You've successfully authenticated`，说明没有问题，可以使用 `SSH` 进行推送了。


6. 最后使用相关命令则可以通过 `SSH` 进行推送了

