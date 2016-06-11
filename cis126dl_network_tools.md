# Basic Network Tools

## Introduction

Here are a few basic command line tools for working with networks.

## Terms You Should Know

ARP
: Address Resolution Protocol

DCHP
: Dynamic Host Configuration Protocol

DNS
: Domain Name System

Host
: Any device on a network.

ICMP
:  Internet Control Message Protocol

Interface
: A device such as a network card for connecting to a network.

IPv4

:  Internet Protocol version 4

IPv6
: Internet Protocol version 8

RJ45

: Ethernet cable jack/plug

## Network Tools

### host (dig)

#### dig

`host` and `dig` are used  find the IP address of a host.

```
$ dig sdf.org

; <<>> DiG 9.9.5-3ubuntu0.7-Ubuntu <<>> sdf.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 53188
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4000
;; QUESTION SECTION:
;sdf.org.			IN	A

;; ANSWER SECTION:
sdf.org.		31304	IN	A	192.94.73.15

;; Query time: 3 msec
;; SERVER: 127.0.1.1#53(127.0.1.1)
;; WHEN: Mon Mar 07 11:11:54 MST 2016
;; MSG SIZE  rcvd: 52

```

#### host

```
$ host mesacc.edu
mesacc.edu has address 140.198.64.99
mesacc.edu mail is handled by 5 alt1.aspmx.l.google.com.
mesacc.edu mail is handled by 5 alt2.aspmx.l.google.com.
mesacc.edu mail is handled by 10 alt3.aspmx.l.google.com.
mesacc.edu mail is handled by 10 alt4.aspmx.l.google.com.
mesacc.edu mail is handled by 1 aspmx.l.google.com.
```

### ip (ifconfig)

Used  to display and configure interface information. `ifconfig` is replaced by `ip`.

```
$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether c4:8e:8f:f4:d9:8d brd ff:ff:ff:ff:ff:ff
    inet 10.12.56.117/23 brd 10.12.57.255 scope global wlan0
       valid_lft forever preferred_lft forever
    inet6 fe80::c68e:8fff:fef4:d98d/64 scope link 
       valid_lft forever preferred_lft forever

```

### netstat

Useful for displaying network connections.

```
$ netstat -ptln
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.1:56368         0.0.0.0:*               LISTEN      9565/cli        
tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN      -               
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      -               
tcp6       0      0 ::1:631                 :::*                    LISTEN      
```

### nmap

Used to map a network. ***Warning:*** Not to be used on a network you don't control.

```
$ nmap localhost

Starting Nmap 6.40 ( http://nmap.org ) at 2016-03-07 11:24 MST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00014s latency).
Not shown: 999 closed ports
PORT    STATE SERVICE
631/tcp open  ipp

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds
```

### ping

Used to test connectivity.

```
$ ping -c4 mesacc.edu 
PING mesacc.edu (140.198.64.99) 56(84) bytes of data.
64 bytes from 140.198.64.99: icmp_seq=1 ttl=63 time=2.65 ms
64 bytes from 140.198.64.99: icmp_seq=2 ttl=63 time=5.50 ms
64 bytes from 140.198.64.99: icmp_seq=3 ttl=63 time=2.27 ms
64 bytes from 140.198.64.99: icmp_seq=4 ttl=63 time=5.14 ms

--- mesacc.edu ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 2.275/3.893/5.503/1.443 ms

```

### route

Display routing information.

```
$ route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         10.12.56.1      0.0.0.0         UG    0      0        0 wlan0
10.12.56.0      *               255.255.254.0   U     9      0        0 wlan0

````

### tracepath

Trace the path to a host.

```
$ tracepath dw.de
 1?: [LOCALHOST]                                         pmtu 1500
 1:  10.12.56.1                                            2.989ms 
 1:  10.12.56.1                                            2.049ms 
 2:  172.16.30.1                                          11.094ms 
 3:  172.16.50.22                                         50.516ms 
 4:  172.16.50.116                                        20.470ms 
 5:  172.16.70.35                                         27.540ms 
 6:  wsip-66-210-249-73.ph.ph.cox.net                     35.239ms 
 7:  wsip-184-178-203-181.ph.ph.cox.net                   16.482ms asymm 10 
 8:  chndcorc03-te-0-0-0-2.ph.ph.cox.net                  15.686ms 
 9:  ae57.bar2.phoenix1.level3.net                        41.555ms asymm 12 
10:  ae-1-60.edge5.frankfurt1.level3.net                 168.544ms asymm 20 
11:  ae-1-60.edge5.frankfurt1.level3.net                 167.341ms asymm 21 
12:  195.16.161.46                                       162.389ms asymm 16 
13:  core-sto2-po9.netcologne.de                         169.944ms asymm 14 
14:  rtkds-sto-po2.netcologne.de                         162.342ms asymm 16 
15:  78.35.29.134                                        168.384ms asymm 16 
16:  194.55.30.1                                         173.287ms asymm 18 
17:  no reply
18:  no reply
```

### Wireshark

GUI tool for examining network packets.

## Resources

 - [Network Troubleshooting at the Command Line](https://www.youtube.com/watch?v=-55X-koiBFg)

[Wireshark](http://wireshark.org)

> Written with [StackEdit](https://stackedit.io/).