
## Scenario

As a new system administrator you need to confirm that the company password policy is being correctly implemented. Settings such as when passwords need to be renewed and the umask value are contained in `/etc/login.defs`. See the man page for this file for a complete list.

## Read the File

`/etc/login.defs` can be read with the `less` command.

## Filtering out comments

Each line that starts with the hashtag character **#** is a comment line and is lot acted on. Lets filter out those lines to make the output easier to read.

	$ grep -Ev '^#' /etc/login.defs

The `grep` command is widely search files to fins a matching string. This command

	$ grep Debian /usr/share/doc/bash/copyright
	
will find all the instances of Debian in the copyright file and print the output to STDOUT. Note that the `grep` command is case sensitive and the output will be different using the term *debian.* Adding the **-i** option makes the search case-insensitive.

	$ grep -E '^#' /etc/login.defs

Will find all the lines that start with the hashtag. The search can be inverted to find only lines that do not start with the # character with the **-v** option.

	$ grep -Ev '^#' /etc/login.defs

## Finding Blank Lines

The output of our previous command still takes up more that one screen. Let's remove the blank lines from the output as well. This command will find blank lines; that is lines that have no characters between the beginning **^** and end **$** of the line.

	$ grep -E '^$' /etc/login.defs

## Combining the Filters

To get the results we want we need a logical **or** to tell `greg` that we want to remove lines that start with **#** and blank lines from the output. **|** does that.

	$ grep -Ev '^#|^$' /etc/login.defs

## Putting the Filter in a Script

	#!/usr/bin/env bash
	# Script to remove comments and blank lines
	grep -Ev '^#|^$' /etc/login.defs
	# END
## Positional Parameters

To make our script more versatile we can use a positional parameter to pass a file name to the script.
	
	#!/usr/bin/env bash
		# Script to remove comments and blank lines. First test if a positional parameter is given and exit with an exit value of 1 if it isn't.
	if 
	[[ $# -eq 0 ]]
	then
	echo "You need to give a file name."
	exit 1
	else
	grep -Ev '^#|^$' $1
	fi
	# END

## Showing the Exit Value

Whenever a program is run it returns to the shell an exit value. an exit value of 1 equals success and any other equals failure. You can show for an exit value with the `echo` command. Try this example:

	$ ls /tmp
	<returns a listing of files>
	$ echo $?
	0
	$ ls /temp
	File or directory does not exist.
	$ echo $?
	2
	
> Written with [StackEdit](https://stackedit.io/).