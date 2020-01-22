---
layout: post
title: WECON LeviStudioU
date: 2020-01-22
excerpt: "."
tags: [exploit]
comments: false
---
## WECON LeviStudioU ShortMessage_Module SMtext Stack-based Buffer Overflow
[ZDI-19-764](https://www.zerodayinitiative.com/advisories/ZDI-19-764/). issue
with the xmlparser.
```
(4e0.c58): Access violation - code c0000005 (!!! second chance !!!)
eax=00125964 ebx=001201dc ecx=8d8d0cc4 edx=8d8d0cc4 esi=00000110 edi=00000000
eip=10004b49 esp=00125948 ebp=0012594c iopl=0         nv up ei ng nz na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00010282
*** ERROR: Symbol file could not be found.  Defaulted to export symbols for C:\Program Files\LeviStudioU\XMLParser.dll - 
XMLParser!CXMLDocument::SaveXmlFile+0x1589:
10004b49 8b12            mov     edx,dword ptr [edx]  ds:0023:8d8d0cc4=????????
*** ERROR: Symbol file could not be found.  Defaulted to export symbols for C:\Program Files\LeviStudioU\ShortMessage_Module.exe - 
0:000> !exchain
00127a5c: ShortMessage_Module!CSVParser::IsEOF+ce51 (00410041)
Invalid exception stack at 00410041
0:000> kv
ChildEBP RetAddr  Args to Child              
WARNING: Stack unwind information not available. Following frames may be wrong.
0012594c 10004d19 00125964 00125980 10001198 XMLParser!CXMLDocument::SaveXmlFile+0x1589
00125958 10001198 00410045 8d8d0cc4 0041e930 XMLParser!CXMLDocument::SaveXmlFile+0x1759
00125980 004122c6 00125a2c 0041e930 9b44daef XMLParser!CXMLDocument::GetAttrib+0x28
00127a68 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xf0d6
00127a6c 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a70 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a74 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a78 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a7c 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a80 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a84 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a88 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a8c 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a90 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a94 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a98 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127a9c 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127aa0 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127aa4 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
00127aa8 00410041 00410041 00410041 00410041 ShortMessage_Module!CSVParser::IsEOF+0xce51
```
[WECON-ZDI-19-764.tar.gz](https://github.com/ceballosm/scratchpad/blob/master/WECON-ZDI-19-764.tar.gz)
