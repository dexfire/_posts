---
title: '[node.js]如何发布自己的程序包到npm官方仓库目录？'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: []
tags: []
date: 2020-05-08 22:05:57
keywords:
description:
authorAbout:
authorDesc:
photos:
---

# {{ post.title }}

对于原创或修改的npm包，可以发布到npm服务器上以获得更简便的安装方式（获得各大镜像站的cdn加速），那么问题来了怎么发布一个项目呢？

## 创建一个npm项目

创建一个项目文件夹:  
`mkdir myProject && cd myProject`

初始化npm项目:  
`npm Init`

这时会要求输入一些基本信息，会用于作为包的识别信息，当然你也可以后续在 `package.json` 中修改这些信息。

创建好的配置文件大致如下：
```json
{
  "name": "myProject",
  "version": "1.0.0",
  "description": "descriptions goes here.",
  "author": "Lvhua Wu <dexfire29@foxmail.com>",
  "engines": {
    "node": ">=4"
  },
  "files": [
    "index.js"
  ],
  "keywords": [],
  "devDependencies": {}
}
```

## 注册npm账号

发布npm包需要首先在npmjs.com上完成注册，注册地址：
- [ヽ(✿ﾟ▽ﾟ)ノ npm ♥ you!](https://www.npmjs.com/)

在本地npm管理器中注册用户信息：
`npm adduser`

输入自己的注册账号、密码、邮箱即可。

## 发布npm包

当编辑完成后，使用这一简单命令即可发布：  
`npm publish`

发布结果：  
![](/img/2020-05-08_225624.jpg)

当然，npm官方要求必须有 `README.md` 项目自述文件，需要添加进项目中来。