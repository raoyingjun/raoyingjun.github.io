---
title: ubuntu 安装可视化界面
date: 2023-11-27 19:48:54
tags: linux
categories: linux
---

### 前言

起因是想为 `linux` 安装可视化界面，各方面使用会方便很多。
> 笔者使用 `linux` 版本为 `ubuntu 18.04`，对于其他版本，亦可以如法炮制或从中参照。

### 安装可视化界面

```
// 更新 apt-get 软件包信息库
sudo apt-get update

// 安装 ubuntu 可视化界面
sudo apt-get install -y ubuntu-desktop

// 等待以上步骤完成后，重启虚拟机
reboot
```

重启虚拟机后，呈现的即是可视化界面。

### 补充

如果你正在 `vmware` 中使用 `ubuntu` ，或者其他 linux 分支（RetHat、CentOS 等等），并且你想要直接拖拽文件从你的电脑到 `ubuntu` 中，请**安装 `open-vm-tools-desktop`**，如下：（可选）

  ```
  sudo apt-get install open-vm-tools-desktop -y
  ```

  > 如果你的 VM Tool 不可用，或者置灰无法重新安装，那么这对你来说则是必选的了！


  
