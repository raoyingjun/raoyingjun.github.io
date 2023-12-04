---
title: webpack 开发库的一些问题
date: 2023-12-04 17:57:15
tags: webpack
categories: webpack
---

### 引言

本人在学习开发前端库并发布到 npm 的过程中遇到了一些问题。故记录以供参照和借阅。

### 将包发布到 npm 问题

首先，发包使用 `npm publish --access=publish` 命令。`public` 表示包的访问权限是公开的。
> 建议 public 你的 npm 包，为开源社区贡献！

其次是版本号，每次修改包后 package.json 中的 `version` 版本号应该变化，否则会报错。

### webpack 构建 ESM 的问题

要使用 webpack 构建 ESM。请参阅如下设置：
```txt
// webpack.config.js
{
    output: {
        path: path.resolve(__dirname, 'dist', esm ? 'es' : 'lib'),
        filename:  "index.esm.js",
         // 必须设置 type 为 module，表示构建类型为 ESM
        library: {type: 'module'}
    },
    ...其他配置项略
    experiments: {
        // 启用实验性的功能，这里是启用构建 ESM 模块
        outputModule: true
    },
}
```

### 将包发布到 npm 后的使用问题

```txt
参照项目目录结构如下：
--------------
root
 -dist
  -lib
   -index.js
  -es
   -index.esm.js
 -types
  -index.d.ts
---------------
...其他略
```

使用 webpack 5 请配置如下设置，再将包发布到 npm，
```json
// package.json
{
    // 入口。当你的包被使用时，将会以这个文件作为入口
    "main": "./dist/lib/index.js",
    // 提供 Typescript 类型支持
    "types": "./types/index.d.ts",
    ...其他略
}
```

> **有必要的自动特性**
> 
> * 无论你 main 入口文件是否是 ESM 版本（index.ems.js 或者 index.js），
>   但构建工具和 IDE 总是能正确识别类型并给出提示。
>   要使用此自动特性，请保证 [name].ems.js、 [name].js、[name].d.ts 中的 [name] 一致
> 
> * 大部分使用构建工具（Webpack、Vite等）的项目，构建工具能根据你使用的导入方式（如 ESM）自动识别并获取所需的依赖文件。
>   如本例中 main 入口文件指定的非 ESM 版本 JS。但你使用 ESM 特性它还是能正常工作的！
