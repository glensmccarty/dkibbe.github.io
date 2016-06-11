# Fail2ban & Logwatch

Fail2ban and Logwatch are easy to configure utilities that increase security on services.

Fail2ban will block the IP address of failed login attempt and Logwatch will email you with a log summary of suspicious activity.

## Assignment Objectives

*After successfully completing this assignment you will be able to:*

- Install and configure fail2ban.
- Install and configure logwatch.

## Preparation

 - Set networking for the CentOS 7 virtual machine to bridged.
 - Take a snapshot of the virtual machine before starting.
 - Test IP address.

### Install EPEL

	# yum install epel-release

## Install Fail2ban

	# yum install fail2ban

After installation `rpm -qi fail2ban` will give you a description of the program.

## Firewalld

Install and enable firewalld if needed.

## Configuration

<!--### Filters and Actions

Fail2ban definds a number of filters..

	# ls /etc/fail2ban/filter.d/ | sed -e 's,\.config'-->

Copy *jail.conf* to *jail.local* or */etc/fail2ban/jail.d/customisation.local* and edit this file rather than the main config file.

### IP Addresses to Ignore

You can set IP addresses that will never be blocked by fail2ban.

	[DEFAULT]
	# "ignoreip" can be an IP address, a CIDR mask or a DNS host
	ignoreip = 127.0.0.1
	bantime  = 3600
	maxretry = 3

### Email

If you wish to be notified of bans by email, modify this line with your email address:

	destemail = your_email@domain.com

Then find the line:

	action = %(action_)s 

and change it to

	action = %(action_mw)s

### Jails

Jails are the rules which fail2ban apply to a given application/log. Here is an example for the SSH server.

	[ssh]

	enabled = true
	port    = ssh
	filter  = sshd
	logpath  = /var/log/auth.log
	maxretry = 3
	
### Logging

	Fail2ban writes to /var/log/fail2ban.

## Start and Enable fail2ban


	# systemctl start fail2ban
	# systemctl enable fail2ban

## fail2ban-client

You can use the `fail2ban-client` utility to monitor bans.

	# fail2ban-client status sshd

## Logwatch

Logwatch monitors logs for "interesting" activity. Logwatch can be configured to email you each day or you can access it directly.

	# logwatch --service sshd --range=Today

## What to Submit

Sumit a screenshot of a log entry showing that Fail2ban blocked an IP address.

## Resources

- [fail2ban](http://lintut.com/install-fail2ban-on-centos-7/)
- [Fail2ban at pycon 2014](https://www.youtube.com/watch?v=xcXheAWy7cU#t=190)
- man 5 jail.conf
- [Linux Magazine: Logwatch](http://www.linux-mag.com/id/7800/)



> Written with [StackEdit](https://stackedit.io/).