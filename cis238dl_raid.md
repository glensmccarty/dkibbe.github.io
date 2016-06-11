![Tux Raid](https://s3.amazonaws.com/CIS238DL/img/tux_raid.png)

## Overview

*RAID is a data storage technology that combines multiple disk drive components into a logical unit for the purposes of data redundancy and performance improvement.* -- Wikipedia

In this assignment you'll create a new CentOS minimal virtual machine with the `/home` directory mounted on a RAID 1 array comprising of three 1GiB virtual disks.  Two being active members of the RAID array and one being held as a hot spare.  A fourth drive will be left unformatted for later addition to the array.

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:*

- Explain the purpose of RAID
- Describe several common RAID set ups
- Explain the purpose of the `/etc/fstab` and `/etc/mtab` files.
- Demonstrate how RAID is used to protect data.
- Degrade a RAID array by failing a device
- Monitor the rebuild process.
- Add a new drive to the RAID array.

## Terms You Should Know

- **RAID** - Redundant Array of Independent Disks
- **RAID 0** - Stripping for performance, no redundancy
- **RAID 1** - Mirroring for redundancy
- **RAID 5** - Comprises block-level striping with distributed parity (fault tolerance).
- `/etc/fstab` - Lists device names mounted at boot time.
- `/etc/mtab` - Shows current mounted filesystems. 
- `mdadm` - CLI tool for administering RAID.
- `fsck` - No, not what you think.  It's Filesystem check.
- **Mirror** - Data duplicated over multiple disks.
- **Strip** - Data fragments spread over multiple disks.
- `/proc/mdstat` - Lists existing RAID volumes and their states.

## Preparation

Create a new virtual machine using the CentOS 7 minimal installation ISO *not* the CentOS OVA.

Add a second and third 8GiB virtual drive in VirtualBox.

![Second virtual drive in VirtualBox](https://s3.amazonaws.com/CIS238DL/raid-2.png)

## Configure RAID During the Install

Start the installation and check *I will configure partitioning.* Select the first 2 drives but leave the third unselected which you will add later as a hot spare.

![Selecting drives during install](https://s3.amazonaws.com/CIS238DL/raid-3.png)

Click done and on the custom partitioning screen click on *Automatically create partitions* and then select *Device Type* as RAID and *RAID Level* as Raid 1. When done the layout should look like this.

![Installation screen](https://s3.amazonaws.com/CIS238DL/raid-5.png)

On the *Installation Summary* screen click *Begin Installation*.

When the installation is finished reboot the virtual machine.

## RAID Management

### Install Mutt

Install the `mutt` email client so you can read the messages `mdadm` will send.

### Examining the Current Setup

Login in as root and run `df -h` to show that `/` is mounted on `/dev/md127`.

The `mdadm` command is used for monitoring and troubleshooting RAID.  See the *Debian Handbook* for an excellent chapter on working with RAID.
```
# mdadm /dev/md127
/dev/md127 1022.44MiB raid1 2 devices, 1 spare. Use mdadm --detail for more detail.
```
Using the *--detail* option you will see that the RAID 1 array is active, in good health but has no spare drive.

### Add a Spare Drive

If the active drives are `/dev/sda` and `/dev/sdb` the spare should be the next letter `/dev/sdc`. Your actual drives could be different.

#### Prepare the Unformatted Drive

Use `fdisk` to prepare `/dev/sdc`.

```
# fdisk /dev/sdc
```

Type *m* to access the help manual from within `fdisk`.

Type *p* to "print" the current partition table which is empty.

Create a new primary partition as `sdc1` using all the space (the default).

Typing *p* will show the default type is /linux/.

6. Use *t* to change the type to *Linux raid auto* or type *fd*.

Type *p* to see the partition table.  The type should now be *Linux raid auto*.

Type *w* to write the partition table and *q* to exit `fdisk`.

### Add the Drive to the Array

1. Add the new drive to the array using `mdadm`.

```
# mdadm /dev/md127 --add /dev/sdc
```

`mdadm --detail /dev/md127` will show that *sdc* was added as a spare.

### Fail a RAID Drive

The `mdadm` command can simulate the failure of a drive.

```
# mdadm /dev/md127 --fail /dev/sda
```

The `mdadm --detail /dev/md127` command shows the array is recovering and that there is one faulty device and no spares.

Open `mutt` and root will have mail reporting the event.

## Removing the Faulty Drive

Remove the failed drive.

```
# mdadm /dev/md127 --remove /dev/sda
```

The RAID array will be healthy but lacking a spare drive.

## Troubleshoot the Assignment

 - If mutt complains that `/var/spool/mail/root` does not exist you can create the file with the `touch` command.
 - If networking isn't active `dhclient -v` will start it.

## What to Submit

Submit a screenshot of the email from mdadm monitoring.

## Resources

- [Redundant Array of Independent Disks (RAID)](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/ch-raid.html)
- [How to repair a software RAID5 volume with more than one failed disk](http://wiki.centos.org/TipsAndTricks/Repair_RAID5_Volumes)
- [RAID and LVM (The Debian Handbook)](http://debian-handbook.info/browse/stable/advanced-administration.html)
- [What is RAID](https://www.youtube.com/watch?v=wTcxRObq738)

> Written with [StackEdit](https://stackedit.io/).