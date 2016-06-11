## Using `su` and `sudo` to Get Work Done as Root

Both `su` and `sudo` can be used to work as the root user. Some distributions like Ubuntu disable the root account by default and all work is done using the `sudo` command. Even on distributions like Red Hat Enterprise Linux and CentOS `sudo` can be used to delegate root privileges to ordinary users. `sudo` is similar to *run as* on Windows.

##Assignment Objectives

*After successfully completing this assignment you will be able to:* 

1.  Use the `su` command to log in as the root user.
2. Create a user and add that user to a group
2.  Explain the value of the -l (dash el) option to `su`.
3.  List the advantages of using `sudo` over `su`.
4.  Modify the `/etc/sudoers` file using `visudo`.
5.  Give a user `sudo` permissions by adding a file to the `/etc/sudoers.d` directory.
6.  Describe where Sudo "incidents" are reported.

## Preparation

Do this assignment on the CentOS 7 virtual machine. In the commands used below the **#** character is the root user prompt and **$** is the prompt for ordinary users.

### Take a Snapshot of the System

See the [instructions](https://www.virtualbox.org/manual/ch01.html#snapshots) in the VirtualBox Users Manual.

### Install Mutt

Mutt is a command line mail client. Install it using Yum. You can use Mutt to read email messages that Sudo sends to root.

	# yum install mutt

### /etc/skel

The */etc/skel* directory contains files that will be copied to the home directory of any new users created.

	# cat >/etc/skel/welcome.txt << EOF
	Welcome aboard!
	EOF

### Create Users

Create two new users *trillian* and *jstudent*.

	# useradd trillian
	# passwd trillian

And *jstudent*:

	# useradd jstudent
	# passwd jstudent

### Virtual Terminals

In this assignment you will be working with two virtual terminals. If you are working from a LiveCD you access virtual terminals with the key combination **Crtl+Alt+Fn1** through **Ctrl+Alt+Fn6** and return to the graphical display with **Ctrl+Alt+Fn7**.  (*Note:*  some distributions put the GUI on **Ctrl+Alt+Fn1** instead of Ctrl+Alt+Fn7*.). The virtual terminals live outside of the GUI and are useful for troubleshooting when some run away program has turned the graphical display to molasses.

In VirtualBox you will use the **host** key plus a function key to access virtual terminals. The default setting for the **host** key is the *right* control key.

## The `su` Command

The `su` command lets you become the root user or another user if you have the password for that account. Using the **-l** (dash el) option gives the full environment including the correct PATH environmental variable so commands work correctly. Always use the dash or you may have problems doing some things as root.

### Without the -l

	# su trillian

Run `ls` to list files in the current directory. The command will fail. Run `pwd` to show you are still in root's home directory, even though the `whoami` command shows you are *trillian* the environment is not set correctly.

Type `exit` to return to the root user.

## With -l

Login as jstudent

	# su -l jstudent

The `pwd` command shows you are in jstudents's home directory. Try the `ls` command and you will see *welcome.txt* file.

Type `exit` to return to the root user.

## The `sudo` Command

A disadvantage to using `su` to allow users to run commands as root is that you must give them the root password and you can't easily limit what they can do. Also, you don't know who (as root) actually ran the command. The `sudo` command lets you give users in the *sudoers* file specific root privileges without the need to give them the root password. Their actions are logged as well so you have a record of what each user did.

The `/etc/sudoers` file is edited with the special program `visudo`. The `visudo` command creates a temporary copy of the sudoers file for editing and verifies that any changes have the correct syntax before saving changes to `/etc/sudoers`. As you may have guessed by the name `visudo` uses the `vi` text editor or the default editor.

### Add a User to the wheel Group

Add `trillian` as a member of the *wheel*  group. Make sure you type a capital **G**.

	# usermod -aG wheel trillian

Use the `groups or `id` command to show that `trillian` is now a member of the `wheel` group.

	# groups trillian
	trillian wheel

### Enabling the wheel Group in the sudoers File

*Note:* In CentOS 7 the *wheel* group is already uncommented. You do not need to do this step.

Use `visudo` to edit **/etc/sudoers**. `visudo` will automatically open the correct file and lock it so no other user can edit it.

Uncomment the line that lets all members of the `wheel` group run commands without using a password. Use the search function in `vi` to easily find the correct line to edit.

### Using sudo

Log in as `trillian` on another virtual terminal (host+Fn2) and run a command that requires root privileges.

	$ shutdown -r 5

The command will fail.

 Now try the command with `sudo`.

	$ sudo shutdown -r 5 Shutting down to replace a faulty component.

You'll be asked for Trillian's password and the command will work. Press **Ctrl+c** to stop the shutdown.

### Members Not in the sudoers File

Log in as `jstudent` and attempt to run the `shutdown` command.

	# su -l jstudent 
	$ sudo shutdown -r 5

The command will fail since `jstudent` is not in the *sudoers* file. Type `exit` to return to the root terminal and notice that you have mail reporting the event.

Use `mutt` to read the email. Use the **SnipIt** tool in Windows to take a screenshot of the email as your assignment submission.

## Logging

All activity of sudoers is logged in **/var/log/secure** on CentOS or **/var/log/audit/audit.log** on Debian. View the end of the log with the `tail` command and you'll see the commands run by `trillian` was logged.

*Sudo logs the following information:* 

- The command executed.
- Who ran the command.
- Which host the command ran on.
- When the command was executed.
- The directory from which the command was executed.

## Removing Sudo Privileges

### Remove Trillian From the Wheel Group

Logi out as Trillian and log in as root. You use the `vipw` command to remove Trillian from the *wheel*  group. When you added Trillian to the *wheel*  group the **-a** option appended the *wheel*  group to Trillian's supplementary groups.  Use `vipw -g` to edit the wheel group removing Trillian. Be sure to remove only Trillian's name.

	# vipw -g
	wheel:x:110:trillian

Go back to Trillian's login screen and try the `sudo` command again. The command will fail since members of the *wheel*  group are no longer permitted `sudo` privileges. This "Sudo Incident" will be logged as well. In addition, root will receive an email reporting the "incident." Use `mutt` to see the email.

## The /etc/sudoers.d/ Directory

If the *sudoers* file includes an `includedir` directive you can add files to the /etc/sudoers.d directory rather than editing the sudoers file directly. This is preferred since it keeps the original file closer to its original state. You should use `visudo -f` to edit the file so the syntax will be checked when you save the file.

*Here is an example:* 

This entry in **/etc/sudoers.d/01_jstudent** the user `jstudent` will be able to run the shutdown command:

	jstudent centos77=/sbin/shutdown -r 5

### Test the Command

As jstudent run the wrong command

	$ sudo shutdown -h now

It will fail since `jstudent` can only run the exact command in the *sudoers* file. Run the correct command and it will work.

## Troubleshoot the Assignment

- Make sure that user `trillian` is a member of the *wheel*  group.
- If the `groups` command doesn't show the wheel group. Log Trillian out than back in.
- Sudoers use their own password and not the root password.
- If Mutt complains that `/var/spool/mail/root` does not exist create it using the `touch` command.

<!--## XKCD

![Cartoon showing sudo incidents being reported to Santa Claus.](https://imgs.xkcd.com/comics/incident.png)-->

## What to Submit

Submit a screenshot of an email from `sudo` showing an incident.

## Resources

- man sudoers`
- `man su`
- `man visudo`
- [Using Sudo](http://aplawrence.com/cgi-bin/printer.pl?arg=/Basics/sudo.html)
- [Sample /etc/sudoers](http://www.sudo.ws/sudo/sample.sudoers)
- [Gaining Privileges (Red Hat docs)](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/7-Beta/html/System_Administrators_Guide/chap-Gaining_Privileges.html)