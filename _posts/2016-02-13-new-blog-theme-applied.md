---
layout: post
title:  "博客新主题"
categories: Blog
comments: true
share: true
---

折腾了两天终于切到了新主题，jekyll 也升级到了 3.x

源码地址：[https://github.com/mdluo/mdluo.github.io](https://github.com/mdluo/mdluo.github.io)，也可点击右上角 GitHub 图标跳转到

主题主要部分基于 [end2end](https://github.com/nandomoreirame/end2end)，文章内容样式参考 [Kiko](https://github.com/gfjaru/Kiko)

调整优化移动设备显示效果：屏幕较小时隐藏右上角 GitHub 图标及分享图标

静态资源使用又拍云 (upyun) CDN 加速：[https://www.upyun.com](https://www.upyun.com)

开启了全站 HTTPS，方法是在 `_config.yml` 中设置 `enforce_ssl: mdluo.github.io`，并在页面头部加入判断代码，参考：[https://github.com/isaacs/github/issues/289](https://github.com/isaacs/github/issues/289)

域名换回 `mdluo.github.io`，防止自己的域名被墙，同时也可以使用 [Git.io](https://git.io/) 为博客设置短 URL

底部个人社交媒体图标来自网上的 SVG 并进行了调整统一样式，加上了网站的颜色

文章详情页底部使用了 CC-BY 的 SVG 图标以及 [share.js](http://overtrue.me/share.js/) 做分享到社交媒体图标

背景使用了 [Dimitrie Hoekstra](http://dhesign.com/) 制作的 [GPlay](http://subtlepatterns.com/gplay/)，更多背景样式可以在 [Subtle Patterns](http://subtlepatterns.com/) 上找到

**Todos:**

- 完善 About、Tags、Wikis 页面
- License 文件及 About 页面加上引用的第三方内容的版权信息
- 参考 [onepice](https://github.com/guovz/onepice)、[Neo-HPSTR](https://github.com/aron-bordin/neo-hpstr-jekyll-theme)、[Scribble](https://github.com/muan/scribble)、[dbyll](https://github.com/dbtek/dbyll) 等主题为博客添加 Tag 页面、前后文章切换、作者信息、焦点图、回到顶部等功能
