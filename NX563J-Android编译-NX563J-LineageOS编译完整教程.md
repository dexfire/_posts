---
title: '[NX563J][Android编译]NX563J LineageOS编译完整教程'
keywords: NX563J Android Android编译 教程分享
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: post
photos: /img/20200503135002.jpg
date: 2020-05-06 21:34:08
description:
authorAbout:
authorDesc:
tags:
  - NX563J
  - Android
  - Android编译
  - 教程分享
---

# [NX563J][Android编译]NX563J LineageOS编译完整教程

Ubuntu18.04编译 lineageOS17.1

## 1. 安装配置git
```bash
sudo apt-get install git
git config user.email "test@test.com"  #注：github帐户注册邮箱
git config user.name "test"  #注：github用户名
```

## 2. 安装java

```bash
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update3 sudo
apt-get install openjdk-8-jdk
```

## 3. 配置PATH环境变量

```bash
mkdir ~/bin
echo "PATH=~/bin:\$PATH" >> ~/.bashrc
source ~/.bashrc
```

将~/bin放入环境变量`gedit ~/.profile`  
加入：

```bash
# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi
```

使改动生效:  
`source ~/.profile`

## 4. 安装依赖库

```bash
sudo apt-get install libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-dev g++-multilib
sudo apt-get install -y git flex bison gperf build-essential libncurses5-dev:i386
sudo apt-get install tofrodos python-markdown libxml2-utils xsltproc zlib1g-dev:i386
sudo apt-get install dpkg-dev libsdl1.2-dev libesd0-dev
sudo apt-get install git-core gnupg flex bison gperf build-essential
sudo apt-get install zip curl zlib1g-dev gcc-multilib g++-multilib
sudo apt-get install libc6-dev-i386
sudo apt-get install lib32ncurses5-dev x11proto-core-dev libx11-dev
sudo apt-get install libgl1-mesa-dev libxml2-utils xsltproc unzip m4
sudo apt-get install lib32z-dev ccache
sudo apt-get install libssl-dev
```

## 5. 下载配置 repo

```bash
curl https://mirrors.tuna.tsinghua.edu.cn/git/git-repo -o repo
chmod +x repo
```

## 6. 修改~/bin/repo 中的REPO_URL 字段为

`REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo'`

## 7. 开始下载代码

建立机型目录并进入:  
`mkdir ~/LineageOS && cd ~/LineageOS`
`repo init -u git://github.com/LineageOS/android.git -b lineage-16.1`

修改manifest.xml:

```xml
<remote  name="github"
        fetch="https://github.com/" />

<remote  name="lineage"
        fetch="https://mirrors.tuna.tsinghua.edu.cn/git/lineageOS/"
        review="review.lineageos.org" />

<remote  name="private"
        fetch="ssh://git@github.com" />

<remote  name="aosp"
        fetch="https://aosp.tuna.tsinghua.edu.cn"
        review="android-review.googlesource.com"
        revision="refs/tags/android-9.0.0_r35" />

<default revision="refs/heads/lineage-16.0"
        remote="github"
        sync-c="true"
        sync-j="4" />
```

开始同步：  
`repo sync -j<core count +1>`

## 8. 下载android_device-niuba-nx563j

## 9. 下载android_device-niuba-nx563j-msm8998-common

提取vendor手机要root  
`adb shell su -c setenforce 0`

终端进入/device/nubia/nx563j目录下。执行  

```bash
chmod 755 *.sh
./setup-makefiles.sh
./extract-files.sh
```

此时，device/vendor/nubia下会出现个nx563j的目录

### 编译前准备

先设定缓存加快编译、方便下次编译提升速度

终端输入：`gedit ~/.bashrc`  
加入：`export USE_CCACHE=1`  
使改动生效: `source ~/.bashrc`  
执行：`ccache -M 50`  
配置jack  
`gedit ~/.bashrc`  

加入：  
`export ANDROID_JACK_VM_ARGS="-Dfile.encoding=UTF-8 -XX:+TieredCompilation -Xmx8G"`

使改动生效: `source ~/.bashrc`  
### 编译整个源码  
```bash
source build/envsetup.sh
brunch nx563j
```

下次编译前请清理上次的编译文件，在lineagos目录下输入执行  `make clobber`  
如果编译成功，终端会出现一行绿色的字  
Zip包可以在 `~/LineageOS/out/target/product/`
