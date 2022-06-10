---
title: 前端Javascript模块化
date: 2021-10-26 20:19:46
tags: 前端
categories: 前端
---

### AMD 规范

AMD（Asynchronous Module Definition）规范指异步模块定义。是 RequireJS 推广模块化规范的产物。

看个例子，AMD 规范是如何导入模块和定义模块的：

```javascript
  /**
 * 第一个参数是依赖的模块列表
 * 第二个参数是工厂函数，允许从该函数返回任何有效的返回值，暴露供外部使用。且该工厂函数的参数列表对应依赖的模块列表
 * 暴露的模块名称默认是文件名称
 */
define(['jquery'], function (jquery) {
    console.log(jquery)
    return {
        add: function () {
        },
        mul: function () {
        }
    }
})
 ```

> **AMD 推崇前置依赖**
>
> 指所需的依赖在定义模块时就要提前引入

### CMD 规范

CMD（Common Module Definition）规范指通用模块定义。是 SeaJS 推广模块化规范的产物。 通过一个例子，看 CMD 规范如何导入模块和定义模块：

```javascript
  /**
 * 接收一个工厂函数作为参数。该工厂函数接受 3 个参数
 * require 是一个函数，用来引入模块
 * exports 是一个对象，可以在其上定义属性和方法。暴露供外部使用
 * module 是一个对象，指向当前模块
 */
define(function (require, exports, module) {
    var $ = require('jquery')
    exports.add = function () {
    }
    exports.mul = function () {
    }
    module.exports.sub = function () {
    }
})
```

> **CMD 推崇就近依赖**
>
> 指依赖在需要时引入

### CommonJS 规范

CommonJS 规范是服务器模端块化规范。由 NodeJS 推广使用。来个例子，了解 CommonJS 是如何导入模块和定义模块规范的：

```javascript
// a.js
/**
 * nodejs 为每个文件提供了一个 module 对象和 exports 对象
 * module 指代当前模块的对象，提供了一些属性供使用
 * exports 是一个对象，暴露供外部使用。同时该对象指向 module.exports。
 * module.exports === exports -> true
 */
module.exports.add = function () {
}
exports.mul = function () {
}
// b.js
var util = require('a.js')
util.add()
util.mul()
```

### ES Module 规范

由 ES6 引入至浏览器原生支持的模块化规范

```javascript
// 导出常量 a
export const a = 10
// 从 a.js 导入常量 a 
import { a } from 'a.js'
```

### UMD 规范

UMD（Universal Module Definition）规范是通用模块定义，为兼容其他模块化规范和无模块化开发的通用模块化规范，兼容在多个运行环境（nodejs、浏览器端）都能正常工作。
最后，还是来个例子来了解它。

```javascript
  (function (root, factory) {
    // AMD 规范或 CMD 规范
    if (typeof define === 'function') {
        define(factory)
    }
    // nodejs 使用的 CommonJS 规范
    else if (typeof exports === 'object') { 
        module.exports = factory()
    }
    // 浏览器环境
    else {
        // NumberUtil 是导出暴露的模块名称
        root.NumberUtil = factory()
    }
})(this, function () {
    return {
        add: function () {
        },
        mul: function () {
        }
    }
})
```

  

  
