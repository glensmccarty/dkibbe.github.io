![OpenSSH][]


## Using SSH for remote connections

The suite of tools that make up the OpenSSH package replace `telnet`, `ftp` and rtools for connecting over insecure networks.

In this assignment you'll use `ssh`, `scp` and `sftp` to connect to another workstation and transfer files. 

## Preparation

On later versions of CentOS and Ubuntu OpenSSH server is installed and running so you may not need to install the service.

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:*

+ Install and configure the OpenSSH Server.
+ Use a command line tool to open the appropriate port in the firewall.
+ Use Secure Shell to log onto a remote computer.
+ Create a public/private key pair with the appropriate security permissions.
+ Transfer the public key to the remote host using `scp`.
+ Use Secure FTP to transfer files.
+ Explain the difference between symmetric and public key encryption.
+ Configure SSH-Agent to cache the SSH key passphrase.
+ Create a SSH configuration file for personal settings.

## Terms and Concepts

+ **ssh:** Secure Shell
+ **scp:** Secure Copy
+ **sftp:** Secure FTP
+ **ssh-copy-id:** A utility to copy your public key to a remote host.
+ **ssh-keygen:** Utility to generate a public/private key pair.
+ **ssh-agent:** A caching utility for keys so you only need to enter the passphrase once.
+ **openssh-server:** The SSH server daemon
+ **authorized_keys:** Contains the public keys used to connect to this host.
+ **known_hosts:** Once a connection is established with ssh the fingerprint is stored here.
+ **fingerprint:** A public key fingerprint is a short sequence of bytes used to authenticate or look up a longer public key.
+ **/etc/ssh/ssh.config:** The system-wide configuration file for the ssh client
+ **/etc/ssh/sshd_config:** Configuration file for the ssh server
+ **~/.ssh:** Personal private keys, configuration settings and a known hosts file is kept in this hidden configuration directory.
+ **~/.ssh/config:** Personal configurations go in this file.
+ **Public key encryption:** A separate public key and private key are used. Messages are encrypted using the public key and decrypted using the private key.
+ **Symmetric key encryption:** A single key is used to encrypt and decrypt a file.
+ **/etc/services:** Lists common services and their default ports.
+ **PGP:** Phil Zimmermann's Pretty Good Privacy public key encryption
+ **GPG:** GNU Privacy Guard, an open implementation of PGP
+ **Passphrase:** A passphrase is stronger that a password since it can contain multiple words separated by spaces.
+ **Host:** A host is just another name for a computer on a network.

## Preparation

In this assignment you will be working with two computer – the workstation you are sitting at and a virtual machine that will be the SSH server. To make it clear what commands are run on each I'll use this prompt for the workstation:

		tux@instr $

And this prompt for the virtual machine:

		jstudent@vm1 $

or if root access is required on the virtual machine:

		root@vm1 #

### Bridging the Network

Both hosts need top be on the same network and have different IP addresses. Before starting the CentOS minimum virtual machine set networking in VirtualBox to bridging:

![Network bridge settings in VirtualBox][bridge]


### Check that the Host is Reachable

Make note of the IP address of the virtual machine. You'll use the IP address to connect to the virtual machine.

		jstudent@vm1 $ ip addr show

Check that you can reach the virtual machine on the network. The virtual machine must have an IP address on the 192.168.201.0 network. For example:

		tux@instr $ ping 192.168.201.106 -c4

### Create an Account on the Host

To complete this lab you'll need to work with another student.

Set up accounts on each virtual machine so that you can each log in remotely. Use a login name appropriate for the student logging in. Login names should be short, lower case and not contain spaces. Be sure to assign a password to the accounts.

		root@vm1 # adduser -m -c "Jack Student" jstudent # -m is the default on CentOS
		root@vm1 # passwd jstudent

### OpenSSH Server

Both the OpenSSH client and server should already be installed but the server may need to be started. The service command is used to start and stop services. The `chkconfig` command configures services to start on boot.

The OpenSSH client is installed on most Linux systems but you may need to install the server to complete this assignment.

### Is the Service Installed?

	# systemctl status sshd

The SSH server listens on port 22. You can use `netstat` from the virtual machine to confirm that the SSH server is listening on port 22.

	# netstat -luntp

Use the `service` command to see check the status of the service. If the **openssh-server** is installed it may just need to be started.

	# service sshd status

#### Install OpenSSH Server (if needed)

On CentOS

	# yum install sshd

On Ubuntu

	$ sudo apt-get install openssh-server

The configuration file for the ssh server (sshd) is:

	/etc/ssh/sshd_config

Start the server using the `service` command:

        # service sshd start
	
You can check that sshd is running with:

	# service sshd status

### Firewall

Starting the SSH server is not enough you also need to open port 22 in the firewall. The easiest way to do this is with a firewall configuration tool. If `system-config-firewall-tui` is not install you can install it with `yum`.
	
Check that the firewall allows traffic over **port 22** on the remote or bring down the firewall for this assignment:

	# iptables-save

If not install and use `system-config-firewall-tui` to open port 22.

![system-config-firewall-tui][firewall-tui]

This command line tool makes it easy to configure the firewall. Select *customize* and use the Tab or arrow keys to move between options and the space bar to select and deselect an option.

## Use SSH to Login

Once the SSH server is started and port 22 is open in the firewall you can log into the remote host from a shell on your local machine using the login name and password on the remote host. To log into the remote computer use this command and substitute your user name and the IP address of the virtual machine you wish to log into.
	
Use `ssh` to login:

	$ ssh user@remote
	
You can omit the user name if it's the same as the local user.

	$ ssh remote

The first time you connect you will be presented with the fingerprint of the server to confirm you are connecting to the correct host. After giving the password for the remote account you will be logged into the remote machine. To close the connection type `exit` and you will be returned to your own virtual machine.

