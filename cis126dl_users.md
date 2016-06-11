# Managing Users & Groups

## Assignment Objectives

Managing users and groups is an important administrative skill. In this assignment you'll add new user account from the command line but before doing that you need to make two changes.

*After successfully completing this assignment you will be able to:*
 
1. Create new user accounts from the command line.
3. Add a user to supplementary groups with the `usermod` command.
2. Create content in the `/etc/skel/` directory that will be copied over to the users' home directory.
4. Describe the difference between a password and a passphrase.
5. Modify system-wide login defaults.

## Terms and Commands You Should Know

- **/etc/passwd:** A text file that describes user login accounts for the system.
- **/etc/shadow:** A text file which contains the password information for the system's accounts and optional aging information.
- **/etc/group:** A text file that defines the groups on the system.
- **/etc/gshadow:** A text file which contains the password information for groups.
- **/etc/login.defs:** A text file that defines the defaults for accounts.
- **/etc/adduser.conf:** Configuration file for the `adduser` command.
- **/etc/skel:** Files placed in this directory will be copied to new users home directory.
- **chage:** Change user password expiry information.
- **chfn:** Change real user name and information.
- **finger:** Read information from a users profile (real name, phone, etc.) if they have one.
- **GECOS:** A field in the `/etc/passwd` file containing the real name and contact information for a user.
- **groupadd:** Create a new group.
- **groupdel:** Remove a group from the system.
- **groupmod:** Modify a group account.
- **id:** Print user and group information.
- **passwd:** Change a user's password.
- **useradd:** Add a new user to the system (red Hat). The `passwd` command must also be run.
- **adduser:** Add a new user to the system (Debian).
- **userdel:** Remove a user.
- **usermod:** Modify a user account.
- **vipw:** Safely edit the `/etc/passwd`, `/etc/shadow`, and `/etc/group` files.
- **who:** Show who is logged into the system.
- **id:** Print real and effective user and group IDs.
- **su:** Switch to another user (always use with the - dash option.

## Preparations

Start a CentOS 7 virtual machine. Commands will be different on a Debian-based machine.

## Adding a File to /etc/skel

The `/etc/skel` directory as defined in `/etc/defaults/useradd` is the place to put any files or directories you want to be copied to a user's home directory when a new user is created. For this assignment add a welcome.txt file (it can be an empty file) to the `/etc/skel` directory so it will copied to the home directories of the new accounts you create.

	# touch /etc/skel/welcome.txt

## Changing the Maximum Days a Password May Be Used

The `/etc/login.defs` file sets defaults for creating user accounts such as when passwords expire. Find the line that reads PASSMAXDAYS 99999 and change it to PASSMAXDAYS 90. Be sure you create a backup before you edit the file.

	$ cd
	$ cp /etc/login.defs login.defs.bak 

## Creating New Users

Use the `useradd` command to create two new accounts.

### First Account

Create a new account with the login of `jstudent` with the password `Pa$$w0rd`. Use the **-c** option to add *Jill Student* to the GECOS field.

	# useradd -c "Jill Student" jstudent
	# passwd jstudent

### Second Account

Create a second new account with the login `trillian` and the passphrase `Heart of Gold`. A passphrase can be more secure than a password since a passphrase can contain spaces and longer passphrases can be more easily remembered.

	# useradd -c "Tricia McMillan, Starship Heart of Gold" trillian
	# passwd trillian

#### Add a supplemental Group

Next add `trillian` to the `wheel` supplementary group.  *Be sure to use the capital -G option.*

	# usermod -aG wheel trillian

#### Modify Account Expiration	

Next change the account expiration to 120 days from today.

	$ sudo grep trillian /etc/shadow
	$ sudo chage -E YYYY-MM-DD trillian
	$ sudo grep trillian /etc/shadow

## What to Submit

*Submit a screenshot of the following:*

- The output of `id jstudent`
- The output of `id trillian`.
- The output of `chage -l trillian`

## Resources

- man 5 login.defs
- man adduser
- man usermod
- man userdel
- man 5 passwd
- man passwd
- man chage
- man 5 login.defs