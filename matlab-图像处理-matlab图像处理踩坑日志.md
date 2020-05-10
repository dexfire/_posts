---
title: '[matlab][图像处理]matlab图像处理踩坑日志'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: []
tags: []
date: 2020-05-10 09:25:39
keywords:
description:
authorAbout:
authorDesc:
photos:
---

# {{ post.title }}

## matlab中的三目运算符？
matlab有类似c语言中的语法？：
```c
ret = cond?'yes':'no';
```

结果有些失望，是没有的，不够可以通过函数实现：
```matlab
function [ result ] = is( a, b )
%IS 判断字符串是否相同
%   输出是和否
    if strcmp(a, b)
        result = '是'; 
    else
        result = '否';
    end;
end
```

然后调用这个函数即可获得想要的结果：
```matlab
fInfo = imfinfo(fullfile,filetype);
truecolor = is(fInfo.ColorType, 'truecolor');
indexed = is(fInfo.ColorType, 'indexed');
grayscale = is(fInfo.ColorType, 'grayscale');

fprintf('(2) BMP 图像格式分析\n===================\n图像后缀名：%s\n是否为全彩色：%s\n是否有调色板：%s\n是否为灰阶图：%s\n', ...
    fInfo.Format, truecolor, indexed, grayscale)
```

输出：
```text
(2) BMP 图像格式分析
===================
图像后缀名：bmp
是否为全彩色：否
是否有调色板：是
是否为灰阶图：否
```

## 读取图像--imread函数
```c++
A = imread(filename)example
A = imread(filename,fmt)
A = imread(___,idx)
A = imread(___,Name,Value)example
[A,map] = imread(___)example
[A,map,transparency] = imread(___)
```

## 显示图像--imshow函数
调用 `imshow` 会在当前的 figure 或者 subplot 中绘制所传入的图像。

```c++
imshow(I)example
imshow(X,map)example
imshow(filename)example
imshow(I,[low high])
imshow(___,Name,Value)
himage = imshow(___)
```

例如：
```matlab
[X,map] = imread('corn.tif');
imshow(X,map)
```

![](/img/QQ截图20200510093155.png)

## imread 无法显示bmp彩色索引(indexed)图像？
- 测试读取灰度索引bmp图像：
```m
imgpath ='images\';                         % 实验图像的文件夹路径
filename ='scenery4.bmp';                       %实验图像名称
%filename ='house.jpg';
filetype = filename(end-2:end);             %获得图像的后缀
fullfile =[imgpath filename];               %将两个字符串组合成文件全名
[img, map] = imread(fullfile);      %读文件，结果放在 img 矩阵中，注意后缀名称要统一

% 预览文件
figure(1), subplot(1,2,1), imshow(img, map); title('输入图像');
```

输出为黑白图像：
![](/img/QQ截图20200510093507.png)

实际图像：
![](/img/scenery4.bmp)

- 测试使用全彩色，jpg图像则可以正常显示
![](/img/QQ截图20200510094127.png)

- 测试索引均值`mean(map)`，输出：
```text
ans =
    0.4432    0.4441    0.3863
```
说明map是正常的。

- 直接使用`imread(filename)`？

- **解决方案**：首先用 `ind2rgb` 转化为RGB格式，之后使用`imshow`
```matlab
% 预览文件
RGB = ind2rgb(img, map);
figure(1), subplot(1,2,1), imshow(RGB); title('输入图像');
```

![](/img/QQ截图20200510095508.png)

## matlab求数组均值
`mean(A)`
