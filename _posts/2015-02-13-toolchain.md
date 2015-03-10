---
layout: post
category : toolchain
tags : [gcc]
---

This page collect the trouble shooting on toolchain.

## GCC Toolchains

There are several gcc toolchain releases, including (suppose little endian, softfloat)

| Vendor  | Machine Word | Bare Metal     | Linux Userspace        | Link
|---------|--------------|----------------|------------------------|----------------------------------------------------
| Linaro  | 32           | arm-none-eabi- | arm-linux-gnueabi-     | <http://releases.linaro.org/latest/components/toolchain/binaries>
| Android | 32           | arm-eabi-      | arm-linux-androideabi- | <https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/arm/arm-eabi-4.8/>

Note 1: Bare Metal toolchain is for some tools without libc, say bootloader, firmware.

Note 2: for Linaro's toolchain, if the code isn't written in good way, it would get problem.

Wrong Way:

```c
void foo(void)
{
	uint8_t data8[32] = {0};	/* won't enforce data8[] to start as machine word
					 * aligned, so it may start as 0x00001003 */
	uint32_t *p32 = (void *)data8;	/* error: can't do in this way, it may get data
					 * abort due to alignment issue */
	*p32 = 10;			/* warning: this may get data abort!!!
					 * happens on linaro bare-metal toolchain */
}
```

Right Way:

```c
void foo(void)
{
	uint32_t data32[8] = {0};	/* declear it as 32-bit types */
	uint32_t *p32 = data32;
	*p32 = 10;
}
```
