---
title: linux的目录和文件
date: 2022-04-01 19:01:12
tags:
categories: linux
---

#### ~/.profile

/usr/bin/sh的登录配置文件。任何兼容sh的shell，登录时也会调用

#### ~/.bash_profile

/usr/bin/bash的登录配置文件。
默认只有一句`[[ -f ~/.bashrc ]] && . ~/.bashrc`，即调用.bashrc

#### ~/.bashrc

启动一个可交互,非登录bash会调用

#### ~/.bash_logout

当用户登出后调用

#### ~/.bash_history

记录输入的命令

#### /var/log/

大多数软件的日志目录

#### ~/.config/

存放软件对于当前用户的配置

#### ~/.cache/

存放软件对于当前用户的缓存

#### ~/.local/

存放当前用户的应用。

#### /usr/local/

存放root用户的应用。一般export出bin目录供本机所有用户使用。一般放置有源码的应用，如mysql，jdk...

#### /opt/

同/usr/local/。如idea，pycharm




