---
title: MinGW安装（gcc）
description: Windows下MinGW详细安装教程
slug: mingw-install
date: 2023-07-22
image:
categories:
- C++
tags:
- gcc
- MinGW
---

## 介绍
> **MinGW，是Minimalist GNU for Windows的缩写。
> 它是一个可自由使用和自由发布的Windows特定头文件和使用GNU工具集导入库的集合，
> 允许你在GNU/Linux和Windows平台生成本地的Windows程序而不需要第三方C运行时（C Runtime）库。
> MinGW 是一组包含文件和端口库，其功能是允许控制台模式的程序使用微软的标准C运行时（C Runtime）库（MSVCRT.DLL）,
> 该库在所有的 NT OS 上有效，在所有的 Windows 95发行版以上的 Windows OS 有效，
> 使用基本运行时，你可以使用 GCC 写控制台模式的符合美国标准化组织（ANSI）程序，
> 可以使用微软提供的 C 运行时（C Runtime）扩展，与基本运行时相结合，
> 就可以有充分的权利既使用 CRT（C Runtime）又使用 WindowsAPI功能**。

## 下载安装
[下载地址](https://sourceforge.net/projects/mingw-w64/files/mingw-w64/)

选择一个版本, 例如 MinGW-W64 GCC-8.1.0
```azure
64位下载 x86_64-posix-seh
32位下载 x86_64-win32-seh
```

点击对应链接等待5秒下载, 下载后解压里面会包含一个mingw64的目录, 只需要保留该目录即可

接着配置环境变量, 将mingw64/bin目录添加到系统变量的Path变量中

## 验证安装
cmd打开一个命令行窗口, 输入gcc -v 得到gcc的版本信息即安装成功