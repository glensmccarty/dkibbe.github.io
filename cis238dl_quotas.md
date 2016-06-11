# XFS Disk Quotas

Disk quotas limit how much space on a partition users can consume. The XFS file system expands the concept of quotas to include:

 - Users
 - Groups
 - Projects

## Assignment Objectives

In this assignment you will enable and configure quotes on a XFS filesystem.

*After successfully completing this assignment you will be able to:*

 1. Enable quotas as a kernel option.
 2. Set hard and soft limits.
 3. Display current quota settings.
 4. Demonstrate how quotas limit a user's ability to hog disk space.

## Terms You Should Know

 - xfs_quota (basic mode)
 - xfs_quota (expert mode)
 - Soft limits
 - Hard limits
 - xfs_info
 - grub2_mkconfig
 - /etc/fstab

## Preparation

Follow the instruction in the [Extend an LVM Logical Volume](https://dkibbe.github.io/cis238dl_lvm.html) assignment to create a CentOS 7 virtual machine with a separate 1 GiB logical volume mounted on `/home`. During install create a user account.

When the system reboots use `df` to confirm that `/home` is on a separate partition and is approximately 1 GiB.

## Enable Quotas

By default quotas are not enabled. The `mount` command shows:

	# mount | grep ' / '
/dev/mapper/centos-root on / type xfs (rw,relatime,attr2,inode64,noquota)

To enable quotas at boot the `/etc/fstab` file must be edited and a kernel option must be added to the GRUB defaults.

### Edit /etc/fstab

Add uquota,pquota to the `/home` entry following defaults.

	defaults,uquota,pquota

### Add Quotas to GRUB

Open `/etc/defaults/grub` and append to the line that starts with `GRUB_CMDLINE_LINUX=` the following:

	 rootflags=uquota,pquota

This will add quotas for users and projects

Now backup and generate a new `grub.cfg`.

	# cp /boot/grub2/grub.cfg /root/grub.cfg.orig
	# grub2-mkconfig -o /boot/grub2/grub.cfg

Reboot the system to make the changes effective. After the system reboots use the `xfs_quota` command to confirm that quotas are now active /home.

	# xfs_quota
	> print
	
![quotas-7][]

## Set Quotas for a User

### Display Current Quota Settings

Use `xfs_quota` to display the current quotas. the **-x** option sets the Expert mode which allows changing the settings.

	# xfs_quota -x /home
	> report

![quotas-5][]

There are no quotas set yet for user *tux*.

### Set Quotas for a User

Here we'll set a hard and soft quota limit for our user. The user will be able to exceed the soft limit for a short period but not the hard limit. the help screen for limit has a example.

	# xfs_quota -x /home
	> help limit

Run report again to display the new settings.

![quotas-4][]

### Set Quotas for Groups

![fixme][]

### Set Quotas for Projects

![fixme][]

### Set the Grace Period for Soft Limits

The manpage says that this is not implemented yet but it does appear to work.

![fixme][]

### Quote Enforcement

Quotas can be set to non-enforcing and used just to monitor disk space.

![fixme][]

## Test Quotas

Login as your user. Here user *tux*.

	# su -l tux

Run `xfs_quota` and type **print** to show that only a few blocks are being used.

###Create a 50 MiB Test File

	$ dd if=/dev/zero of=TestFile bs=50M count=1

Check the quota and note that block usage has increased.

Run the `dd` command again and increase the count.

	$ dd if=/dev/zero of=TestFile bs=50M count=2

This time checking the quota shows that the soft limit has been exceeded.

The third time the hard limit has been exceeded and even a small file can not be created.

	$ dd if=/dev/zero of=TestFile1 bs=1M count=1
	dd: failed to open 'testFile1': Disk quota exceeded.
	
## What to Submit

Submit a screenshot showing that your user has exceeded the quota limit.

![quotas-8][]

## Resources

- [Storage Administration Guide][quotas-9]
- [Setting up quotas on an XFS partition][quotas-10]
- [Manpage for xfs_quotas][quotas-11]
- [XFS Users Guide][quotas-12]

[fixme]: http://dennisk.freeshell.org/img/fixme.png "Fix me icon"
[quotas-4]: http://dennisk.freeshell.org/img/cis238dl_quotas-5.png "Screenshot of xfs_quota/"
[quotas-5]: http://dennisk.freeshell.org/img/cis238dl_quotas-5.png "Screenshot of xfs_quota/"
[quotas-6]: http://dennisk.freeshell.org/img/cis238dl_quotas-6.png) "Screenshot of xfs_quota/report"
[quotas-7]: http://dennisk.freeshell.org/img/cis238dl_quotas-7.png "Screenshot of xfs_quota/print"
[quotas-8]: http://dennisk.freeshell.org/img/cis238dl_quotas-8.png "Screeshot of sample submission"
[quotas-9]: https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/xfsquota.html "RHEL Storage Admin Guide"
[quotas-10]: http://help.directadmin.com/item.php?id=557 "Setting up quotas on an XFS partition"
[quotas-11]: http://linux.die.net/man/8/xfs_quota "Manpage for xfs_quotas"
[quotas-12]: http://xfs.org/docs/xfsdocs-xml-dev/XFS_User_Guide/tmp/en-US/html/index.html "XFS Users Guide"

> Written with [StackEdit](https://stackedit.io/).