---
title: '[前端][JavaScript]JS代码放到HTML中的不同位置有何区别？'
keywords: Sakura
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ["前端"]
photos: /img/20200503135002.jpg
date: 2020-05-08 09:01:47
description:
authorAbout:
authorDesc:
tags: ["前端", "JavaScript", "Web"]
---

# [前端][JavaScript]JS代码放到HTML中的不同位置有何区别？

## 1. js了解一下

一直以来都是将js文件写在 `</body>` 之前，外部引入的js脚本文件也同样放在这个位置。却只知道一个模糊的大概原因，现在来深度剖析一下。

先明白js能放在HTML的那个位置，分别是head和body中。大部分人都是放到head里面的。下面为大家介绍下放到这两个地方的区别

## 2. 该把js文件放在html那个位置呢？

首先了解页面结构，浏览器组成的都会明白一点。在我使用Google浏览器访问一个页面的时候，谷歌的webkit页面渲染引擎 渲染页面之前，需要通过解析html标记来构建DOM树。如果解析器遇到了一个脚本，就会停下来执行这个脚本，然后才会继续解析html。要是遇到的是一个外部引用的脚本，他就必须停下来等待这个脚本资源的下载，这样就会降低页面首次的渲染时间。并且引入外部脚本会阻塞浏览器的并行下载，跟图片不一样，浏览器一个只能同时从服务器并行加载两个脚本，也就是说我们的网站加载脚本的时候，浏览器不会再启动其他任何下载。所以js文件不管外部的还是本页面的我一般都是会写或引入在`</body>`之前。
    
但是里，也并不是都一股脑的放在`head`里面就是了，看一下一些大的网站很多脚本还是会放在头部的，这里涉及到一个新的属性：`async`（只限于外部脚本的引入）。自行百度去吧。。  

还有的就是一些不得不引入到头部的脚本，比如说jquery必须放在jquery代码之前才能保证代码的正常运行，这总不能引入到`body`里面吧

## 3. 不同位置的Js代码，有何区别？

首先看一段 html 代码：  
```html
<html> 
    <head> 
        <title> New Document </title> 
        <meta http-equiv="content-type" content="text/html;charset=utf-8"> 
        <script type="text/javascript" src="test.js"></script> 
    </head> 
    <body> 
        <div id="target"> </div> 
        <button id="btn">按钮</button> 
    </body> 
</html> 
```

test.js文件：  
```js
var test = function(){ 
    var span = document.createElement("span"); 
    span.innerHTML="添加"; 
    document.getElementById("target").appendChild(span); 
} 
document.getElementById("btn").onclick=test; 
```

**如果这段代码放到head里面就不能运行**。为什么？  
这就要说一下HTML的运行顺序了，应该确切点说不是HTML的运行顺序，是js的运行顺序。  
HTML从上运行到`<script type="text/html" src="test.js"></script>`的时候进入test.js文件。
前面的不会运行，也就是被function包起来的不会被运行，这个时候就执行最后一句。
去页面中取元素Id为btn的元素。但是这个时候，HTML页面并没有加载完。
肯定取不到id为btn的元素。会报错。这个时候有人说可以改为下面的代码:

```js
document.body.onload = function(){
document.getElementById("btn").onclick=test;
};
```

但是这样写还不如，写到</body>的前面呢。
有没有注意到，上面的`document.getElementById("btn").onclick=test;`中test没有括号，那如果改成`test()`.会怎么样呢?

![](https://files.jb51.net/file_images/article/201308/201382193545206.png?201372193634)

结果如图，页面载入就是是这个样子，点击按钮没有反应。将js代码改成如下: 
```js
var test=function(){ 
        var span = document.createElement("span"); 
        span.innerHTML="添加"; 
        document.getElementById("target").appendChild(span); 
        return function(){ 
            alert("aaaa"); 
    }; 
} 
document.getElementById("btn").onclick=test(); 
```

页面载入的时候，还是和上面一个样子，当点击按钮的时候，有反应了弹出一个框内容是”aaaa“;说明点击的时候执行了函数中return的值。也就是加括号的时候，不触发事件也会执行函数。触发事件的时候执行函数的返回值。不加括号的时候，触发事件才执行函数。

## html的事件触发器，内容能写什么？

比如`onclick="";` 双引号里面能写什么。一般看到的可以写函数，比如，`onclick="test();"`。除了这个还能写什么呢?好有这个分号能不写吗?
 
看上面的js代码，每一行都有分号，分号的作用就是为了语句被混淆，那也就是说onclick里面可以写js代码。写一个试试，如下：

```html
 
<html> 
    <head> 
        <title> New Document </title> 
        <meta http-equiv="content-type" content="text/html;charset=utf-8"> 
    </head> 
    <body> 
        <div id="target"></div> 
        <button id="btn" onclick="var espan = document.createElement('span');espan.innerHTML='添加';document.getElementById('target').appendChild(espan);">按钮</button> 
    </body> 
</html> 
```

运行结果如下：
![](https://files.jb51.net/file_images/article/201308/201308210937123.gif?201372193750)

说明是可以运行的。这说明，不止可以放函数名了。

## 事件绑定方式？

事件绑定方式常用有两种一是前面介绍的在事件中加入js代码。如：`onclick="test();"`。这种绑定方式有缺点，就是你要修改美工已经写好的代码。
还有一种方式就是我开始代码写的那样，通过id，只需要美工将每个元素都加上id就行。
并不需要修改HTML代码。
