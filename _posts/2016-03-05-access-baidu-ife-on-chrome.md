---
layout: post
title:  "使用 Chrome 访问百度前端学院 IFE"
tags: Web 前端 Chrome
comments: true
share: true
---

<p class="lead"></p>

1. 下载 Chrome 插件：[User-Agent Switcher for Chrome](https://chrome.google.com/webstore/detail/user-agent-switcher-for-c/djflhoibgkdhkhhcedjiklpkjnoahfmg)

2. 在插件的选项里添加一条记录，`User-Agent String` 为：

{% highlight bash linenos %}
Mozilla/5.0 (Linux; U; Android 5.0.2; zh-cn; Redmi Note 3 Build/LRX22G) AppleWebKit/534.24 (KHTML, like Gecko) Version/4.0 Mobile Safari/534.24 T5/2.0 rabbit/1.0 baiduboxapp/7.1 (Baidu; P1 5.0.2)
{% endhighlight %}

3. `Indicator Flag` 为 `IP6`

4. 在已经登录了百度账号的情况下访问：[http://ife.baidu.com/user/editprofile](http://ife.baidu.com/user/editprofile) 
