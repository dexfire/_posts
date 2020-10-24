---
title: '[Android编译][NX563J]从源码编译 LineageOS for Nubia Z17 Max'
author: dexfire
avatar: //q2.qlogo.cn/headimg_dl?dst_uin=1944404463&spec=5
authorLink: dexfire.cn
categories: ['Android编译']
tags: ['Android编译', 'NX563J']
date: 2020-05-17 14:17:04
keywords:
description:
authorAbout:
authorDesc:
photos:
---

# {{ post.title }}

## 编译中的一些问题

```text
### 
dexfire@dexfire-PC:/media/dexfire/mm/lineageos$ m | tee build_log.txt
============================================
PLATFORM_VERSION_CODENAME=REL
PLATFORM_VERSION=10
LINEAGE_VERSION=17.1-20200517-UNOFFICIAL-nx563j
TARGET_PRODUCT=lineage_nx563j
TARGET_BUILD_VARIANT=userdebug
TARGET_BUILD_TYPE=release
TARGET_ARCH=arm64
TARGET_ARCH_VARIANT=armv8-a
TARGET_CPU_VARIANT=generic
TARGET_2ND_ARCH=arm
TARGET_2ND_ARCH_VARIANT=armv8-a
TARGET_2ND_CPU_VARIANT=generic
HOST_ARCH=x86_64
HOST_2ND_ARCH=x86
HOST_OS=linux
HOST_OS_EXTRA=Linux-4.15.0-30deepin-generic-x86_64-Deepin-15
HOST_CROSS_OS=windows
HOST_CROSS_ARCH=x86
HOST_CROSS_2ND_ARCH=x86_64
HOST_BUILD_TYPE=release
BUILD_ID=QQ2A.200501.001.B2
OUT_DIR=out
PRODUCT_SOONG_NAMESPACES=device/nubia/msm8998-common vendor/nubia/msm8998-common vendor/nubia/nx563j hardware/qcom-caf/msm8998
============================================
ninja: no work to do.
[100% 1/1] out/soong/.bootstrap/bin/soong_build out/soong/build.ninja
FAILED: out/soong/build.ninja
out/soong/.bootstrap/bin/soong_build -t -l out/.module_paths/Android.bp.list -b out/soong -n out -d out/soong/build.ninja.d -globFile out/soong/.bootstrap/build-globs.ninja -o out/soong/build.ninja Android.bp
fatal error: runtime: out of memory

runtime stack:
runtime.throw(0xa1f4ab, 0x16)
	prebuilts/go/linux-x86/src/runtime/panic.go:617 +0x72
runtime.sysMap(0xc158000000, 0x4000000, 0xf517d8)
	prebuilts/go/linux-x86/src/runtime/mem_linux.go:170 +0xc7
runtime.(*mheap).sysAlloc(0xf39fc0, 0xc000, 0xf39fd0, 0x6)
	prebuilts/go/linux-x86/src/runtime/malloc.go:633 +0x1cd
runtime.(*mheap).grow(0xf39fc0, 0x6, 0x0)
	prebuilts/go/linux-x86/src/runtime/mheap.go:1232 +0x42
runtime.(*mheap).allocSpanLocked(0xf39fc0, 0x6, 0xf517e8, 0x7f6f2f8f8e70)
	prebuilts/go/linux-x86/src/runtime/mheap.go:1150 +0x3a7
runtime.(*mheap).alloc_m(0xf39fc0, 0x6, 0x450063, 0x7f6f2f8f8e70)
	prebuilts/go/linux-x86/src/runtime/mheap.go:977 +0xc2
runtime.(*mheap).alloc.func1()
	prebuilts/go/linux-x86/src/runtime/mheap.go:1048 +0x4c
runtime.systemstack(0x0)
	prebuilts/go/linux-x86/src/runtime/asm_amd64.s:351 +0x66
runtime.mstart()
	prebuilts/go/linux-x86/src/runtime/proc.go:1153

goroutine 1 [running]:
runtime.systemstack_switch()
	prebuilts/go/linux-x86/src/runtime/asm_amd64.s:311 fp=0xc103a421f8 sp=0xc103a421f0 pc=0x4587f0
runtime.(*mheap).alloc(0xf39fc0, 0x6, 0x10063, 0xc0001a4360)
	prebuilts/go/linux-x86/src/runtime/mheap.go:1047 +0x8a fp=0xc103a42248 sp=0xc103a421f8 pc=0x42434a
runtime.(*mcentral).grow(0xf3bc00, 0x0)
	prebuilts/go/linux-x86/src/runtime/mcentral.go:256 +0x95 fp=0xc103a42290 sp=0xc103a42248 pc=0x417285
runtime.(*mcentral).cacheSpan(0xf3bc00, 0x0)
	prebuilts/go/linux-x86/src/runtime/mcentral.go:106 +0x2ff fp=0xc103a422f0 sp=0xc103a42290 pc=0x416d8f
runtime.(*mcache).refill(0x7f6f457ea460, 0x63)
	prebuilts/go/linux-x86/src/runtime/mcache.go:135 +0x86 fp=0xc103a42310 sp=0xc103a422f0 pc=0x416826
runtime.(*mcache).nextFree(0x7f6f457ea460, 0x63, 0x0, 0x0, 0x92)
	prebuilts/go/linux-x86/src/runtime/malloc.go:786 +0x88 fp=0xc103a42348 sp=0xc103a42310 pc=0x40b488
runtime.mallocgc(0x1b00, 0x9454a0, 0xc153ff9d01, 0x92)
	prebuilts/go/linux-x86/src/runtime/malloc.go:939 +0x76e fp=0xc103a423e8 sp=0xc103a42348 pc=0x40bd9e
runtime.makeslice(0x9454a0, 0x0, 0x1a97, 0x6bf9d7)
	prebuilts/go/linux-x86/src/runtime/slice.go:49 +0x6c fp=0xc103a42418 sp=0xc103a423e8 pc=0x441fac
strings.(*Builder).grow(...)
	prebuilts/go/linux-x86/src/strings/builder.go:67
strings.(*Builder).Grow(...)
	prebuilts/go/linux-x86/src/strings/builder.go:81
strings.Join(0xc0fe2d4000, 0x2e, 0x2e, 0xa0c4e8, 0x1, 0x2e, 0x0)
	prebuilts/go/linux-x86/src/strings/strings.go:438 +0x4d0 fp=0xc103a424f0 sp=0xc103a42418 pc=0x4e0db0
android/soong/cc.(*libraryDecorator).androidMkWriteExportedFlags(0xc08da7fb80, 0xb04020, 0xc10bf092c0)
	/media/dexfire/mm/lineageos/build/soong/cc/androidmk.go:144 +0xb4 fp=0xc103a42560 sp=0xc103a424f0 pc=0x6fc7e4
android/soong/cc.(*libraryDecorator).AndroidMk.func2(0xb04020, 0xc10bf092c0, 0xb0f0e0, 0xc0fb9b3290)
	/media/dexfire/mm/lineageos/build/soong/cc/androidmk.go:171 +0x50 fp=0xc103a425e8 sp=0xc103a42560 pc=0x77e3b0
android/soong/android.WriteAndroidMkData(0xb04020, 0xc10bf092c0, 0xa183fa, 0x10, 0xa0f366, 0x7, 0x0, 0x0, 0x0, 0x1, ...)
	/media/dexfire/mm/lineageos/build/soong/android/androidmk.go:438 +0xef fp=0xc103a42660 sp=0xc103a425e8 pc=0x64e22f
android/soong/android.translateAndroidModule(0xb26440, 0xc10bf091d0, 0xb04020, 0xc10bf092c0, 0xb08760, 0xc08daa2d80, 0x7f6f2fba3840, 0xc08daa2d80, 0x5eb310, 0xc0ee58d3f0)
	/media/dexfire/mm/lineageos/build/soong/android/androidmk.go:420 +0x969 fp=0xc103a433a0 sp=0xc103a42660 pc=0x64dc49
android/soong/android.translateAndroidMkModule(0xb26440, 0xc10bf091d0, 0xb04020, 0xc10bf092c0, 0xb08760, 0xc08daa2d80, 0x0, 0x0)
	/media/dexfire/mm/lineageos/build/soong/android/androidmk.go:348 +0x29b fp=0xc103a43400 sp=0xc103a433a0 pc=0x64cffb
android/soong/android.translateAndroidMk(0xb26440, 0xc10bf091d0, 0xc00d3de450, 0x23, 0xc14f37e000, 0xb814, 0xbc00, 0xc00017e000, 0x0)
	/media/dexfire/mm/lineageos/build/soong/android/androidmk.go:293 +0x7b2 fp=0xc103a436a0 sp=0xc103a43400 pc=0x64cb42
android/soong/android.(*androidMkSingleton).GenerateBuildActions(0xf50888, 0xb26440, 0xc10bf091d0)
	/media/dexfire/mm/lineageos/build/soong/android/androidmk.go:275 +0x3c7 fp=0xc103a43998 sp=0xc103a436a0 pc=0x64c1f7
android/soong/android.(*singletonAdaptor).GenerateBuildActions(0xc00016d980, 0xb26740, 0xc0ee58d3f0)
	/media/dexfire/mm/lineageos/build/soong/android/singleton.go:92 +0xb7 fp=0xc103a439c8 sp=0xc103a43998 pc=0x69bcd7
github.com/google/blueprint.(*Context).generateSingletonBuildActions.func1(0xc093d85ac8, 0xc0ee58d3f0)
	/media/dexfire/mm/lineageos/build/blueprint/context.go:2378 +0x81 fp=0xc103a439f8 sp=0xc103a439c8 pc=0x5f70f1
github.com/google/blueprint.(*Context).generateSingletonBuildActions(0xc00009a9c0, 0xa08f00, 0xc00017e000, 0xc0000c4900, 0x11, 0x20, 0xc016894a20, 0x0, 0x0, 0x0, ...)
	/media/dexfire/mm/lineageos/build/blueprint/context.go:2379 +0x299 fp=0xc103a43b30 sp=0xc103a439f8 pc=0x5cbcd9
github.com/google/blueprint.(*Context).PrepareBuildActions.func1(0xb0ef20, 0xc08ba926f0)
	/media/dexfire/mm/lineageos/build/blueprint/context.go:1911 +0x158 fp=0xc103a43c68 sp=0xc103a43b30 pc=0x5f3328
runtime/pprof.Do(0xb0ef20, 0xc08ba926f0, 0xc038129a20, 0x1, 0x1, 0xc093d85d00)
	prebuilts/go/linux-x86/src/runtime/pprof/runtime.go:35 +0xca fp=0xc103a43cb0 sp=0xc103a43c68 pc=0x59c22a
github.com/google/blueprint.(*Context).PrepareBuildActions(0xc00009a9c0, 0xa08f00, 0xc00017e000, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0)
	/media/dexfire/mm/lineageos/build/blueprint/context.go:1892 +0x12e fp=0xc103a43d40 sp=0xc103a43cb0 pc=0x5ca0ce
github.com/google/blueprint/bootstrap.Main(0xc00009a9c0, 0xa08f00, 0xc00017e000, 0xc00056bf68, 0x3, 0x4)
	/media/dexfire/mm/lineageos/build/blueprint/bootstrap/command.go:171 +0x99e fp=0xc103a43ed8 sp=0xc103a43d40 pc=0x63ee9e
main.main()
	/media/dexfire/mm/lineageos/build/soong/cmd/soong_build/main.go:75 +0x2d4 fp=0xc103a43f98 sp=0xc103a43ed8 pc=0x8f0f54
runtime.main()
	prebuilts/go/linux-x86/src/runtime/proc.go:200 +0x20c fp=0xc103a43fe0 sp=0xc103a43f98 pc=0x42df5c
runtime.goexit()
	prebuilts/go/linux-x86/src/runtime/asm_amd64.s:1337 +0x1 fp=0xc103a43fe8 sp=0xc103a43fe0 pc=0x45a741
ninja: build stopped: subcommand failed.
12:04:36 soong bootstrap failed with: exit status 1

#### failed to build some targets (03:19 (mm:ss)) ####
```

