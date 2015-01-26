---
layout: post
title:  "使用 Jekyll 和 Github Pages 搭建博客"
categories:
comments: true
share: true
---
[Github Pages][Github Pages] 提供免费无限流量的静态 HTML 网站托管，[Jekyll][Jekyll] 是基于 Ruby 的用于生成静态网站的程序，支持 Markdown 撰写内容，以及解析 Liquid 模板。Github Pages 官方支持 Jekyll，只需上传 Jekyll 网站源文件到与 Github Pages 对应的代码仓库的对应分支即可自动生成网站，并可绑定自己的域名。

### 1. 创建 Github Pages 源代码仓库

在 Github 上新建一个 Repository ，命名为 `username.github.io`，其中 username 就是账户名。在 master 分支里放入静态 HTML
文件，通过网址 `http://username.github.io` 即可直接访问到。

### 2. 搭建本地测试环境

如果不搭建本地环境，更改任何代码、添加或编辑文章，只能通过 commit 和 push 上传到 Github 才能查看效果，速度很慢。所以需要在本地搭建和
Github Pages 相同的环境来进行测试。由于 Github 上不支持 Jekyll 插件（插件需要运行 Ruby 程序，这样 Github Pages 就成 Github Server 了）

[Github Pages]: https://pages.github.com/
[Jekyll]:       http://jekyllrb.com/
