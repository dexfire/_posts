---
title: "[Linux][Python]Linux系统下，自行编译的Python3.8 用pip安装 bs4 报错ModuleNotFoundError: No module named '_ctypes'"
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ['Linux']
tags: ['Python', 'Linux']
date: 2020-05-16 18:34:32
keywords: "Linux Python Python3.8 pip ModuleNotFoundError: No module named '_ctypes'"
description:
authorAbout:
authorDesc:
photos:
---

# {{ post.title }}

在Deepin系统（debian体系下）均没有Python3.8的预编译包，所以只有下载源码自行编译，结果遇到的问题就是，编译过程没有报错，但是实际使用的时候，很多软件安装不上。

`$ python3 setup.py install`

```text
Traceback (most recent call last):
  File "setup.py", line 1, in <module>
    from setuptools import (
  File "/usr/local/lib/python3.8/site-packages/setuptools/__init__.py", line 20, in <module>
    from setuptools.dist import Distribution, Feature
  File "/usr/local/lib/python3.8/site-packages/setuptools/dist.py", line 35, in <module>
    from setuptools import windows_support
  File "/usr/local/lib/python3.8/site-packages/setuptools/windows_support.py", line 2, in <module>
    import ctypes
  File "/usr/local/lib/python3.8/ctypes/__init__.py", line 7, in <module>
    from _ctypes import Union, Structure, Array
ModuleNotFoundError: No module named '_ctypes'
```

但是在python交互界面中引用`_ctypes`这个包是没问题的。

## 失败尝试：尝试从源码编译 bs4

中间尝试从 bs4 官网下载代码编译，但依然相同报错。

## 解决方案：补充安装 `libffi-dev`，重新编译Python

查找资料发现是编译过程中缺少了必要的dev软件包，导致部分功能不完全。
需要首先安装`libffi-dev` ，之后重新 configure 并编译 Python。
- [libffi-dev](https://pkgs.org/download/libffi-dev)

`./configure --enable-optimizations`  
`make -j5 && sudo make install`

重新编译后，bs4安装不再报错，问题解决。
```text
$ pip3 install bs4
Defaulting to user installation because normal site-packages is not writeable
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting bs4
  Using cached https://pypi.tuna.tsinghua.edu.cn/packages/10/ed/7e8b97591f6f456174139ec089c769f89a94a1a4025fe967691de971f314/bs4-0.0.1.tar.gz (1.1 kB)
Collecting beautifulsoup4
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/e8/b5/7bb03a696f2c9b7af792a8f51b82974e51c268f15e925fc834876a4efa0b/beautifulsoup4-4.9.0-py3-none-any.whl (109 kB)
     |████████████████████████████████| 109 kB 319 kB/s 
WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ReadTimeoutError("HTTPSConnectionPool(host='pypi.tuna.tsinghua.edu.cn', port=443): Read timed out. (read timeout=15)")': /simple/soupsieve/
Collecting soupsieve>1.2
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/05/cf/ea245e52f55823f19992447b008bcbb7f78efc5960d77f6c34b5b45b36dd/soupsieve-2.0-py2.py3-none-any.whl (32 kB)
Could not build wheels for bs4, since package 'wheel' is not installed.
Installing collected packages: soupsieve, beautifulsoup4, bs4
    Running setup.py install for bs4 ... done
Successfully installed beautifulsoup4-4.9.0 bs4-0.0.1 soupsieve-2.0
```