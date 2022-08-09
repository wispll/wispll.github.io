---
title: 系统更新后virtualbox打不开镜像
date: 2022-08-09 10:08:56
tags: 
categories: virtualbox
---

不久前，更新系统后，virtualbox的win10镜像打不开。

因为不怎么用，所以一直没有怎么管它。

最近想用一用，决定修一修。

各种排查后发现是插件`virtualbox-ext-oracle`版本不对

```bash
pacman -Qs virtualbox

local/linux515 5.15.57-2
    The Linux515 kernel and modules
local/linux515-virtualbox-host-modules 6.1.36-4 (linux515-extramodules)
    Virtualbox host kernel modules for Manjaro Kernel
local/virtualbox 6.1.36-1
    Powerful x86 virtualization for enterprise as well as home use
local/virtualbox-ext-oracle 6.1.34-1
    Oracle VM VirtualBox Extension Pack
local/virtualbox-guest-iso 6.1.36-1
    The official VirtualBox Guest Additions ISO image
```

可以看到里面有一个`6.1.34-1`的版本

通过`pacman -Qi`对比查看，可以发现上一次滚动更新这小子没有更新。

通过`pacman -Ss`发现除了`virtualbox-ext-oracle`是aur仓库，其他全是comunity仓库的。

原因猜测大概是更新的时候，aur的源相对community的源滞后了。


