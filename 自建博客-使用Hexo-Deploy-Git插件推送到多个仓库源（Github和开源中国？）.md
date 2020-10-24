---
title: '[自建博客]使用Hexo-Deploy-Git插件推送到多个仓库源（Github和开源中国？）'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: []
tags: []
disableNunjucks: true
date: 2020-05-19 14:54:26
keywords:
description:
authorAbout:
authorDesc:
photos:
---
{% raw %}
# [自建博客]使用Hexo-Deploy-Git插件推送到多个仓库源（Github和开源中国？）
首先，我们下载好hexo-deploy-git插件，普通使用就是在`_config.yml`中写上配置如下即可：

```yaml
# Deployment
# Docs: https://hexo.io/docs/one-command-deployment
deploy:
    type: git
    repo: https://github.com/dexfire/hmm_sakura
    branch: master
    message: Site updated at {% raw %} {{ now('YYYY-MM-DD HH:mm:ss') }} {% endraw %}
```

那么，问题来了，如果想同时推送两个源怎么办呢？比如，同时在github和gitee上搭建博客，这里首先想到的居然是看源码...费时费力，也没看到处理多分支的代码，然后看了官方文档，发现是原生支持的...

[![](/img/2020-05-19_145822.jpg)](https://hexo.io/docs/one-command-deployment)

所以最终效果：


```yaml
# Deployment
# Docs: https://hexo.io/docs/one-command-deployment
deploy:
  - type: git
    repo: https://github.com/dexfire/hmm_sakura
    branch: master
    message: Site updated at {% raw %} {{ now('YYYY-MM-DD HH:mm:ss') }} {% endraw %}
  - type: git
    repo: git://git@gitee.com:dexfire/dexfire.git
    branch: gh-pages
    message: Site updated at {% raw %} {{ now('YYYY-MM-DD HH:mm:ss') }} {% endraw %}
```


推送看效果：
```
INFO  Start processing
INFO  Files loaded in 10 s
INFO  Generated: archives/page/6/index.html
INFO  Generated: img/bfebc17a6f2cb9452fb2642f67488755cb062561.jpg@518w_1e_1c.jpg
...
INFO  Generated: img/0072Vf1pgy1fodqpglwr2j312w0rnx6p.jpg
INFO  Generated: vid/1074_0b53mjitoaibcqadf3wehjpdgyqeg53adwsa.f20.mp4
INFO  123 files generated in 27 s
INFO  Deploying: git
INFO  Clearing .deploy_git folder...
INFO  Copying files from public folder...
INFO  Copying files from extend dirs...
[gh-pages d5bb5882] Site updated at 2020-05-21 00:42:15
 123 files changed, 30583 insertions(+), 1988 deletions(-)
 ...
 create mode 100644 "tags/\350\275\254\345\217\221/index.html"
 create mode 100644 vid/1074_0b53mjitoaibcqadf3wehjpdgyqeg53adwsa.f20.mp4
Enumerating objects: 243, done.
Counting objects: 100% (243/243), done.
Delta compression using up to 4 threads
Compressing objects: 100% (104/104), done.
Writing objects: 100% (154/154), 5.16 MiB | 2.56 MiB/s, done.
Total 154 (delta 65), reused 0 (delta 0)
remote: Resolving deltas: 100% (65/65), completed with 23 local objects.
To https://github.com/dexfire/hmm_sakura
   f41ef22e..d5bb5882  HEAD -> master
Branch 'gh-pages' set up to track remote branch 'master' from 'https://github.com/dexfire/hmm_sakura'.
[32mINFO [39m Deploy done: [35mgit[39m
[32mINFO [39m Deploying: [35mgit[39m
[32mINFO [39m Clearing .deploy_git folder...
[32mINFO [39m Copying files from public folder...
[32mINFO [39m Copying files from extend dirs...
On branch gh-pages
nothing to commit, working tree clean
Enumerating objects: 243, done.
Counting objects: 100% (243/243), done.
Delta compression using up to 4 threads
Compressing objects: 100% (104/104), done.
Writing objects: 100% (154/154), 5.16 MiB | 1.18 MiB/s, done.
Total 154 (delta 65), reused 0 (delta 0)
remote: Resolving deltas: 100% (65/65), completed with 23 local objects.
remote: Powered by GITEE.COM [GNK-5.0]
To https://gitee.com/dexfire/dexfire/
   f41ef22e..d5bb5882  HEAD -> gh-pages
Branch 'gh-pages' set up to track remote branch 'gh-pages' from 'https://gitee.com/dexfire/dexfire/'.
[32mINFO [39m Deploy done: [35mgit[39m
```


