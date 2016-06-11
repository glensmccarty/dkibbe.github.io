![enter image description here](https://s3.amazonaws.com/CIS238DL/img/grub_rescue.png)

## Introduction

The Grand Unified Bootloader (GRUB) is used by almost all Linux distributions. In this assignment you will "break" a CentOS 7 system and then repair it using a rescue CD.

## Learning Objectives

*After successfully completing this assignment you will be able to:*

1. Boot into single user mode.
2. Boot from a rescue CD.
2. Use `chroot` to access the broken system.
3. Use `grub2-mkconfig` to rebuild the GRUB configuration file.

## Useful Terms

 - GRUB
 - `chroot`
 - `grub2-mkconfig

## Preparation

- Import the CentOS 7 minimal ova.
- Boot the system and move */boot/grub2/grub.cfg* to */root/grub.cfg*
- Reboot the system to see that it fails to boot.
- From the GRUB prompt type `halt` and close the virtual machine window.

## Rescue

### Boot the Rescue Disk

- Load the *CentOS 7 install ISO* into the virtual CD drive.
- Make sure the CD is set as the first boot device.
- Boot the system and you should see this screen.

![enter image description here](https://s3.amazonaws.com/CIS238DL/img/grub_rescue-1.png)

Select *Troubleshooting* 

![enter image description here](https://s3.amazonaws.com/CIS238DL/img/grub_rescue-2.png)

and then *Rescue a CentOS system* from the next screen. The rescue CD gives you a number of options. Tab to *Continue*.

![enter image description here](https://s3.amazonaws.com/CIS238DL/img/grub_rescue-3.png)

### Chroot into the Broken System

Use the `chroot` command to access the broken system. 

![enter image description here](https://s3.amazonaws.com/CIS238DL/img/grub_rescue-4.png)

### Make a New GRUB Configuration

Use `cd` to navigate to `/boot/grub2` and run `grub2-mkconfig` to recreate the configuration file.

	# grub2-mkconfig --output=grub.cfg

Type `halt` to stop the system and then remove the rescue CD.

![enter image description here](https://s3.amazonaws.com/CIS238DL/img/grub_rescue-0.png)

Reboot the system and you should be at a login prompt.

## Single User or Rescue Mode

You can modify the GRUB boot string to change the target boot mode or boot into rescue mode from a working system. See the instructions here.

[24.9.1. Booting to Rescue Mode](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-Terminal_Menu_Editing_During_Boot.html)

## 24.8. GRUB 2 OVER A SERIAL CONSOLE

[24.8. GRUB 2 OVER A SERIAL CONSOLE](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-GRUB_2_over_a_Serial_Console.html)

It appears that VirtualBox supports this. Anyone want to test it?

## What to Submit

Submit a screenshot of the output of `grub2-mkconfig` showing that a new config file is being created in the correct directory *not* in stdout.

## Resources

 - man chroot
 - man grub2-mkconfig
 - [GRUB2 Tutorial](http://dedoimedo.com/computers/grub-2.html)
 - [LILO and GRUB: Boot Loaders Made Simple](http://www.linuxdevcenter.com/pub/a/linux/2008/01/22/lilo-and-grub-boot-loaders-made-simple.html)

> Written with [StackEdit](https://stackedit.io/).