---
layout: post
category : android
tags : [ndk]
---

## Download NDK

Here is the example in Linux.

	ndkroot=~/ndk   # change the default directory if necessary
	ndkver=10d
	ndk=$ndkroot/android-ndk-r$ndkver

	#
	# Install NDK
	# refer to https://developer.android.com/tools/sdk/ndk/index.html
	#
	ndk_install()
	{
		mkdir -p $ndk
		cd $ndk
		ndkbin=android-ndk-r$ndkver-linux-x86_64.bin
		wget http://dl.google.com/android/ndk/$ndkbin
		chmod a+x $ndkbin
		./$ndkbin

		export PATH=$PATH:$ndk/
	}

	#
	# build sample code to test it
	#
	ndk_test()
	{
		cd $ndk
		cd samples/hello-jni
		ndk-build
	}

## Build Applications with NDK

### Application with jni/Android.mk

For example, the directory is as bellow:

	samples/hello-jni/
	.
	├── AndroidManifest.xml
	├── default.properties
	├── jni
	│   ├── Android.mk
	│   ├── Application.mk
	│   └── hello-jni.c

Just run:

	ndk-build

Then, you can get the final results in
	./libs

### Application without jni directory

	app
	.
	├── Android.mk
	├── Application.mk
	└── main.c

Then need set NDK_PROJECT_PATH(for output) and NDK_MODULE_PATH(for Android.mk).
And can use -C to change the build directory first.

So, run as bellow:

	ndk-build -C path/to/app NDK_MODULE_PATH=Android.mk NDK_PROJECT_PATH=out

It will use path/to/app/Android.mk to build, and output to *out* directory.

Note: NDK_APPLICATION_MK can be used to specified the Application.mk too.

## NDK Standalone Toolchain

NDK Standalone Toolchain is for user to build applications as a pure gcc
toolchain.

It is built as bellow.

	cd ndk
	./build/tools/make-standalone-toolchain.sh \
			--toolchain=arm-linux-androideabi-4.9 \
			--llvm-version=3.5 \
			--platform=android-21 \
			--install-dir=/home/chenys/ndk/ndk-chenys/

The direcroty structure:

	tree -L 2
	.
	├── arm-linux-androideabi
	│   ├── bin
	│   └── lib
	├── bin
	│   ├── arm64-v8a
	│   ├── armeabi
	│   ├── armeabi-v7a
	│   ├── armeabi-v7a-hard
	│   ├── x86
	│   └── x86_64
	├── include
	│   ├── c++
	│   ├── gdb
	│   └── python2.7
	├── lib
	│   ├── clang
	│   ├── gcc
	│   └── python2.7
	├── lib64
	├── libexec
	│   └── gcc
	├── share
	│   └── gdb
	├── SOURCES
	└── sysroot
	    └── usr

## Use NDK to Simulate Android mm and mmm

put bellow scripts in build/envsetup.sh. And load it every time before start to build by

	. build/envsetup.sh

build/envsetup.sh

	TOP=`pwd`
	
	function hmm() {
		cat <<EOF
		Invoke ". build/envsetup.sh" from your shell to add the following functions to your environment:
		- mm:      Builds all of the modules in the current directory, but not their dependencies.
		- mmm:     Builds all of the modules in the supplied directories, but not their dependencies.

		Look at the source to view more functions. The complete list is:
		EOF
			local A
			A=""
			for i in `cat $TOP/build/envsetup.sh | sed -n "/^function /s/function \([a-z_]*\).*/\1/p" | sort`; do
				A="$A $i"
			done
			echo $A
	}
	
	function setpaths()
	{
		# setup ndk
		export ANDROID_NDK_PATH=$TOP/ndk/android-ndk-r10d/
		export ANDROID_NDK_TOOLCHAIN=$ANDROID_NDK_PATH/ndk-build
		export PATH=$PATH:$ANDROID_NDK_PATH
		# setup toolchain
		export ARM_EABI_TOOLCHAIN_PATH=$TOP/prebuilts/gcc/linux-x86/arm/arm-eabi-4.6/
		export PATH=$PATH:$ARM_EABI_TOOLCHAIN_PATH/bin
		export ARM_EABI_TOOLCHAIN=$ARM_EABI_TOOLCHAIN_PATH/bin/arm-ebi-
		# setup kernel
		export KDIR=$TOP/kernel/linux-3.10
		export ANDROID_PRODUCT_OUT=$TOP/out/
	}
	setpaths
	
	function mmm()
	{
		$ANDROID_NDK_TOOLCHAIN -C $1 APP_BUILD_SCRIPT=Android.mk NDK_PROJECT_PATH=$ANDROID_PRODUCT_OUT
	}
	
	function mm()
	{
		mmm .
	}

## Reference

[1] https://developer.android.com/tools/sdk/ndk/index.html
