---
title: '[Python][多媒体处理]用Python执行批量*.flv文件格式转换mp4'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: [Python]
tags: [Python, 多媒体处理, 日常]
date: 2020-05-20 23:18:53
keywords:
description:
authorAbout:
authorDesc:
photos:
---

# {{ post.title }}

实现当前目录下的全部 `.flv` 文件转化为 `.mp4` 格式。

- **Python**：v3.7
- **注意**：需要提前安装 ffmpeg 并加入到 PATH 中。
- 使用的是更方便易用的 `subprocess` 库， 相比 `os.exec*()` 系列函数好用不是一点点。

代码如下：


```python
# coding=utf8
import sys
import os
import subprocess

flvs = [fp for fp in os.listdir() if fp.endswith('.flv')]
for fp in flvs:
	fp = str(fp)
	print('# 开始处理：' + fp)
	cmd = 'ffmpeg -i "' + fp + '" "' + fp[:-4] + '".mp4'
	print('# Command line: ', cmd)
	subprocess.call(cmd, timeout=1e6);
```