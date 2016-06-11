# Bash Config Files

## Overview

In this assignment you will work with two Bash configuration files in your home directory.  ~/.profile is the main Bash configuration script and is run when first logging into a terminal or when opening a Bash login shell using `bash -l`. The ~/.bashrc file is executed when opening a new Bash shell. 

*Tested on Ubuntu 14.01.1 LTS*

## Terms You Should Know

 - `~/.profile`
 - `~/.bash_profile`
 - `~/.bashrc`
 - `~/.bash_login`
 - `~/.bash_logout`
 - `~/.bash_history`
 - Nano text editor
 - `Hidden "dot" files
 - `bash`
 - `history`
 - `env`
 - `exit`
 - `ls -a`

## Preparation

Do this assignment on the Ubuntu LiveCD or from a guest session. Click the gear icon in the upper right corner of the desktop and select Guest Session, a new Guest Session will open.

If you do this assignment in your home directory make backup copies of `~/.profile` , `~/.bashrc` and `.bash_logout` before continuing. 

	$ cp .profile profile.bak
	cp .bashrc. bashrc.bak
	$ cp .bash_logout bash_logout.bak
	
Clear the Bash history with `history -c` before starting.

### Edit ~/.bashrc

Click on the Dash search icon in the upper left corner of the desktop and type *terminal* to bring up the bash shell.  Open `~/.bashrc` with the Nano text editor.

	$ nano .bashrc

Scroll to the bottom of the file and after the last line press Enter and type `echo "This line from .bashrc. The time is $(date +%R) and you are logged into $(hostname)."`

The `$(date +%R)` will be replaced by the current time.

Press **Ctrl+O** to save the changes and **Ctrl+X** to exit Nano.

### Edit ~/.profile

Open `~/.profile` in Nano and scroll to the bottom of the file.
After the last line press **Enter** and type `echo "This line is from .profile."`

### Edit ~/.bash_logout

Open `~/.bash_logout` scroll to the last; press **Enter** and type `echo "The time is now $(date +%R), goodbye."` Save the changes to the file. Exit Nano.

## Start Assignment

### ~/.bashrc

1. Click on Dash and type *terminal*. Select the Terminal icon to open the GNOME Terminal.
2. Observe that the line from `.bashrc.` shows above the prompt. Only the `.bashrc` file is sourced when an interactive shell is opened.
3. Leave the Terminal open for the next step.

### ~/.profile

1. At the terminal prompt type `bash -l` to open a new login session.
2. Observe that both the line from `.bashrc` and `.profile` appear above the prompt. The `.bashrc` file is sourced from  `.profile`.
3. Leave the Terminal open for the next step.

### ~/.bash_logout

1. Type `exit` to close the login shell and return to the previous shell.
2. Observer that the line from `.bash_logout` displays on the screen.
3. Type `exit` or **CTRL+D** as many times as needed to logout of the terminal.

## Quick nano Tutorial

![nano tutorial](http://classfiles.dennisk.fastmail.net/nano_tutorial.png)

## What to Submit

Submit a screenshot of the Terminal showing the line from the `.bashrc_logout` file.

## Resources

 - man bash
 - [The Urban Penguin](http://theurbanpenguin.com/wp/?p=3011)
 - [How to master Ubuntu's Unity Desktop](http://www.howtogeek.com/113330/how-to-master-ubuntus-unity-desktop-8-things-you-need-to-know/)
 - [Bash Reference Manual - Start Up Files](https://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files.html)

> Written with [StackEdit](https://stackedit.io/).