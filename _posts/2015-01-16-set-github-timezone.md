---
layout: post
title:  "配置 Github 提交代码时区"
categories:
comments: true
share: true
---

Github 上的 [帮助文档][Github help] 说明了对于 commit ，使用 commit 中 timestamp 所包含的时区来计算时间；对于在 Github 上的 Pull requests 和 issues ，使用浏览器的时区计算。如果不对本地 git 的时区进行配置，每次 commit 的时区是美国西海岸[太平洋时区][PST] PST(UTC-8)，所以在国内要到下午的4点以后提交的 commit 才会算成今天提交的。

使用一天简单的命令即可把这个时区更改成操作系统设置的时区：

{% highlight bash%}
git config --global log.date local
{% endhighlight %}

如果去国外了先把系统的时区改成当地的时区，然后再运行这条命令就可以了。

[Github help]: https://help.github.com/articles/viewing-contributions-on-your-profile-page/#how-contribution-event-times-are-calculated
[PST]: http://zh.wikipedia.org/wiki/%E5%A4%AA%E5%B9%B3%E6%B4%8B%E6%97%B6%E5%8C%BA
