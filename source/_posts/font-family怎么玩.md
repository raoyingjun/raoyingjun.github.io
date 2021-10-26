---
title: font-family怎么玩
date: 2021-10-26 20:19:46
tags: css
---

### 什么是font-family啊？

定义文字所使用的字体族（family name）或者从通用字体族（generic-name）中选出的一种字体。如果不手动指定其值，则由浏览器决定

### 什么是字体族？

* 字体族是指代一个具体的字体名称。 `Microsoft YaHei`、`Arial`等，表示我要使用什么字体

* 通用字体族是系统自带的通用的字体族，css中有自带五个通用字体族

    * 衬线字体（Serif）在每个字母的边缘都有一个小的笔触。它们营造出一种形式感和优雅感。
    * 无衬线字体（Sans-serif）字体线条简洁（没有小笔画）。它们营造出现代而简约的外观。
    * 等宽字体（Monospace）这里所有字母都有相同的固定宽度。它们创造出机械式的外观。
    * 草书字体（Cursive）模仿了人类的笔迹。
    * 幻想字体（Fantasy）是装饰性/俏皮的字体。

  这里拿 `sans-serif` 和 `serif` 做个图示：

  ![image-20210323232956973](C:\Users\HASEE\AppData\Roaming\Typora\typora-user-images\image-20210323232956973.png)

### font-family的具体用法

多个属性值用 `,`分割

```css

selector {
  /* Microsoft YaHei和Helvetica为两个不同的字体，sans-serif为通用字体族*/
  font-family: "Microsoft YaHei", Helvetica, sans-serif
}

```

### 使用font-family的注意事项

* 如果一个字体有空格，也就是由多个单词组成。比如 `Courier New` 字体，则必须使用引号包裹：`”Courier New“`

* 一般必须提供一个字体的回退策略。应该在 `font-family` 列表最后添加一个通用字体族，因为无法保证用户的计算机内已经安装了你首选的字体，也不能保证使用 `@font-face`
  提供的字体能够正确地下载。通用字体族可以让浏览器最后回退使用你所指定的备选字体。



