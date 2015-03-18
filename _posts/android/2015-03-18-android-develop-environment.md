---
layout: post
category : android
tags : [android, environment]
---

# install oracal jdk 6/7/8 for ubuntu

* http://askubuntu.com/questions/56104/how-can-i-install-sun-oracles-proprietary-java-jdk-6-7-8-or-jre
* http://askubuntu.com/questions/521145/how-to-install-oracle-java-on-ubuntu-14-04
* Oracle: https://blogs.oracle.com/roumen/entry/installing_sun_s_jdk_6
    ```
    You can find out where is java installed by running "which java".
    The version can be determined by running "java -version".
    To install Sun's JDK 6, switch to root and run "apt-get install sun-java6-jdk". You can also run sudo if you don't want to switch to root: "sudo apt-get install sun-java6-jdk".
    Proceed with the installation and confirm the license terms.
    Now you should get the correct message when running "java -version":
    java version "1.6.0"
    Java(TM) SE Runtime Environment (build 1.6.0-b105)
    Java HotSpot(TM) Client VM (build 1.6.0-b105, mixed mode, sharing)
    ```
