Getting Down with TCP Wrappers

![http://www.centos.org/docs/5/html/Deployment_Guide-en-US/images/tcp-wrappers/tcp_wrap_diagram.png](http://www.centos.org/docs/5/html/Deployment_Guide-en-US/images/tcp-wrappers/tcp_wrap_diagram.png)

## Overview

TCP Wrappers provides an extra layer of security for network services by allowing fine-grained control on what hosts can connect to a server. In this assignment you will use TCP Wrappers to allow or deny access to the SSH server.

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:*

*   Selectively deny access based on IP address.
*   Selectively allow access based on IP address
*   Explain the function of the xinetd server.
*   Use `ldd` to determine if a service is protected by TCP Wrappers.

## Terms You Should Know

/etc/hosts.allow
: Allow rules go here.

/etc/hosts.deny
: Deny rules go here.

ldd
: Print shared library dependencies

xinetd
: Extended Internet services daemon

## Preparation

Do this assignment on a CentOS virtual machine with the SSH daemon installed and running.

CentOS protects most network services with TCP Wrapper. You can use the `ldd` command to determine if OpenSSH is linked to TCP Wrappers:

## /etc/hosts.allow

The **/etc/hosts.allow** file is read before the **/etc/hosts.deny** file and rules are applied from the top down. If no rules for the service are found in either file, or if neither file exists, access to the service is granted. *Remember for the last rule to effective there must be a blank line below it.*

1.  Place this line in **/etc/hosts.allow** Use the IP address of the host you will be using to connect to the server.
2.  *Place a blank line below the rule.*
3.  Try logging in from another virtual machine or from the Windows host using PuTTY. The login should succeed.

## /etc/hosts.deny

1.  Add a line to **/etc/hosts.deny** that will deny all connections to the SSH server.
2.  *Place a blank line below the rule.*
3.  Try to log in again. The login should still succeed since the rule in **/etc/hosts.allow** is applied first.
4.  Comment out the rule in **/etc/hosts.allow** and try again to log in. This time the log in should fail.

## One File Rules Them All

Both allow and deny rules can be put in a single files either **/etc/hosts.allow** or **/etc/hosts.deny** by using the proper format.

## Setting a Trap with Twist

Set a trap for the bad guys!

## Troubleshoot the Assignment

The most common problem is not putting a new blank line after the last rule.
*   Check rule order and if you have conflicting rules in **/etc/hosts.allow** and **/etc/hosts.deny**

## What to Submit

*Copy and paste these questions in the text submission box.*

1.  What is the most common mistake made with TCP Wrappers?
2.  In what order are the rules in the **/etc/hosts.allow** and **/etc/hosts.deny** files processed?
3.  If you have **sshd: ALL** in both **/etc/hosts.allow** and **/etc/hosts.deny** will SSH connections be allowed? Why?
4.  What will this rule in **/etc/hosts.allow** do?
5.  In **/etc/hosts.deny**?

## Resources

- [CentOS Documentation](http://www.centos.org/docs/5/html/Deployment_Guide-en-US/ch-tcpwrappers.html)
- [xinetd man page](http://www.linuxcommand.org/man_pages/xinetd8.html)
- [Getting started with SSH security and configuration](https://www.ibm.com/developerworks/aix/library/au-sshsecurity/)

> Written with [StackEdit](https://stackedit.io/).