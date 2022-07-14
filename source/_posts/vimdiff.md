---
title: vimdiff
date: 2022-07-14 09:40:21
tags: 
categories: vim
---

vimdiff 可以比较两个文件的差异。`vimdiff file1 file2`

## 快查表

`do` get change from other window into the current window

`dp` put the changes from current window into the other window

`]c` jump to the next change

`[c` jump to the previous change

`zo` upen fold

`zc` close flod

`zr` reducing folding level

`zm` one more folding level

`zR` extend Most

`zM` fold Most

`:diffupdate :diffu` recalculate the diff

`:e` reload the files if they have been modified outside of vimdiff

`set noscrollbind` temporaily disable simultaneous scrolling

`set diffopt=context:n` set a fold context lines. default is 6
