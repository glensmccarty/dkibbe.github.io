![links-1][]

# Links: Hard and Soft

The `ln` command is used to create links or shortcuts between files.

## Linux File Types

When files are listed with `ls -l` the first character indicates what type a file is.

![links-2][]

There are seven basic types of file types in Linux.

| Symbol    | File Type       |
|-----------|-----------------|
| \- (dash) | Ordinary file   |
| d         | Directory       |
| l         | Symbolic Link   |
| c         | Character Device|
| b         | Block device    |
| s         | Local socket    |
| p         | Named pipe      |

The `ls` command is used to show information about a file.

	$ touch foo
	$	 ls -l foo
	-rwxrwxr-x 1 ubuntu ubuntu 0 Feb 13 2012 foo

The listing shows:

- File type (-, d-, l, etc.)
- User, Group, Other permissions
- User ID and Group ID
- Link counter
- Size in bytes
- Date last modified
- File name
  
# Inode

  An inode points to where the data is on disk.

	$ ls -il foo
	16914416 -rwxrwxr-x 1 ubuntu ubuntu 0 Feb 13 2012 foo

As long as there is at least one pointer to the inode of a file the file is still accessible. When the pointer counter is zero the data is still there but the file is not accessible.

The inode of the symbolic link is different from the file it points to. If the original file is deleted the link is broken.

	$ ls -il /media/Debian/README.txt
	1355 -r--r--r-- 1 dennisk dennisk 5512 Jun 15 16:06 /media/Debian/README.txt

# The `ln` command

Files with multiple pointers have multiple hard links to the same data.

The `ln` or link command is used to create multiple pointers to the data.

	$ ls -il foo
	16914416 -rwxrwxr-x 1 ubuntu ubuntu 0 Feb 13 2012 foo

$ ln foo foobar

$ ls -il foobar*
16914416 -rwxrwxr-x 2 ubuntu ubuntu 0 Feb 13  2012 foobar
16914416 -rwxrwxr-x 2 ubuntu ubuntu 0 Feb 13  2012 foo

## Symbolic Links

![Diagram showing soft file link] [links-3]

Symbolic or soft links can span file systems and can link to directories. Hard links can not.

	$ ln -s /media/Debian/README.txt /home/dennisk
	$ ls -il README.txt
	16914528 lrwxrwxrwx 1 dennisk dennisk 38 Oct  2 13:53 README.txt -> /media/Debian 7.1.0 amd64 1/README.txt

## Hard Links

![Diagram showing hard file link] [links-4]

Either file name can be deleted and the data will still be accessible.

	$ ls -il foobar*
	16914416 -rwxrwxr-x 2 ubuntu ubuntu 401 Feb 13 2012 foobar
	16914416 -rwxrwxr-x 2 ubuntu ubuntu 401 Feb 13 2012 foo

$ rm foo
$ ls -il foobar
16914416 -rwxrwxr-x 1 ubuntu ubuntu 401 Feb 13 2012 foobar

### Hard Links Limitations

Hard links can not be made across file systems or to directories.

	$ ln /media/Debian/README.txt /home/dennisk
	ln: failed to create hard link 
	./README.txt => /media/Debian/README.txt: Invalid cross-device link

$ ls -il /media/Debian/README.txt
1355 -r--r--r-- 1 dennisk dennisk 5512 Jun 15 16:06 /media/Debian/README.txt

### Hard Links and Backups
 
The files in blue are unchanged so a hard link in used to save disk space.
 
 ![Diagram showing hard file link used for backups] [links-5]

## What to Submit

Change to the `/tmp` directory and create a file named `foo` with the `touch` command. Link `foobar` symbolically to `foo` and link `foo2` as a hard link to `foo`. Submit a screenshot of the `ls -li foo*` command showing that the inodes of `foo` and `foo2` are the same and that `foobar` is linked to `foo` and the inode numbers are not the same.

# Resources

- [Speaking UNIX: It is all about the inode](http://www.ibm.com/developerworks/aix/library/au-speakingunix14/ "Speaking UNIX: It is all about the inode")

- [What’s an inode?](http://www.linux-mag.com/id/8658/ "What is an inode?")
  
  <!-- Links -->
  
  [links-1]:http://dennisk.freeshell.org/img/cis126dl_links-1.png "Chain icon"
  [links-2]:http://dennisk.freeshell.org/img/cis126dl_links-2.png "Listing of ls showing file type"
  [links-3]: http://dennisk.freeshell.org/img/cis126dl_links-3.png "soft link"
  [links-4]: http://dennisk.freeshell.org/img/cis126dl_links-4.png "hard link"
  [links-5]: http://dennisk.freeshell.org/img/cis126dl_links-5.png "Using hard links for backup"


> Written with [StackEdit](https://stackedit.io/).<!--se_discussion_list:{"TPUII4PDW3buDdymUzoAv726":{"selectionStart":2860,"selectionEnd":2886,"commentList":[{"content":"This is confusing."}],"discussionIndex":"TPUII4PDW3buDdymUzoAv726"}}-->