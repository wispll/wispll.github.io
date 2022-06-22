---
title: linux时间
date: 2022-06-22 09:19:48
tags: time
categories: linux
---

linux时间，分为系统时间和bios时间。每次开机，系统时间由bios时间决定。

### 修改系统时间

#### date命令

```
date -s "2006-11-23"
date -s "22:07:21" 
date -s "2005-6-4 17:26"
```
#### 通过ntp服务器同步时间

```
ntpdate -u ntp5.aliyun.com
```

### 修改bios时间

```
hwclock --show 显示bios时间
hwclock --systohc 将系统时间写入bios
hwclock --hctosys 将bios时间写入系统
hwclock --help 显示帮助
```
