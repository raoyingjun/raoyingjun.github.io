---
title: webpack 踩坑之 process.env.NODE_ENV
date: 2021-10-26 20:19:46
tags: webpack
categories: webpack
---

##### 问题引入

当你尝试在 `webpack.config.js` 文件中访问 `process.env.NODE_ENV`（以下简称 `NODE_ENV`） 。很遗憾，结果是 `undefined`

##### 解析原因

webpack是在编译后运行时提供了 `NODE_ENV` 。而当 Webpack读取配置文件 `webpack.congig.js` 时，此时 ``NODE_ENV` 并未赋值

##### 解决办法

使用 npm包 `cross-env`，该命令支持跨系统设置环境变量。使用如下命令安装：

```bash
npm install cross-env -D
```

可以通过 `cross-env` 设置环境变量 `NODE_ENV` 解决来这个问题。在 `package.json` 中的 `scripts` 字段中添加如下配置（博主用的是 webpack 5.X）：

```json
{
  "scripts": {
    "build": "cross-env NODE_ENV=production webpack",
    "serve": "cross-env NODE_ENV=development webpack serve"
  }
}
```

至此，你可以在 `webpack.config.js` 文件中访问 `NODE_ENV` 了。

