---
title: webpack的hmr原理
date: 2022-2-21 21:07:24
tags: webpack
categories: webpack
---

### HMR介绍

webpack 是通过 热模块替换 HMR（ Hot Module Replacement）来实现资源的热更新的，可以仅针对部分资源进行更新而无需重载整个页面

### HMR实现原理

HMR 的更新原理大致分为以下部分：

* WDS（Webpack Dev Server）与浏览器维护了一个 WebSocket，当本地资源发生变化，WDS 会向浏览器推送更新，同时会带上本次构建的 Hash。
* 浏览器与上一次的资源进行对比，如果对比发现有差异，则浏览器发起 Ajax 请求获取更改的内容，WDS 会返回一个 json，该 json 包含了所有要更新模块的 Hash 值，接着再通过 jsonp 请求最新的模块代码。
* 对比新旧模块来决定是否更新模块，在决定更新模块后，检查模块之间的依赖关系，更新模块的同时更新模块之间的依赖引用。如果 HMR 失败了，则回退到 Live reload 操作，也就是通过刷新浏览器来获取最新代码。

