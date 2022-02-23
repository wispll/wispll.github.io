---
title: linux安装
date: 2022-02-16 22:57:32
tags:
categories: linux
---

## Linux系统安装

### 1.格式化U盘

#### linux 格式化U盘

```bash
#check your usb device name
sudo fdisk -l 
#/dev/sdb is my usb
sudo mkfs.vfat /dev/sdb 
```

#### windows 格式化u盘

* 我的电脑右键 -> 管理

    ![](/images/linux_install/format_1.jpg)

* 可以看到U盘是磁盘1 打开cmd 输出diskpart

    ![](/images/linux_install/format_2.jpg)

* 选择 刚才查看的磁盘 select disk 1 ；格式化 clean

    ![](/images/linux_install/format_3.jpg)

* 右键磁盘1 ，新建分卷

    ![](/images/linux_install/format_4.jpg)

* 分卷格式

    ![](/images/linux_install/format_5.jpg)

### 2.制作U盘启动盘 

#### linux下制作启动盘

```bash

# check usb device name
sudo fdisk -l 
 
sudo dd if=your_iso_file_path of=your_usb_device
```

#### windows下制作启动盘

* 下载镜像文件(.iso)

* 用rufus 将下载的.iso文件制作启动盘 

    ![](/images/linux_install/rufus_1.jpg)

    ![](/images/linux_install/rufus_2.jpg)

### 3.bios 设置

开机按F2（不同的主板有不同快捷键），进入bios。

Boot         -> Boot Mode &emsp;&emsp;   UEFI

&emsp;&emsp; -> USB Boot  &emsp;&emsp;   Enabled

Security     -> Secure Boot &emsp;&emsp; DIsabled

同时需要将USB作为第一启动项(放在设备列表的第一个)，或者开机的时候按F12选择启动方式。

### 4.系统分区

| 挂载点    | 标记        | 类型      | 大小      |
|-----------|-------------|-----------|-----------|
| /boot/efi | boot    esp | Fat32     | 300m      |
| /swap     | swap        | linuxswap | =内存     |
| /         |             | ext4      | 剩余空间  |

