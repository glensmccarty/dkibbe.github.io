# The Apache Web Server on Ubuntu 14.04 LTS
![Apache on Ubuntu](http://rtfq.net/wp-content/uploads/2012/01/apache-ubuntu1.png)

## Overview

Installing Apache on Ubuntu is different than the installation on CentOS.  The package name is different.  Configuration files are different as well. 

## Terms You Should Know

- **LAMP:** Linux, Apache, MySQL and PHP
- **tasksel:** A user interface for installing tasks such as a LAMP server.
- **aptitude:** High-level interface to the package manager *dpkg*.
- **/usr/share/doc/apache2:** Contains sample configuration files and READMEs *Note:* This directory should be one of the first places to look for additional documentation about a package.
- **a2ensite:** Created the symlink in */etc/apache2/sites-enabled*

## Preparation

Use bridged networking in VirtualBox so you can access Apache from Windows.

## Tasksel

![Ubuntu tasksel](http://dennisk.freeshell.org/img/ubuntu_tasksel.png)

**tasksel** is a Debian tool for installing services that require multiple packages similar to **yum groupinstall.**  When you first install Ubuntu Server it will offer to install a LAMP server.  You can run **tasksel** later to install any services such as a mail server or OpenSSH server.

Since we don't need all the features of a LAMP (Linux, Apache, MySQL, PHP) server for this assignment you will just install Apache2.

## Installing Apache2

For this assignment you'll just install the Apache2 web server.  You can use the search option to *aptitude* to find the Apache2 metapackage.  If Aptitude isn't installed you can use the same commands with *apt-get.*

	$ sudo apt-get install aptitude

Here we'll pipe the search through the `head` command since it's a very long list.

	$ sudo aptitude search apache | head
	p apache2  - Apache HTTP Server metapackage

This command installs both the Apache2 and Elink packages at the same time.

	$ sudo aptitude install apache2 elinks

Did you notice that Apache was already up and running?  You still need to configure the firewall which is disabled by default.

## The ufw Firewall Tool

Ubuntu comes with **ufw** which is a very friendly and intuitive command line tool for configuring the Linux firewall.  You can type **ufw help** for a list of options.

The firewall is disabled by default.  You should enable it and allow traffic to port 80 for the main site and port 8080 for the virtual host.

Current status of the firewall.

 sudo ufw status
tatus: inactive

Open port 80 for web traffic.

	$ sudo ufw allow http
	Rule added
	Rule added (v6)

Open port 8080

	$ sudo ufw allow 8080
	Rule added
	Rule added (v6)

New status of the firewall

	$ sudo ufw status verbose
	Status: active
	Logging: on (low)
	Default: deny (incoming), allow (outgoing)
	New profile: skip
 
To | Action | From
---|---|---
80 | ALLOW IN | Anywhere
80 | ALLOW IN | Anywhere (v6)
8080 | ALLOW IN | Anywhere
8080 | ALLOW IN | Anywhere (v6)

## Apache Configuration Files

On Ubuntu the Apache2 configuration files are in */etc/apache2* and are split between several files. see [this page](https://help.ubuntu.com/12.04/serverguide/httpd.html#http-configuration) for what each file does.

## Creating an IP-Based Virtual Hosts

Since we can't use domain names in Firefox to identify our virtual host because there are no DNS records for them we will set up IP address-based hosts on ports 80 and  8080.

On Ubuntu virtual hosts are placed in the *sites-available* directory and then sym-linked to the *sites-enabled* directory to make them active. Ubuntu (Debian) provides `a2ensite` to make this easier.

See the last lines in */etc/apache2/apache2.conf* for more information.  Especially the *README.Debian* file in */usr/share/doc/apache2.*

You can copy the default virtual host file to use as template for the new virtual host. Give the new file the name *001-staff.example.conf.*

The *Listen 8080* is placed in *ports.conf.*

The files in */etc/apache2/sites-available* need to be linked to */etc/apache2/sites-enabled*. The `a2ensite` command makes that easy.

As in CentOS you need to create the DocumentRoot directories and create an *index.html* file in each.  Create  */var/www/example.com/* and */var/www/staff.example.com/*. Place a unique *index.html* file there.

Don't forget to restart Apache.

	$ sudo /etc/init.d/apache2 restart

or

	$ sudo service restart apache2

or

	$ sudo apache2crl restart
	
## What to Submit

Create a cropped screenshot of configuration file for the staff.example.com virtual host and upload it to the assignment.

## Resources

- [The Debian Administrator's Handbook](http://debian-handbook.info "The Debian Administrator's Handbook")
- [Ubuntu Server Guide](https://help.ubuntu.com/12.04/serverguide/index.html "Ubuntu Server Guide")
- [UFW - Uncomplicated Firewall](https://help.ubuntu.com/community/UFW "UFW - Uncomplicated Firewall")
- [Ubuntu Firewall Guide](https://help.ubuntu.com/12.04/serverguide/firewall.html "Ubuntu Firewall Guide")
- [a2ensite/a2dissite man page](http://manpages.ubuntu.com/manpages/jaunty/man8/a2ensite.8.html)

> Written with [StackEdit](https://stackedit.io/).