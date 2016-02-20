---
layout: post
title:  "Rails 为 Controller 指定 JS 和 CSS"
categories:
comments: true
share: true
---

新建的 Rails App 的 `app/assets/javascript/application.js` 中通常会有以下两项：

{% highlight javascript linenos %}
//= require_tree .
//= require turbolinks
{% endhighlight %}

第一项的作用是启用递归调用，将 `assets/javascript/`下的所有文件包括子文件夹下的文件全部包含到页面中，CSS 同理。第二项的作用是启用 turbolinks 机制，即点击页面上的应用内的跳转链接，会通过 Ajax 比较两个页面的不同从而快速加载。

这两个功能造成了几个坑爹的现象：

* 页面会一次性加载所有的 CSS 文件，如果对于不同的 Controller 下的 view 使用了同名的 CSS 选择器名，则会出现冲突

* 如果把 `require_tree .` 选项关掉，在头部使用

{% highlight erb linenos %}
<%= javascript_include_tag params[:controller] %>
<%= stylesheet_link_tag params[:controller] %>
{% endhighlight %}

来为每个  Controller 之间 指定 JS 和 CSS 文件，同时也开启了 `require turbolinks`，则在 Controller 之间链接跳转的时候，不会重新加载 CSS 。

* 开启了 `require turbolinks`，链接跳转的时候页面载入完成不能通过 document.ready 来判断，对应的 CoffeeScript 的 `$ ->`，如果使用这个会导致 Javascript 失效。

以下是解决方法：

* CSS 冲突问题：

在 `app/views/layouts/application.html.erb` 中，为 <body> 指定 Controller 样式，在 body 内、yield 外包裹一层 div，指定 Action 样式，即

{% highlight html linenos %}
<body class="#{controller.controller_name}">
    <div class="#{action_name}">
        = yield
    </div>
</body>
{% endhighlight %}

在 SCSS 中通过层级关系即可方便的实现 Controller 和 Action 指定的样式

* JS 页面状态问题

使用

{% highlight coffeescript linenos %}
ready = ->
# JS代码
$(document).ready(ready)
$(document).on('page:load', ready)
{% endhighlight %}

代替 `$ ->`
