---
title: 搭建hexo博客踩坑指南~
date: 2020-05-02 02:59:15
tags:
  - 个人博客
  - dev
  - cs
---

# 搭建hexo博客踩坑指南~

最近无意间看到这个Sakura主题的 cnblogs 的博客，[](https://www.cnblogs.com/lavender1221/p/12689426.html)

## [sprintf] unexpected placeholder

这个错误的确有些摸不着头脑，这个tag没问题的？

```js
{% raw %}
ERROR D:\CreatingSpace\hexo\themes\Sakura\layout\tag.ejs:9
    7| <div class="pattern-center ">
    8|   <div class="pattern-attachment-img">
 >> 9|     <img <% if(__(img)){%>src="<%- theme.lazyloadImg %>" data-src="<%= __(img)%>"<%} else {%>src="<%- theme.lazyloadImg %>" data-src="https://view.moezx.cc/images/2017/12/03/writing.jpg"<% } %> class="lazyload" onerror="imgError(this,3)" style="width: 100%; height: 100%; object-fit: cover; pointer-events: none;">
    10|   </div>
    11|   <header class="pattern-header ">
    12|     <h1 class="cat-title"><%= __(page.tag) %></h1>

[sprintf] unexpected placeholder
SyntaxError: D:\CreatingSpace\hexo\themes\Sakura\layout\tag.ejs:9
    7| <div class="pattern-center ">
    8|   <div class="pattern-attachment-img">
 >> 9|     <img <% if(__(img)){%>src="<%- theme.lazyloadImg%>" data-src="<%= __(img)%>"<%} else {%>src="<%- theme.lazyloadImg %>" data-src="https://view.moezx.cc/images/2017/12/03/writing.jpg"<% } %> class="lazyload" onerror="imgError(this,3)" style="width: 100%; height: 100%; object-fit: cover; pointer-events: none;">
    10|   </div>
    11|   <header class="pattern-header ">
    12|     <h1 class="cat-title"><%= __(page.tag) %></h1>

[sprintf] unexpected placeholder
    at Function.sprintf.parse (D:\CreatingSpace\hexo\node_modules\sprintf-js\src\sprintf.js:164:23)
    at sprintf (D:\CreatingSpace\hexo\node_modules\sprintf-js\src\sprintf.js:19:34)
    at vsprintf (D:\CreatingSpace\hexo\node_modules\sprintf-js\src\sprintf.js:174:24)
    at Object.__ (D:\CreatingSpace\hexo\node_modules\hexo-i18n\lib\i18n.js:88:12)
    at eval (D:\CreatingSpace\hexo\themes\Sakura\layout\tag.ejs:16:11)
    at tag (D:\CreatingSpace\hexo\node_modules\ejs\lib\ejs.js:682:17)
    at viewFn._compiled (D:\CreatingSpace\hexo\node_modules\hexo\lib\theme\view.js:136:48)
    at viewFn.View.render (D:\CreatingSpace\hexo\node_modules\hexo\lib\theme\view.js:41:15)
    at D:\CreatingSpace\hexo\node_modules\hexo\lib\hexo\index.js:61:21
    at tryCatcher (D:\CreatingSpace\hexo\node_modules\bluebird\js\release\util.js:16:23)
    at D:\CreatingSpace\hexo\node_modules\bluebird\js\release\method.js:15:34
    at RouteStream._read (D:\CreatingSpace\hexo\node_modules\hexo\lib\hexo\router.js:126:3)
    at RouteStream.Readable.read (_stream_readable.js:459:10)
    at resume_ (_stream_readable.js:948:12)
    at processTicksAndRejections (internal/process/task_queues.js:84:21)
{% endraw %}
```
