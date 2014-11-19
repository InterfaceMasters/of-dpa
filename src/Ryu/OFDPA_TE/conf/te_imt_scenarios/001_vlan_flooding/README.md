Scenario Overview
=================
The purpose of this scenario is to show vlan flooding functionality implemented thru OF-DPA.

Topology
========
Interface Masters Technologies switch n2948-6xl connected to traffic generator/capturer.
In our case we use two n2948-6xl, on traffic side we run Broadcom diagnostic shell that allows to
send/receive traffic.

+-----------+ xe0    xe24 +-----------+
| n2948-6xl +-------------+ n2948-6xl |
|  of-dpa   | xe1    xe25 |    SDK    |
|           +-------------+ (traffic) |
|           | xe2    xe26 |           |
|           +-------------+           |
+-----------+             +-----------+

Description
===========
Once RYU script is executed and install rules to OF-DPA switch you can send traffic from one port
and see copies on the other two.

Run on traffic bcm shell:

    BCM.0> pw start
    BCM.0> vlan add 1 PortBitMap=cpu
    BCM.0> tx 1 PortBitMap=xe26 VLantag=1
    BCM.0> [bcmPW.0]
    [bcmPW.0]Packet[31]: data[0000]: {000101010103} {000101010101} 8100 0001
    [bcmPW.0]Packet[31]: data[0010]: ea9c 0000 0000 0000 0000 1234 5bad 1234 
    [bcmPW.0]Packet[31]: data[0020]: 5bae 1234 5baf 1234 5bb0 1234 5bb1 1234 
    [bcmPW.0]Packet[31]: data[0030]: 5bb2 1234 5bb3 1234 5bb4 1234 5bb5 1234 
    [bcmPW.0]Packet[31]: data[0040]: 5bb6 1234 5bb7 1234 5bb8 1234 5bb9 1234 
    [bcmPW.0]Packet[31]: data[0050]: 5bba 1234 5bbb 1234 5bbc 1234 5bbd 1234 
    [bcmPW.0]Packet[31]: data[0060]: 5bbe 1234 5bbf 1234 5bc0 1234 5bc1 1234 
    [bcmPW.0]Packet[31]: data[0070]: 5bc2 1234 5bc3 1234 5bc4 1234 5bc5 1234 
    [bcmPW.0]Packet[31]: data[0080]: 5bc6 1234 5bc7 1234 5bc8 1234 5bc9 1234 
    [bcmPW.0]Packet[31]: data[0090]: 5bca 1234 5bcb 1234 5bfb d21b 87
    [bcmPW.0]Packet[31]: length 157 (157). rx-port 26. cos 0. prio_int 0. vlan 1. reason 0x0. Outer tagged.
    [bcmPW.0]Packet[31]: dest-port 1. dest-mod 0. src-port 26. src-mod 0. opcode 2.  matched 0. classification-tag 0.
    [bcmPW.0]
    [bcmPW.0]Packet[32]: data[0000]: {000101010103} {000101010101} 8100 0001
    [bcmPW.0]Packet[32]: data[0010]: ea9c 0000 0000 0000 0000 1234 5bad 1234 
    [bcmPW.0]Packet[32]: data[0020]: 5bae 1234 5baf 1234 5bb0 1234 5bb1 1234 
    [bcmPW.0]Packet[32]: data[0030]: 5bb2 1234 5bb3 1234 5bb4 1234 5bb5 1234 
    [bcmPW.0]Packet[32]: data[0040]: 5bb6 1234 5bb7 1234 5bb8 1234 5bb9 1234 
    [bcmPW.0]Packet[32]: data[0050]: 5bba 1234 5bbb 1234 5bbc 1234 5bbd 1234 
    [bcmPW.0]Packet[32]: data[0060]: 5bbe 1234 5bbf 1234 5bc0 1234 5bc1 1234 
    [bcmPW.0]Packet[32]: data[0070]: 5bc2 1234 5bc3 1234 5bc4 1234 5bc5 1234 
    [bcmPW.0]Packet[32]: data[0080]: 5bc6 1234 5bc7 1234 5bc8 1234 5bc9 1234 
    [bcmPW.0]Packet[32]: data[0090]: 5bca 1234 5bcb 1234 5bfb d21b 87
    [bcmPW.0]Packet[32]: length 157 (157). rx-port 25. cos 0. prio_int 0. vlan 1. reason 0x0. Outer tagged.
    [bcmPW.0]Packet[32]: dest-port 1. dest-mod 0. src-port 25. src-mod 0. opcode 2.  matched 0. classification-tag 0.
    BCM.0>
