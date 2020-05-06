---
title: '[Android移植]将定制ROM移植为sGSI版本'
keywords: Sakura
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: post
photos: /img/20200503135002.jpg
date: 2020-05-06 18:56:52
description:
authorAbout:
authorDesc:
tags:
  - NX563J
  - GSI
  - Android
  - 刷机
  - 永久收藏
---

# 【教程】把定制ROM移植成sGSI（适用于Android P）：参考此教程可把OEM定制的ROM制作成GSI镜像，可以在支持Project Treble 的设备上运行，仅适用于高通平台。

**来源**：[https://jmxl.github.io](https://jmxl.github.io/2018/08/07/%E3%80%90%E6%95%99%E7%A8%8B%E3%80%91%E6%8A%8A%E5%AE%9A%E5%88%B6ROM%E7%A7%BB%E6%A4%8D%E6%88%90sGSI%EF%BC%88Android-P%EF%BC%89/)

本文来自[xda论坛](https://forum.xda-developers.com/project-treble/trebleenabled-device-development/reference-port-p-preview-images-semi-gsi-t3825572)，翻译：九面相柳
本文介绍了将定制ROM移植成semi-GSI的主要步骤，旨在介绍应该处理的关键文件，而非手把手教学的教程，也许参考本文仅仅能够制作出一个可启动的镜像，我不会保证真给你带来什么。

## 需要准备的东西
1. 一台电脑和一部支持PT的手机（官方或土制均可）；
2. P DP3 semi-GSI（目前大部分OEM厂商的安卓P(9.0)都是基于DP3的）；
3. 一个你想移植的高通平台的安卓P镜像；
4. 最好有最新版本的ROM移植工具（方便解包等操作）

似乎目前只有高通平台的手机有官方P预览版系统，我不确定麒麟和猎户座的手机是否也已经有了安卓P。
理论上，安卓P镜像可以在同一平台的不同芯片之间移植。

当然，搞机有风险，请你做好救砖的准备。

## 开始移植
首先，解包安卓P的semi-GSI 镜像（以下称为底包）和你要移植的ROM。

（下文中的 `lib&lib64` 意思是你要替换的文件在`lib`和`lib64`下同时存在，请分别替换）

1. 将移植包的`/system/lib&lib64/libselinux.so`替换成底包的；
2. 找到移植包 `/system/etc` 下以 `ld.config` 开头的txt文件，用底包的 `/system/etc/ld.configs.txt` 替换；
3. 删除 `/system/etc/permissions/qti-permissions.jar`
4. 修改 `/system/etc/prop.default` 关闭adb安全设置并打开调试选项，以便于debug
5. 解包移移植包的vendor 镜像，找到OEM厂商在 `manifest.xml`中添加的服务项；manifest可能会在 `/vendor` 或者 `/vendor/etc/vintf`，挑出所有与你在manifest找到的服务项有关的hal，通常它们会位于：
    /vendor/bin/hw
    /vendor/etc/init
    /vendor/lib&lib64/
    /vendor/lib&lib64/hw
并找出一些其他与移植包有关的文件如`framework`, `overlays`等；
然后把你移植好的system打包成img.
刷入 8.1 的 vendor ， P semi-GSI boot 和 vendor 补丁.
刷入你移植好的 `system.img`

添加你在vendor分区找到的额外的文件，还需要修改你的手机的manifexts.xml并添加OEM相关的文件。

可刷入FBE Disabler和permissiver来关闭FBE（文件加密）和seLinux。
格式化data，把adb keys推送到手机里以便于调试，重启。

如果你足够幸运，就可以见到开机动画并开始调试了。
可以用adb命令抓取log.

打开log文件搜索“died”，可以定位到bug的位置，剩下的就看你的经验了。

## 补充：一些常见问题的解决方案
- `dumplicate permission : XXX`
解决方案：在 /system/etc/permissions 的文件中找到XXX ，删除报错的权限；
- `fail to make lockscreen ready`
解决方案：将底包中的libpuresoftkeymasterdevice.so添加到你的系统中；
- 进入系统后重启或黑屏（常见于骁龙845）
解决方案：替换以下文件：
    /system/bin/surfaceflinger
    /system/lib&lib64/libsurfaceflinger.so
    /system/lib&lib64/libtimestats_pronto.so
