# Partitioning a Disk

## Introduction

Before a new hard disk can be used it must be partitioned and formatted. In this assignment you will create a new virtual disk in VirtualBox and then partition, format and mount it for use. First using a graphical tool and then the command line.

### Drive Letters

Unlike Windows Linux hides the drive letters of storage devices. Hard drives and removable drives are always mounted under directories that are, for the most part, consistent between Linux distributions. The diagram below shows a single SATA hard drive (shown in blue) with two partitions mounted under the device or */dev* directory.  The device name is */dev/sda* and the partitions are */dev/sda1* and */dev/sda2*.

![Linux file system](http://dennisk.fastmail.net/gallery/cis126dl_fsh-1.png)

## Terms You Should Know

- **Partition**
- **mount**
- **umount**
- **fdisk**
- **IDE**
- **SATA**
- **/etc/fstab**
- **gdisk**

## Preparation

Import the Ubuntu 14.04 LTS appliance (ova) into VirtualBox but do not start the virtual machine.

### Add a Virtual Disk

Open the Storage Settings for the Ubuntu virtual machine and add a new virtual disk to the SATA controller using the default settings except make the disk 1GB in size.

*Note:* The virtual machine must not be running to attach a new drive.

![VirtualBox Storage settings](http://dennisk.fastmail.net/gallery/vbox_fdisk-1.png)

After the drive has been added you should see it listed under the SATA controller. Once the drive is added you can boot the virtual machine.

![VirtualBox Storage dialog box](http://dennisk.fastmail.net/gallery/vbox_fdisk-2.png)

*Note:* To do the `fdisk`section you will need to add  a second virtual disk with a new name or remove the one formated with **Disks** with [Virtual Media Manager]
(https://www.virtualbox.org/manual/ch05.html#vdis) under the File menu.


## Using Disks

**Disks** is the graphical program for adding and removing partitions on disks, as well as formatting the disk. Click the Dash which is the first icon on the launcher and type *disk* to find disk related utilities.

![Disks](http://dennisk.fastmail.net/gallery/vbox_fdisk-3.png)

Once **Disks** is open select the correct drive and click the gear symbol below **Volumes** to format it. Choose **FAT** under type and click **Format...** That's it. The new drive is ready to use.

![enter image description here](http://dennisk.fastmail.net/gallery/vbox_fdisk-5.png)

## Using `fdisk`

`fdisk` is the command line tool for working with disk partition tables. With `fdisk` you create and remove partitions and change a partition's type.

Click on the Dash and type *term* to find the GNOME terminal which is the first terminal listed. If you can press **Ctrl++** (Control key and the plus sign) to increase the font size or **Ctrl+-** (Control key and the minus sign) to reduced the font size. You can also use the menu on the Taskbar at the top of the screen to set different font and background colors.

## Listing Attached Disks

From a terminal type `sudo fdisk -l`. This will list the drives attached to the virtual machine. Notice that */dev/sdb* doesn't have a partition table yet.

Type **q** to quit `fdisk`.

### Create the Partition Table

Use the up arrow on the keyboard to recall the `fdisk` command and replace the **-l** with **/dev/sdb** so you can create a partition table on the drive. Be sure to use `sudo` since you need to run the command with root privileges.

You can type **m** in `fdisk` to view a menu of options.

To create a new partition type **n** and accept the defaults by pressing **Enter** each time.

When done type **p** to "print" the partition table.

### Change the Partition Type

Next you will change the partition type from Linux (83) to W95 FAT32 (b).

Type **t** to change the partition type and **l** to show a long list of partition types. Press **b** to select W95 FAT32.

Type **p** again to show that the partition type has been changed to W95 FAT32.

Type **w** to write changes and sychronise the disks.

## Format the disk

The disk isn't useable until formated with a filesystem. N ow you will use the **mkfs** command to create a **VFAT** filesystem.

Type *sudo mkfs* followed by pressing the Tab key twice to see a list of possible completions. Type **v** then Tab to complete the selection.

	$ sudo mkfs.vfat /dev/sdb1

As soon as the partition is formatted it is detected by the kernel and mounted temporarily under */media/tux/*. Typing `mount` at the command line will show that */dev/sdb* is mounted. The device will show in the **Files** file manager as well.

## Create the Mount Point

Unmount the device so you can mount it under the */mnt/* directory.  (notice that the *n* is missing.)

	$ umount /dev/sdb1

Our new drive needs to be mounted to be available to use. */dev/mnt* is a good place to do that. First you'll make a directory under */dev/mnt* than mount the filesystem on that directory.

	$ sudo mkdir /mnt/data

	$ sudo mount /dev/sdb1 /mnt/data

The `mount` command now shows that */dev/sdb1* is mounted on */mnt/data* with read/write permissions.

![mnt mount point](http://dennisk.fastmail.net/gallery/cis126dl_fsh-mnt.png)

## Unmounting the Filesystem

Unmounting a filesystem removes it from use and makes the data unavailable.

	$ umount /mnt/data

## Removable Media

Removable filesystems such as CDs and Flash drive are mounted automatically by the kernel on */media/\$USER/device_name* or */run/media/\$USER/device_name*. Where $USER is the user login name and *device_name* is the label for the device being mounted.

![enter image description here](http://dennisk.fastmail.net/gallery/cis126dl_media.png)

## Resources

 - [GUID Partition Type](https://en.wikipedia.org/wiki/GUID_Partition_Table)
 - [MBR Boot Record](https://en.wikipedia.org/wiki/Master_boot_record)

> Written with [StackEdit](https://stackedit.io/).