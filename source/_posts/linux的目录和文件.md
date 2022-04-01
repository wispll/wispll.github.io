---
title: linux的目录和文件
date: 2022-04-01 19:01:12
tags:
categories: linux
---

#### ~/.profile

/bin/sh 的登录配置文件。当一个可登录交互式shell成功登录后会调用该文件。
兼容sh的shell，如bash，也会调用该文件。

#### ~/.bashrc

当启动一个可交互bash会调用该文件。

#### ~/.bash_profile

/bin/bash的登录配置文件。

#### ~/.bash_logout

当用户登出后调用

#### ~/.bash_history

记录输入的命令

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




