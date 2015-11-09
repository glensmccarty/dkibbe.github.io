# Links: Hard and Soft

## Linux File Types

There are seven basic types of file types in Linux.

| Symbol    | File Type       |
|-----------|-----------------|
| -- (dash) | Ordinaly file   |
| d         | Directory       |
| l         | Symbolic Link   |
| c         | Character Device|
| b         | Block device    |
| s         | Local socket    |
| p         | Named pipe      |

The `ls` command is used to show information about a file.

```
$ ls -l cpuhog.sh
-rwxrwxr-x 1 dennisk dennisk 401 Feb 13 2012 cpuhog.sh
```

- File type (-, d-, l, etc.)
- User, Group, Other permissions
- User ID and Group ID
- Link counter
- Size in bytes
- Date last modified
- File name
  
# Inode

  An inode points to where the data is on disk.

```
$ ls -il cpuhog.sh
16914416 -rwxrwxr-x 1 dennisk dennisk 401 Feb 13 2012 cpuhog.sh
```

As long as there is at least one pointer to the inode of a file the file still exist. When the pointer counter is zero the data is still there but the file is not accessible.

The inode of the symbolic link is different from the file it points to. If the original file is deleted the link is broken.

```
$ ls -il /media/Debian/README.txt
1355 -r--r--r-- 1 dennisk dennisk 5512 Jun 15 16:06 /media/Debian/README.txt
```

# The `ln` command

Files with multiple pointers have multiple hard links to the same data.

The `ln` or link command creates multiple pointer to the data.

```
$ ls -il cpuhog.sh
16914416 -rwxrwxr-x 1 dennisk dennisk 401 Feb 13 2012 cpuhog.sh

$ ln cpuhog.sh cpuhog

$ ls -il cpuhog*
16914416 -rwxrwxr-x 2 dennisk dennisk 401 Feb 13  2012 cpuhog
16914416 -rwxrwxr-x 2 dennisk dennisk 401 Feb 13  2012 cpuhog.sh
```
## Symbolic Links

![Diagram showing soft file link] [link-soft]

Symbolic or Soft links can span file systems and can link to directories.

```
$ ln -s /media/Debian/README.txt /home/dennisk
$ ls -il README.txt
16914528 lrwxrwxrwx 1 dennisk dennisk 38 Oct  2 13:53 README.txt -> /media/Debian 7.1.0 amd64 1/README.txt
```

## Hard Links

![Diagram showing hard file link] [link-hard]

Either file name can be deleted and the data will still be accessible.

```
$ ls -il cpuhog*
16914416 -rwxrwxr-x 2 dennisk dennisk 401 Feb 13 2012 cpuhog
16914416 -rwxrwxr-x 2 dennisk dennisk 401 Feb 13 2012 cpuhog.sh

$ rm cpuhog.sh
$ ls -il cpuhog
16914416 -rwxrwxr-x 1 dennisk dennisk 401 Feb 13 2012 cpuhog
```
### Hard Links Limitations

Hard links can not be made across file systems or to directories.

```
$ ln /media/Debian/README.txt /home/dennisk
ln: failed to create hard link 
./README.txt => /media/Debian/README.txt: Invalid cross-device link

$ ls -il /media/Debian/README.txt
1355 -r--r--r-- 1 dennisk dennisk 5512 Jun 15 16:06 /media/Debian/README.txt
```
### Hard Links and Backups
 
The files in blue are unchanged so a hard link in used to save disk space.
 
 ![Diagram showing hard file link used for backups] [link-backup]

# Resources

- [Speaking UNIX: It is all about the inode](http://www.ibm.com/developerworks/aix/library/au-speakingunix14/ "Speaking UNIX: It is all about the inode")

- [What’s an inode?](http://www.linux-mag.com/id/8658/ "What is an inode?")
  
  <!-- Links -->
  
  [link-soft]: https://s3.amazonaws.com/CIS126DL/Images/link-soft.png "soft link"
  [link-hard]: https://s3.amazonaws.com/CIS126DL/Images/link-hard.png "hard link"
  [link-backup]: https://s3.amazonaws.com/CIS126DL/Images/link-backup.png "Using hard links for backup"


> Written with [StackEdit](https://stackedit.io/).