## Secure FTP

The secure FTP command is used to transfer files to and from the remote host.

Create a file on your workstation to practice with.

	S touch example.txt

Now connect using secure FTP.

	$ sftp -i .ssh/id_rsa jstudent@192.168.201.106

You are now at a Secure FTP prompt and can use commands to list files, get files from and put files on the remote host. Type **help** for a list of commands.

The **put** command will upload example.txt on your local machine to the remote host.

	sftp> put example.txt
	Uploading example.txt to 192.168.201.106/home/jstudent/example.txt
	example.txt                                   100%    0     0.0KB/s   00:00
	sftp> ls
	example.txt 

Use the **bye** command to close the connection.

	sftp> bye
	tux@instr $

## Secure Copy

Secure Copy can be used to copy a single file to the remote host.

	$ scp exaample.txt jstudent@192.168.201.106:

Notice the colon at the end of the command. Without the colon `scp` just creates a new file named `jstudent@192.168.201.106` in the current directory. If you want the file to have a different name on the remote system place the new name after the colon.

## Using SSH with Public Key Authorization

Public key authorization is more secure that using a password and more convenient. To use public key authorization you create a key pair on your local machine and then upload the *public key* to the remote host. The *private key* stays on the local machine and is protected by a passphrase.

First generate a public/private key pair on the localhost. The password protects the private key from unauthorized use. Later in this assignment you will configure ssh-agent so you do not have to enter the password each time. The ssh-keygen command suggests a default key pair name but you can use a more descriptive name if you like. Be sure to enter the complete path to your .ssh directory.

You should not create the keys as root!

		tux@vm1 $ ssh-keygen
		Generating public/private rsa key pair.
		Enter file in which to save the key (/home/jstudent/.ssh/id_rsa):
		Enter passphrase (empty for no passphrase): 
		Enter same passphrase again: 
		Your identification has been saved in /home/jstudent/.ssh/id_rsa.
		Your public key has been saved in /home/jstudent/.ssh/id_rsa.pub.
		The key fingerprint is:
		51:75:0f:56:08:7f:78:d4:dd:87:0d:de:1e:d4:f9:dd
		The key's randomart image is:
		+--[ RSA 2048]----+
		|        E        |
		|         +       |
		|  . o   o o      |
		|   = o o +       |
		|    o + S o      |
		|     . o O o     |
		|        + =..    |
		|         ....    |
		|         .o...   |
		+-----------------+
		[jstudent@d630 ~]$

The randomart image serves the same purpose as the artwork you may have selected when you set up online access to your bank account. It helps assure you are connected to the correct host.

## Placing the Public Key on the Remote Host

Before you can use the keys the public key must be appended to *~.ssh/authorized_keys* on the remote host. You will use `ssh-copy-id` to copy the *public key* to the remote host.

## ssh-copy-id

The `ssh-copy-id` command makes the task of uploading the public key easy.

		tux@instr $ ssh-copy-id -i .ssh/id_rsa.pub jstudent@192.168.201.106

## Connecting Using Public/Private Keys

Now that you have the public key added to *authorized_keys* on the virtual machine you can connect using the private key.

		tux@instr $ ssh -i .ssh/id_rsa jstudent@192.168.201.106

If you used a passphrase to protect the private you will need to enter it. If not after a short wait you should see the shell prompt on the virtual machine.

## SSH Agent and Key Chain

The `ssh-agent` command caches the private key passphrase so you only need to enter it once per session. Refer to this [IBM developerworks][agent] tutorial on setting up SSH-Agent and key chain.

## The SSH Client Configuration

The global SSH client file is */etc/ssh/ssh_config* and each user can have a local configuration file named *config* in that user's `~/.ssh* directory. The customizations make it easy to log in to multiple hosts. Here is an example from my *config*:

		Host ironman
			HostName 72.208.176.109
			Port 4444
			User profx
			PubkeyAuthentication yes
			IdentityFile ~/.ssh/srv.rsa

With this entry you just need to type `ssh ironman` to connect to the host.

## Troubleshot the Assignment

+ Make sure you are logged into the correct computer before you run a command.
+ For a successful SSH connection several things are needed.
+ The virtual machine must have a IP address on the same network as the workstation.
+ There must be an opening on the firewall of the virtual machine for port 22.
+ The SSH daemon must be running on the virtual machine.
+ The correct permissions on the different files are important. If after creating the public/private keys you are still asked for a password to log in or Secure Shell refuses to connect that a either the private key or *authorized_keys* has the wrong permissions.

## What to Submit

Submit a screenshot of the ~/.ssh/config file you created to automate login to the virtual machine. For full credit include the two lines that shoe public key encription is being used to login.

## Resources

1. man 5 sshd_config
2. man ssh_config
3. [ssh_config(5) - Linux man page][ssh_config]
4. [sshd_config(5) - Linux man page][sshd_config]
5. [OpenSSH.com][]

[OpenSSH]: http://openssh.com/images/openssh.gif
[OpenSSH.com]: http://openssh.com
[firewall-tui]: https://s3.amazonaws.com/CIS126DL/Images/firewall-tui_trusted.png "system-config-firewall-tui"
[bridge]: https://s3.amazonaws.com/CIS126DL/Images/vbox_bridged.png "Network bridge setting in VirtualBox"
[ssh_config]: http://linux.die.net/man/5/ssh_config "ssh_config(5) - Linux man page"
[sshd_config]: http://linux.die.net/man/5/sshd_config "sshd_config(5) - Linux man page"
[agent]: http://www.ibm.com/developerworks/library/l-keyc/index.html "Setting up SSH Agent"

> Written with [StackEdit](https://stackedit.io/).