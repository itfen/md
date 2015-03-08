---
layout: post
title:  "管理 Rails 前端框架或库的最佳方法"
categories:
comments: true
share: true
---

对于 Node.js 家族，[Bower](http://bower.io/) 是比较流行的用来管理各种框架的工具。对于
Rails，普通的方法是在 [RubyGems](https://rubygems.org/) 上找需要的前端框架对应的
Gem，并添加到 Gemfile 中。但这种方法并不能很好的解决依赖关系，而且大多数的这种 Gem
是由第三方的开发者开发，并不能保证框架的原汁原味以及与最新版同步。

后来发现个网站：[Rails Assets](https://rails-assets.org/) 可以很好的解决这个问题，相当于
Bundler 和 Bower 之间的桥梁。直接搜索需要的框架名，安装指示将其添加到 Gemfile，运行 Bundle
Install，然后在 application.js、application.css 或者其他地方引用框架即可。
