---
layout: post
title:  "Rails 为 Controller 指定 JS 和 CSS"
categories:
comments: true
share: true
---

新建的 Rails App 的 `app/assets/javascript/application.js` 中通常会有以下两项：

//= require_tree .

//= require turbolinks

第一项的作用是启用递归调用，将 `assets/javascript/`下的所有文件包括子文件夹下的文件全部包含到页面中，CSS 同理。第二项的作用是启用 turbolinks 机制，即点击页面上的应用内的跳转链接，会通过 Ajax 比较两个页面的不同从而快速加载。

这两个功能造成了几个坑爹的现象：

1. 页面会一次性加载所有的 CSS 文件，如果对于不同的 Controller 下的 view 使用了同名的 CSS 选择器名，则会出现冲突

2. 如果把 `require_tree .` 选项关掉，在头部使用 `<%= javascript_include_tag params[:controller] %>` 和 `<%= stylesheet_link_tag params[:controller] %>` 来为每个  Controller 之间 指定 JS 和 CSS 文件，同时也开启了 `require turbolinks`，则在 Controller 之间链接跳转的时候，不会重新加载 CSS

3. 开启了 `require turbolinks`，链接跳转的时候页面载入完成不能通过 document.ready 来判断，对应的 CoffeeScript 的 `$ ->`
