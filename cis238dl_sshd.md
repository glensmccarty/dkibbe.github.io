# Secure Shell Server

## Assignment Objectives

SSH is widely used to administer remote hosts and as such is a prime target for exploitation attempts. In this assignment you will configure the SSH server for added security.

*When you have successfully completed this assignment you will be able to:*

1. Identify the configuration file for the SSH server daemon.
1. Configure SSH to use a non-standard port.
1. Improve security be disabling remote root logins.
1. Reduce the number failed login attempts allowed.
1. Add a SSH banner.

## Terms and Concepts

Daemon
: A background process that handles requests for services such as print spooling and is dormant when not required.

Well-Known Ports
:  Ports 0-1023 are reserved for common services and can only be accessed by root.

`/etc/ssh/sshd_conf`
: Configuration file for the SSH server daemon

Fingerprint
: "...a cryptographic hash function to a public key. Since fingerprints are shorter than the keys they refer to, they can be used to simplify certain key management tasks." [Wikipedia](https://en.wikipedia.org/wiki/Public_key_fingerprint)

Netcat
: "...is a feature-rich network debugging and investigation tool" [Wikipedia](https://en.wikipedia.org/wiki/Netcat)

Nmap
: Network port scanner

`lsof`
: List open files.

`rpm -qc`
: The **-qc** option is useful to discover what configuration files a package uses.

`/etc/services`
: Lists services and their default ports. This file is for information only and does no configuration itself.

## Preparation

Start both a CentOS 7 and Ubuntu virtual machine or work with another student using two CentOS 7 VMs. Create an ordinary account on the CentOS 7 Virtual machine.

### Networking

1.  Make sure the virtual machines are powered off.
2.  Set the network adapter in VirtualBox to *Bridged Network* and refresh the MAC address..
3.  Start the CentOS virtual machine and log in as root.
4.  Run `ip addr` on both VMs to confirm that the IP addresses are on the 192.168.201.0/24 network.

### Install Nmap

Use `yum` or `apt-get` as appropriate to install `nmap` and possibly `zenmap`.

### Scanning Ports

Use `nmap` to do a simple scan of the SSH server and you should see that port 22 is open for ssh traffic.

## Connect to the SSH Server 

You should now be able to use `ssh` from the second virtual machine to connect to the SSH server as *root*. 

`ssh root@192.169.201.nnn` 

Replace *nnn* with the last octet of the actual IP address of the SSH server. The first time you connect SSH will ask you to confirm the connection.

After you accept the connection you will be logged in as root. Type `exit` to close the connection.

## Securing the SSH Server Daemon

### The SSH Server Configuration File

Use the `rpm -qc openssh-server` command to show that the SSH server configuration settings are in `/etc/ssh/sshd_conf`. Like most Linux configuration files it is plain text and, at least, on CentOS is well commented. Notice that lines need to be uncommented for a change to be effective. Also, You need to reload the configuration file for changes to become effective using the `systemctl restart sshd.service` command.

### Disabling Root Logins

There is no reason for the *root* user to login directly. Root should also have an ordinary user account for that purpose and that use either `su` or `sudo` to perform root functions. Change this line in the `/etc/ssh/sshd_conf` file from **PermitRootLogin** *yes* to *no*. *Note:* In `vi` use /Root to search for the line.

Restart the service and attempt to log in again as *root* this time the attempt will fail.

You should be able to log in as the user you created. For example:

	$ ssh tux@192.168.201.123

### Change Default Port

SSH by default listens on port 22. You can change this by uncommenting the line **port 22** and changing the port number to an unused port in the **registered** or **ephemeral** range. See Wikipedia link to ports under *Resources* below.

Be sure to follow the instructions in the *sshd_config* to set SELinux. Use `yum whatprovides` to see what package contains `semanage`.

#### Open the Port in the Firewall

Install `firewalld`. Since port **2222** (our example) is not a standard service you need to use this command to open the port.

	# firewall-cmd --add-port=2222/tcp

Use `firewall-cmd --list-ports` to see that the change was made.

#### Disable Port 22

And remove the default port.

	# firewall-cmd --remove-service ssh

Use `firewall-cmd --list-services` to see that the change was made.

Run a `nmap` scan and there should be no "interesting" ports open.

#### Making Changes Permanent

None of these changes will survive a reboot unless the **--permanent** option is added to the above commands.

### SELinux

Use the instructions in the configuration file to configure SELinux to recognise the new port. Use `yum provides` if needed to find the correct package to install.

## Mapping the New Port

Run a` nmap` scan on a port range that includes the port you opened for SSH.

	$ nmap -p 2200-2250 192.168.201.nnn

The Netcat command can useful as well. It has different package names on different Linux distros so use `yum search` or `apt-cache search`.

### Protocol

Assure that the more secure **Protocol 2** is being used. This is the default.

### Reducing the Number of Login Tries

The default is **6** failed attempt but you can reduce this to a smaller number by changing **MaxAuthTries**. Edit **MaxAuthTries** to allow only attempts.

### Disabling Password Logins (Optional)

If you created SSH keys you can disable password logins entirely. Uncomment and change **PasswordAuthentication** to *no* to disable password logins. *Warning:* If you lose your SSH keys you will not be able to login.

## Adding an SSH Banner

Adding a welcome banner that warns that all activity on the server is a good idea. Creating a banner text file and adding a line to the *sshd_config* file is all that is needed.

First create the banner using `vi` or `emacs`.

Leave a blank line or two below the banner text so the banner appears above the login prompt.

Next add this line to the */etc/ssh/sshd_config* file.

Now reload the configuration file for the change to take effect.

## SSH to the New Port

Since port 22 is no longer used the ssh command much be modified. For example:

	$ ssh -p 222 tux@192.168.201.123

## What to Submit

Submit a screenshot of the Netcat command showing that SSH on port 2222 (or another non-standard port) is listening.

## Resources

- [List of TCP and UDP port numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)
- [Securing OpenSSH](http://wiki.centos.org/HowTos/Network/SecuringSSH)
- [The Debian Administrator's Handbook](http://debian-handbook.info)
- [Public key fingerprint](https://en.wikipedia.org/wiki/Public_key_fingerprint)
- [Netcat](https://en.wikipedia.org/wiki/Netcat)
- [Permanent link to assignment](http://dennisk.freeshell.org/cis238dl_sshd.html)<!--se_discussion_list:{"T9sEVghCbgAq0Xk1Dn5ut16R":{"selectionStart":2107,"selectionEnd":2121,"commentList":[{"content":"nmap -p 2222 ip.addr.range"}],"discussionIndex":"T9sEVghCbgAq0Xk1Dn5ut16R"}}-->