![tar-1][]

# Archiving and Compressing Data

## Introduction

The `tar` command was originally designed for backing up data to tape. While it is still used for that purpose it is more commonly used to create a "tarball", that is an archive of files.

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:*

 1. Create a Tar archive with and without compression.
 2. Extract files from a Tar archive.
 3. List files in a Tar archive.
 4. Use Gzip and Bzip2 to compress files.
 5. Use the `find` command to create an archive or specific files.
 5. Identify the advantages of Xz compression.

## Useful Terms

 - TAR (Tape Archive)
 - Gzip
 - Bzip2
 - Xz
 - Zip
 - Archive
 - Compression
 - Tarball
 - `find`
 - `xargs`
 - `file`

## Preparation

TThis assignment will work on most Linux distributions.

### Reading

Archiving data is covered in chapter 8 of the textbook. There is a man page for `tar` and an info page for both `tar` and `find`.

### Create Files

Change to the `/tmp` directory and use the `dd` command to create 5 files each 1MiB in size. This **for loop** will create the files in one step. After typing the first line press **Enter** bash will open a new prompt (**>**) for you to continue the command.

	$ for i in 1 2 3 4 5
	> do dd if=/dev/zero of=foo$i bs=1M count=1
	> done

## Tape Archive (TAR)

### Basic Syntax

The `tar` command uses the same syntax format as most commands. Some options are required and `tar` will complain if they are not given.

	tar option(s) archive_name file_name(s)

Options can be preceded by a single dash (**-**) but it is common to omit the dash.

### Common Options

Some of these options can not be used together. For example **c** and **x**.

| Option | Description |
--- | ---
c | Create archive
x | Extract archive
t | List files in archive
u | Append newer files
r | Add files to archive
d | Compare files in archive to files on disk

### Create an Archive

Create a new archive including all files named *foo*. This command will create an archive of the files you created. By default `tar` does not compress files.

	$ tar cf foo.tar foo*

### List the Contents of an Archive

The **t** option will list the contents of an archive.

	$ tar tf foo.tar
	foo1
	foo2
	foo3
	foo4
	foo5

Adding the **v** gives a more complete listing.

	$ tar tvf foo.tar
	-rw-rw-r-- tux/tux 1048576 10:10 foo1
	-rw-rw-r-- tux/tux 1048576 10:00 foo2
	-rw-rw-r-- tux/tux 1048576 10:00 foo3
	-rw-rw-r-- tux/tux 1048576 10:00 foo4
	-rw-rw-r-- tux/tux 1048576 10:00 foo5

### Extracting Files from an Archive

Delete all the *foo* files in the `/tmp` directory

The question mark is a wildcard character which means *foo* followed by one character.

	$ rm foo?

then restore the files from the archive.

	$ tar xvf foo.tar

#### Extract a Single File

Delete *foo2*.

	$ rm foo2

Now extract just *foo2* from the archive.

	$ tar xf foo.tar foo2
	$ ls foo?
	foo1
	foo2
	foo3
	foo3
	foo4
	foo5

### Updating Files in an Archive

You can append a newer file to the archive. First refresh the timestamp on *foo2*.

	$ touch foo2
	ls -l foo*

*foo2* is newer than the version in the archive.

Compare the files in the archive to those on disk.

	$ tar df foo.tar
	foo2: Mod time differs

Add the newer *foo2* to the archive.

	$ tar uf foo.tar foo2

The newer file is appended to the archive. You can update multiple files the same way.

	$ touch foo1 foo2 foo3
	$ tar uf foo.tar foo1 foo2 foo3

The list option along with the verbose option shows the newer files.

	$ tar tvf foo.tar
	-rw-rw-r-- tux/tux 1048576 10:18 foo1
	-rw-rw-r-- tux/tux 1048576 11:05 foo2
	-rw-rw-r-- tux/tux 1048576 10:34 foo3
	-rw-rw-r-- tux/tux 1048576 10:00 foo4
	-rw-rw-r-- tux/tux 1048576 10:00 foo5
	-rw-rw-r-- tux/tux 1048576 11:24 foo1
	-rw-rw-r-- tux/tux 1048576 11:24 foo2
	-rw-rw-r-- tux/tux 1048576 11:24 foo3

### Using Compression

Option | Compression |
--- | ---
g | Gzip
j | Bzip2
J | xz	

Tar by itself does not compress the files. Listing the files with `ls -lh foo*` shows that the archive is slightly larger that the sum of the individual files.

	$ ls -lh foo*
	-rw-rw-r-- 1 tux/tux 1.0M Nov 14 11:13 foo1
	-rw-rw-r-- 1 tux/tux 1.0M Nov 14 11:24 foo2
	-rw-rw-r-- 1 tux/tux 1.0M Nov 14 11:24 foo3
	-rw-rw-r-- 1 tux/tux 1.0M Nov 14 11:24 foo4
	-rw-rw-r-- 1 tux/tux 1.0M Nov 14 10:00 foo5
	-rw-rw-r-- 1 tux/tux 5.1M Nov 14 11:30 foo.tar

#### Compress an Archive with Gzip

Gzip is a common compression algorithm used with `ar`. Create a new archive with Gzip compression.

	$ tar czf foo.tar.gz foo*

The `tar.gz` extension shows that this is a compressed archive.

	$ ls -lh foo.tar.gz
	-rw-rw-r-- 1 tux tux 5.3K Nov 14 11:37 foo.tar.gz

The degree of compression will depend on the type of files being compressed. Image and sound files which are already compressed will benefit least from compression.

#### Compress an Archive with Bzip2

	$ tar cjf foo.tar.bz2 foo*
	$ ls -lh foo.tar.bz2
		-rw-rw-r-- 1 dennisk dennisk  715 Nov 14 11:42 foo.tar.bz2

## Find and Tar

The `find` comamnd is useful to create an archive from a list of files. Here `find` searchs in `/usr/share/doc/` for all text files and dumps them into a tarball.

	find /usr/share/doc/ -name *.txt | xargs tar cf archive.tar

## Extensions on the Command Line

While it is common to use extensions to make it easy to identify files types. The command line doesn't require it. Try renaming the foo archive to something else  and then run the `file` command find its true identity.

	$ mv foo.tar.gz foo.jpg
	$ file foo.jpg 
	archive.tar.gz: gzip compressed data

## What to Submit

Submit a screenshot showing the output of `tar -tvf foo.tar.gz` showing the contents of the archive.

## Resources

 - man tar
 - info find
 - man file
 - man xargs

[fixme]: http://dennisk.freeshell.org/img/fixme.png "Fix me icon"
[tar-1]: http://dennisk.freeshell.org/img/cis126dl_tar-1.png "file cabinet clipart"

> Written with [StackEdit](https://stackedit.io/).