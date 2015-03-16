---
layout: post
category : android
tags : [android, makefile]
---

# Best Guide:
* http://www.ibm.com/developerworks/cn/opensource/os-cn-android-build/
* [Understanding of Android Build system](http://www.programering.com/a/MDN5EDNwATM.html)
* [深入浅出Android makefile](http://blog.csdn.net/memechashang/article/details/23428841)

# Add your applications into products

1. Need add it to PRODUCT_PACKAGES, otherwise it won't be built to final product.
2. Need define the application's Android.mk under TOP, so it can be scaned by build system.

If you don't want your application to be built into final product, then just remove it from PRODUCT_PACKAGES.

# Add Prebuilts

1. Use PRODUCT_COPY_FILES, "+= src:dst".
2. Use BUILD_PREBUILT
3. Use BUILD_MULTI_PREBUILT, only support known types.
4. use add-prebuilt-files. do as bellow: "$(call add-prebuilt-files, class, filename)"

   here, the class can be any of: ETC, APPS, EXECUTABLES, SHARED_LIBRARIES, STATIC_LIBRARIES

## BUILD_MULTI_PREBUILT

When use BUILD_MULTI_PREBUILT, multiple LOCAL_MODULE will be created, and each
module name is the basename of each LOCAL_SRC_FILES.

See build/core/multi_prebuilt.mk

Say

```makefile
LOCAL_PATH := $(call my-dir)

include $(CLEAR_VARS)
LOCAL_SRC_FILES := out/libA.so out/libB.so
LOCAL_MODULE_PATH := $(TARGET_OUT_VENDOR_SHARED_LIBRARIES)
include $(BUILD_MULTI_PREBUILT)
```

* http://www.phonesdevelopers.com/1724715/
