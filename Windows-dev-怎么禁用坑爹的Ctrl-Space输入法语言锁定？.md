---
title: '[Windows][dev]怎么禁用坑爹的Ctrl+Space输入法语言锁定？'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ["Windows"]
tags: ["Windows", "dev"]
date: 2020-05-10 10:36:47
keywords:
description:
authorAbout:
authorDesc:
photos:
---

# [Windows][dev]怎么禁用坑爹的Ctrl+Space输入法语言锁定？
这个设计不得不说是Windows的一大槽点，`Ctrl+Space`基本在任何大型IDE中都设计为语法提示快捷键，相当于编码人员的命门呀，Windows上似乎无论使用哪种中文输入法，都无法彻底禁用`Ctrl+Space`快捷键。

起初以为是输入法的锅，果断换掉了百度(默哀:-D)，结果用了QQ输入法也是一样的效果...

找到了系统设置，隐藏得非常到位，具体路径：  
"设置" - 设备 - 输入 - “高级键盘设置”  - “输入语言热键”

![](/img/QQ截图20200510104347.png)

这里找到了久违的设置选项：  
Ctrl+Space的确是被系统占用的快捷键，替换掉不就好了？
- 首先尝试禁用掉，发现重新打开这个对话框，**它会自动复原！！**，这操作简直不敢直视。
- 然后尝试替换掉原有快捷键，这次不会复原了...

问题就这么结束了么？  
可怕的来了，按Ctrl+Space，原有的设置依然生效...  
这个快捷键设计者到底是什么妖魔鬼怪？？？  
