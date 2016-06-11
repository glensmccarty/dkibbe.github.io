# Vi Text Editor

## Overview

Learning to use a command line text editor in Linux is an important skill every system administration must have. Linux and UNIX both use plain text files for system configuration and a system administrator needs an efficient tool for editing text files. The `vi` text editor (or `vim` for *vi improved*) is such a tool and can be found in one form or another on any Linux system. In fact, it may be the only text editor you have access to.

In this assignment you will create a paper cheat sheet for the `vi` editor that you will hand in for grading.

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:*

1. Explain the advantages of plain text configuration files.
1. Open a text file in vi or vim (vi improved).
1. Navigate a text file in the Command mode.
1. Use the Edit mode to make changes to the file.
1. Use search to find words in the file.
1. Use replace to replace a single word or all the words that match the term.
1. Save the changes to the file and exit.
1. Exit vi without saving any changes.
1. Save the file under a new name.

## Terms You Should Know

- **ASCII** - Plain unformatted text.
- `vi` - The vi text editor. On some system vi may link to vim.
- `vim` - VI Improved
- vimtutor - Vim Tutor opens a sample file to edit.
- Emacs - The text editor created by Richard Stallman – a popular alternative to vi.
- nano - A light-weight text editor found on many system. A free implementation of the `pico` text editor.
- Command Mode - In vi this mode is used for navigation. You can return to the command or normal mode at any time by pressing the `Esc` key.
- Edit Mode - In vi this mode is used for editing text.
- git - A popular version control system created by Linus Torvalds.

## Preparation

This assignment requires pencil or pen and paper (yes, old school). I'll have graph paper available but you should have a pen or pencil – several color would be great.

## Install `vim` (vi improved)

### On Ubuntu

	$ sudo apt-get install vim

### On CentOS

	# yum install vim

## Why Text Files And Not A Binary Registry?

Using plain text files for system configuration has several advantages over using a database such as the Windows' registry to store configuration parameters. Some of the advantages are:

- No special tool is needed to edit the files any text editor will work.
- Comments and instructions can be included in the configuration file itself. (The hash or # symbol is usually used to mark these.)
- Text files can be easily backed up with the `cp` (copy) command or placed under version control.
- Version control makes it easy to document changes and undo changes if needed.
- Using the `diff` command to compare a modified file with the original makes it easy to spot mistakes and acts as a reminder of what changes were made.
- Since separate files are used for each program file sizes are small.

Many programs store system-wide configuration files in the `/etc/` directory and also let normal users have a customized configuration file in their home directory. *Example:* The nano text editor has a sample configuration file in `/usr/share/doc/nano/examples/` that you can copy to your home directory and modify.

## Vi Cheat Sheet

See the cheat sheet link under *Resources* for instructions. You will need a text file that is longer than one screen to work with. You can copy `/usr/share/doc/bash/copyright` to your home directory for that purpose.

	$ cd
	$ cp /usr/share/doc/bash/copyright .

Notice the period at the end of the command. It means copy to the current directory. The `cd` command made sure you ran the command from your home directory

## What to Submit

Hand in your paper cheat sheet for grading. Your sheet should include all the commands found on the example cheat sheet for full credit. The cheat sheet will be returned to you so you can use it in class.

<!--## XKCD

![http://imgs.xkcd.com/comics/real_programmers.png](http://imgs.xkcd.com/comics/real_programmers.png)-->

## Resources

- [VIM home page](http://www.vim.org/)
- [Vim Cheat Sheet Method](http://www.ibm.com/developerworks/linux/tutorials/l-vi/)