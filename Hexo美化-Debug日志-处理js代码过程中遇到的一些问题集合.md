---
title: '[Hexo美化][Debug日志]处理js代码过程中遇到的一些问题集合'
keywords: Sakura
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ["Hexo美化"]
photos: /img/20200503135002.jpg
date: 2020-05-08 09:56:25
description:
authorAbout:
authorDesc:
tags: ["Hexo美化", "Debug日志"]
---

# [Hexo美化][Debug日志]处理js代码过程中遇到的一些问题集合

本身就是静态站，要是再没有js帮忙撑场面，就真的安静了...处理js代码中遇到了一些问题，这里简单说明一下解决的方法，帮助踩坑的同学找到思路。

## 1. js文件防在主题哪个位置？可以使用hexo脚本代码么？

js代码，一般放在主题的`/source/js/`文件夹下，且**不支持**采用hexo脚本语法，这一点是比较蛋疼的，有些需要结合主题配置的部分都无法用hexo处理了。

当然，不支持也是有好处的，那么这一部分代码就可以采用免费的cdn，比如[![jsDelivr](https://www.jsdelivr.com/img/logo-horizontal.svg)](https://www.jsdelivr.com/)来进行缓存加速，毕竟免费的午餐还要吃得酸爽，不掏腰包就得动动脑子呢。

## 2. js中想放代码要动态处理怎么办呢？
`source/js/` 下的js文件不支持，但是`layout/*.ejs`是支持的呀，所以有些需要动态处理的脚本，可以添加到到模板的 ejs文件内，比如：

用于生成博客首页的index.ejs：  
```js
<script type="text/javascript">
    $(document).ready(function () {
        // 生成主页图
        bgs = "<%= theme.bg %>".split(",");
        $(".headertop")[0].style.height = "550px";
    });
</script>
```

这里的theme.bg是在`_config.yml`中定义的一个字符串数组，这里输出的结果为（`bgs`）：
```js
bgs = 
[
    "https://cdn.jsdelivr.net/gh/dexfire/cdn@v1.0/images/cover/IMG_7631.JPG", 
    "https://cdn.jsdelivr.net/gh/dexfire/cdn@v1.0/images/cover/IMG_7632.JPG", 
    "https://cdn.jsdelivr.net/gh/dexfire/cdn@v1.0/images/cover/IMG_7633.JPG", 
    "https://cdn.jsdelivr.net/gh/dexfire/cdn@v1.0/images/cover/IMG_7634.JPG", 
    "https://cdn.jsdelivr.net/gh/dexfire/cdn@v1.0/images/cover/IMG_7635.JPG", 
    ...
]
```

可以看到已经实现了在主题配置`_config.yml`中自定义的图片到js代码变量数组的转换。

## 3. js代码在html中的放置有何区别？
按道理来说，html是顺序加载的，而且是一边还在读取，另一边同时就开始执行格式化了，所以也就产生了一个js代码的插入顺序问题。

- html头部最先被读取，所以说`*.css`格式定义文件会放在头部，即`<head></head>`标签中，在所有实体标签加载之前就读取完成了，才能无遗漏地应用于全部应有标签；
- 通常的js脚本文件会放置于html末尾，是因为放在中途的js脚本，一旦读取完成后即开始执行，可能代码的目标作用对象尚未加载完成，导致访问错误。

e.g. 还是刚刚那段代码，放置于`index.ejs`之中，而非`footer.ejs`中，所以产生了这样一个结果：
```text
(index):953 
    Uncaught ReferenceError: $ is not defined
        (anonymous) @ (index):953
```
这个结果很显然，`jquery.js`是放在`</body>`前面，即html末尾位置，所以加载之时jQuery尚未初始化完成，所以考虑改用DOM模型访问，即：
```js
document.getElementsByClassName("headertop")[0].style.height = "550px";
```

### 