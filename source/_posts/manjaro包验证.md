---
title: manjaro包验证
date: 2021-07-08 23:44:33
tags: pacman
categories: manjaro
---

## pacman-key 
pacman-key是pacman用来管理受信任证书(公钥)的工具。

`pacman-key --init`

在/etc/pacman.d/gnupg建立新密钥并生成系统主密钥。

`pacman-key --populate keyring`

加载keyring里的公钥

`pacman-key --refresh-keys`

通过远程服务器，更新本地的keyring

## 包更新

一般我们用以下命令进行安装或升级。

`pacman -S <package_name>`

manjaro的软件包是基于PGP进行验证的，所于有时会出现：

`Import PGP key public_key_id, “author_name author_mail”? [Y/n]`

这说明本地，没有下载包的公钥，无法验证这个包的合法性

按Y之后，会从远端服务器下载这个公钥，但前提是要在/etc/pacman.d/gnupg/gpg.conf配置公钥证书服务器的地址

manjaro默认是没有配置这个地址的，所以：

`error: key “public_key” could not be looked up remotely`

但一般只要更新keyring，就能获取最新的公钥

`pacman -Sy archlinuxcn-keyring manjaro-keyring`

pacman的密钥信息存储在/etc/pacman.d/gnupg 默认是只导入了manjaro的keyring。所以为了用arch的包，我也导入了archlinuxcn-keyring

## 包降级

### downgrade

`downgrade <package_name>` 就会列出可以降级的版本，根据命令提示从中选择就行

需要注意的是，它会从本地缓存提取以前的安装版本和远端可回退的版本。但是，如果软件是包属于stable分支,那只会提供本地的版本。

### 本地安装覆盖

1.下载以前版本的安装包

2.`pacman -U /root/Download/packagename.tar.gz`


