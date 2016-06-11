# Postfix

## Overview

![http://classfiles.dennisk.fastmail.net/postfix_logo.jpg](http://classfiles.dennisk.fastmail.net/postfix_logo.jpg)

Postfix is a popular Mail Transfer Agent and is the default on RHEL and CentOS.

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:*

- Install and configure Postfix
- Dovecot for basic operation. (optional)
- Describe the functions of a MTA, MDA and MUA.
- Use a text-based mail client.
- Use Netcat to test Postfix.

## Terms You Should Know

- **MTA:** Mail Transfer Agent (sendmail, Sendmail, Postfix, Exim)
- **MDA:** Mail Delivery Agent (procmail)
- **MUA:**  Mail User Agent (Thunderbird, mutt, Sylpheed)
- **IMAP:** Internet Message Access Protocol Client connects to the IMAP server and the messages stay on the server.
- **POP:** Post Office Protocol Client downloads mail to host.
- **SMTP:** Simple Mail Transport Protocol
- **Mail Submission Port 587:** Alternate to port 25
- **mbox:** The mbox format stores mail in a single large file.
- **Maildir:** The Maildir format stores each email message as a separate file with a unique name. Messages are stored in a special Maildir directory structure.
- /var/log/maillog
- **/etc/postfix/main.cf:** The main configuration file for Postfix
- **/etc/aliases:** Email address aliases, an example would be mail to postmaster@example.com is routed to joeadmin@example.com. Run `newaliases` after making any changes to this file.
- **newaliases:** This command should be run after any changes to **/etc/aliases**.</dd>
- **/etc/dovecot/covecot.conf:** The main Dovecot configuration file.
- **postsuper:** The Postfix superintendent
- **mailq:** Command to print contents of mail queue to STDOUT.
- **mutt:** The Mutt Mail User Agent "All mail clients suck. This one just sucks less."
- **Reverse DNS lookup:** Used to check if the message was sent from a MTA with a legitimate **MX** record.
- **Open Relay:** In the distant past when life was good any MTA would gladly forward your email to its destination for you. No authentication was required.
- **SPAM:** SPAM is defined as… Well, I think you know already.
- **Dovecot:** IMAP and POP server
- **postconf:** Postfix utility
- **MX Record:** Mail exchange record

## Preparation

### Set Networking

In VirtualBox set Networking to *Bridged Adapter* for the SMTP virtual machines. 

Do this assignment on a CentOS 7 virtual machine connected to the 192.168.201.0/24 classroom network with the following software installed.

- nmap
- firewalld
- mutt
- nmap-ncat

These can be installed with a single `yum install` command.

If you are working from the BA lab the network will be 192.168.203.0/24. From home you will have to use the `ip addr show` command to make sure it's on your home network. This has not be tested.

### Set HOSTNAME on Server

CentOS 7 uses a Systemd utility to set a hostname using your first initial and last name. 

*Example for John Doe use:*

	# hostnamectl set-hostname jdoe.centos7
	
Reboot after making this change.

### Add User Accounts

Add an account for yourself.

## Install Postfix

Postfix will already be installed and running.

	# systemctl status postfix.service

## Configure Postfix

To set Postfix as an open relay on the local network here are the options that need to be changed in the *main.cf* file. Configuration settings starting with a **$** are variables that you will set. A good way to learn about Postfix's capabilities is the read the comments in */etc/postfix/main.cf*.

Be sure to backup the file first!

### INTERNET HOST AND DOMAIN NAMES

#### myhostname

Uncomment **myhostname** and replace *host.domain.tld* with the *hostname* of the server.

*Example:* jdoe.centos7.

#### mydomain

Uncomment **mydomain** and replace *domain.tld* with the domain of the mail server. 

### SENDING MAIL

#### myorigin

Uncomment **myorigin = $mydomain**

### RECEIVING MAIL

#### Interfaces

Uncomment **inet_interfaces = all**.
Comment out **inet_interfaces = localhost**

#### Destination

This line should already be uncommented.

	mydestination  =  $myhostname, localhost.$mydomain, localhost

### TRUST AND RELAY CONTROL

#### mynetworks

Uncomment **mynetworks_style = subnet**

Uncomment **mynetworks** and replace *168.100.189.0/24* with *192.168.201.0/24*.

Save changes to the file, check the configuration file and reload the configuration file using the `postfix` command.

	# postfix check
	# postfix reload

You can use `postconf -n` to display the configuration options.

Postfix will now accept mail for outside delivery.

<!--## Configure Dovecot (optional)

Dove does not require any changes to the configuration file but you should create a fresh set of keys for IMAPS.

1.  Move the default keys from */etc/pki/dovecot/certs/dovecot.pem* and */etc/pki/dovecot/private/dovecot.pem* to root's home directory. Rename the private does so it does not overwrite the cert.
2.  Run this script to generate a new private key and self-signed certificate.
3.  Restart the Dovecot service to make changes effective.-->

## Configure the Firewall

Open ports **25** (SMTP) on the firewall

	firewall-cmd --add-service smtp

Use Nmap to confirm a service is listening on that port.

	nmap localhost

## Add an Alias for Root Mail

Edit */etc/aliases* and redirect root mail to the user you created. Be sure to run the `newaliases` command for your change to take effect.

## Sending Email Directly to the Server (optional)

You can send an email directly to port 25 to test Postfix. Follow the Linux Journal article below – *Sending Email with Netcat.*

<!--## Troubleshoot the Assignment

- Are the needed ports open on the firewall? Use `iptables-save` to check.
- Typos or missing configuration options? Check with `postconf -n`.
- Was `newaliases` run after making changes?
- Was Postfix and Dovecot configuration files reloaded after making changes?
- You may need to manually configure a network interface.-->

## No Mail Spool for Root

If when you run `mutt` you get and error that the spool file for root doesn't exist you can create it with these commands.

	# touch /var/spool/mail/root
	# chmod 0660 /var/spool/mail/root

## What to Submit

This submission is in two parts.

1. Send an email from your SMTP server to dennis.kibbe@mesacc.edu
2. Submit a screenshot of the tail end of */var/log/maillog* showing the message was sent.

## Resources

- [Postfix Basic Configuration](http://www.postfix.org/BASIC_CONFIGURATION_README.html)
- [Mail Transport Agents](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-email-mta.html)
- [Securing Postfix](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Security_Guide/sect-Security_Guide-Server_Security-Securing_Postfix.html)
- [Quick Configuration](http://wiki2.dovecot.org/QuickConfiguration)
- [SMTP stage checks](https://www.fastmail.fm/help/spam_virus_protection_smtp_stage.html)
- [How to Use Telnet to Test SMTP Communication](http://technet.microsoft.com/en-us/library/aa995718%28v=exchg.65%29.aspx)
- [Verifying Which Ports Are Listening](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Security_Guide/sect-Security_Guide-Server_Security-Verifying_Which_Ports_Are_Listening.html)
- [Simple Mail Transport Protocol](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol)
- [Why is Comcast supporting port 465?](http://customer.comcast.com/help-and-support/internet/email-port-25-no-longer-supported/)
- [Sending Email with Netcat](http://www.linuxjournal.com/content/sending-email-netcat)
- /etc/services
- /usr/share/doc/postfix
- /usr/share/doc/dovcot
- [Dovecot](http://dovecot.org)
- [Setting the Hostname with hostnamectl](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/sec_Configuring_Host_Names_Using_hostnamectl.html)
- [What is the Difference Between POP and IMAP?](https://www.youtube.com/watch?v=MlvksPMunQ0)
- [What is SMTP](https://www.youtube.com/watch?v=tmE9OqjdK7s)