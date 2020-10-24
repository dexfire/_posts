---
title: '[NX563J][Android]努比亚Z17 Max最新系统Root(Magisk v20.4)教程'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ['Android', 'NX563J']
tags: ['NX563J', 'Android']
date: 2020-05-17 09:18:17
keywords: NX563J Android 努比亚 Z17 Max Root Magisk v20.4 教程
description:
authorAbout:
authorDesc:
photos:
---

# {{ post.title }}

首先需要安装绯色的TWRP刷入工具，刷入这个版本的TWRP。  
- [nubia Z17 forAndroid P-TWRP-3.3.0版本发布-牛仔DIY-努比亚/红魔社区](https://bbs.nubia.com/forum.php?mod=viewthread&tid=1462097&extra=page1&page=1&)

刷入方法大致如下：  
1. 下载好附件中的文件：  
![](/img/2020-05-17_092304.jpg)

2. 手机进入 `Fastboot` 模式 或者 正常开机并开启USB调试。

方法是，关机或者重启后，按住`音量减` `+` `开机键` 开机，效果如下：

![](/img/223406hoa33a6abcbot8ci.png.thumb.jpg)

3. 安装好 ADB 驱动，方法很多，自行百度，不再赘述。

4. 开始刷入 绯色 TWRP  
  1. 打开`nubia Z17-for Android P-TWRP-3.3.0.exe`这个文件
  2. ![](/img/2020-05-17_092718.jpg)
  3. 这里按照自己手机的状态选择不同选项，推荐直接进Fastboot刷入。  
![](/img/2020-05-17_092824.jpg)
  4. 刷入后开机按 `音量加` `+` `开机键`即可进入TWRP。
  
5. 点`高级选项` - `绯色工具箱` - `刷入Magisk`  

6. 再回到`高级选项` - `绯色工具箱` - `内核签名`  
其实核心功能就在于这里的内核签名功能，其他的很多内核签名的版本尝试过后都不行。

7. 最后一步：开机后，手动安装 `Magisk-Manager-7.x.x.apk` 管理器！  
这一步是比较特别的，因为正常安装Magisk是不需要这一步的，不知道是否在TWRP签名过程中有没有一些特殊的后续处理，往后再来研究 ~ 

总之，做好以上步骤之后，手机就成功Root到了，Magisk最新版本，还是很香的！！

## 常见问题
1. 无法开机，卡机重启进Fastboot  
这个主要是 Android 版本和 Magisk 版本不兼容导致的，下载最新版的Magisk就可以了。  
小编亲测的是 `Nubia UI 7.0 (v6.25 under Android 9.0)`，配合 Magisk v20.4 完美开机Root。