---
layout: post
category : linux
tags : [kernel, driver]
---
{% include JB/setup %}

## Generate Environment to Build Kernel Object

There is no necessary to build driver with full kernel source tree.

For example, in ubuntu, only bellow files are required:

	~$ ls /usr/src/linux-headers-3.13.0-32
	arch           drivers   init     kernel    net       sound   virt
	block          firmware  ipc      lib       samples   tools
	crypto         fs        Kbuild   Makefile  scripts   ubuntu
	Documentation  include   Kconfig  mm        security  usr

Most of it are header files.

But only kernel headers is not enough. For example, bellow way to generate headers can only be used for userspace.

	#cd to the top directory of the kernel source
	cd linux-3.9
	make mrproper
	make ARCH=arm integrator_defconfig
	make ARCH=arm headers_check
	make ARCH=arm INSTALL_HDR_PATH=path/to/install/headers headers_install

refer to [stackoverflow](http://stackoverflow.com/questions/11702960/how-to-generate-kernel-headers-of-a-toolchain-for-arm-integrator-target-machine)

Here is the document for how to build it.

[1] [How to Rebuild An Official Debian Kernel Package](https://wiki.debian.org/HowToRebuildAnOfficialDebianKernelPackage)

[2] [Driver Porting: compiling external modules](http://lwn.net/Articles/21823)

If need to do it by yourself, bellow scripts may help.

	# remove code in directory
	rmcode()
	{
		find $1 ! -path '*.git' -name '*.s' -delete
		find $1 ! -path '*.git' -name '*.S' -delete
		find $1 ! -path '*.git' -name '*.c' -delete
		find $1 ! -path '*.git' -name '*.cc' -delete
		find $1 ! -path '*.git' -name '*.cpp' -delete
		find $1 ! -path '*.git' -name Android.mk -delete
	}
	
	# release the kernel source
	release_kernel()
	{
		cd $src
		make clean ARCH=arm CROSS_COMPILE=arm-eabi-	# maybe can't clean
		cd $dst
		cp -rf $src $dst
		rmcode $dst
		cp -rf $src/scripts $dst/scripts  # scripts must be original
	}

TODO: can we clean it more? Or just do after upon stackoverflow scripts to generate headers?

## Build Kernel Object

Here is an example.

	.
	hello
	├── hello.c
	└── Makefile

hello.c

	#include <linux/module.h>
	#include <linux/kernel.h>

	static int __init hello_init(void)
	{
		printk(KERN_INFO "%s: hello\n", __func__);
		return 0;
	}

	static void __exit hello_exit(void)
	{
		printk(KERN_INFO "%s: bye\n", __func__);
	}

	MODULE_LICENSE("GPL v2");
	MODULE_AUTHOR("Yongsen Chen");
	MODULE_DESCRIPTION("Kernel Module Test Code");
	MODULE_VERSION("1.00");

	module_init(hello_init);
	module_exit(hello_exit);

Makefile

	CROSS_COMPILE ?= arm-eabi-
	ARCH ?= arm

	# if define KERNELRELEASE, then build from kernel
	ifneq ($(KERNELRELEASE),)
		obj-m += hello.o
	# else, it's called from current directory
	# must call -C to change the directory
	else
		KDIR ?= ../kernel/linux-3.10/

	default:
		$(MAKE) -C $(KDIR) M=$(CURDIR) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) modules

	clean:
		$(MAKE) -C $(KDIR) M=$(CURDIR) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) clean
	endif

Run make, then get the hello.ko.

You can inject it to target device to test it.
