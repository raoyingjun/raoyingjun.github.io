---
title: javascript模块化。AMD，CMD，UMD，CommenJS
date: 2021-10-26 20:19:46
tags: nodejs
---

* AMD(Asynchronous Module Definition)指异步模块定义。是requirejs推广模块化规范的产物。

  看个例子，了解其是如何定义一个AMD模块的：

  ```javascript
  /**
   * 第一个参数是依赖的模块列表
   * 第二个参数是工厂函数，允许从该函数返回任何有效的返回值，暴露供外部使用。且该工厂函数的参数列表对应依赖的模块列表
   * 暴露的模块名称默认是文件名称
   */
  define(['jquery'], function (jquery) {
      console.log(jquery)
      return {
          add: function () {}
          mul: function () {}
      }
  })
  ```

> **AMD推崇前置依赖**
>
> 指所需的依赖在定义模块时就要提前引入

* CMD

  CMD(Common Module Definition)指通用模块定义。是seajs推广模块化规范的产物。

  通过一个例子，看如何定义一个CMD模块：

  ```javascript
  /**
   * 接收一个工厂函数作为参数。该工厂函数接受3个参数
   * require是一个函数，用来引入模块
   * exports是一个对象，可以在其上定义属性和方法。暴露供外部使用
   * module是一个对象，指向当前模块
   */
  define(function (require, exports, module) {
  	var $ = require('jquery')
  	exports.add = function () {}
  	exports.mul= function () {}
      module.exports.sub = function () {}
  })
  
  ```

  > **CMD推崇就近依赖**
  >
  > 指依赖在需要时引入


* CommonJS

  CommonJS是服务器模端块化规范。由nodejs推广使用。

  来个例子，帮助了解使用CommonJS模块：

  ```javascript
  // a.js
  /**
   * nodojs 为每个文件提供了一个module对象和exports对象
   * module指代当前模块的对象，提供了一些属性供使用
   * exports是一个对象，暴露供外部使用。同时该对象指向module.exports。
   * module.exports === exports -> true
   */
  module.exports.add = function () {}
  exports.mul = function () {}
  
  
  // b.js
  var util = require('a.js')
  util.add()
  util.mul()
  ```


* UMD

  UMD(Universal Module Definition)通用模块定义，为兼容其他模块化规范和无模块化开发的通用模块化规范。

  最后，还是来个例子来了解它。

  ```javascript
  (function (global, factory) {
  	 // AMD 或 CMD
  	 if (typeof define === 'function') {
  		 define(factory)
  	 } else if (typeof exports === 'object') {
  		 // nodejs 使用的 CommonJS
  		 module.exports = factory()
  	 } else {
  		 // 浏览器环境
  		 global.util = factory()
  	 }
   })(this, function () {
  	 return {
           add: function () {}
           mul: function () {}
       }
   })
  ```

  

  
