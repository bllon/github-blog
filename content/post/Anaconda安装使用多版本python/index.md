---
title: Anaconda安装
description: Windows下anaconda安装，使用多版本python
slug: anaconda-install
date: 2023-07-22
image:
categories:
- Python
tags:
- Python
- Anaconda
---

## anaconda官网下载地址
[官网地址](https://www.anaconda.com/download)

直接下一步安装即可

## 配置环境变量
```
D:\ProgramData\anaconda3
D:\ProgramData\anaconda3\Scripts
D:\ProgramData\anaconda3\Library\mingw-w64\bin
D:\ProgramData\anaconda3\Library\usr\bin
D:\ProgramData\anaconda3\Library\bin
```

```
查看python版本
python

查看conda版本
conda --version

查看环境
conda info
conda info -e
conda env list
conda info --envs
```

## 创建虚拟环境
```
conda create --name env python=3.9.0

切换环境
conda activate env

退出环境
conda deactivate

删除环境
conda remove -n env --all
```

## PowerShell无法切换环境
```
允许本地脚本
Set-ExecutionPolicy RemoteSigned

重置conda环境
conda init powershell

重新打开窗口
conda env list
```