# Create a Local DNS Caching Server

![A DNS query](http://static.ddmcdn.com/gif/dns-rev-1.gif)

## Overview

In this assignment your create a caching DNS nameserver using **dnsmasq**.

*Note:* Ubuntu uses **dnsmasq** by default.  Use a CentOS LiveCD, LiveUSB or virtual machine for this assignment.

After completing this assignment you will be able to:

1. Define the tern FQDN.
2. Describe how DNS works.
3. Configure **dnsmasq** for basic operation.
4. Use **dnsmasq** to "blacklist" a website.

## Install dnsmasq on CentOS

Check if **dnsmasq** is installed.

	$ rpm -q dnsmasq

If **dnsmasq** isn't installed on CentOS use this command to install it.

	# yum install dnsmasq

## Configuring dnsmasq

1. Backup */etc/dnsmasq.conf* and */etc/resolv.conf* before editing the files.
2. Edit */etc/resolv.conf* to add *127.0.0.1* as a nameserver before the other nameserver entries in the file. (Note: CentOS 7, use `nmtui`.
3. Comment out the default nameservers in */etc/resolv.conf* and add lines for the Google's Public DNS nameservers.
4. In *dnsmasq.conf* uncomment *listen-address=* and add 127.0.0.1 after the equal sign.
5. Save your changes and start **dnsmasq**.  You can ignore the message about not recognizing the host.  *Note:* If you make changes to the *dnsmasq.conf* restart **dnsmasq**.

	#systemctl restart dnsmasq.service

## Testing dnsmasq

1. You can use the **dig** command to test that **dnsmasq** is working.
2. Use **dig** to query a website and note how long it took.  Dig also tells you that the DNS server used is localhost. (Note: CentOS 7 install *bind-utils*.
3. Now query the website again and it should take a much shorter time.
4. On CentOS **dnsmasq** logs to */var/log/messages*

## Blacklisting a website (optional)

Search *dnsmasq.conf* for "doubleclick" and replace the name with another site such as slashdot.org.  Try connecting to the site.  The connection should fail.

## Troubleshooting the Assignment

+ Typos?
+ Was **dnsmasq** restarted?

## What to Submit

Copy and paste into the text submission box the last lines from */var/log/messages* that show **dnsmasq** reading *resolv.conf* and using the Google nameservers.

## Resources

+ [Debian Wiki](http://wiki.debian.org/HowTo/dnsmasq)
+ [DNS Explained](http://www.youtube.com/watch?v=72snZctFFtA)
+ [DNS Tutorial](http://www.vtc.com/products/DNS-tutorials.htm)
+ [Google Public DNS](https://developers.google.com/speed/public-dns/)
+ [dig How-To](http://www.madboa.com/geek/dig/)
+ [dig Web Interface](http://www.digwebinterface.com)
+ [Domain Name System (DNS) History](http://www.livinginternet.com/i/iw_dns_history.htm)


> Written with [StackEdit](https://stackedit.io/).