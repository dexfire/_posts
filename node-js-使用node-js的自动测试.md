---
title: '[node.js]使用node.js的自动测试'
keywords: node.js
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ["node.js"]
tags: ["node.js"]
date: 2020-05-08 21:11:57
description:
authorAbout:
authorDesc:
photos: /img/sky.jpg
---

# {{ post.title }}

自动测试方法： `npm test`  
可实现node包的用例测试：  

![](/img/2020-05-08_211052.jpg)  

## 编写测试脚本

- 测试脚本`test.js`:  
```ts
const markdownIt = require('markdown-it')
const generate = require('markdown-it-testgen')
const m = require('..')

describe('markdown-it-todo', () => {
  const md = markdownIt().use(m)
  generate(`${__dirname}/fixtures/enml-todo.txt`, {header: true}, md)
})
```

- 提前编好测试用例：  
```text
should not render todos without list
.
[ ] unchecked item 1
[ ] unchecked item 2
[x] checked item 3
.
<p>[ ] unchecked item 1
[ ] unchecked item 2
[x] checked item 3</p>
.

should render todos with ordered list
.
1. [ ] unchecked ordered 1
2. [ ] unchecked ordered 2
3. [x] checked ordered 3
.
<ol class="task-list">
<li class="task-list-item"><input disabled="true" class="markdown-todo"></input> unchecked ordered 1</li>
<li class="task-list-item"><input disabled="true" class="markdown-todo"></input> unchecked ordered 2</li>
<li class="task-list-item"><input disabled="true" checked="true" class="markdown-todo"></input> checked ordered 3</li>
</ol>
.

[...]
```

## 测试

- 运行 `npm test`:

- 输出（失败）：
```text
> markdown-it-todo@1.0.0 test D:\CreatingSpace\markdown-it-todo
> npm run lint && mocha

> markdown-it-todo@1.0.0 lint D:\CreatingSpace\markdown-it-todo
> xo

  markdown-it-todo

      √ should not render todos without list
      1) should render todos with unordered list
      2) should render todos with ordered list
      3) should only render valid todos
      4) should render todos with nested list

  1 passing (131ms)
  4 failing

  1) markdown-it-todo

         should render todos with unordered list:

      AssertionError: expected '<ul class="task-list">\n<li class="task-list-item"><input disabled="true" class="markdown-todo"></input> unchecked item 1</li>\n<li class="task-list-item"><input disabled="true" class="markdown-todo"></input> unchecked item 2</li>\n<li class="task-list-item"><input disabled="true" checked="true" class="markdown-todo"></input> checked item 3</li>\n</ul>\n' to equal '<ul class="task-list">\n<li class="task-list-item"><en-todo></en-todo> unchecked item 1</li>\n<li class="task-list-item"><en-todo></en-todo> unchecked item 2</li>\n<li class="task-list-item"><en-todo checked="true"></en-todo> checked item 3</li>\n</ul>\n'
      + expected - actual

       <ul class="task-list">
      -<li class="task-list-item"><input disabled="true" class="markdown-todo"></input> unchecked item 1</li>
      -<li class="task-list-item"><input disabled="true" class="markdown-todo"></input> unchecked item 2</li>
      -<li class="task-list-item"><input disabled="true" checked="true" class="markdown-todo"></input> checked item 3</li>
      +<li class="task-list-item"><en-todo></en-todo> unchecked item 1</li>
      +<li class="task-list-item"><en-todo></en-todo> unchecked item 2</li>
      +<li class="task-list-item"><en-todo checked="true"></en-todo> checked item 3</li>
       </ul>

      at Function.assert.strictEqual (node_modules\chai\lib\chai\interface\assert.js:169:32)
      at Context.<anonymous> (node_modules\markdown-it-testgen\index.js:196:26)
      at processImmediate (internal/timers.js:456:21)

  2) markdown-it-todo

         should render todos with ordered list:

```

- 输出（成功）：
```text
> markdown-it-todo@1.0.0 test D:\CreatingSpace\markdown-it-todo
> npm run lint && mocha

> markdown-it-todo@1.0.0 lint D:\CreatingSpace\markdown-it-todo
> xo

  markdown-it-todo

      √ should not render todos without list
      √ should render todos with unordered list
      √ should render todos with ordered list
      √ should only render valid todos
      √ should render todos with nested list

  5 passing (45ms)
```
