---
layout: post
category : android
tags : [android, environment]
---

# install oracal jdk 6/7/8 for ubuntu

1. download http://www.oracle.com/technetwork/java/javase/downloads/index.html
2. install it
```sh
tar -xvf jdk-6*
sudo mkdir -p /usr/lib/jvm
sudo mv jdk1.6.0_45 /usr/lib/jvm/oracle_jdk1.6.0_45
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/oracle_jdk1.6.0_45/bin/java" 1
sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/oracle_jdk1.6.0_45/bin/javac" 1
sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/lib/jvm/oracle_jdk1.6.0_45/bin/javaws" 1
sudo chmod a+x /usr/bin/java
sudo chmod a+x /usr/bin/javac
sudo chmod a+x /usr/bin/javaws
# sellect the new one
sudo update-alternatives --config java
sudo update-alternatives --config javac
sudo update-alternatives --config javaws
```

* http://askubuntu.com/questions/56104/how-can-i-install-sun-oracles-proprietary-java-jdk-6-7-8-or-jre
* http://askubuntu.com/questions/521145/how-to-install-oracle-java-on-ubuntu-14-04
* Oracle: https://blogs.oracle.com/roumen/entry/installing_sun_s_jdk_6
```
    You can find out where is java installed by running "which java".
    The version can be determined by running "java -version".
    To install Sun's JDK 6, switch to root and run "apt-get install sun-java6-jdk".
    You can also run sudo if you don't want to switch to root: "sudo apt-get install sun-java6-jdk".
    Proceed with the installation and confirm the license terms.
    Now you should get the correct message when running "java -version":
    java version "1.6.0"
    Java(TM) SE Runtime Environment (build 1.6.0-b105)
    Java HotSpot(TM) Client VM (build 1.6.0-b105, mixed mode, sharing)
```
* http://stackoverflow.com/questions/9918093/installing-sun-java6-jdk-on-ubuntu-10-04-64-bit-os
```
    you could install sun jdk for Ubuntu 10.04 in the same way as 10.10.
    The steps for installing java in 10.10 is described in http://java.dzone.com/articles/sun-java-6-ubuntu-1004-1010
    here's the steps of installing sun jdk, taken from that article:
    
    add-apt-repository ppa:sun-java-community-team/sun-java6
    apt-get update
    apt-get install sun-java6-jdk
    update-java-alternatives -s java-6-sun
    
    in case the repository mentioned above not available anymore, here is a manual-ish alternative in installing JDK:
    http://codingforme.wordpress.com/2012/05/14/installing-oracle-java-jdk-6-or-7-on-ubuntu-12-04/
```
