---
title: vim写Qt
date: 2021-07-25 13:03:17
tags: Qt 
categories: vim
---

## Qt项目结构

Qt的项目结构写在.pro文件中。下面是一个最基本的.pro文件。

```
QMAKE_CC = clang 
QMAKE_CXX = clang++

#qt module
QT += core gui
QT += widgets

#output file name
TARGET    = output

#build an application
TEMPLATE  = app

#resource file
RESOURCES = res/res.qrc

#output directory
DESTDIR = $$PWD/builds

#build directory
OBJECTS_DIR = $${DESTDIR}/.objects
MOC_DIR = $${DESTDIR}/.moc
RCC_DIR = $${DESTDIR}/.rcc
UI_DIR = $${DESTDIR}/.ui

#cpp file
SOURCES  += src/*.cpp

#header file
HEADERS  += include/*.h

```

有了.pro文件，通过qmake命令就可以生成Makefile文件。

## 代码补全

补全我是用YCM插件，YCM有两种方法可以提供补全。
- 编译器是clang，可以使用编译数据库文件compile_commands.json

- 其他编译器，需要将编译标志写在.ycm_extra_conf.py文件中

### compile_commands.json

首先安装bear这个软件，项目地址`https://github.com/rizsotto/Bear`。
bear可以通过Makefile文件生成compile_commands.json文件。
执行命令`bear -- make`，就可以将Makefile中的编译标志告诉bear生成compile_commands.json。

### .ycm_extra_conf.py 

对于.ycm_extra_conf.py, 可以通过YCM-Generator这个vim插件来生成。
注意，这个插件生成的编译标志只适用于Qt。
vim执行`:CCGenerateConfig`, 然后就会在当前目录生成.ycm_extra_conf.py文件，注意当前目录，必须存在Makefile文件。


