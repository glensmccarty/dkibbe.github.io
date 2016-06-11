# netcat

## Overview

Netcat is called the "TCP/IP Swiss army knife." In this assignment you'll use it to test that an SMTP service is listening on a certain port. This can be useful in setting up a mail client.

## Assignment Objectives

When you have successfully completed this assignment you will be able to:_

*   Use **netcat** to connect to an SMTP server.

## Terms You Should Know

- **SMTP** - Simple Mail Transfer Protocol
- **/etc/services** - Lists common ports and protocols.

## Preparation

Install **netcat** on Debian or **nc* on CentOS-minimal.

## Netcat

Cox has a SMTP server at _smtp.cox.net_ but it doesn't listen on the default port 25 but does accept connections on the mail submission port and SMTP over SSL. Use **netcat** to connect to the mail submission port 587.

This shows that there is an SMTP server listening. Next query the server for a list of options.

## Sending Mail with `netcat`

If you have an account on the SMTP server you can send mail directly by sending the same commands that a mail client would use.

This server is actually using greylisting as an anti-spam measure. A legitimate mail server will retry sending the mail in a few minutes an spammer might not.

## What to Submit

Grab a screenshot of netcat connecting to an SMTP server.

## XKCD

![http://imgs.xkcd.com/comics/file_transfer.png](http://imgs.xkcd.com/comics/file_transfer.png)

## Resources

- [Greylisting](https://en.wikipedia.org/wiki/Greylisting)
- [Netcat – a couple of useful examples](http://www.g-loaded.eu/2006/11/06/netcat-a-couple-of-useful-examples/)
- man netcat (nc)
- [Benchmarking LAN connectivity](http://techthrob.com/2014/01/13/benchmarking-lan-network-connectivity-in-linux/)

> Written with [StackEdit](https://stackedit.io/).