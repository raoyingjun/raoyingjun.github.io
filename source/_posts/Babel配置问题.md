### @babel/core

是babel进行语法转换的核心实现

### @babel/plugin-transform-runtime

该包用于将babel的一些辅助函数整合到一起，以免编译输出有重复。

> 由于babel依赖少数辅助函数实现某些功能，并且辅助函数会被添加到每个需要它的文件内。所以会用到`@babel/plugin-transform-runtime`

### @babel/preset-env

使用预设环境。当你使用最新的JS语法，自动帮你转换兼容低版本的语法

### babel-loader

babel官方制作了loader，使babel支持在webpack构建工具中使用

### 常用的配置如下

```js
// webpack.config.js
// 以下省略了其他的loader
{
    test: /\.js$/,
        exclude:/node_modules/,
        use:{
         loader: 'babel-loader', 
         options:{
            presets: [
                [
                    '@babel/preset-env',
                    {
                        // usage表示按需加载
                        useBuiltIns: 'usage',
                        corejs: {
                            /**
                             * corejs的版本。低版本不在维护和更新。
                             * 官方推荐使用具体的版本号。例如`3.11`，而不是`3`
                             */
                            version: '3.11',
                            // 提供了对处于提议阶段的js语法的支持
                            proposals: true
                        }
                    }
                ]
            ],
            plugins: ['@babel/plugin-transform-runtime']
        }
    }
}
```



