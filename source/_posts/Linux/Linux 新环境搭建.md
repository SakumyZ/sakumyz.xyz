---
title: Linux 新环境搭建
date: 2022-11-02
author: SakumyZ
img: https://www.freecodecamp.org/news/content/images/size/w300/2022/02/gabriel-heinzer-4Mw7nkQDByk-unsplash.jpg
categories: Linux
tags: Linux
---

# Linux 新环境搭建

## 1. ZSH 安装及其美化

### 1.1 zsh 本体安装

```shell
# 安装
$ sudo yum install -y zsh

# 切换shell
$ chsh -s /bin/zsh
```

### 1.2 oh-my-zsh 安装

```shell
$ sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

如果出现以下界面表示成功

```shell

__                                     __
  ____  / /_     ____ ___  __  __   ____  _____/ /_
 / __ \/ __ \   / __ `__ \/ / / /  /_  / / ___/ __ \
/ /_/ / / / /  / / / / / / /_/ /    / /_(__  ) / / /
\____/_/ /_/  /_/ /_/ /_/\__, /    /___/____/_/ /_/
                        /____/                       ....is now installed!


Please look over the ~/.zshrc file to select plugins, themes, and options.

p.s. Follow us at https://twitter.com/ohmyzsh.

p.p.s. Get stickers and t-shirts at http://shop.planetargon.com.

```

### 1.3 主题安装

安装 `powerlevel9k`

先下载主题

```shell
$ git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```

下载主题对应字体

```shell
$ mkdir -p ~/.local/share/fonts
$ cd ~/.local/share/fonts
$ curl -fLo "DejaVu Sans Mono Nerd Font Complete.ttf" https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/DejaVuSansMono/Regular/complete/DejaVu%20Sans%20Mono%20Nerd%20Font%20Complete.ttf
```

安装字体

```shell
$ yum install -y fontconfig mkfontscale

$ cd /usr/share/fonts/

$ mkfontscale

$ mkfontdir

$ fc-cache
```

验证字体是否安装成功

```shell
$ fc-match
# 显示下面则成功
# DejaVuSans.ttf: "DejaVu Sans" "Book"
```

在 `.zshrc` 修改主题

```shell
ZSH_THEME="powerlevel9k/powerlevel9k"
```

## 2. Screenfetch

```shell
# 放在bin里，方便调用
$ cd /bin
$ wget -O screenfetch https://git.io/vaHfR
# 增加运行权限
$ chmod +x screenfetch
```

将 `screenfetch` 添加到 `.zshrc` 里，访问系统则自动显示

```shell
                   ..                    root@VM-8-4-centos
                 .PLTJ.                  OS: CentOS
                <><><><>                 Kernel: x86_64 Linux 3.10.0-1127.19.1.el7.x86_64
       KKSSV' 4KKK LJ KKKL.'VSSKK        Uptime: 4h 28m
       KKV' 4KKKKK LJ KKKKAL 'VKK        Packages: 589
       V' ' 'VKKKK LJ KKKKV' ' 'V        Shell: zsh 5.0.2
       .4MA.' 'VKK LJ KKV' '.4Mb.        Disk: 2.8G / 41G (8%)
     . KKKKKA.' 'V LJ V' '.4KKKKK .      CPU: Intel Xeon Gold 6133 @ 2.494GHz
   .4D KKKKKKKA.'' LJ ''.4KKKKKKK FA.    GPU: Cirrus Logic GD 5446
  <QDD ++++++++++++  ++++++++++++ GFD>   RAM: 319MiB / 1837MiB
   'VD KKKKKKKK'.. LJ ..'KKKKKKKK FV
     ' VKKKKK'. .4 LJ K. .'KKKKKV '
        'VK'. .4KK LJ KKA. .'KV'
       A. . .4KKKK LJ KKKKA. . .4
       KKA. 'KKKKK LJ KKKKK' .4KK
       KKSSA. VKKK LJ KKKV .4SSKK
                <><><><>
                 'MKKM'
                   ''
```

## 3. ZPLUG

```shell
$ curl -sL --proto-redir -all,https https://raw.githubusercontent.com/zplug/installer/master/installer.zsh | zsh
```

## 4. Docker

安装

修改镜像源

## 5. EMQX

