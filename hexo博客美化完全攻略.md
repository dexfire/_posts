---
title: hexo博客美化完全攻略
author: dexfire
photos: /img/20200503135002.jpg
date: 2020-05-04 09:24:52
keywords:
description:
tags:
---

# hexo博客美化完全攻略

Hexo 是一款开源的模板（template）网站搭建系统，是搭建一个轻量级网站（产品主页、Docs、个人博客、个人简历容器）的最佳选择。Hexo的技术栈大致有：
- Web 层
  - `html`
  - `js`
  - `css`
- 应用模板层
  - `Nunjucks`
  - `ejs`
  - `stylus`
- 底层插件实现
  - `Node.js`

## 主题项目结构

```
├─ layout
│  ├─ layout.ejs
│  ├─ index.ejs
│  ├─ archive.ejs
│  ├─ post.ejs
│  ├─ page.ejs
│  ├─ tag.ejs
│  ├─ category.ejs
├─ source
│  ├─ scss
│  ├─ css
│  ├─ fonts
│  ├─ js
│  ├─ images
├─ _config.yml
├─ LICENSE
├─ package.json
├─ README.md
```

### 模板

| Template | Page              | Fallback |
| -------- | ----------------- | -------- |
| index    | Home page         |          |
| post     | Posts             | index    |
| page     | Pages             | index    |
| archive  | Archives          | index    |
| category | Category archives | archive  |
| tag      | Tag archives      | archive  |

#### layouts

假定 `layout.ejs` `index.ejs` 内容如下：

```html
<!DOCTYPE html>
<html>
  <body><%- body %></body>
</html>
```

```html
  Homepage.
```

那么渲染结果为：  
```html
<!DOCTYPE html>
<html>
  <body>Homepage.</body>
</html>
```

### templating 语法 : hexo-ejs

hexo中的ejs与nunjucks

### templating 语法 : Nunjucks

模板语法主要涉及

## 使用jsDeliver服务器cdn加速
github pages 使用 亚马逊服务器，本身在国内访问速度很慢，所以一些常用的资源文件，采用cdn分布式加速网络可以显著提高响应速度。

- [jsDelivr](https://www.jsdelivr.com/)

怎么操作？
1. 在github创建一个项目，名称假定设为`cdn`，之后将assets文件推送到github repo中
2. 使用 `git tag -a "v1.0.x" -m "initial version of cdn assets."`，为当前commit设置标签
3. 使用 `git push --tags` 推送标签到 github 服务器
4. 使用 https://cdn.jsdelivr.net/gh/user/repo@version/file 来访问你的文件，这里的例子是
`https://cdn.jsdelivr.net/gh/dexfire/cdn@v1.0.x/js/custom.css`

```
// load any GitHub release, commit, or branch
// note: we recommend using npm for projects that support it
https://cdn.jsdelivr.net/gh/user/repo@version/file

// load jQuery v3.2.1
https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/dist/jquery.min.js

// use a version range instead of a specific version
https://cdn.jsdelivr.net/gh/jquery/jquery@3.2/dist/jquery.min.js
https://cdn.jsdelivr.net/gh/jquery/jquery@3/dist/jquery.min.js

// omit the version completely to get the latest one
// you should NOT use this in production
https://cdn.jsdelivr.net/gh/jquery/jquery/dist/jquery.min.js

// add ".min" to any JS/CSS file to get a minified version
// if one doesn't exist, we'll generate it for you
https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/src/core.min.js

// add / at the end to get a directory listing
https://cdn.jsdelivr.net/gh/jquery/jquery/
```

## 添加并配置TOC侧栏目录
使用`tocbot`插件：
- [tocbot @ npm](https://www.npmjs.com/package/tocbot)
- [tocbot homepage](http://tscanlin.github.io/tocbot/)

![tocbot](/images/QQ截图20200504093916.png)

**在body末尾添加**
`<script src="https://cdnjs.cloudflare.com/ajax/libs/tocbot/4.4.2/tocbot.min.js"></script>`

**在head中添加**
`<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/tocbot/4.4.2/tocbot.css">`

**配置文件**
```js
    // 渲染的目录显示位置选择器
    tocSelector: '.js-toc',
    // 正文筛选器
    contentSelector: '.js-toc-content',
    // Which headings to grab inside of the contentSelector element.
    headingSelector: 'h1, h2, h3',
    // Headings that match the ignoreSelector will be skipped.
    ignoreSelector: '.js-toc-ignore',
    // For headings inside relative or absolute positioned containers within content.
    hasInnerContainers: false,
    // Main class to add to links.
    linkClass: 'toc-link',
    // Extra classes to add to links.
    extraLinkClasses: '',
    // Class to add to active links,
    // the link corresponding to the top most heading on the page.
    activeLinkClass: 'is-active-link',
    // Main class to add to lists.
    listClass: 'toc-list',
    // Extra classes to add to lists.
    extraListClasses: '',
    // Class that gets added when a list should be collapsed.
    isCollapsedClass: 'is-collapsed',
    // Class that gets added when a list should be able
    // to be collapsed but isn't necessarily collapsed.
    collapsibleClass: 'is-collapsible',
    // Class to add to list items.
    listItemClass: 'toc-list-item',
    // How many heading levels should not be collapsed.
    // For example, number 6 will show everything since
    // there are only 6 heading levels and number 0 will collapse them all.
    // The sections that are hidden will open
    // and close as you scroll to headings within them.
    collapseDepth: 0,
    // Smooth scrolling enabled.
    scrollSmooth: true,
    // Smooth scroll duration.
    scrollSmoothDuration: 420,
    // Callback for scroll end.
    scrollEndCallback: function (e) { },
    // Headings offset between the headings and the top of the document (this is meant for minor adjustments).
    headingsOffset: 1,
    // Timeout between events firing to make sure it's
    // not too rapid (for performance reasons).
    throttleTimeout: 50,
    // Element to add the positionFixedClass to.
    positionFixedSelector: null,
    // Fixed position class to add to make sidebar fixed after scrolling
    // down past the fixedSidebarOffset.
    positionFixedClass: 'is-position-fixed',
    // fixedSidebarOffset can be any number but by default is set
    // to auto which sets the fixedSidebarOffset to the sidebar
    // element's offsetTop from the top of the document on init.
    fixedSidebarOffset: 'auto',
    // includeHtml can be set to true to include the HTML markup from the
    // heading node instead of just including the textContent.
    includeHtml: false,
    // onclick function to apply to all links in toc. will be called with
    // the event as the first parameter, and this can be used to stop,
    // propagation, prevent default or perform action
    onClick: false,
    // orderedList can be set to false to generate unordered lists (ul)
    // instead of ordered lists (ol)
    orderedList: true,
    // If there is a fixed article scroll container, set to calculate titles' offset
    scrollContainer: null,
    // prevent ToC DOM rendering if it's already rendered by an external system
    skipRendering: false,
    // Optional callback to change heading labels.
    // For example it can be used to cut down and put ellipses on multiline headings you deem too long.
    // Called each time a heading is parsed. Expects a string in return, the modified label to display.
    headingLabelCallback: function (string) => string,
    // ignore headings that are hidden in DOM
    ignoreHiddenElements: false,
    // Optional callback to modify properties of parsed headings.
    // The heading element is passed in node parameter and information parsed by default parser is provided in obj parameter.
    // Function has to return the same or modified obj.
    // The heading will be excluded from TOC if nothing is returned.
    // function (object, HTMLElement) => object | void
    headingObjectCallback: null,
    // Set the base path, useful if you use a `base` tag in `head`.
    basePath: '',
```
