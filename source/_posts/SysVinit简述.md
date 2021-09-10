---
title: SysVinit简述
date: 2021-09-10 22:43:45
tags: [Linux, init]
categories: SysVinit
---

## 什么是SysVinit

/sbin/init是Linux内核加载后执行的第一个进程，是所有进程的父进程，pid=1。
SysVinit是init程序的一种。当使用SysVinit时，/sbin/init指向SysVinit。

## 配置文件

SysVinit的配置文件位于/etc/inittab，格式如下：

`id:runlevels:action:process`

下面一个例子，表示当进入运行级别为3的时候，执行/etc/rc.d/rc.3目录下的脚本

`1:3:wait:/etc/rc.d/rc.3`

## 运行级别

- 0：关机

- 1：单用户模式(又叫S)

- 2：多用户模式（不联网，基于文本）

- 3：多用户模式（联网，基于文本）

- 5: X11（基于GUI）

- 6：关机

不同发行版运行级别略有不同，但0，1，6是通用的。

## init.d

一般在配置文件中会配置有各个级别脚本的存放目录，如rc.0、rc.1、rc.2、rc.3、rc.4、rc.5、rc.6。

但所有rc.x目录中的脚本其实都是指向/etc/init.d/目录下脚本的软链接。

```bash
cd /etc/rc.d/rc.4
ls -l
K01apache-htcacheclean -> ../../init.d/apacheclean
S01cron -> ../../init.d/cron
...
...
...
```

K(Kill)，表示该脚本会停用某些服务。
S(start). 表示启用某些服务。
01是编号，代表执行顺序。

## 小结

一般我们只想在init.d下面写一些启动脚本，而不想手动维护SysVinit繁琐的配置，可以借助chkconfig等一些工具。

SysVinit是继承自System V的一套init方案，历史悠久，被众多发行版效仿。但它也有自己的局限，如脚本串行执行，脚本书写复杂等。

所以当systemd诞生后，越来越多的发行版已经迁移到systemd上了。

## 附录

#### 文章参考

- [SysVint](https://wiki.archlinux.org/title/SysVinit)

- [An introduction to services, runlevels, and rc.d scripts](https://www.linux.com/news/introduction-services-runlevels-and-rcd-scripts/)

- [Starting Your Software Automatically on Boot](https://tldp.org/HOWTO/HighQuality-Apps-HOWTO/boot.html)

- [The Story Behind ‘init’ and ‘systemd’](https://www.tecmint.com/systemd-replaces-init-in-linux/)
