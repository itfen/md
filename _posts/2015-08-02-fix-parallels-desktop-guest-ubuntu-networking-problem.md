---
layout: post
title:  "修复 Parallels Desktop 的 Ubuntu 虚拟机网络问题"
categories:
comments: true
share: true
---

最近在 Ubuntu 下做了些配置导致 Ubuntu 不能联网，右上角网络符号为不断连接的无线网络符号，打开网页无法访问。

Parallels Desktop > Preferences > Advanced > Network > Change Settings > Restore Defaults 重制 Parallels 的网络接口

然后在 Ubuntu 中编辑 `/etc/resolv.conf` （如果没有则创建），添加：
{% highlight bash linenos %}
nameserver 114.114.114.114
nameserver 8.8.8.8
{% endhighlight %}
