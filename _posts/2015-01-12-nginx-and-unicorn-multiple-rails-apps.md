---
layout: post
title:  "使用 nginx 和 unicorn 部署多个 Rails 应用"
categories:
comments: true
share: true
---
nginx 做反向代理是很常见的做法，unicron 是比较流行的 Ruby 语言的 HTTP 服务器，这两者结合
起来在一台服务器上部署多个 Rails 程序也是一种常见的应用常见。本文将介绍如何配置及启动服务。

- 1. 在 Rails 目录下添加 unicorn 配置文件

{% highlight sh linenos%}
config/unicorn.rb
{% endhighlight %}
