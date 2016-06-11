# Create a Command Aliases

## Overview

Command aliases and Bash functions which we'll look at under scripting let a Linux system administrator create custom commands. In this assignment you will create a custom aliasfor the `ping` command.

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:*

1. Determine a command type using the `type` command.
2. Use the `alias` command to create a new alias.
3. Use the `unalias` command to remove an alias.
5. Make aliases permanent by adding them to `~/.bashrc` or `~/.bash_aliases`.

## Terms You Should Know

`type`
:  Shows what type a command is -- alias, shell builtin or stand alone.

`alias`
: Used to create a command alias or show all aliases.

 `unalias`
 : Removes an alias
 
`~/.bash_aliases`
: Commands in this file will be sourced (included in) by the `~/.bashrc` file.

Dot files
: hidden files and directories that start with a peroid.

`ls`
: List files

`ping`
: Send an ICMP ECHO\_REQUEST (Are you there?) packet to a network host and record whether an ICMP ECHO\_RESPONSE (Yes, I'm here.) packet was received back.

## Preparation

Tested on Ubuntu 14.04 and CentOS 7

## Scenario

You are a system administration who works on both Windows and Linux servers. You want to create an command alias for the `ping` command so it works the same way on both servers. That is, ping a web site four times then stop.

## Using the `type` Command

When you type the `ls` command you are actually running this alias:

	$ type ls
	ls is aliased to `ls --color=auto'

The `type` command shows that the `ls` you type is actually an alias. The `--color=auto` option to `ls` displays files, directories, links and executables in different colors.

## Using the `unalias` Command

The color option on a dark background sometimes makes directories very hard to see. Let's remove the color option with the `unalias` command. Using Tab completion you only need to type the first three letters of `unalias` the command.

	$ unalias ls

The `type` command now shows that `ls` has no options when you run the command.

$ type ls
ls is /bin/ls

## Using the `alias` Command

Without the color option it is hard to tell whether a file is an ordinary file, a directory, an executable or a link so we'll use `alias` to map `ls` to `ls -F` which will add an indicator to each file type (See the table below). Be sure to include the quote marks in the command so the shell treats the space character correctly.

| Indicator | Type of File|
| --------- | ----------- |
| none | ordinary file |
| slash (/) | directory |
| at (@) | symbolic link |
| asterisk (*) | executable |

Here us a sample output.

	$ alias ls="ls -F"
	$ ls /home/jstudent/
	Desktop/ Documents/ Downloads/ Music/ /Videos
	some-link@ some-file.txt some-script.sh*

The new alias isn't permanent and will disappear when the current shell closes. To make the alias permanent add it to the `.bashrc` or a hidden `.bash_aliases` file in your home directory. The `.bash_aliases` may not exist but you can create it using the `nano` or `vi` text editor. Using a separate file is safer than editing `.bashrc` and makes your customizations more portable.

Here is a sample `.bash_aliases` file.

	alias ls='ls -F'
	alias ll='l -lh'
	alias du=`du -sh * | sort -nr'

## Removing an Alias

To temporarily run a command without the alias use **\** before the command.

	$ \ls

## Troubleshoot the Assignment

1. Files that start with a period like `.bashrc` are hidden from the `ls` command unless you use the `-a` option.
2. Don't forget the quotes around `ls -F` they are required because of the space character.

## What to Submit

Submit a screenshot of the `.bash_alias` you created showing the alias you created for the `ping` command so it functions the same on Linux as on Windows.

## Resources

- [An Introduction to Useful Bash Aliases and Functions][intro]
- [The very complete BSD `ls` manpage][ls]
- [Sample bash_alias file][sample]

<!-- links -->
[intro]: https://www.digitalocean.com/community/tutorials/an-introduction-to-useful-bash-aliases-and-functions "An Introduction to Useful Bash Aliases and Functions"
[id]: http://example.com/  "Optional Title Here"
[ls]: http://www.freebsd.org/cgi/man.cgi%3Fquery%3Dls "BSD ls manpage"
[sample]: http://www.codeuniversity.com/templates/bash_alias "sample bash_alias file"
[fixme]: https://s3.amazonaws.com/CIS126DL/Images/fixme.png "Fix me clipart"


> Written with [StackEdit](https://stackedit.io/).