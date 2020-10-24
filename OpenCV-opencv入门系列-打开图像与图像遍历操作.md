---
title: '[OpenCV]opencv入门系列--打开图像与图像遍历操作'
categories: []
tags: []
date: 2020-09-11 11:35:31
keywords:
description:
photos:
---

# {{ post.title }}

## Numpy、base64、OpenCV 等基础操作

### 遍历ndarray对象
遍历在程序语言中常用`迭代`一词指代。numpy除了可以批量操作以外，还可以使用迭代器进行遍历。

### base64 加密解密

```python
# %% Base64 测试
s = "你好\\(^o^)/~"
b = base64.b64encode(s.encode(encoding="utf8"))
c = base64.b64decode(b)
d = c.decode()
print(s, b, c, d, sep="\n")
```

```text
# %% Base64 测试...

你好\(^o^)/~
b'5L2g5aW9XCheb14pL34='
b'\xe4\xbd\xa0\xe5\xa5\xbd\\(^o^)/~'
你好\(^o^)/~
```