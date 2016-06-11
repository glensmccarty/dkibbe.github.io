# Extend a LVM Logical Volume

![Logical Volume Management](https://s3.amazonaws.com/CIS238DL/lvm_layout.png)

## Assignment Objectives

An advantage of Logical Volume Management (LVM) is how easy it can be extended.  In this assignment you will extend the `/home` logical volume you created by adding LVM extents.

*When you have successfully completed this assignment you will be able to:*

- Add a second virtual hard drive in VirtualBox.
- Create a LVM Physical Volume (PV).
- Add a PV to a LVM Volume Group (VG).
- Extend a LVM Logical Volume (LV).
- Extend an XFS filesystem.

## Terms and Commands  You Should Know

- **Extents** - LVM divides storage into extents (physical and logical extents)
- **Physical Volume** - LVM physical volume are built on block devices such as a partition or physical disk.
- **Volume Group** - Physical volumes are combined into volumes groups creating a pool of storage.
- **Logical Volume** - Volume Groups are divided into logical volumes.
- `pvcreate` - Creates a LVM Physical Volume.
- `pvdisplay` - Display info for PVs
- `vgdisplay` - Display info for VGs
- `vgextend` - Extend the size of a VG
- `lvdisplay` - Display info for LVs
- `lvextend` - Extend the size of a LV
- `resize2fs` - ext2/ext3/ext4 file system resizer
- xfs_growfs` - XFS resizer

## Preparation

Use the CentOS 7 minimal installation ISO to create a new virtual machine. Do *not* use the CentOS ova.

## Install CentOS 7 with a Custom Layout

Create a virtual machine with the default settings.

![Centos LVM Screenshot](https://s3.amazonaws.com/CIS238DL/img/centos_lvm-1.png)

Set the correct time zone and enable networking

![CentOS LVM screenshot](https://s3.amazonaws.com/CIS238DL/img/centos_lvm-2.png)

Click INSTALLATION DESTINATION and select *I will configure partitioning*

![CentOS LVM screenshot](https://s3.amazonaws.com/CIS238DL/img/centos_lvm-3.png)

Select *Standard Partition*

Make a note of how much space is available

![CentOS LVM screenshot](https://s3.amazonaws.com/CIS238DL/img/centos_lvm-4.png)

Add mount points for:

 - /boot (500MB)
 - / home (1GB)
 - swap (500MB)
 - / (remaining space)

![CentOS LVM screenshot](https://s3.amazonaws.com/CIS238DL/img/centos_lvm-5.png)

Set root, home and swap to *LVM Partition*. Leave `/boot` as XFS.

![CentOS LVM screenshot](https://s3.amazonaws.com/CIS238DL/img/centos_lvm-6.png)

Click *Begin Installation*

![CentOS LVM screenshot](https://s3.amazonaws.com/CIS238DL/img/centos_lvm-7.png)

Set the root password to Pa$$w0rd
![CentOS LVM screenshot](https://s3.amazonaws.com/CIS238DL/img/centos_lvm-8.png)

## Add a Second Virtual Drive to the Virtual Machine

Add a second virtual 1 GiB hard disk to your virtual machine.  You will need to `poweroff` the virtual machine before adding the drive.

Select the SATA controller

![https://s3.amazonaws.com/CIS238DL/vbox-add_storage.png](https://s3.amazonaws.com/CIS238DL/vbox-add_storage.png)

Add a second virtual drive to the SATA controller

![https://s3.amazonaws.com/CIS238DL/vbox-add_storage2.png](https://s3.amazonaws.com/CIS238DL/vbox-add_storage2.png)

## Partition the Drive

Before the drive can be added as a Physical Volume it needs to be partitioned using `fdisk`.

```
# fdisk /dev/sdb
```

Add a new primary partition set to type *Linux LVM (8e)*.
## Create the Physical Volume (PV)

Before you can attach additional storage to the volume group */dev/sdb* must be formatted as an physical volume using `pvcreate`.

```
# pvcreate /dev/sdb
```
	
## Add the Physical Volume to the Volume Group

Use the `vgdisplay` command to display information about the volume group.  Note that there are no free Physical Extents (PE) available.

Now add the physical volume to the volume group.

	# vgextend centos /dev/sdb

Run `vgdisplay` again and you should now have about 255 free extents or 1024 MiB available.

## Extend the logical Volume

Use the `lvextend` command to extent the *home* logical volume.  You can extend using size (MiB, GiB) or extents.  See the `lvextend` man page for examples.  Here we'll add half the available extents.

```
# lvextend -l +125 /dev/centos/home
```

Use `vgdisplay` again to show that there are fewer extents available.

## Extend the /home filesystem

Extending the logical volume isn't enough you also need to extend the filesystem as well.  The `df` command shows that */home* is still 1 GiB. in size.

```
	# df -h
```

Use `xfs_growfs` to extend the XFS filesystem to the full capacity of the logical volume.

```
# xfs_growfs /dev/centos/home
```

## Extend the / file system

Follow the same procedure to extend / by the remaining extents.

## What to Submit

Submit a screen-shot (cropped, of course) of the `df -h` command showing that */home* and */* have been extended.

## Resources

- man lvm
- [Managing Storage with the Linux Logical Volume Manager (LVM)](https://www.youtube.com/watch?v=BysRGDgqtwY)
- [Logical Volume Manager Administration](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6-Beta/html/Logical_Volume_Manager_Administration/index.html)
- [The Debian Administrator's Handbook](http://debian-handbook.info/browse/stable/advanced-administration.html#section.lvm)
- [Extending a LVM Logical Volume](#dennisk.freeshell.org/cis238dl_lvm.html)

> Written with [StackEdit](https://stackedit.io/).