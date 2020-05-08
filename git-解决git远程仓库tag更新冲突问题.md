---
title: '[git]解决git远程仓库tag更新冲突问题'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ["git"]
tags: ["git"]
date: 2020-05-08 21:46:04
keywords: git tag 冲突
description:
authorAbout:
authorDesc:
photos: /img/07A0CD8B-9B0F-43F9-9F7E-FDD4B18FF7DD-1593-000001D89138AFE8.jpg
---

# {{ post.title }}

## 添加标签(tag)

**添加tag语法**：  
`git tag -a <tag name> -m <tag message>`

## 强制更新本地tag

加上 `-f` 选项即可，全称 `--force`  
`git tag -f -a <tag name> -m <tag message>`

```text
> git tag -f -a 1.0.3 -m "changed `<en-todo>` tag to `<input>`"
Updated tag '1.0.3' (was 1f1e147)
```

## 强制更新远程仓库tag

如果直接推送本地更新过的tag到远程服务器，会被服务器拒绝：

`> git push origin master --tags`

![](/img/QQ截图20200508215449.png)

```text
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 335 bytes | 83.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/dexfire/markdown-it-todo
   80c72f8..754cdc8  master -> master
 ! [rejected]        1.0.3 -> 1.0.3 (already exists)
error: failed to push some refs to 'https://github.com/dexfire/markdown-it-todo'
hint: Updates were rejected because the tag already exists in the remote.
```

这时我们同样需要强制推送，更新远程tag，同样增加`-f`选项即可：  
`git push origin master --tags --force`

```text
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 175 bytes | 175.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To https://github.com/dexfire/markdown-it-todo
 + 1f1e147...1b62e7d 1.0.3 -> 1.0.3 (forced update)
```
