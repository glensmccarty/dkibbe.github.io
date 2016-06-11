# vsFTP - The Very Secure FTP Server

## Assignment Objectives

FTP or File Transfer Protocol is one of the oldest protocols used on the Net. Before there was Dropbox or Google Drive files were shared using the File Transfer Protocol

_After completing this assignment you will be able to:_

1.  Install the `vsFTPd` daemon (server)
2. Install the FTP client.
3.  Create virtual FTP accounts.
4.  Deny and allow specific users access to FTP.
5.  Add a login banner.
6.  Demonstrate how SELinux works to protect system files.

## Preparation

You will need two user accounts for this assignment.  Create an account for `tux` and `jstudent` on the CentOS 7 virtual machine.  Be sure to assign a simple password to each account so you can remember it.

You should also watch Thomas Cameron's [SELinux For Mere Mortals](https://www.youtube.com/watch?v=MxjenQ31b70).

## Terms You Should Know

- **FTP** - File Transfer Protocol
- `/usr/sbin/vsftpd` - The Very Secure FTP server
- `/etc/vsftpd/vsftpd.conf` - Main configuration file for `vsftp`.
- `/etc/vsftpd/ftpusers` - Lists users _not_ allowed to log into the FTP server.
- `/etc/vsftpd/userlist` - Either allow or deny users depending on `userlist_deny` in `vsftpd.conf`.
- `/var/ftp`- FTP working directory
- `/var/ftp/pub` - Directory for anonymous FTP access.
- `etc/services` - A plain  ASCII  text file  that provides a mapping between human-friendly textual names for internet services, and their  underlying assigned port numbers and protocol types.
- **MOTD** - Message of the Day
- Client/Server model
- **FileZilla** - Popular cross-platform FTP client.
- **SELinux** - Security Enhanced Linux

## How FTP works

### Active vs. Passive mode

#### Active Mode

1.  Client initiates data transfer to local unprivileged (greater than 1023) port.
2.  Server opens data connection from port 20 to client's selected port.

#### Passive Mode

1.  Client asks server to listen on an unprivileged port of the server's choice.  Server responses with the high port it's listening on.

## Using FTP

Open a terminal and type `ftp` to start an FTP session.

	$ ftp> open ftp.freebsd.org
	Connected to ftp.geo.freebsd.org.
	220 This is ftp0.nyi.freebsd.org - hosted at NYI.net.

You will be asked to login as *anonymous*. (No not that anonymous) There is no password but as a courtesy you could enter your email address.

Once logged in you can type `help` for a list of commands. Many shell commands like `ls` and `cd` work as you expect.

Change to the *pub* directory then the *FreeBSD* directory. Use *get* to fetch the *README.TXT* file to your local current directory. Type *exit* to close the connection.

## Install the Very Secure FTP server and FTP client

vsFTPd is in the CentOS official repository and can be installed using `yum`. The FTP client is not installed by default and can be installed at the same time as the server.

```
# yum install vsftpd ftp
```

### Starting the Service

The service must be started before it can be used.  CentOS 7 uses *systemd* so the commands are different that CentOS 6.

```
# systemctl start vsftpd.service
```
You can check if the server is running with this command.

```
# systemctl status vsftpd.service
```

To make sure the service starts on reboot.

```
# systemctl enable vsftpd
```

## Configure the Firewall

Use `yum install firewall.d` if needed than

```
# systemctl start firewalld.service
# systemctl enable firewalld.service
```

Next add the default port for FTP.

```
# firewall-cmd --add-service ftp
# firewall-cmd --list-services
``

You should see the service enable in the firewall.
```

## FTP Banner

First make a backup of the `vsftpd` main configuration file to root's home directory.

```
# cp /etc/vsftpd/vsftpd.conf ~/vsftpd.conf.bak
```
Find the section with the login banner string.

Create a new FTP banner warning users that all activity on the server is logged. If your banner has more than a single line you can point to a file containing the banner with this directive.

## Adding a File to the FTP Directory

Change to `/var/ftp' and create a new file.

``` 
# cd /var/ftp
# touch hello.txt
```

## Use FTP to access the file


Open a new virtual terminal by pressing the *host* key (right Ctrl plus F2)  and log in as user Tux. 

Start the FTP client and try to open a connection to *localhost* .
```
	# ftp
	ftp> open localhost
