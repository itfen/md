---
layout: post
title:  "MacOS X 连上 Wi-Fi 后任务栏图标仍带感叹号"
categories:
comments: true
share: true
---

配置无线网络的时候，可能是由于路由器的 DNS 配置有问题，导致电脑 Wi-Fi 连上了也能访问 Internet，但是任务栏图标还是会出现带感叹号的图标:
![icon](http://support.apple.com/library/APPLE/APPLECARE_ALLGEOS/TS3611/TS3611_new----en.png)
提示信息是： No Internet Connection...

![My helpful screenshot]({{ site.url }}/assets/img/20150120-3.png)

解决这个问题的方法很多，网上甚至有通过 Terminal 删除配置文件的做法，但其实有个更简单的方法：

打开 Network Preferences 在窗口的顶部有个 Location 选项，点击它选 Edit Locations，添加一项，确定后点 Apply
这时候会重新连接网络，连上了应该就会回到正常的网络图标了。

使用 Location 选项还能用来切换网络 DNS ，使用路由器的时候选择配置了 8.8.8.8 的 DNS 的设置，使用诸如 CMCC
这种需要打开验证网页的网络时就切换到 DNS 为空白的设置。
