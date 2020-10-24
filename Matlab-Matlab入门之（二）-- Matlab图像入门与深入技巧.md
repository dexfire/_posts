---
title: '[Matlab]Matlab入门之（二）-- Matlab图像入门与深入技巧'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ["Matlab"]
tags: ["Matlab", "绘图", "可视化"]
date: 2020-05-10 12:00:42
keywords: Matlab 绘图 可视化
description:
authorAbout:
authorDesc:
photos:
---

# {{ post.title }}

开启一个新的绘图窗口：
```matlab
figure(1)
% 或者也可以省略参数，自动开启一个独占的编号窗口。
figure
```


## 绘制2d函数图像

```matlab
x=-pi:0.01:pi;
y=sin(x);
plot(x,y);
```

![](/imgs/QQ截图20200514005100.png)

## 绘制3d函数图像

## 图像处理
 Matlab作为工程中的数据可视化工具是非常的方便的。但是在具体的生成过程中通常会遇见以下几个比较常见的问题，这里以我最近在写论文中用图遇到的问题作为例子。简要说明输出图像大小位置规范的重要性。

 
  1：colorbar的位置大小范围不一致、不合理
这一点可以参照我的另一篇博客：http://blog.csdn.net/misayaaaaa/article/details/53326395    其中有详细的colorbar的各项操作。

          2：输出图像的尺寸不合理，在插入论文的过程中需要拖拽放大，导致图像不可避免的不一致。

          3：输出图像的分辨率和清晰度太低，这在论文中是非常不可取的，所以需要进行一定的调整。

          4：输出图像的坐标轴上下限等不合理、不一致。

          5：输出图像的位置不合理。
————————————————
版权声明：本文为CSDN博主「MISAYAONE」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/misayaaaaa/article/details/53421221
  https://img-blog.csdn.net/20161201162204473?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center
  
另外另存为的时候，将其保存为tiff格式的矢量图，这样放大以后不会失真。

输出图像的坐标上下限设置

        这个可以通过程序中的语句来设定：

设置坐标轴上下限：axis([xmin,xmax,ymin,ymax]);       分别是x,y轴的上下限；

设置图片大小：set(gcf,'position',[x1,y1,dx,dy]);     x1,y1是图的左下角坐标(相对于整个屏幕)，dx,dy是图沿x,y方向的大小；

坐标轴名称设定：set(gca,'FrontName','Times New Roman','FrontSize',7,'LineWidth',1.5)；

坐标轴反向：set(gca,'zdir','reverse');     将坐标轴数值反向；
————————————————
版权声明：本文为CSDN博主「MISAYAONE」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/misayaaaaa/article/details/53421221


## matlab figure大小设置
https://zhidao.baidu.com/question/139946719.html
通过set指令可以指定图像大小，语法为set(gcf,'position',[centerX,centerY,width,height])，其中“width”和“height”分别代表宽度和高度来。

centerX为figure的中心点在屏幕的x坐标，centerY为figure的中心点在屏幕的y坐标，和固定图像尺寸没有关系。

figure框菜单
file-->export setup-->size,
输入宽，高，选择相应单位抄
点右边apply to figure按钮就可以zd了
或者使用命令：如
set (gcf,'Position',[400,100,300,300], 'color','w')
http://wuzhi3495.blog.163.com/blog/static/11777398200912611912871/

## matlab 交互编程、Word notebook、发布为pdf
非常高端洋气的功能！！！

## 交互编程、动态图像
各位大侠：
      最近在用notebook时，发现在一段代码中要画多个图形时，notebook中只能显示最后一幅图形，不知该如何解决这个问题，请各位大虾指教！！
	  
	  
谢谢楼上的回答，只是觉得奇怪，书上只是说一个细胞群只能显示一张图，如果生成多张图的话，最后一张图会覆盖前面的图形，并没有提出解决办法，网上也搜不到类似的问题，真是晕啊


好像notebook是有这么个问题

建议你直接用MATLAB做，然后复制到word里
或者直接用publish，也可以自动生成一个word文件

## 公式
MATLAB打印显示LaTeX文本格式的公式
https://jingyan.baidu.com/album/574c52195006476c8d9dc1d9.html?picindex=4


