---
title: Go环境安装
description: Go语言环境详细安装教程
slug: go-install
date: 2023-07-21 17:00:00+0000
image:
categories:
- Go
tags:
- Go
---

#### Windows下安装
一. 下载Go语言sdk
[sdk下载地址](https://golang.google.cn/dl/)
找到stable version版本, 目前已经更新到1.20.6
windows系统64位下载windows-amd64.zip, 32位下载windows-386.zip, 一般都是64位
下载完解压到一个go的目录下

二. 配置环境变量
打开windows文件管理器, 鼠标右键点击此电脑, 点击属性, 点击高级系统设置进入系统属性, 点击环境变量
新建系统变量
GOROOT  =>  go的sdk解压存放目录（例如D:/go）
GOPATH  =>  新建go的项目目录（例如D:/project/go）
找到系统变量中的Path, 双击进入, 新建
%GOROOT%\bin
%GOPATH%\bin

三. 验证安装
win + R 组合键, 输入cmd进入命令行, 输入go version, 输出得到go version go1.20.6 windows/amd64, 即代表安装成功

四. 配置go的代理环境
继续在命令行终端里输入并回车
```shell
go env -w GO111MODULE=on
```
```shell
go env -w GOPROXY=https://goproxy.cn,direct
```

至此windows下的Go环境安装完毕

####Linux下安装
一. 下载Go语言sdk
找到stable version版本, 目前已经更新到1.20.6
linux系统64位下载linux-amd64.tar.gz, 32位下载linux-386.tar.gz, 一般都是64位, 鼠标右键可以复制对应链接
下载完解压到一个go的目录下
```shell
#下载
wget https://golang.google.cn/dl/go1.20.6.linux-amd64.tar.gz

#解压
tar -xzvf go1.20.6.linux-amd64.tar.gz
```

二. 配置环境变量
修改环境变量文件
```shell
vim /etc/profile
```
在最后添加
export GOROOT=/usr/local/go     //GOROOT为解压的go sdk目录
export PATH=$PATH:$GOROOT/bin

保存文件, 执行source /etc/profile使环境变量生效

三. 验证安装
直接在终端输入go version, 输出得到go version go1.20.6 linux/amd64, 即代表安装成功

四. 配置go的代理环境
继续在命令行终端里输入并回车
```shell
go env -w GO111MODULE=on
```
```shell
go env -w GOPROXY=https://goproxy.cn,direct
```

至此linux下的Go环境安装完毕