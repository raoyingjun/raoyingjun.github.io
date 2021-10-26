---
title: linux的screen命令
date: 2021-10-26 20:19:46
tags: linux
---

### 前言

一般部署在linux的服务器的项目如何在退出shell后仍然保持进程运行状态。可以使用nohub、screen等命令解决，这里讲解screen命令

### `screen`命令介绍

`screen`表示会话窗口，该会话内运行的进程在shell关闭后，仍然可以保持运行

### 常用参数及作用

* `-S <会话名称>` 新建一个会话

* 参数 `-r <会话ID> `恢复到某个离线会话

* `-ls` 查看所有会话

* `ctrl+A+D` 退出该会话（会话仍然在后台运行）

* 当处于该会话内，在shell中输入 `exit`终止该会话

  
