---
layout: post
title:  "《JavaScript 高级程序设计》读书笔记"
categories: JavaScript 前端 书籍
comments: true
share: true
---

作为JavaScript技术经典名著，《JavaScript高级程序设计（第3版）》承继了之前版本全面深入、贴近实战的特点，在详细讲解了JavaScript语言的核心之后，条分缕析地为读者展示了现有规范及实现为开发Web应用提供的各种支持和特性。

**《JavaScript高级程序设计（第3版）》**

![](http://img3.douban.com/mpic/s8958650.jpg)

- 豆瓣链接：[http://book.douban.com/subject/10546125/](http://book.douban.com/subject/10546125/)
- 京东链接：[http://item.jd.com/10951037.html](http://item.jd.com/10951037.html)

<hr /><br />

#### **第 1 章 JavaScript 简介**

**JavaScript 实现：**  包括 ECMAScript + DOM + BOM

**ECMAScript：**  ECMAScript-262（ES5，2009年）包括 语法、类型、语句、关键字、保留字、操作符、对象

**DOM：**  DOM 级别：DOM1级（映射文档结构）、DOM2级（视图、事件、样式、遍历和范围）、DOM3级（加载和保存、验证等）

**BOM：**  浏览器窗口、navigator、location、screen、cookies、XMLHttpRequest 等

<br />
<hr />
<br />

#### **第 2 章 在 HTML 中使用 JavaScript**

**\<script\> 元素属性：**

- `async`： 异步下载脚本，用法为 `async="async"`，会在 load 事件前、DOMContentLoaded 事件触发前或后执行，不保证执行顺序，只用于外部文件
- `defer`： 延迟脚本到 `<html>` 后执行，用法为 `defer="defer"`，HTML5 规范中，defer 的脚本会在 DOMContentLoaded 事件触发前执行，且保证执行顺序，只用于外部文件
- `src`： 指定外部文件
- `type`： 一般为 `text/javascript`

**\<script\> 元素示例：**

{% highlight html%}
<script type="text/javascript" src="example.js"></script>
{% endhighlight %}

**\<script\> 标签位置：**  放在 `<body>` 标签内页面元素最后，防止下载、解析和执行过程阻碍页面显示

**\<!DOCTYPE\> 文档模式：**

- 混杂模式：IE 的行为与 IE5 相同
- 标准模式：IE 的行为接近标准行为

{% highlight html%}
<!-- HTML 4.01 严格型 -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

<!-- XHTML 1.0 严格型 -->
<!DOCTYPE html PUBLIC
"-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

<!-- HTML 5 -->
<!DOCTYPE html>
{% endhighlight %}

**\<noscript\> 元素：**  浏览器不支持脚本或禁用脚本时显示

<br />
<hr />
<br />

#### **第 3 章 基本概念**

**严格模式：**  `"use strict";`，可在脚本顶部或函数中使用

**基本数据类型：**  undefined、null、boolean、number、string

**复杂数据类型：**  object

**typeof 操作符：**
