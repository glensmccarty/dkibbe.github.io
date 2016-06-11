# Self-Signed SSL Cert

## Overview

![https://www.secure-travel.co.uk/images/ssl_padlock.jpg](https://www.secure-travel.co.uk/images/ssl_padlock.jpg)

SSL is the encryption technology used to protect your confidentiality on the web. It is similar to using SSH keys in that there is a public and private key involved. In addition the public key (in the certificate sent to Firefox) is signed by Certificate Authority (CA) that vouches for the authenticity of the web site. It is somewhat like using a Notary Public to verify your signature.

In this assignment you will create and install a self-signed certificate for the Apache web server.

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:*

*   Create a SSL self-signed certificate and private key
*   Open a port in the firewall for `https`.
*   Connect to the Apache web server using SSL.
* Create a Virtual Host file for SSL.

## Terms You Should Know

- **Secure Socket Layer** – The encryption technology that protects sites on the web.</dd>
- **PKI:** Public Key Infrastructure
- **CA:** Certificate Authority, a recognized agency that issues SSL certificates such as Verisign.
- **.key:** The extension for the private key
- **.csr:** The extension for the signing request sent to the registrar. (Not used here.)
- **.crt:** The extension for the self-signed key
- **x509:** X.509 is an ITU-T standard for a public key infrastructure (PKI).
- **Port 443:** Secure https

## Preflight Checklist

- Import CentOS 7 OVA
- Set Networking to **Bridged**
- Refresh the MAC address
- Install Apache
- Install mod_ssl
- Check that openssl is installed
- Start Apache and test that the site is reachable on port 80 (http) and port 443 (https) before installing *firewall.d*.

## Remove Default Cert and Key

Apache may not recognize your new certification and key files if the default ones are still in place.

1.  Remove the default **localhost.crt** file from `/etc/pki/tls/certs`
2.  Remove the default **localhost.key** file from `/etc/pki/tls/private`

## Generate Self-Signed Certificate and Sign the Private Key

Create the self-signed cert (.crt) and private key (.key) in root's home directory with this command.

	# openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout mykey.key -out mycert.crt

*Be sure to fill out the required fields!* See **What to Submit** below.

### Copy the New Certificate to the PKI Directory

Copy the cert to */etc/pki/tls/certs/*.

### Copy the New Private Key to the PKI Directory

Copy the key to */etc/pki/tls/private/*.

## Enable the New Certificate

The last step is to enable the new certificate in `/etc/httpd/conf.d/ssl.conf`. There are several directives that must be edited.

 - DocumentRoot
 - ServerName (Keep the default and create a DocumentRoot to match.)
 - SSLCertificateFile
 - SSLCertificateKeyFile

Comment out these lines and add a new entry below each with your key and certificate paths. Make sure the crt and key names match the ones you used. Oh, and you did make a backup of  *ssl.conf* in roots home directory, yes?

Use `apachectl -S` to test the syntax of your virtual host.

### Reload the Apache configuration

	# apachectl restart

## Open Port 443 in the Firewall

Add the *https* service

	# firewall-cmd --add-service https

## Troubleshoot the Assignment

- Make sure your name appears in the certificate screenshot.
*   Did you copy the files to the correct directories?
- Make sure to remove the old `Localhost.crt` and `localhost.key` files.
- Make sure to edit the `/etc/httpd/conf.d/ssl.conf` file with the correct file names.
- In Firefox you can view the certificate details again under the *Tools, Page Info* menu.
- Do you restart Apache?

## What to Submit

Submit a screenshot of the certificate details from the warming dialog in Firefox. Make sure that your first and last name show in the **Common Name** field.

![http://classfiles.dennisk.fastmail.net/ssl_cert.png](http://classfiles.dennisk.fastmail.net/ssl_cert.png)

## Resources

- [Apache Module mod_ssl](https://httpd.apache.org/docs/current/mod/mod_ssl.html)
- [Public key infrastructure](https://en.wikipedia.org/wiki/Public_key_infrastructure)
- https Everywhere

> Written with [StackEdit](https://stackedit.io/).