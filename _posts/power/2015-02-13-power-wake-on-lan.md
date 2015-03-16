---
layout: post
category : power
tags : [network, wol]
---

Wake on Lan (WoL) can work in bellow ways:

- Network: <http://www.wakeonlan.me/>
- Windows:
  - Guide: <http://windows7-issues.blogspot.com/2011/03/wake-on-lan-wol-for-windows-7-made-easy.html>
  - Tool: <http://www.matcode.com/wol.htm>
  - Command: `mc-wol.exe 00:32:53:99:25:4a`
- Ubuntu:
  - Command: `etherwake -i eth0 00:32:53:99:25:4a`
