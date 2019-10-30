---
layout: post
title: Phoenix Contact Automationworx
date: 2019-10-30
excerpt: "."
tags: [exploit]
comments: false
---
## Config+ 1.60.2519
looking at CVE-2019-16675. invalid pointer read in 'Topology.dll'
```
(c4c.e18): Access violation - code c0000005 (!!! second chance !!!)
eax=57400000 ebx=00000000 ecx=002c8ef0 edx=00001d1a esi=002c8ef0 edi=00000000
eip=0265a26c esp=0012e82c ebp=0012e8f4 iopl=0         nv up ei pl nz na pe nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00010206
Topology!DllRegisterServer+0x345dc:
0265a26c 8b4810          mov     ecx,dword ptr [eax+10h] ds:0023:57400010=????????
```
[trigger](https://github.com/ceballosm/scratchpad/blob/master/CVE-2019-16675.bcp)
