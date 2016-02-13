---
layout: post
title:  "使用 PHP 和 GitHub Webhooks 实现自动部署"
categories:
comments: true
share: true
---

[https://github.com/mdluo/github-webhook-handler-php](https://github.com/mdluo/github-webhook-handler-php)

- Add a weebhook in the Settings/Webhooks page of your respostory.

- Update the `$secret` and `$path` in the  `github-webhook-handler.php`.

- Upload `github-webhook-handler.php` to your server and copy the URL to it.

- Fill in the webhooks page.

- ssh to your server.

{% highlight bash%}
#if you are using Apache as web server, change `www-data` to `www`
chown -R www-data /path/to/the/repository/
chmod -R g+s /path/to/the/repository/
cd /path/to/the/repository/
sudo -u www-data git pull
{% endhighlight %}

- Save your webhook.

- Reference:
- [http://www.lovelucy.info/auto-deploy-website-by-webhooks-of-github-and-gitlab.html](http://www.lovelucy.info/auto-deploy-website-by-webhooks-of-github-and-gitlab.html)
- [http://www.v2ex.com/t/224238#2](http://www.v2ex.com/t/224238#2)
