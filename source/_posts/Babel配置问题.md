---
title: Babel 配置问题
date: 2021-10-26 20:19:46
tags: webpack
categories: webpack
---

### @babel/core

是 babel 进行语法转换的核心实现

### @babel/plugin-transform-runtime

该包用于将 babel 的一些辅助函数整合到一起，以免编译输出有重复。

> 由于babel依赖少数辅助函数实现某些功能，并且辅助函数会被添加到每个需要它的文件内。所以会用到`@babel/plugin-transform-runtime`

### @babel/preset-env

使用预设环境。当你使用最新的JS语法，自动帮你转换兼容低版本的语法

### babel-loader

babel 官方制作了 loader，使babel支持在webpack构建工具中使用

### 常用的配置如下

```js
// webpack.config.js
module.exports = {
    // 其他项略..
    module: {
        rules: [
            // 其他 rule 略...
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: [
                            [
                                '@babel/preset-env',
                                {
                                    // usage 表示按需加载
                                    useBuiltIns: 'usage',
                                    corejs: {
                                        /**
                                         * corejs 的版本。低版本不在维护和更新。
                                         * 官方推荐使用具体的版本号。例如 '3.11'，而不是 '3'
                                         */
                                        version: '3.11',
                                        // 提供了对处于提议阶段的 js 语法的支持
                                        proposals: true
                                    }
                                }
                            ]
                        ],
                        plugins: ['@babel/plugin-transform-runtime']
                    }
                }
            }
        ]
    },
}
```



