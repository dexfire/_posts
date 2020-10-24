---
title: '[Matlab][图像处理]Matlab中的直方图显示、高斯均衡化、自定义线型均衡化'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ['Matlab', '图像处理']
tags: ['Matlab', '图像处理', '直方图', '均衡化']
date: 2020-05-14 00:44:02
keywords: Matlab 直方图 高斯均衡化 均衡化
description:
authorAbout:
authorDesc:
photos:
---

# \[Matlab\]\[图像处理\]Matlab中的直方图显示、高斯均衡化、自定义线型均衡化
直方图是

## 显示直方图

## 反色及其直方图

```matlab
img = imread('images\\scenery3.jpg');
[h,w,c] = size(img);
white = uint8([255,255,255]);
rev = @(c) white-c;
img_rev = zeros(h,w,c);
for i=1:h
    for j=1:w
        c = img(i,j,:);
        rc = rev(c(:)'); % 反色结果
        img_rev(i,j,:) = rc;
    end
end
img_rev = uint8(img_rev);

figure;
subplot(2,2,1), imshow(img), title('原图');
subplot(2,2,2), imshow(img_rev), title('反色');
subplot(2,2,3);
h=imhist(rgb2gray(img)); bar(h); title('原图直方图');
subplot(2,2,4), 
h=imhist(rgb2gray(img_rev)); bar(h, 'r'); title('反色直方图');
```

效果图：
![](/img/QQ截图20200514010012.png)