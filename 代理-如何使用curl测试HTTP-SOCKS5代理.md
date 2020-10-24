---
title: '[代理]如何使用curl测试HTTP/SOCKS5代理'
categories: [代理]
tags: [代理]
date: 2020-06-19 17:14:21
keywords:
description:
photos:
---

# {{ post.title }}

## 测试socks5代理IP的命令：

`curl --socks5 127.0.0.1:1080  https://www.baidu.com/`

输出：

```
> curl --socks5 127.0.0.1:1080 https://www.baidu.com

<!DOCTYPE html>
<!--STATUS OK--><html> <head><meta http-equiv=content-type content=text/html;charset=utf-8><meta http-equiv=X-UA-Compatible content=IE=Edge><meta content=always name=referrer><link rel=stylesheet type=text/css href=https://ss1.bdstatic.com/5eN1bjq8AAUYm2zgoY3K/r/www/cache/bdorz/baidu.min.css><title>鐧惧害涓€涓嬶紝浣犲氨鐭ラ亾</title>

...

om/img/gs.gif> </p> </div> </div> </div> </body> </html>
```

也可以添加 `-I` 参数，只获得响应头：

`curl --socks5 127.0.0.1:1080 -I https://www.baidu.com/`

响应信息为：

```
> curl --socks5 127.0.0.1:1080 https://www.baidu.com -I

HTTP/1.1 200 OK
Accept-Ranges: bytes
Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform
Connection: keep-alive
Content-Length: 277
Content-Type: text/html
Date: Fri, 19 Jun 2020 09:17:31 GMT
Etag: "575e1f72-115"
Last-Modified: Mon, 13 Jun 2016 02:50:26 GMT
Pragma: no-cache
Server: bfe/1.0.8.18


```


## 测试http代理IP的命令：

`curl --connect-timeout 10 -x 127.0.0.1:8080 https://www.baidu.com/`

