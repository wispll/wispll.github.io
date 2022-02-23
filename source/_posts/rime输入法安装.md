---
title: rime输入法安装
date: 2022-02-16 23:02:19
tags:
categories: rime
---

最近，我把电脑重装了。本想装回googlepinyin，无奈看了下github最后一次提交已是5年前。

```bash

pacman -S fcitx5-im #fcitx5框架和一些基础工具
pacman -S fctx5-rime #rime输入法引擎
pacman -S rime-pinyin-zhwiki #中文词典


环境变量
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx

```

rime输入法切换中文时默认是繁体的，需要配置一下

```bash

#新建
#rime引擎自带多种输入方案，我用luna_pinyin
#其他输入方案，name.custom.yaml
> ~/.local/share/fcitx5/rime/luna_pinyin.custom.yaml

#写入以下内容
# encoding: utf-8
patch:
  switches:
    - name: ascii_mode
      reset: 0
      states: ["中文", "西文"]
    - name: full_shape
      states: ["半角", "全角"]
    - name: simplification
      reset: 1                     #切换默认简体
      states: ["漢字", "汉字"]
    - name: ascii_punct
      states: ["。，", "．，"]
```
