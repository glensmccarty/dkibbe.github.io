# Package Management with YUM & RPM

## Introduction

Yellowdog Updater Modified or YUM is the package management system for [Red Hat][redhat] based distributions such as [CentOS][centos], [Scientific Linux][scilinux] and [openSuSE][suse].
  
## Why a Package Management System
  
If you are used to Goggling for a software program and that downloading the *exe* file you may wonder why Linux is different. First, Software programs like [LibreOffice][soffice] are maintained by an upstream project often consisting of hundreds of volunteer that code and update the software. Each distribution downloads the latest source code, compiles the program for that that distribution and assures there are no bugs that prevents the program from running smoothly on that distro.
  
Once the software is compiled and tested the binary is digitally signed and placed in an online software repository from which the package management system can download and install.
  
Wherever possible you should only install software from a distribution's official repository or a reliable third-part repo. The advantages are:
  
1. The software has been compiled and tested to work well with that distro.
2. The required dependencies will be automatically downloaded as needed.
3. The package will have a digital signature assuring that it is authentic.
4. Security updates will be provided automatically.
5. Installation is easily done even from the command line.

## Learning Objectives

*When you have successfully completed this assignment you will be able to:*

1. Install a software package using `yum`.
 2. Remove a software package using `yum`.
3. Use `rpm` to obtain package information.
4. Use `rpm` to add a third-party repository to the system. (pending)
5. Check for package dependencies using `rpm`.

## Terms You Should Know

+ **yum**
+ **rpm**
+ **/etc/yum.repos.d**
+ **/etc/yum.conf**
+ **source code**
+ **object code**
+ **distro**
+ **software repository**
+ **mirror**
  
## Preparation

Do this assignment on the CentOS 7 virtual machine. Clear the Bash history before starting.
  
	$ history -c
    
You will need a command history to submit.
  
## RPM Package Naming
  
The RPM' package label uniquely identifies every installed package. The package label contains three pieces of information:

1. The name of the packaged software.
2. The version of the packaged software.
3. The package's release number.

Her are two examples:

	kernel-3.10.0-123.el7.x86_64.rpm
	bash-completion-2.1-6.el7.noarch.rpm
  
The bash-completion package can be installed on any architecture.

## YUM and RPM

Yum is the high-level tool for package installation and removal. Yum handles package updates as well.

### Check for Package Updates

Installing software requires root privileges. Since CentOS does not use `sudo by default the first` step is to become root. 

	$ su -
	# yum check-update
    
### Update the System

This command will update all installed packages.

	# yum update
    
## Using Yum to Search for a Software Package

You can search using `yum` without root privileges. Here we'll search for Zenmap which is a GUI for the Nmap network Scanner.
  
	$ yum search "Zenmap"
	nmap-frontend.noarch : The GTK+ front end for nmap..
    
### Get Information on a Package

Yum is used for finding more information on a package.

	# yum info nmap

### Install Software

Yum can download and install new software with Yum. Notice that you do not need the full package name.
  
	# yum install nmap-frontend
    
If Zenmap requires any dependencies `yum` will download them as well.

## Find the Version of Installed Software

Use the `rpm` command to see if a package is installed.

	$ rpmquery nmap
	nmap-1.2.1-1-fc20.x86_64
    
*Note:* See Backporting Security Fixes below.
  
### Check Dependencies
  
You can use `rpm` to check the dependencies of an installed package.
  
	$ rpm -qR <package-name>
    
### List All Installed Packages

This command will list all installed packages.

	$ rpm -qa
    
Pipe the command though `less` to view on screen at a time. 
  
	$ rpm -qa | less
    
Press the spacebar to move through the list one screen at a time. Type **q** to quit `less` and return to the prompt.
  
Pipe though `wc` to get a count of the number of installed packages.
  
	S rpm -qa | wc -l
  
### Remove a Software Package

Yum can remove a package as easily as it can install one.
  
	# yum remove nmap

### List all the Files in an Installed Package

	$ rpm -ql nmap

### Discover Which Package a File Belongs to

	$ rpm -qf /etc/passwd
	setup-2.8.71.2-2.fc20.noarch
    
### Verify a Package

This command will list any missing files or simply return to the prompt if there are no missing files.

	# rm /usr/share/doc/nmap/README
	# rpm -V nmap
	missing d /usr/share/doc/nmap/README

Verify all files
  
	# rpm -qaV

<!-- ## Debug the Assignment -->

<!--## XKCD-->

### Adding a Third Party Repository to CentOS

Search for htop.
  
	$ yum search htop
    
The package is not in the offical CentOS repositories. Not all distributions have the same software in their repositories. Debian has more packages over more architectures while CentOS and RHEL have a much narrower focus. So what if a program you want to install isn't in the official CentOS repositories? Are you out of luck? No, you can add a third party repo which has additional software built for CentOS.
  
There are times, however, when you may not want to change CentOS too much. See the link under Resources about CentOS Package Management.
  
#### Adding the EPEL Repository

A reliable third party repository for CentOS is [EPEL][epel] or Extra Packages for Enterprise Linux. EPEL packages are usually based on their Fedora counterparts and will never conflict with or replace packages in the base Enterprise Linux distributions.
  
Adding EPEL to CentOS is easy as the latest releases of CentOS include the EPEL setup package in the official CentOS repository.
  
	# yum search epel
	epel-release.noarch
	# yum install epel-release
    
The package installs a set of small configuration files in the *etc/yum.repos.d/* directory. The next time `yum update` is run the package names available from EPEL will be added to the local package database.

## What to Submit

Copy and paste the command history you saved.
  
	$ history > history.txt

## Resources

+ [Nmap -- The Network Scanner][nmap]
+ [Backporting Security Fixes][backport]
+ [Yum and RPM Tricks][tips]
+ [CentOS Package Management][package management]
+ [Available Repositories for CentOS][repos]
  
<!-- Links

This is [an example](http://example.com/ "Title") inline link.
This is [an example][id] reference-style link.
[id]: http://example.com/  "Optional Title Here"
-->

[redhat]: http://redhat.com "Red Hat"
[nmap]: http://nmap.org/ " Nmap - the network scanner"
[backport]: https://access.redhat.com/security/updates/backporting/ "Backporting Security Fixes"
[centos]: http://centos.org "CentOS"
[tips]: http://wiki.centos.org/TipsAndTricks/YumAndRPM "Yum and RPM Tricks"
[scilinux]: http://scientificlinux.org "Scientific Linux"
[suse]: http://opensuse.org "openSuSE"
[soffice]: http://libreoffice.org "LibreOffice"
[package management]: http://wiki.centos.org/PackageManagement "CentOS package management"
[repos]: http://wiki.centos.org/AdditionalResources/Repositories "Available Repositories for CentOS"
[epel]: https://fedoraproject.org/wiki/EPEL "Extra Packages for Enterprise Linux"
[deploy]: https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-yum.html "Red Hat deployment Guide: Yum"
[develworks]: http://www.ibm.com/developerworks/library/l-lpic1-v3-102-5/index.html "Learn Linux, 101: RPM and YUM package management"
[mirror]: https://s3.amazonaws.com/CIS126DL/Images/mirror_listing.jpg "Mirror listing"