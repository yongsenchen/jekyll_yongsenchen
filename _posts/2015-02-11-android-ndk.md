---
layout: post
Category : android
tags : [ndk]
---
{% include JB/setup %}

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

## Reference

[1] https://developer.android.com/tools/sdk/ndk/index.html
