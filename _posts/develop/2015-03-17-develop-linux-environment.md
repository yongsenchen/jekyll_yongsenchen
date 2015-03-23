---
layout: post
category : development
tags : [tools]
---

# Linux Tools

## Bash

* Bash Config: http://tldp.org/LDP/abs/html/sample-bashrc.html

## Screen
* User Guide: http://www.cnblogs.com/mchina/archive/2013/01/30/2880680.html
* Screen Configurations: http://www.snooda.com/read/268 or http://www.opstool.com/article/177 or http://vincentzhwg.iteye.com/blog/2021803
* 使用tmux替代screen: http://www.opstool.com/article/253

Common Commands:

    screen -dmS t   # create a screen
    screen -r       # restore a detached screen

can use bellow to simplify the flow.

    screen -R       # Reattach if possible, otherwise start a new session.

Split screen:
* C-a S         水平分割
* C-a |         vertical split
* C-a <tab>     switch windows
* C-a X         close current window
* C-a Q         close all other windows

## VI
* VI Configurations: https://github.com/ma6174/vim
* VIM config: https://code.google.com/p/jeffy-vim

## SHELL for Putty
* http://www.putty.org/
* Change color of blue to "0/0/187", and save.
  * another setting: http://blog.csdn.net/pan_tian/article/details/8111390
  * http://jimingsong.iteye.com/blog/1559012 or http://www.cnblogs.com/nayitian/archive/2013/01/18/2866690.html
* Putty connect to Android adb (not verified): http://blog.sina.com.cn/s/blog_4502d59c01018eus.html
