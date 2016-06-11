# Bringing Up eth0 on Boot

##  Assignment Objectives

Until now you have been manually starting networking with `ifup eth0`.  Now you will set eth0 to come on line when the computer boots up.

_After you successfully complete this assignment you will be able to:_

1. Make _eth0_ active with the `ip` command.
2. Manually start DCHP with `dhclient`.
3. Edit the _/etc/sysconfig/network-scripts/ifcfg-eth0_ script to start _eth0_ on boot.

## Terms and Commands You Should Know

+ __DHCP:__ Dynamic Host Configuration Protocol
+ __ip:__ Replaces `ifconfig` for managing network card.
+ __iw:__ Replaces `iwconfig` for managing wireless network cards.
+ __dhclient:__ Dynamic Host Configuration Protocol Client
+ __eth0:__ First NIC (Network Interface Card)
+ __wlan0:__ First wireless card
+ __NetworkManager:__ The dynamic daemon that maintains a network connection.
+ __/etc/hosts:__ Static table lookup for hostnames
+__/etc/resolv.conf:__ Resolver configuration file
+ __/etc/hostname:__ Contains the hostname of the computer.
+ __hostname:__ Display the hostname of the computer
+ __/etc/sysconfig/network:__ Routing and host information for all interfaces
+ __/etc/sysconfig/network-scripts/ifcfg-interface-name:__ Network configuration file for the named network device.

## Preparation

Do this lab on the CentOS virtual machine.  If _eth0_ is up bring it down with `ifdown eth0`.

## Bringing up eth0 manually.

There are two steps to bringing up _eth0_ manually.

	# ip link set eth0 up
	# dhclient -v eth0
	
 The first command makes the _eth0_ active and the second requests an IP address from the DHCP server.

<pre>
# ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 1000
    link/ether 00:0c:29:28:fd:4c brd ff:ff:ff:ff:ff:ff
    inet 192.168.201.27/24 brd 192.168.201.255 scope global eth0
    inet6 fe80::20c:29ff:fe28:fd4c/64 scope link
       valid_lft forever preferred_lft forever
</pre>

## Setting eth0 to Come Up on Boot

Each interface has a configuration file in the _/etc/sysconfig/network-scripts_ directory.  Here is the configuration file for _eth0_.

<pre>
DEVICE="eth0"
BOOTPROTO=static
ONBOOT=no
TYPE="Ethernet"
IPADDR=192.168.50.2
NAME="System eth0"
HWADDR=00:0C:29:28:FD:4C
GATEWAY=192.168.50.1
</pre>

To enable _eth0_ on boot change __ONBOOT=no__ to _yes_.  On the next boot _eth0_ will be the active interface.

## What to Submit

Submit a cropped screenshot of the the _eth0_ configuration file showing the change you made.

## Resources

+ [Red Hat Documentation][]

[Red Hat Documentation]:https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/part-Networking.html "networking" 
