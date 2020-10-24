---
title: '[Matlab][Debug]Matlab输出值异常情况处理（一个uin8引发的灾难）'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ['Matlab']
tags: ['Matlab']
date: 2020-05-14 01:42:38
keywords:
description:
authorAbout:
authorDesc:
photos:
---

# \[Matlab\]\[Debug\]Matlab输出值异常情况处理（一个uin8引发的灾难）

Matlab是一种灵活性很高，而并不甚兼顾效率的实用程序。但没有效率是不可能有大作为的，就连饱受诟病的Python，做起爬虫或者AI运算都是不错的，加上其高度的灵活易用性，否则根本早就被淘汰了。

那么，既然要追求一定的效率，必然也就要进行优化，所以也就有了一些了不可言喻的似Bug非Bug的情形出现，比如这个`uint8`引发计算精度大幅降低而出现的巨坑（愣是调了半小时）。

首先这个程序是这样的，用于对图像进行线性灰度变换：
```matlab
%% 2.2.2 图像灰度变换并分析直方图

img = rgb2gray(imread('images\\scenery3.jpg'));
t1 = @(A) exp2_T1(A,0,255,0,250);
timg = t1(img);
figure
subplot(2,2,1), imshow(img);title('原图');
subplot(2,2,2), imshow(timg);title('灰度变换: 0,255 -> 50,205');
```

其中的变换函数位于`exp2_T1.m`：
```matlab
function img_out = exp2_T1(img_in,a,b,c,d )
%EXP2_T1 对img进行灰度变换
%   线型变换（伪）
    fprintf('输入参数： a,b,c,d=%d,%d,%d,%d',a,b,c,d);
    [h,w] = size(img_in);
    img_out = zeros(h,w);
    for i = 1:h
        for j=1:w
            if img_in(i,j)<a
                img_out(i,j)=a;
            elseif img_in(i,j)>=b && img_in(i,j)<=255
                img_out(i,j)=b;
            elseif img_in(i,j)>=a && img_in(i,j)<b
                img_out(i,j)=c+(img_in(i,j)-a)*(d-c)/(b-a);
            end
        end
    end
    img_out = uint8(img_out);
end
```

输出的值、图像都非常奇怪：

![](2020-05-14_080905.jpg)

按说是有一定灰阶的，但是这里完全没有显现。

## Bug复现

```matlab
a=0;b=255;c=0;d=240;
i=10;j=20;
img = rgb2gray(imread('images\\scenery3.jpg'));
img_in = img;
img_in(i,j)
ans =79;
```

![](/img/2020-05-14_082724.jpg)

之后计算输出坐标灰度值：

```matlab
c+(img_in(i,j)-a)*(d-c)/(b-a)
```

输出为一个很奇怪的量：
```
ans =

    1
```

将输入变量`img_in(i,j)`换成常量试试：
```matlab
img_in(i,j)
ans =79;
c+(79-a)*(d-c)/(b-a)
```

输出正常！！：
```
ans =

   74.3529
```

到这里原因就很清楚了：  
灰度图像变量`img_in`是`uint8`类型，而参与乘除的数字也都是整型变量，结果被视为整数乘除法，造成小于1的结果视作0，从而产生奇怪的输出。

奇怪的是：`(d-c)/(b-a)` 输出是 `ans = 0.9412`，是正常的，
```matlab
(img_in(i,j)-a)* 0.9412

ans =

   74
```
结果舍弃掉了一些小数，但整体是正常的。

整体来看：
```matlab
img_in(i,j)
ans =

   79

(d-c)/(b-a)
ans =

    0.9412

(img_in(i,j)-a)* 0.9412
ans =

   74

c+(79-a)*(d-c)/(b-a)
ans =

   74.3529

(img_in(i,j)-a)*(d-c)/(b-a)
ans =

    1

c+(img_in(i,j)-a)*(d-c)/(b-a)
ans =

    1
```

事实证明，在计算前加一个浮点数是不影响后续计算的。
也就是说，**即使返回结果为double类型，计算过程中也涉及小数，但依然可能包含纯整数计算**；
相比之下，还是python中用`//`表示整数除法比较科学且直观了。

```matlab
0.0 + (img_in(i,j)-a)*(d-c)/(b-a)
ans =

    1

>> 1.0 + (img_in(i,j)-a)*(d-c)/(b-a)
ans =

    2

>> 1.1 + (img_in(i,j)-a)*(d-c)/(b-a)
ans =

    2
```

整个流程看下来也是非常违背常识的，也许新版会有改进吧。
编写过程中多注意变量，尤其是完全整形变量需要加`1.0`倍乘因子，也是一种方案。

...

奇葩的事又来了， 这个用1.0乘都不行QwQ！

```matlab
a + 1.0*(img_in(i,j)-a)*(d-c)/(b-a)
ans =

    1

a + double(1.0)*(img_in(i,j)-a)*(d-c)/(b-a)
ans =

    1
```

## 最终解决方案
本例中，这两种是等价的：
```matlab
>> a + (double((img_in(i,j))-a)*(d-c)/(b-a))
ans =

   74.3529

>> a + (double(img_in(i,j)-a)*(d-c)/(b-a))
ans =

   74.3529
```

或者：
```matlab
img_in = double(img);
>> a + (img_in(i,j)-a)*(d-c)/(b-a)
ans =

   74.3529
```
最终的输出结果：  
![](/img/2020-05-14_090602.jpg)
![](/img/2020-05-14_090747.jpg)

## 补充：另外一些实验
```matlab
double(1)/uint8(5)
```

 输出：
```
ans =

    0
```

测试一下系统内置函数：
```
>> x = power(uint8(3.0),2)
x =

    9

>> whos x
  Name      Size            Bytes  Class    Attributes

  x         1x1                 1  uint8      
```

对于double参数：
```matlab
y = power(double(5),2)

y =

    25

>> whos y
  Name      Size            Bytes  Class     Attributes

  y         1x1                 8  double      
```

也就是说，matlab系统不会强制转换类型，即便可能出现小数。  
此外，参与乘除运算，只要有一个uint类型变量，这一组运算都会变成整形运算（头秃...QwQ）  
使用uint变量时时需要格外注意。

好在，matlab默认变量就是double类型。   
所以只要不涉及强制uint的函数和声明，还是不容易出错的。