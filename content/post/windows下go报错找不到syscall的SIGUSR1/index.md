---
title: go 报错undefined syscall.SIGUSR1
description: windows下兼容go linux进程退出
slug: go-windows-syscall-SIGUSR1
date: 2023-07-22
image:
categories:
- Go
tags:
- Go
- error
---

## 解决
> 找到go包的src目录下的syscall/types_windows.go文件
修改如下：
```go
var signals = [...]string{
	1:  "hangup",
	2:  "interrupt",
	3:  "quit",
	4:  "illegal instruction",
	5:  "trace/breakpoint trap",
	6:  "aborted",
	7:  "bus error",
	8:  "floating point exception",
	9:  "killed",
	10: "user defined signal 1",
	11: "segmentation fault",
	12: "user defined signal 2",
	13: "broken pipe",
	14: "alarm clock",
	15: "terminated",
	/** 兼容windows start */
	16: "SIGUSR1",
	17: "SIGUSR2",
	18: "SIGTSTP",
	/** 兼容windows end */
}

/** 兼容windows start */
func Kill(...interface{}) {
	return
}

const (
	SIGUSR1 = Signal(0x10)
	SIGUSR2 = Signal(0x11)
	SIGTSTP = Signal(0x12)
)
/** 兼容windows end */
```