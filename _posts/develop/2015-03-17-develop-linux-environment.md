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

## SHELL for Putty

