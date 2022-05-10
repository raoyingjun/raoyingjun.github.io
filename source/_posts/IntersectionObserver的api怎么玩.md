---
title: IntersectionObserver 的 api 怎么玩
date: 2021-10-26 20:19:46
tags: javascript
categories: javascript
---

### 首先来看看 MDN 的对它介绍

IntersectionObserver，一种异步观察目标元素与其容器元素或顶级文档视窗（Viewport）相交状态的方法。

**看图解释相交**（图片来源于网络）

Viewport 是可视区域（容器/视窗），绿色背景的为元素（目标元素）。

![元素和容器/视窗相交和未相交时的示例](http://mms0.baidu.com/it/u=3362364854,2905473064&fm=253&app=138&f=PNG&fmt=auto&q=75?w=499&h=216)

左图表示还未相交，而右图表示的是元素和容器/视窗相交了。

### 用在什么地方

一般使用在需要检测元素和容器元素或视窗的交叉情况，例如

* 内容出现在视窗/容器元素窗懒加载

* 滚动到视窗/容器元素底部加载更多

* 滚到到视窗执行动画等

### 为什么用它？

* 以前对于相交的检测比较麻烦，常用到 Scroll 事件
* 频繁调用 `Elment.getBoundingClientRect()` 等获取元素位置大小信息的属性，造成性能问题

### IntersectionObserver 的基本用法

**IntersectionObserver 构造器**

```javascript
const observer = new IntersectionObserver(callback, options) // 创建观察者
const target1 = document.getElementById('target1') // 要观察的元素
const target2 = document.getElementById('target2')
observer.observe(target1) // 观察 target1
observer.observe(target2) // 同时观察 target1 和 target2
```

* callback 当目标元素和容器元素/视窗相交大小到达该阈值则触发该回调函数，该回调接受两个参数，形式如下：

  ```txt
  callback((entries, observer) => {
    // Do something
  };
  ```

    * entries

      一个 [`IntersectionObserverEntry`](#IntersectionObserverEntry接口) 对象的数组，将在下面介绍，或者直接点击该链接跳转过去

    * observer

      被调用的 `IntersectionObserver` 实例。

* options 传入的可选的参数：
  
  | 字段                   | 说明                                                                                                                                                                                                                                                      |
    | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | `options.root`       | 指定根（root）元素，也就是要观察的目标元素的容器元素/视窗。如果未指定或者为 `null`，则默认为浏览器视窗                                                                                                                                                                                               |
  | `options.rootMargin` | 该属性用于计算相交的区域范围，例如 `10px 20px 30px 40px` 分别指代 top, right, bottom, left。默认值为 0。实际的计算相交的区域范围为 `root.width + rootMargin`                                                                                                                                    |
  | `options.threshold`  | 一个 `number` 数字，或者是一个 `number[]` 数字数组，当目标和容器元素/视窗到达该阈值时回调函数将会执行。例如 `0.4` ，表示目标元素在容器元素/视窗的可见性超过了 40% ，则执行回调。如果你需要可见性每增 `30%` 就调用执行回调，可以传入一个数组 `[0, 0.3, 0.6, 0.9, 1]`。（总共会调用 n 次）默认值为 `0`，只要目标元素有一个像素出现在容器元素/视窗，则调用回调，值为 `1` 则指目标元素完全出现在容器元素/视窗中， 回调才会被执行 |

**IntersectionObserver 实例的方法**

| 方法                                   | 说明                                                 |
| ------------------------------------ | -------------------------------------------------- |
| `IntersectionObserver.disconnect()`  | 使 `IntersectionObserver` 对象停止监听工作                  |
| `IntersectionObserver.observe()`     | 使 `IntersectionObserver` 开始监听一个目标元素。**可以监听多个目标元素** |
| `IntersectionObserver.takeRecords()` | 返回所有观察目标的 `IntersectionObserverEntry` 对象数组         |
| `IntersectionObserver.unobserve()`   | 使 `IntersectionObserver` 停止监听特定目标元素                |

**注意，如果调用 `IntersectionObserver.takeRecords()` ，此方法会清除挂起的相交状态列表，因此不会运行回调方法。**

### IntersectionObserverEntry 接口

该接口描述了目标元素与其根容器元素或视窗在某一特定过渡时刻的交叉状态，该接口的实例（`entries`）作为参数传递给 `IntersectionObserver` 的 `callback` 中，以下参考自 `MDN`

| 字段                                             | 说明                                                                                                                                                                                                             |
| ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `IntersectionObserverEntry.boundingClientRect` | 返回包含目标元素的边界信息的 `DOMRectReadOnly`。边界的计算方式与 `Element.getBoundingClientRect()` 相同                                                                                                                                 |
| `IntersectionObserverEntry.IntersectionRatio`  | 返回 `intersectionRect` 与 `boundingClientRect` 的比例值。值范围为 0.0 到 1.0 之间的数字，表示在根和目标元素的相交矩形内实际上可见多少目标元素，也就是交点矩形比目标元素矩形                                                                                               |
| `IntersectionObserverEntry.intersectionRect`   | 返回一个 `DOMRectReadOnly` 用来描述根和目标元素的相交区域                                                                                                                                                                         |
| `IntersectionObserverEntry.isIntersecting`     | 返回一个布尔值, 如果目标元素与相交区域观察者对象(Intersection Observer) 的根相交，则返回 `true` 。如果返回 `true`, 则 `IntersectionObserverEntry` 描述了变换到相交时的状态，白话形容就是目标元素进入根视窗了，也就是可见了; 如果返回 `false`, 那么可以由此判断,变换是从相交状态到非相交状态，白话形容就是目标元素离开根视窗了，不可见了 |
| `IntersectionObserverEntry.rootBounds`         | 返回一个 `DOMRectReadOnly` 用来描述相交区域观察者(Intersection Observer)中的根。没有指定根，则根为视窗                                                                                                                                       |
| `IntersectionObserverEntry.target`             | 与根出现相交区域改变的元素。白话形容就是当目标元素进入或者离开了根视窗了，而这个 `IntersectionObserverEntry.target` 指的就是这个目标元素                                                                                                                         |
| `IntersectionObserverEntry.time`               | 返回一个记录从 `IntersectionObserver` 的时间原点（时间原点一般是指创建浏览器上下文的时间）到交叉被触发的时间的时间戳。                                                                                                                                        |

### 注意事项

* `IntersectionObserver` 对象被创建后，则无法更改其配置
* 该 API 的部分特性是部分是实验性技术，可能存在兼容性问题