**解决方法**：增加swap虚拟内存。


### no kernel
```text
[ 99% 485/486] finishing build rules ...
vendor/lineage/build/tasks/kernel.mk:111: warning: ***************************************************************
vendor/lineage/build/tasks/kernel.mk:112: warning: * Using prebuilt kernel binary instead of source              *
vendor/lineage/build/tasks/kernel.mk:113: warning: * THIS IS DEPRECATED, AND IS NOT ADVISED.                     *
vendor/lineage/build/tasks/kernel.mk:114: warning: * Please configure your device to download the kernel         *
vendor/lineage/build/tasks/kernel.mk:115: warning: * source repository to kernel/nubia/msm8998
vendor/lineage/build/tasks/kernel.mk:116: warning: * for more information                                        *
vendor/lineage/build/tasks/kernel.mk:117: warning: ***************************************************************
[100% 486/486] writing build rules ...
out/build-lineage_nx563j-package.ninja is missing, regenerating...
[ 99% 487/489] initializing packaging system ...
[ 99% 488/489] including distdir.mk ...
[100% 489/489] writing packaging rules ...
Starting ninja...
14:14:23 ninja failed with: exit status 1
FAILED: ninja: 'out/target/product/nx563j/kernel', needed by 'out/target/product/nx563j/boot.img', missing and no known rule to make it

```

