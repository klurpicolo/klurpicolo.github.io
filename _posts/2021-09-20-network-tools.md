---
layout: post
title:  "Network tools101"
date:   2021-09-20 19:00:00 +0700
categories: network
tags: [network]
---

# TCP/IP Model

|Layer|Example|
|-----|-------|
| Application layer | HTTP, SMTP, SSH |
| Transport layer | TCP, UCP |
| Internet layer | IP, ICMP |
| Network access layer | Ethernet |

# ping
The most basic command used for determine if able to reach destination and also latency. It bases on ICMP protocal.
- Ping able be disabled if destination disable ICMP protocal.

# telnet
Use for check the destination port
- Telnet able to used for identiy if destination port is opened.

# ipconfig/ifconfig
To get current network IP and the IP of gateway that we're connecting
```
Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::94c:63fe:66c8:2416%12
   IPv4 Address. . . . . . . . . . . : 194.168.182.210
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 194.168.182.1
```
- IPv4 Address : the current IP that get assigned by router
- Default Gateway : IP of router

# route table
Route table is the set of rules that used for determind the destination of data package on IP address
command : netstat -rn
```
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         10.244.1.1      0.0.0.0         UG        0 0          0 eth0
10.244.1.0      0.0.0.0         255.255.255.0   U         0 0          0 eth0
```

# ngrok
ngrok helps create reverse proxy and point to local pc and also give public IP temporary.
- Local development with webhook API(Line bot, Zoom chat)

# Advance network tools
- Zenmap (nmap GUI)
- Wireshark
