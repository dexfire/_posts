---
title: '[Git]Git从入门到熟练教程（十五）———— 实用教程篇：git 记住密码、忘记密码、使用SSH登录Git服务器'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ['Git']
tags: ['Git']
date: 2020-05-16 16:33:41
keywords:
description:
authorAbout:
authorDesc:
photos:
---

# [Git]Git从入门到熟练教程（十五）———— 实用教程篇：git 记住密码、忘记密码、使用SSH登录Git服务器

## git 记住密码？

## git 忘记密码？

## 使用SSH登录Github等远程仓库？

Github使用密码登录本身存在风险，因为加密保存的密码在输入过程中可能被监听，或者本地密码文件被暴力破解（可能性不大），那么有没有办法使用一种无需密码的认证方式呢？当然有，答案很简单，只要使用加密证书即可，通常的证书采用128或者256位加密，就已经远远超过当前计算机所能暴力破解的极限，以至于利用人性的漏洞远比利用计算机算力破解更为可取，当然这也证明了证书加密方式的有效性；另外我们完全可以生成更长位数的证书，从而完全杜绝暴力破解的可能性；此外网络认证与本地解密不同的是，Github服务器也会对频繁进行错误验证的主机实施屏蔽措施，从而更加确保密匙认证方式的安全性（前提是：密匙不要泄露）。

1. 首先，使用ssh-key创建一个RSA密匙
`$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

一路跟随提示即可，有疑惑的地方可以选择直接回车选用默认值。要注意的是，这里的密匙密码，为了方便使用可以不填写（降低了安全性，但的确方便不少）。

    
2. 在本地计算机中，将刚刚生成的密匙用作自己的ssh身份标示
`$ ssh-add ~/.ssh/id_rsa`

如果出现问题，可以考虑事先运行这一步：
`$ eval "$(ssh-agent -s)"`
输出为 ssh-agent 的 pid（不用理会）：
`> Agent pid 59566`

3. 在 Github 中添加刚刚生成的密钥对中的公钥到Github个人设置的SSH Key中。
