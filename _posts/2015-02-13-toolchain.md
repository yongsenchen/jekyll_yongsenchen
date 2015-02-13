---
layout: post
category : toolchain
tags : [gcc]
---
{% include JB/setup %}

This page collect the trouble shooting on toolchain.

## GCC Toolchains

There are several gcc toolchain releases, including (suppose little endian, softfloat)

Vendor  | Machine Word | Bare Matel     | Linux Userspace        | Link
--------|--------------|----------------|------------------------|-------------------------------------------------------------
Linaro  | 32           | arm-none-eabi- | arm-linux-gnueabi-     | <http://releases.linaro.org/latest/components/toolchain/binaries>
Android | 32           | arm-eabi-      | arm-linux-androideabi- | <https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/arm/arm-eabi-4.8/>