**解决方法**：  
克隆这个仓库[android_kernel_nubia_msm8998](https://github.com/LineageOS/android_kernel_nubia_msm8998).

放置位置看下一节！

## FAILED: ninja: 'out/.../kernel', needed by 'out/.../boot.img', missing and no known rule to make it

`18:38:42 ninja failed with: exit status 1`

```text
$ m -j5 | tee build_log4.txt
============================================
PLATFORM_VERSION_CODENAME=REL
PLATFORM_VERSION=10
LINEAGE_VERSION=17.1-20200517-UNOFFICIAL-nx563j
TARGET_PRODUCT=lineage_nx563j
TARGET_BUILD_VARIANT=userdebug
TARGET_BUILD_TYPE=release
TARGET_ARCH=arm64
TARGET_ARCH_VARIANT=armv8-a
TARGET_CPU_VARIANT=generic
TARGET_2ND_ARCH=arm
TARGET_2ND_ARCH_VARIANT=armv8-a
TARGET_2ND_CPU_VARIANT=generic
HOST_ARCH=x86_64
HOST_2ND_ARCH=x86
HOST_OS=linux
HOST_OS_EXTRA=Linux-4.15.0-30deepin-generic-x86_64-Deepin-15
HOST_CROSS_OS=windows
HOST_CROSS_ARCH=x86
HOST_CROSS_2ND_ARCH=x86_64
HOST_BUILD_TYPE=release
BUILD_ID=QQ2A.200501.001.B2
OUT_DIR=out
PRODUCT_SOONG_NAMESPACES=device/nubia/msm8998-common vendor/nubia/msm8998-common vendor/nubia/nx563j hardware/qcom-caf/msm8998
============================================
ninja: no work to do.
[100% 1/1] out/soong/.bootstrap/bin/soong_build out/soong/build.ninja
No need to regenerate ninja file
No need to regenerate ninja file
No need to regenerate ninja file
Starting ninja...
FAILED: ninja: 'out/target/product/nx563j/kernel', needed by 'out/target/product/nx563j/boot.img', missing and no known rule to make it
18:38:42 ninja failed with: exit status 1
```

从device入手，也就是 `device/nubia/nx563j.mk`  
其中，根makefile是 `Android.mk`，其中调用了同目录下所有的mk文件。  
其中的`lineage_nx563j.mk`当中，引用了另外两条。  
```make
$(call inherit-product, device/nubia/nx563j/full_nx563j.mk)

# Inherit some common Lineage stuff.
$(call inherit-product, vendor/lineage/config/common_full_phone.mk)
```

另外一个：`full_nx563j.mk`  
```make
# Inherit from those products. Most specific first.
$(call inherit-product, $(SRC_TARGET_DIR)/product/core_64_bit.mk)
$(call inherit-product, $(SRC_TARGET_DIR)/product/full_base_telephony.mk)

# Inherit from nx563j device
$(call inherit-product, device/nubia/nx563j/device.mk)
```

其中也没看到相应的代码。不过最后在`device/nubia/msm8998-common`下，`BoardConfigCommon.mk`下面看到：

```make
# Kernel
BOARD_KERNEL_CMDLINE := androidboot.hardware=qcom user_debug=31 msm_rtb.filter=0x37 ehci-hcd.park=3 
BOARD_KERNEL_CMDLINE += lpm_levels.sleep_disabled=1 sched_enable_hmp=1 sched_enable_power_aware=1 
BOARD_KERNEL_CMDLINE += service_locator.enable=1 swiotlb=2048 androidboot.usbconfigfs=true 
BOARD_KERNEL_CMDLINE += androidboot.usbcontroller=a800000.dwc3 
BOARD_KERNEL_CMDLINE += loop.max_part=7
BOARD_KERNEL_BASE := 0x00000000
BOARD_KERNEL_PAGESIZE := 4096
BOARD_KERNEL_TAGS_OFFSET := 0x00000100
BOARD_RAMDISK_OFFSET := 0x01000000
BOARD_KERNEL_IMAGE_NAME := Image.gz-dtb
BOARD_MKBOOTIMG_ARGS := --ramdisk_offset $(BOARD_RAMDISK_OFFSET) --tags_offset $(BOARD_KERNEL_TAGS_OFFSET)

TARGET_COMPILE_WITH_MSM_KERNEL := true
TARGET_KERNEL_ARCH := arm64
TARGET_KERNEL_CLANG_COMPILE := true
TARGET_KERNEL_HEADER_ARCH := arm64
TARGET_KERNEL_SOURCE := kernel/nubia/msm8998
```

其中`TARGET_KERNEL_SOURCE := kernel/nubia/msm8998`指定了内核源码的位置...  

把相应的内核，
[android_kernel_nubia_msm8998](https://github.com/LineageOS/android_kernel_nubia_msm8998).，
放进这里重新编译！

### 小结
1. Android Repository 仓库中，单独包的命名方式是，将`/`用下划线`_`替换，即该包在Android源码树中的位置。  

例如刚刚提到的，`android_kernel_nubia_msm8998` 对应的目录位置就是： `android/kernel/nubia/msm8998`  
或者`android_device_nubia_nx563j`，对应的位置应该是：`android/device/nubia/nx563j`

2. 每一个编译目录，都是有有自己特定的指定位置的

比如刚刚 Z17 Max 的 `device` 和 `kernel` 位置，是有代码明确指定了的，不可以随意更改。  
当然，`Android.mk`是无论在哪里都会被包含，但是特殊的依赖还是基于路径来的，不规范的位置很可能出错。

