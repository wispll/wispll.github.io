---
title: vim容易忘记的命令操作
date: 2021-12-21 17:06:40
tags:
categories: vim
---

#### 不退出vim，重新加载.vimrc

```vim
:so <path_of_vimrc> "so是source的缩写，符号%指当前打开的文件。

```

#### 输出所有按键映射

```vim
:nmap  "显示所有normal模式下的映射
:vmap  "...
:imap  "... 这种方式有个缺点，显示的映射无法用`/`快速查找

"一般我会输出到文件，再慢慢看
:redir! > vim_keys.txt   "redir表示接下来的输出会重定向到某个文件，!为overwrite
:silent verbose map      "silent [function] 不在屏幕显示函数的输出
:redir END               "重定向结束

```
