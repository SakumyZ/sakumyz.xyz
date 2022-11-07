---
title: Nginx安装配置（Ubuntu）
date: 2019-04-15
author: SakumyZ
img: https://tse1-mm.cn.bing.net/th/id/OIP-C.17t0ZrA27MIJWhrH4eCdbAHaCf?pid=ImgDet&rs=1
categories: Linux
tags: Nginx
---

# Nginx

## 1. 安装

进入 `nginx` 下载页 http://nginx.org/en/download.html

选择稳定版（Stable version），右键复制链接地址，以备后用（博主本次下载版本为 1.14.2）

然后在终端中进行一下操作

```shell
cd /usr/loacl/src

wget http://nginx.org/download/nginx-1.14.2.tar.gz

tar -zxvf nginx-1.14.2.tar.gz
```

安装**依赖包 pcre**

```shell
sudo apt-get install libpcre3 libpcre3-dev
```

```shell
sudo ./configure --prefix=/usr/local/nginx
```

运行成功后显示

```
  nginx path prefix: "/usr/local/nginx"
  nginx binary file: "/usr/local/nginx/sbin/nginx"
  nginx modules path: "/usr/local/nginx/modules"
  nginx configuration prefix: "/usr/local/nginx/conf"
  nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
  nginx pid file: "/usr/local/nginx/logs/nginx.pid"
  nginx error log file: "/usr/local/nginx/logs/error.log"
  nginx http access log file: "/usr/local/nginx/logs/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http proxy temporary files: "proxy_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"
  nginx http uwsgi temporary files: "uwsgi_temp"
  nginx http scgi temporary files: "scgi_temp"
```

## 2. 编译

```shell
sudo make && make install
```

## 3. 启动

至此，nginx 已经完全编译，在`/usr/local`下你就可以看到一个`nginx`文件夹,运行它便可以启动 nginx 服务器

```shell
sudo ./usr/local/nginx/sbin/nginx
```

出现以下情况说明 80 端口已经被占用，需要手动解除占用

![1551601586061](http://sakumyz.xyz/static/images/1551601586061.png)

```shell
sudo netstat -antp
```

上面的命令可以看到端口的占用情况

![1551602135039](imgs/1551602135039.png)

上面图中，是我已经启动过了 nginx 所以，自然被 nginx 占用了 80 端口，如果是其他应用，则需将进程杀死，例如上面，我们已知进程号是 25255，则需要

```shell
kill -9 25255
```

### 3.1 欢迎界面

解除占用后，输入域名，就能看到 Nginx 的欢迎界面

![1551601688227](imgs/1551601688227.png)

## 4. Nginx 信号

> Nginx 信号控制表

| 信号      | 说明                                                                       |
| --------- | -------------------------------------------------------------------------- |
| TERM, INT | 立即停止进程                                                               |
| QUIT      | 等待进程结束后再结束进程                                                   |
| HUP       | 平滑地重读配置文件(开启一个新的 worker 进程读取配置文件，然后再关闭旧进程) |
| USR1      | 重读日志，分割日志时使用                                                   |
| USR2      | 平滑地升级 Nginx                                                           |
| WINCH     | 等待进程结束后关闭旧进程(配合 USR2 来进行升级)                             |

## 5. 命令控制

测试配置文件 `./nginx -t`

重启：`./nginx -s reload`

## 6. 配置文件

```shell
sudo vi /usr/local/nginx/conf/nginx.conf
```

### 6.1 配置文件详解

```
# Nginx配置段

# 全局区
#user  nobody;
worker_processes  1;  #子进程的个数，可以修改，一般为CPU数*核数

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;

# 配置Nginx连接的特性
events {
    worker_connections  1024; #一个子进程最多接受1024个连接
}

# 配置http主要段
http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

	# 虚拟主机段
    server {
        listen       80;	#监听端口
        server_name  localhost;	#域名

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {	#响应文件夹
            root   html;	#根目录
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}
```

### 6.2 配置虚拟主机

需要在配置文件的 server 段中配置，配置方法很简单，主要有基于域名，IP 以及端口的配置，其实基本上没有区别

```
 server {
        listen       80;	#监听端口
        server_name  localhost;	#域名

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {	#响应文件夹
            root   html;	#根目录
            index  index.html index.htm;
        }
```

### 6.3 日志管理

Nginx 可以允许针对不同的网站启用不同的 logs，方便管理

在 server 段加上`access_log logs/xxx.log main;`,建议日志名字起网站域名，方便识别。

此时测试配置文件时可以会报错，无法识别 main 格式，是因为配置文件中关于 main 格式的地方被注释掉了，开启就好，大概位于配置文件 20 行左右

### 6.4 反向代理

本文通过 nginx 反向代理 node,以示实验

```
    server {
        listen       80;	#监听端口
        server_name  localhost;	#域名

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm;
        }

         location / {
            proxy_pass http://127.0.0.1:8080;
        }
```

这意味着当有请求路径为“/api”时，nginx 会将请求代理到服务器的 8080 端口去*（即 node 监听的端口）*。我们可以看到主要是要配置` proxy_pass http://127.0.0.1:8080;`

这时候运行我们提前写好的 node 测试代码

```js
const http = require('http')

const server = http.createServer((req, res) => {
  res.statusCode = 200
  res.setHeader('Content-Type', 'text/plain')
  res.end('Hello Nginx\n')
})

server.listen(8080, () => {
  console.log(`server has been launched/`)
})
```

![1551621092991](http://sakumyz.xyz/static/images/1551621092991.png)
