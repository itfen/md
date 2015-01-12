---
layout: post
title:  "使用 nginx 和 unicorn 部署多个 Rails 应用"
categories:
comments: true
share: true
---
[nginx][nginx] 做反向代理是很常见的做法，[unicron][unicorn] 是比较流行的 Ruby 语言的 HTTP 服务器，这两者结合起来在一台服务器上部署多个 [Rails][Rails] 程序也是一种常见的应用场景。本文将介绍如何配置及启动服务。

### 1. unicorn 配置文件

在 Rails 应用目录下新建文件

{% highlight bash%}
config/unicorn.rb
{% endhighlight %}

并在 unicorn.rb 文件中添加

{% highlight ruby%}
# Set the working application directory
# working_directory "/path/to/your/app"
working_directory "/home/todos"

# Unicorn PID file location
# pid "/path/to/pids/unicorn.pid"
pid "/home/todos/pids/unicorn.pid"

# Path to logs
# stderr_path "/path/to/log/unicorn.log"
# stdout_path "/path/to/log/unicorn.log"
stderr_path "/home/todos/log/unicorn.log"
stdout_path "/home/todos/log/unicorn.log"

# Unicorn socket
listen "/tmp/unicorn.todos.sock"

# Number of processes
# worker_processes 4
worker_processes 1

# Time-out
timeout 30
{% endhighlight %}

> - ##### 把以上代码中的 todos 替换成自己的 Rails 应用名

### 2. nginx 配置文件

打开文件

{% highlight bash%}
/etc/nginx/nginx.conf
{% endhighlight %}

在 http 配置内添加

{% highlight bash%}
upstream rails_todos {
    server unix:/tmp/unicorn.todos.sock fail_timeout=0;
}

server {
    listen 80;
    server_name todos.nsmss.com;
    root /home/todos/public;
    try_files $uri/index.html $uri @app;
    location @app {
        proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header  Host $http_host;
        proxy_redirect    off;
        proxy_pass        http://rails_todos;
    }
}
{% endhighlight %}

> - ##### 把 upstream 的内容替换成上面 unicorn 配置中 listen 项的 sock 文件
> - ##### 把 server 的 server_name 替换成访问这个 Rails 应用的域名
> - ##### 把 server 的 root 替换成这个 Rails 应用的目录下的 /public

### 3. 启动 unicorn 服务

进入 Rails 应用目录，运行命令

{% highlight bash%}
unicorn_rails -c config/unicorn.rb -D
{% endhighlight %}

### 3. 重启 nginx 服务

{% highlight bash%}
service nginx restart
{% endhighlight %}

[nginx]:        http://nginx.org/
[unicorn]:      http://unicorn.bogomips.org/
[Rails]:        http://rubyonrails.org/