```shell
$ docker run -d --name emqx -p 1883:1883 -p 8083:8083 -p 8883:8883 -p 8084:8084 -p 18083:18083 -v /etc/emqx.conf:/etc/emqx.conf  emqx/emqx:4.2.1
```

## 6. Redis

先创建 `Dockerfile`， 建立一个带有配置文件的镜像（6.0.9 版本默认不含配置文件，需要自行打包）

## 7. MySQL

先拉取 Mysql 的镜像。

MySQL 官方 docker hub 镜像仓库地址：[https://hub.docker.com/\_/mysql](https://hub.docker.com/_/mysql)

```shell
$ docker pull mysql{:tag}
# eg: docker pull mysql:8.0
```

[全部 tag](https://hub.docker.com/_/mysql?tab=tags&page=1&ordering=last_updated)

然后 Run 一个容器出来

```shell
 $ docker run --name [some-mysql] -e MYSQL_ROOT_PASSWORD=[my-secret-pw] -d mysql{:tag}
 # eg: docker run --name mysql -e MYSQL_ROOT_PASSWORD=12345678 -d mysql
```

进入该容器

```shell
$ docker exec -it [container-name]|[container-id] /bin/bash
# eg: docker exec -t mysql /bin/bash
```

进入 MySQL 数据库

```shell
$ mysql -u root -p
# 然后输入密码, 就可以进入mySQL了
```

下面介绍如何快速进入 MySQL

先使用 `vi mysql-cli` 命令创建一个 shell 脚本，当然脚本的名称随意，我这里就取名叫 `mysql-cli`内容如下

```shell
#!/bin/bash

mysql -u root -p
```

然后将脚本提权并复制到容器内

```shell
# 提权
$ chmod 777 mysql-cli
# 复制到mysql 容器内
$ docker cp mysql-cli mysql:/bin
```

上述 `docker cp` 命令的意思是，将当前目录下的 mysql-cli 文件，复制到 mysql 容器的 `/bin` 目录下

然后最后一步，进入 `.zshrc` 里，将设置一个快速访问的别名

```shell
alias mysql-cli="docker exec -it /bin/mysql-cli"
```

使用 `source ~/.zshrc` 命令 更新下 .zshrc 文件，就可以使用，`mysql-cli` 命令，直接进入 docker 容器中的 mysql 数据库了。

## 8. Nginx

先新建一个用于存放挂载文件的文件夹 `/usr/local/docker/nginx`

```shell
$ mkdir -p /usr/local/docker/nginx
$ cd /usr/local/docker/nginx
$ mkdir -p html conf logs
```

拉取 Nginx 镜像

```shell
$ docker pull nginx
```

先采用不挂载的方式，启动一个容器，我们主要是先获取 Nginx 的默认配置

```shell
docker run -d --name nginx nginx

# 拷贝容器内 Nginx 默认配置文件到本地当前目录下的 conf 目录（$PWD 当前全路径）
$ docker cp nginx:/etc/nginx/nginx.conf $PWD/conf
$ docker cp nginx:/etc/nginx/conf.d $PWD/conf
```

删除刚才创建的容器

```shell
$ docker stop nginx
$ docker rm nginx
```

挂载运行容器

```shell
docker run -d -p 80:80  \
              -p 443:443  \
 --name nginx \
 -v /usr/local/docker/nginx/html:/usr/share/nginx/html \
 -v /usr/local/docker/nginx/conf/nginx.conf:/etc/nginx/nginx.conf \
 -v /usr/local/docker/nginx/conf/conf.d:/etc/nginx/conf.d \
 -v /usr/local/docker/nginx/logs:/var/log/nginx \
 nginx
```

> -d _# 表示在一直在后台运行容器_

    -p 80:80 _# 对端口进行映射，将本地80端口映射到容器内部的80端口_
    --name _# 设置创建的容器名称_
    -v _# 将本地目录(文件)挂载到容器指定目录；_

## 9. Jupyter

```shell
$ docker run -i -t  -d --name jupyter-server -p 8888:8888 continuumio/miniconda3 /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --allow-root --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser"
```

## 常用命令添加别名

在 `.zshrc` 中添加一下代码

```shell
alias cls="clear"
alias ll="ls -l"
alias la="ls -a"
alias lla="ls -la"
alias home="cd ~"
alias python="python3"
alias pip="pip3"
```
