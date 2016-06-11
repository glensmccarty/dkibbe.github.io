# Apache on CentOS 7

## Assignment Objectives

*After successfully completing this assignment you will be able to:*

 1. Install the Apache web server on CentOS 7
 2. Configure IP-based virtual hosts on Apache.
 2. Install Firewalld
 2. Add a service to the firewall.
 3. Open a custom port in the firewall.
 4. Make firewall rules permanent.

## Preparation

Use the CentOS 7 ova for this assignment. CentOS uses a basic `vi` text editor by default so you might want to install `vim` or `nano`.

### Set Networking to Bridged

In VirutalBox set the network adapter to *Bridged Network* and under *Advanced* generate a new random MAC address. When you boot up the virtual machine use `ip addr show` to confirm you are on the 192.168.**2xx**.0/24 network. Where **xx** is the classroom number. *Example:* BA 1E is 201 and BA 13 is 213.

<!--## Terms You Should Know-->

### Install Apache

Use `yum grouplist` to find the *Basic Web Server* and the install it using group install.

	# yum groupinstall "Basic Web Server"

If bandwidth is limited you can just install the httpd server.

	# yum install httpd
	
The `rpm` command will show that the Apache daemon is installed and where to find the configuration files. It will also tell you the version of Apache that you are running so you can consult the correct Apache documentation.

	# rpm -qa | grep httpd
	# rpm -qc httpd

#### Start Apache

Apache is installed but not yet running. The *status* option to `systemctl` show that A[ache is not running and disabled on boot.

	# systemctl status httpd
	
Use `systemctl` to start Apache and enable it on reboot.

	# systemctl start httpd.service
	# systemctl enable httpd.service
	
## Test Apache

Try opening the default web page from Firefox or Chrome on the Windows host. Use `ip` to discover the correct IP address for your server.

	# ip addr show

The web page can not be reached yet since the *http* service has not been added to the firewall.

## Adding a Service to the Firewall

If Firewalld is not already running and enabled if install it with Yum. Use the `firewall-cmd` command to open the default port 80 for Web traffic. Port 80 is the [well-know port](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers) for http.

	# firewall-cmd --add-service http
	# firewall-cmd --list-services

Refresh the web page in Firefox and you should still see the testing 1, 2, 3 page.

### Apache Virtual Hosts

Virtual hosts let one Apache web server deliver content for many domains. There are two types of virtual hosts *IP-based* and *named-based*. You will be creating two IP-based virtual hosts *example.com* on port 80 and *staff.example.com* on port 8080. The content for these sites will be served from two separate directories */var/www/example.com* and */var/www/staff.example.com*.

#### Create the Directories and Content

	# mkdir /var/www/example.com /var/www/staff.example.com
	
	# echo "<h1>This is example.com.</h1><p>Put your name here if you want credit for the assignment.</p>" > /var/www/example.com/index.html

	# echo "<h1>This is staff.example.com.</h1><p>Put your name here if you want credit for the assignment.</p>" > /var/www/staff.example.com/index.html

#### Add the First Virtual Host

Next you will create the necessary configuration file so Apache knows where to find the correct content to server for each domain. The file will be in */etc/httpd/conf.d* and must end in *.conf*. You can put both virtual host directives in one file or put each in its own file.

The configuration file will contain standard Apache directives placed between starting and ending tags.  See the [Apache Virtual Hosts Documentation](https://httpd.apache.org/docs/2.4/vhosts/ip-based.html) for the correct format.

Create the first virtual host using the information in the Apache Virtual Hosts documentation.

The Apache Docs under *Resources* below will explain the purpose of each directive.  Add directives for each domain as follows:

 - ServerAdmin
 - DocumentRoot
 - ServerName
 - ErrorLog
 - CustomLog

You should add a **Listen 8080** directive in the configuration file but place it *outside* the **VirtualHost** tags. Do not add a **Listen** directive for port 80 since that directive already exists in the main configuration file.

When you are finished editing the config file save it and run `apachectl configtest` to check for errors. You should receive no errors accept for a *ServerName not found* warning. Follow the directions in the *httpd.conf* configuration file to fix this error. Run `apachectl` a second time to see that the error message is gone.

Finally reload the confiuration file.

	# apachectl graceful

#### Test the example.com domain

Open the IP address for your *example.com* in Firefox or Chrome and you should see the correct web page.

#### Add the Second Virtual Host

Use the **yy** command in **vi** to copy and paste a second virtual host stanza for *staff.example.com* in the *vhosts.conf* file you created or create a second file..

Test the configuration and reload the config file with `apachectl`.

#### Test staff.example.com

Try the same with *staff.example.com* You need to enter the address followed by a colon and the 8080 for the domain as in this example

	192.168.201.123:8080

It will fail since port 8080 is still closed in the firewall. 

### Open Port 8080

Our second virtual host, *staff.example.com* is served from a different port so that port needs to be opened in the firewall. Port 8080 is not a standard port is it needs to be added this way.

	# firewall-cmd --add-port=8080/tcp
	# firewall-cmd --list-ports 

Retry the IP address and it will still fail since Apache is listening only on the default port 80.

### Listen on Port 8080

Add a *Listen* directive to the top of the *vhosts.conf* file outside of the virtual host stanza. Reload the config file as you did above and retry *staff.example.com*. You should see the correct content.

## Debug the Assignment

## What to Submit

Use the Snipping tool in Windows (or Screenshot in Linux) to submit a cropped screenshot of the contents of the index.html page for each site being displayed in a browser on Windows.  *Be sure to include the address bar in your screenshot.* See example below.

![enter image description here](http://classfiles.dennisk.fastmail.net/apache_submit.png)

## Resources

- [Apache HTTP Server](hhttps://httpd.apache.org/ABOUT_APACHE.html)
- [Apache Virtual Host documentation](https://httpd.apache.org/docs/2.4/vhosts/)
- `/etc/services`
- `man apachectl`
- `man  firewall-cmd`

> Written with [StackEdit](https://stackedit.io/).