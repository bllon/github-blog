---
title: docker build缓存依赖项
description: docker构建镜像时获取缓存的依赖项,以节省构建时间
slug: docker-build-cache
date: 2023-07-26
image:
categories:
- Docker
tags:
- Docker
---

## 使用命令
[docker build 缓存使用](https://docs.docker.com/engine/reference/builder/#run---mount)

Go项目使用缓存依赖示例，Dockerfile中使用--mount
```shell
RUN --mount=type=cache,mode=0777,id=go-mod,target=/go/pkg/mod \
    go env -w GOPROXY=https://goproxy.cn,direct && \
    go mod tidy && \
    go build -o main
```