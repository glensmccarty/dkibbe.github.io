# Access Control Lists (ACL)

![Checklist icon][checklist]

## Overview

Traditional Unix/Linux file permissions do not let you narrow permissions beyond UGO.  Access Control Lists let users define finer-grained permissions for files and directories.

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:*

- Remount a filesystem to use ACL. (ext4 only)
- Edit the `/etc/fstab` file to add the ACL option. (ext4 only)
- List ACL permissions for a file.
- Modify ACL permissions for a file.
- Add a group to ACL permissions.

## Terms You Should Know

ACL
: Access Control Lists package

Access ACLs
: Specific to a file or directory

Default ACLs
: Applies to directories only.

`setfacl`
: Sets ACLs for files and directories.

`/var/tmp`
: Unlike the `/tmp` directory

`/var/tmp`
: is not cleared on reboot so it make a good place to put files you want others to see.

`getfacl`
: Get ACLs for files and directories.

`umask`
: file mode creation mask

## Preparation

1.  Import and boot the *centos.ova*.
2.  Networking isn’t needed for this assignment so you don’t need to set bridging in VirtualBox.
3.  Create users *tux*, *jill* and *sam*

## Add Users

Use `useradd` and `passwd` to create three new accounts *tux*, *jill* and *sam*.

## Setup ACL on ext4

### Remounting a Filesystem

*Not needed for CentOS 7*

To use ACL permissions without first rebooting the system you need to remount root with the `acl` option. *note:* Your actual device name may be difference.

    # mount -o remount -o acl /
    /dev/mapper/centos/root on / type ext4 (rw,acl)

### Editing fstab

*Not needed for CentOS 7*

The `/etc/fstab` file defines filesystems mounted on boot and their options.  You need to add the `acl` option to root to use Access Control Lists.  Edit `/etc/fstab` adding the `acl` option after `defaults`.

    /dev/mapper/centos/root / ext4 defaults,acl 1 1

## Modify the ACL Permissions

### Create a File and List its Permissions

Sam wants other users to read *report.txt* and also to allow Tux to add comments to the file.  With ordinary Linux permissions Sam would have to allow all users to write to the file not just Tux.  With Access Control Lists Sam can accomplish his goal.  Sam puts the *report.txt* file in the `/var/tmp` directory so all can read the file and then assigns *read/write* permissions for Tux.

    $ touch /var/tmp/report.txt

The `getfacl` command shows the ACL permissions.

    $ getfacl /var/tmp/report.txt
    # file: var/tmp/report.txt
    # owner: sam
    # group: sam
    user::rw-
    group::rw-
    other::r--

Login as Tux on another terminal and try to edit the file.  `vi` shows that the file is *read-only*.  Close `vi` and return to Sam’s terminal.

### Add Read/Write Permissions

Next Sam will add *read/write* permissions for Tux only.

    $ cd /var/tmp
    $ setfacl -m u:tux:rw report.txt

The `getfacl` command shows the change.

    $ getfacl --omit-header report.txt
    user::rw-
    user::tux;rw-
    group::rw-
    other::r--

The `ls` command shows a plus sign indicating the file has ACL permissions.

    $ ls -l report.txt
    -rw-rw-r--+1 sam Apr 24 report.txt

Have Tux open the file again and this time Tux can edit the file.

Open another terminal and log in as Jill.  Try to edit the *reports.txt* file as Jill.  Jill can’t edit the file.

### Remove ACL Permissions

As user Sam remove Tux from the ACL permissions so he can no longer edit *reports.txt*.

    $ setfacl -x u:tux report.txt

The `getfacl` command shows Tux no longer has write permissions.

### Add a Group to the ACL Permissions

Sam has several users that he would like to comment on the report so he asks the administrator to create the *docmaster* group and add both Jill and Tux to the group.

    # groupadd docmaster && usermod -aG docmaster tux && usermod -aG docmaster jill
    # grep docmaster /etc/group
    docmaster:506:x:tux,jill

Now Sam modifies *reports.txt* to allow members of the *docmaster* group to edit the file.

    $ setfacl -m g:docmaster:rw report.txt

Sam uses the `getfacl` command to confirm the change.

    $ getfacl --omit-header /var/tmp/report.txt
    user::rw-
    group::rw-
    group::docmaster:rw-
    mask::rwx
    other::r--

### Applications and ACL

Not all applications support Access Control Lists.

## What to Submit

After completing the assignment submit a screenshot of `getfacl` showing that the *docmaster* group has *rw-* permissions to *report.txt*.

## Resources

- man acl
- man getfacl
- man setfacl
- [Access Control Lists in Linux][acl-2]

[checklist]: http://dennisk.freeshell.org/img/checklist.png "Checklist icon"
[acl-2]: https://doc.opensuse.org/documentation/html/openSUSE_113/opensuse-security/cha.security.acls.html "Access Control Lists in Linux"

> Written with [StackEdit](https://stackedit.io/).