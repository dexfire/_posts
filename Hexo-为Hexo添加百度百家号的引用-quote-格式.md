---
title: '[Hexo]为Hexo添加百度百家号的引用(quote)格式'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: []
tags: []
date: 2020-05-12 19:21:58
keywords:
description:
authorAbout:
authorDesc:
photos:
---

# {{ post.title }}

效果图：  
![](/img/QQ截图20200512192245.png)

CSS代码：  
```css
.bjh-blockquote:before {
    content: "";
    display: inline-block;
    height: 14px;
    width: 18px;
    background-image: url(https://gss0.bdstatic.com/5bd1bjqh_Q23odCf/static/newsdetail/img/BdrainrwLandingMainContent/quote.png);
    background-repeat: no-repeat;
    background-size: contain;
    position: absolute;
    left: 0;
    top: 3px;
}
```

添加到自定义css中，渲染后看到效果：

由此，“Google 三巨头” 正式形成。

### Eric Schmidt 的商业之道

对于 Eric Schmidt，硅谷有这样一个评价：

> Eric Schmidt 绝对是个举足轻重的人，其经历之丰富，堪称业界老狐狸。

当然，"老狐狸" 是一个正面评价。对于 Eric Schmidt 来说，这意味着他不仅仅是一个技术从业者，更是一个善于将技术转化成利润的人。

