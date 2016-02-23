---
layout: post
title:  "CSS 结构性伪类（Structural Pseudo-Class）详解"
tags: CSS 前端
comments: true
share: true
---

<p class="lead">最近在看 CSS 相关文章，在《CSS3 专业网页开发》的第 4 章的结构伪类（Structural Pseudo-Class）小节讲的不是很容易理解，所以在此写个笔记，结合在线手册、W3C 规范和其他人写的博客把这一部分详细解析一下。</p>

### 1. 关于伪类

首先要明白的是，伪类是对元素不同状态或者类型进行区分的选择器。在 CSS 中定义了 `:active`、`:focus`、`:hover`、`:visited` 等用来描述元素状态的伪类和 `:first-child` 这个用来描述结构的伪类，具体可以参考 [MDN 中文手册 伪类部分 ](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-classes) 和 [Pseudo-classes - CSS Level 2 (Revision 1)](https://www.w3.org/TR/CSS2/selector.html#pseudo-class-selectors)。

CSS 的 [Selectors Level 3](https://drafts.csswg.org/selectors-3/) (通俗的说也就是 CSS3) 中新增了近二十个新的伪类，但本文仅选择结构性伪类中的  `:nth-child` 和 `:nth-last-child`， `:nth-of-type` 和 `:nth-last-of-type`， `:last-child` 来解析。

结构性伪类的作用很明显，可以帮助我们省去 HTML 中描述结构的 class 或 ID，其中一个重要用途就是表格的个性化显示。

### 2. `:first-child`

{% highlight css linenos %}
E:first-child { /* properties */ }
{% endhighlight %}

这是在 CSS Level 2 里定义的伪类，用来选择 **E 中的每个元素在其兄弟元素中的位置是处在第一的 E 的集合**，伪类名中的 child 表示每个元素的父元素的所有子元素，即兄弟元素。`:last-child` 和 `:first-child` 类似，只不过是选择位置是在最后一个的 E，下面的例子可以看出来。

**为了展示不同的效果，故在第 4 行不符合规范地放了一个 p 元素。后面内容均使用这段 HTML，所以可以稍微留意一下结构**

**示例 HTML <i class="fa fa-caret-down"></i>**

{% highlight html linenos %}
<ul>
  <li>1. List 1-1</li>
  <ul>
    <p>2. Paragraph 2-1</p>
    <li>3. List 2-2</li>
    <li>4. List 2-3</li>
    <li>5. List 2-4</li>
  </ul>
  <li>6. List 1-3</li>
  <li>7. List 1-4</li>
</ul>
{% endhighlight %}

**示例 CSS <i class="fa fa-caret-down"></i>**

{% highlight css linenos %}
li:first-child { color: red; }
li:last-child { color: blue; }
{% endhighlight %}

**效果 <i class="fa fa-caret-down"></i>**

<style type="text/css">
#example-code-1 li:first-child { color: red; }
#example-code-1 li:last-child { color: blue; }
</style>
<div class="example-code" id="example-code-1">
  <ul>
    <li>1. List 1-1</li>
    <ul>
      <p>2. Paragraph 2-1</p>
      <li>3. List 2-2</li>
      <li>4. List 2-3</li>
      <li>5. List 2-4</li>
    </ul>
    <li>6. List 1-3</li>
    <li>7. List 1-4</li>
  </ul>
</div>

### 3. `:nth-child` 和 `:nth-last-child`

{% highlight css linenos %}
E:nth-child(n) { /* properties */ }
E:nth-last-child(n) { /* properties */ }
{% endhighlight %}

这两个是 CSS Level 3 里定义的伪类，其中括号里的 n 可以替换成 **整数** ( 1 ~ 兄弟元素个数 )、**关键字** ( odd / even ) 或 **公式** ( an+b )

`:nth-child` 用来选择 **E 中的每个元素在其兄弟元素（无论是否符合 E）中的位置索引符合括号里的表达式的 E 的集合**。<i class="fa fa-exclamation-triangle"></i> 注意，第一个兄弟元素的位置索引是 1 ，往后依次加 1 ，遇到非亲结点兄弟元素（如堂兄弟元素）将重置计数 ；如果括号里是公式 an+b，则其中 n 的值将是使 an+b 的值尽可能覆盖位置索引的非负整数。

`:nth-last-child` 用来选择 **E 中的每个元素在其兄弟元素（无论是否符合 E）中的逆向位置索引符合括号里的表达式的 E 的集合**。<i class="fa fa-exclamation-triangle"></i> 注意，这里的逆向位置索引和上面的正好反过来，即最后一个元素的位置索引是 1，往前依次加 1

用法示例：

- `tr:nth-child(1)`，等同于 `tr:first-child`，选择第一行
- `tr:nth-child(3)`，选择第三行
- `tr:nth-child(2n+1)`，等同于 `tr:nth-child(odd)`，选择奇数行
- `tr:nth-child(2n)`，等同于 `tr:nth-child(even)`，选择偶数行
- `tr:nth-child(-n+3)`，选择前三行，
- `tr:nth-last-child(-n+3)`，选择最后三行

**示例 HTML <i class="fa fa-caret-down"></i>**
{% highlight html linenos %}
<ul>
  <li>1. List 1-1</li>
  <ul>
    <p>2. Paragraph 2-1</p>
    <li>3. List 2-2</li>
    <li>4. List 2-3</li>
    <li>5. List 2-4</li>
  </ul>
  <li>6. List 1-3</li>
  <li>7. List 1-4</li>
</ul>
{% endhighlight %}

**示例 CSS <i class="fa fa-caret-down"></i>**

{% highlight css linenos %}
li:nth-child(1) { text-decoration: line-through; }  /* 第一个 */
li:nth-child(3) { text-decoration: underline; }     /* 第三个 */
li:nth-child(odd) { text-transform: uppercase; }    /* 奇数个 */
li:nth-child(-n+2) { font-weight: bold; }           /* 前两个 */
li:nth-last-child(-n+2) { font-style: italic; }     /* 后两个 */
{% endhighlight %}

**效果 <i class="fa fa-caret-down"></i>**

<style type="text/css">
#example-code-2 li:nth-child(1) { text-decoration: line-through; }
#example-code-2 li:nth-child(3) { text-decoration: underline; }
#example-code-2 li:nth-child(odd) { text-transform: uppercase; }
#example-code-2 li:nth-child(-n+2) { font-weight: bold; }
#example-code-2 li:nth-last-child(-n+2) { font-style: italic; }
</style>
<div class="example-code" id="example-code-2">
  <ul>
    <li>1. List 1-1</li>
    <ul>
      <p>2. Paragraph 2-1</p>
      <li>3. List 2-2</li>
      <li>4. List 2-3</li>
      <li>5. List 2-4</li>
    </ul>
    <li>6. List 1-3</li>
    <li>7. List 1-4</li>
  </ul>
</div>

由于 CSS 中能够相互覆盖的属性有限，所有接下来使用 JavaScript 来为每个选中的元素附上其被选中的规则

**示例 JavaScript (部分) <i class="fa fa-caret-down"></i>**

{% highlight javascript linenos %}
(function() {
  var nth_child_1 = document.querySelectorAll("li:nth-child(1)");
  Array.prototype.forEach.call(nth_child_1, function( node ){
    node.innerText += "<span style='color: red;'> nth-child(1)</span>";
  });
})();
{% endhighlight %}

<div class="example-code" id="example-code-3">
  <ul>
    <li>1. List 1-1</li>
    <ul>
      <p>2. Paragraph 2-1</p>
      <li>3. List 2-2</li>
      <li>4. List 2-3</li>
      <li>5. List 2-4</li>
    </ul>
    <li>6. List 1-3</li>
    <li>7. List 1-4</li>
  </ul>
</div>

<script type="text/javascript">
(function() {
  var nth_child_1 = document.querySelectorAll("#example-code-3 li:nth-child(1)");
  var nth_child_3 = document.querySelectorAll("#example-code-3 li:nth-child(3)");
  var nth_child_odd = document.querySelectorAll("#example-code-3 li:nth-child(odd)");
  var nth_child_n_2 = document.querySelectorAll("#example-code-3 li:nth-child(-n+2)");
  var nth_last_child_n_2 = document.querySelectorAll("#example-code-3 li:nth-last-child(-n+2)");
  Array.prototype.forEach.call(nth_child_1, function( node ){
    node.innerHTML += "<span style=\"color: red;\">\tnth-child(1)</span>";
  });
  Array.prototype.forEach.call(nth_child_3, function( node ){
    node.innerHTML += "<span style=\"color: maroon;\">\tnth-child(3)</span>";
  });
  Array.prototype.forEach.call(nth_child_odd, function( node ){
    node.innerHTML += "<span style=\"color: fuchsia;\">\tnth-child(odd)</span>";
  });
  Array.prototype.forEach.call(nth_child_n_2, function( node ){
    node.innerHTML += "<span style=\"color: olive;\">\tnth-child(-n+2)</span>";
  });
  Array.prototype.forEach.call(nth_last_child_n_2, function( node ){
    node.innerHTML += "<span style=\"color: teal;\">\tnth-last-child(-n+2)</span>";
  });
})();
</script>

### 4. `:nth-of-type` 和 `:nth-last-of-type`

{% highlight css linenos %}
E:nth-of-type(n) { /* properties */ }
E:nth-last-of-type(n) { /* properties */ }
{% endhighlight %}

`:nth-of-type` 用来选择 **E 中的每个元素在其只符合 E 的兄弟元素中的位置索引符合括号里的表达式的 E 的集合**

`:nth-last-of-type` 与 `:nth-last-child` 同理，把 `:nth-of-type` 位置索引逆序查找即可

**示例 HTML <i class="fa fa-caret-down"></i>**
{% highlight html linenos %}
<ul>
  <li>1. List 1-1</li>
  <ul>
    <p>2. Paragraph 2-1</p>
    <li>3. List 2-2</li>
    <li>4. List 2-3</li>
    <li>5. List 2-4</li>
  </ul>
  <li>6. List 1-3</li>
  <li>7. List 1-4</li>
</ul>
{% endhighlight %}

**示例 CSS <i class="fa fa-caret-down"></i>**

{% highlight css linenos %}
li:nth-of-type(1) { text-decoration: line-through; }  /* 第一个 */
li:nth-of-type(3) { text-decoration: underline; }     /* 第三个 */
li:nth-of-type(odd) { text-transform: uppercase; }    /* 奇数个 */
li:nth-of-type(-n+2) { font-weight: bold; }           /* 前两个 */
li:nth-last-of-type(-n+2) { font-style: italic; }     /* 后两个 */
{% endhighlight %}

**效果 <i class="fa fa-caret-down"></i>**

<style type="text/css">
#example-code-4 li:nth-of-type(1) { text-decoration: line-through; }
#example-code-4 li:nth-of-type(3) { text-decoration: underline; }
#example-code-4 li:nth-of-type(odd) { text-transform: uppercase; }
#example-code-4 li:nth-of-type(-n+2) { font-weight: bold; }
#example-code-4 li:nth-last-of-type(-n+2) { font-style: italic; }
</style>
<div class="example-code" id="example-code-4">
  <ul>
    <li>1. List 1-1</li>
    <ul>
      <p>2. Paragraph 2-1</p>
      <li>3. List 2-2</li>
      <li>4. List 2-3</li>
      <li>5. List 2-4</li>
    </ul>
    <li>6. List 1-3</li>
    <li>7. List 1-4</li>
  </ul>
</div>

同样，下面使用 JavaScript 来使结果更加直观

<div class="example-code" id="example-code-5">
  <ul>
    <li>1. List 1-1</li>
    <ul>
      <p>2. Paragraph 2-1</p>
      <li>3. List 2-2</li>
      <li>4. List 2-3</li>
      <li>5. List 2-4</li>
    </ul>
    <li>6. List 1-3</li>
    <li>7. List 1-4</li>
  </ul>
</div>

<script type="text/javascript">
(function() {
  var nth_of_type_1 = document.querySelectorAll("#example-code-5 li:nth-of-type(1)");
  var nth_of_type_3 = document.querySelectorAll("#example-code-5 li:nth-of-type(3)");
  var nth_of_type_odd = document.querySelectorAll("#example-code-5 li:nth-of-type(odd)");
  var nth_of_type_n_2 = document.querySelectorAll("#example-code-5 li:nth-of-type(-n+2)");
  var nth_last_of_type_n_2 = document.querySelectorAll("#example-code-5 li:nth-last-child(-n+2)");
  Array.prototype.forEach.call(nth_of_type_1, function( node ){
    node.innerHTML += "<span style=\"color: red;\">\tnth-of-type(1)</span>";
  });
  Array.prototype.forEach.call(nth_of_type_3, function( node ){
    node.innerHTML += "<span style=\"color: maroon;\">\tnth-of-type(3)</span>";
  });
  Array.prototype.forEach.call(nth_of_type_odd, function( node ){
    node.innerHTML += "<span style=\"color: fuchsia;\">\tnth-of-type(odd)</span>";
  });
  Array.prototype.forEach.call(nth_of_type_n_2, function( node ){
    node.innerHTML += "<span style=\"color: olive;\">\tnth-of-type(-n+2)</span>";
  });
  Array.prototype.forEach.call(nth_last_of_type_n_2, function( node ){
    node.innerHTML += "<span style=\"color: teal;\">\tnth-last-of-type(-n+2)</span>";
  });
})();
</script>

通过对比可以明显发现 `:nth-child` 和 `:nth-of-type` 的区别。比如第 5 行，尽管这个 li 处于父 ul 的第 4 的位置，但是由于兄弟元素的第一个为 p，所以要从第二个元素开始计数的第 3 就是第 5 行的这个 li

### 5. 扩展阅读

- [Pseudo Classes Specifications](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
- [CSS 选择器兼容性表](https://kimblim.dk/css-tests/selectors/)
- [交互式结构性伪类测试器](http://lea.verou.me/demos/nth.html)
