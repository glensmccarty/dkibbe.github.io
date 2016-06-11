# Samba


![Samba server](http://classfiles.dennisk.fastmail.net/samba.png)

## Overview

Samba provides secure, stable and fast file and print services for Linux and Windows clients using the SMB/CIFS protocol.

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:* 

- Configure a Samba server on CentOS &
- Configure SELinux to work with Samba
- Connect to the Samba server from a Windows workstation.

## Terms You Should Know

/etc/samba/smb.conf
: The Samba configuration file.

smb
: Server Message Block daemon

nmb
: NetBIOS Message Block daemon

## Preparation

Use a CentOS7 virtual Machine on the 192.168.201.0/24 network.

Take a [snapshot](https://www.virtualbox.org/manual/ch01.html#snapshots) in VirtualBox so you can roll back if you have problems.

## Install Samba

	# yum install samba samba-commons samba-client cups-libs cifs-utils policycoreutils-python

## Create directory to share

	# mkdir -p /srv/smb/data

Add a file SUCCESS to the directory.

### Add Samba Group

	# groupadd staff

### Set Permissions and Owership

	# chgrp -R staff /srv/smb/data
	# chmod 0755 /srv/smb/data

### Set Security

	# chcon -R -t samba_share_t /srv/smb/data
	# semanage fcontext -a -t samba_share_t /srv/smb/data
	# setsebool -P samba_enable_home_dirs on

## Add User

If you haven't done so already add a user.

	# useradd tux
	# passwd tux

### Add to Samba Group

	# usermod -aG staff tux
	# smbpasswd -a tux

## Configure Samba

### The Comment Characters

*Samba configuration file uses two types of comments.*

(hash) #
: Comments and text

(semicolon) ;
: Options

*Be sure to uncomment options that you change.*

### Interfaces and Hosts [global]

	interfaces = lo eth0 192.168.201.0/24
	hosts allow = 127. 192.168.201.

*Make sure the interface you enter is your active interface!*

### Public Share [public]

At the bottom of `/etc/samba/smb.conf`edit and uncomment the appropriete lines in [public]

## Testing the Configuration

Use `testparm` to check the configuration. 

## Start Samba

	# systemctl start smb.service
	# systemctl start nmb.service

## Enable Samba On Boot

	# systemctl enable smb.service
	# systemctl enable nmb.service

## NetBIOS Ports

Should already be there.

	# grep netbios /etc/services

## Firewall

	# firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="192.168.201.0/24" service name="samba" log prefix="samba" level="info" limit value="1/m" accept'
	
	# firewall-cmd --add-service=samba

	# firewall-cmd --reload

## Connect from Windoze

From the Windows Run Dialog box connect to the Samba server.

	\\192.168.201.123\srv\smb\data

## Connect from Linux

	$ smbclient -L \\192.168.201.123 -U tux

	$ smbclient \\192.168.201.123 -U tux

## Mount Samba Directory

	# mount -cifs //192.168.201.123/srv/smb/data -o username=tux /mnt/

## From Ubuntu

Click Dash and type ` smb://192.168.201.123/`

## What to Submit

Submit a screenshot of the Windows or Linux accessing the Samba server.

## Resources

- [Red Hat Deployment Guide](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-File_and_Print_Servers.html#s1-Samba)
- Samba Documentation
- man (5) smb.conf
- [Samba Website](http://samba.org)
- [Latest version of this assignment](https://dkibbe.github.io/cis240dl_samba.html)

> Written with [StackEdit](https://stackedit.io/).<!--se_discussion_list:{"u39tFcc7WOkbRkYt79DXWPlT":{"selectionStart":2547,"selectionEnd":2567,"commentList":[{"content":"net config workstation"},{"content":"Try mapping the share from Command Prompt using;\nnet use * \\\\servernameorIP\\sharename /user:SMBUser 'Password'\nThis will force the share to be mapped by authenticating the user account you created using smbpasswd"}],"discussionIndex":"u39tFcc7WOkbRkYt79DXWPlT"},"mcMeTqPjDN8XRJciGo6TIIos":{"selectionStart":2292,"selectionEnd":2300,"commentList":[{"content":"firewall-cmd --permanent --zone=public --add-service=samba"}],"discussionIndex":"mcMeTqPjDN8XRJciGo6TIIos"}}-->