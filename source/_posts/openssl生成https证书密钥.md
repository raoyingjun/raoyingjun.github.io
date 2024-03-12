---
title: openssl 生成 https 证书密钥
date: 2024-3-12 14:09:46
tags: web安全
categories: web安全
---

### 前言

**如何使用 openssl 生成 https 证书及密钥**。当你的在开发、调试、测试等阶段需要使用 https 协议而非 http 时，它对你非常有用。

### openssl 生成证书及密钥

```cmd
openssl req -x509 -nodes -newkey rsa:2048 -keyout key.pem -out cert.pem
```
> 注意，上面的代码表示在**当前**所在目录下生成证书及密钥。 
### 参数介绍

仅对本文章所示内容中用到的选项进行介绍，其余请自行查阅 `openssl` 相关文档。

* `req` 表示需要使用 `openssl` 请求证书相关的操作。

* `-x509` 表示需要使用 `openssl` 生成自签名证书。

*  `-nodes` 表示不对私钥进行加密

* `-keyout` 指定生成的 `RSA` 私钥文件的输出位置

* `-out` 指定生成的自签名证书的输出位置

  