```

Login as user *anonymous* with no password. You can than type `help` to get a list of commands. Refer to the FTP beginner's guide under *Resources* below.

## Setting a Different Root Directory For anonymous Logins

The default login directory for *anonymous* user is `/var/ftp/`.  Next you'll change the default to `/var/ftp/pub/` by adding a new directive to the vsftpd configuration file.

1.  Add `anon_root=/var/ftp/pub` below the line that allows *anonymous* logins.
2.  Close the connection as *anonymous*.
3.  Place a file in `/var/ftp/pub`.
4. Open the connection again as *anonymous*.
4.  Use `ls` to show that you are in the directory containing your test file.  An *anonymous* user has no access to a higher directory.

## Disable anonymous Logins

Anonymous logins are allowed by default.  Next you'll disable anonymous logins.

1.  Change the line in the *vsftpd.conf* allowing anonymous logins from YES to NO.
2.  Restart the vsFTPd daemon.
3.  Try to login as *anonymous*.
4.  The login should fail.

## Root login

The `ftpusers` file lists accounts that are not permitted to use FTP.  The root user is included in this list.

1.  Try logging in as the root user.
2.  The login should fail and the attempt logged.

## Disable FTP for a User

Even if local users are allowed to use FTP you can blacklist a user by adding them to `ftpusers` or `userlist`. See the comments in these files to see which takes priority.


## SELinux

This part of the assignment will demonstrate how SELinux steps in to prevent vsFTP from serving a mislabeled file.

### Create Files

In root's home directory is a kickstart configuration file. First you will copy this file to two new files than copy and move the files to `/var/ftp/pub`

```
# ls 
anaconda-ks.cfg
# cp anaconda-ks.cfg anaconda-ks.cfg.copy
# cp anaconda-ks.cfg anaconda-ks.cfg.move
```
#### Check the SELinux Security Context

Use the `ls -Z` command to list the SELinux
```
# ls -Z anaconda*
```

All three files have the same security context - *admin_home_t*.

### Copy and Move the files

Use the `cp` command to *copy* `anaconda-ks.cfg.copy to `/var/ftp/pub`

```
#  cp anaconda-ks.cfg.copy /var/ftp/pub/
```
and the `mv` command to *move* `anaconda-ks.cfg.move` to `/var/ftp/pub`

```
# mv anaconda-ks.cfg.move /var/ftp/pub
```

#### Use FTP to list the files

Use the FTP client to login as *anonymous* and list the files in the pub directory. `anacond-ks-cfg.move` is missing.

#### Change the permissions

Use `chmod` to change the permissions on `anaconda-ks.cfg.move` to 066. Everyone should be able to read the files but they can't.

SELinux has stepped in to block vsFTP from serving the file because the security context is wrong. Use the following command to show that 
`anaconda-ks.cfg.move` has the wrong security context.
```
# cd /var/ftp/pub
ls -lZ
```

### Restoring the correct security context

Use `restorecon` restores the correct security context to all files based on the security context of the directory they are in.

```
# ls -ldZ /var/ftp/pub
```
shows that the correct security context for files in this directory is *public_content_t*.

```
# ls -lZ /var/ftp/pub/*
```
## SELinux

SELinux has stepped in to prevent vsFTP from serving a mis-configured file.

Run `getenforce` to show that SELinux is in *enforcing* mode. Next put SELinux in *permissive* mode.

```
# setenforce 0
```

Refresh the listing and `anaconda-ks.cfg.move` now shows up.

## Correcting a Mis-configured File

The most common problem is moving a file rather than copying a file.  Moved files retain the original security context.  Next you'll use SELinux tools to fix the problem.

### Restoring the Correct Security Contexts

The `restorecon` tool will restore the correct contexts for all files in a directory.

```
# restorecon -r /var/ftp/*
```

### Change the Security Context of a File

Another tool `chcon` can be used to manually configure the security contexts of a file.  You can use the **–reference=** option to copy the security contexts from another file.

## What to Submit

Submit a screenshot of `ls -lZ /var/ftp/pub/*` showing that each file has the correct security context.

## Resources

- [RHEL Deployment Guide](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/index.html)
- [CentOS Wiki page for SELinux](http://wiki.centos.org/HowTos/SELinux)
- [SELinux For Mere Mortals](https://www.youtube.com/watch?v=MxjenQ31b70)
- `man vsftpd` Man page for vsFTP daemon
- `man 5 vsftpd.conf` Man page for the `vsftp` configuration file
- [FTP for Beginners](http://www.webmonkey.com/2010/02/ftp_for_beginners/)

> Written with [StackEdit](https://stackedit.io/).