# Scheduling Jobs with cron

### Overview of Assignment

1.  Create directory in home directory for personal shell scripts.
2.  Add that directory to your PATH variable.
3.  Create a simple shell script for cron to run.
4.  Make script executable.
5.  Use `crontab` to run the script at one minute intervals.
6.  Monitor the output of the script.
7.  Make changes to see how `crond` reports errors.

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:*

1.  Use the `crontab` command to list, edit and remove cron jobs.
2.  Add a directory to your PATH variable.
3.  Use a command line mail client to read mail.
4.  Create a simple script to run as a cron job.

## Terms You Should Know

- **crond:** The cron daemon
- **crontab:** The command to add, edit or remove cron jobs.
- **anacron:** Runs commands periodically. Unlike `cron` it does not assume that the machine is running continuously.
- **at:** Run a command at a later time.
- **script:** A text file containing bash commands similar to a DOS batch file.
- **PATH:** Environmental variable that tells the shell where to look for programs to execute.

## Preparation

Any user can create a cron job using the `crontab` utility. You should do this assignment as an ordinary user not as root. This assignment should work with minor differences on either the workstation or a virtual machine. Install `mutt` to read mail from `cron`.

## The crond Configuration File

In this assignment you'll create a new "cron job" that will append the current time to a file. Since cron uses the `sh` command to run jobs we can put the `date` command in a script. **Note:** Do not include the user-name in the crontab you create.

## Create a Directory for Personal Shell Scripts

It is common to place personal scripts in `~/bin` (don't confuse with `/bin`) and add that directory to your PATH variable. Use `echo $PATH` to see if `~/bin` is already included. Also look for a line in `/.bashrc/` or `/.bash_profile/` that includes that directory. If that line exists you don't need to modify your PATH.

If `~/bin/` is not already in your PATH variable add it with these lines placed in `~/.bash_profile`.

	PATH=$PATH:/home/jstudent/bin

The change will become effective the next time you open a new shell.

## Create a Script in Your ~/bin Directory

Now create a script in that directory named `mycrontest.sh` using the `echo` command to copy the code below into the `~/bin/mycrontest.sh`.

The single quotes around the echo string are required so the shell does not interpreted the date command or the append redirect. The Bash has a built-in editor that makes editing long commands easier. Type **Ctrl+x, Ctrl+e** to open the command in the editor defined in the EDITOR environmental variable.

### Make the Script Executable

Before you can run the script it must be executable.

Test the script to make sure it works before creating the cron job.

## Adding a new Cron Job

The `crontab` command is used to write the `crontab` file and notify the cron daemon that there is a new job. Every minute `crond` wakes up and looks to see if any jobs need to be run.

The options to `crontab` are:

- **crontab -l:** List a user's cron jobs
- **crontab -e:** Edit a user's crontab file
- **crontab -r:** Remove a user's cron jobs. *Note:* This will remove everything in the `crontab` file to remove individual jobs comment them out with the **#** character at the start of the line.</dd></dl>

Use `crontab -e` to add an entry running your script every minute. See the manpage for `crontab` for the correct syntax.

Since the PATH that cron uses may not be the same as your PATH you should give the absolute path to any command you include in the crontab. Use the `which` command to find the path to the `echo` command. If all goes well you will see a message that a new crontab has been installed. If you make a mistake in syntax `crontab` will recognize it.

## Monitor the Output of cron

One a minute `cron` will update `~/mycrontestoutput.txt` with the current date and time. You can monitor the file with `tail -F` which will display the last lines as the file changes.

## Receiving Mail from cron

If cron fails to run a job you will receive an email from the cron daemon about it. The email may contain information useful should the job fail. You will receive a message in the terminal that you have mail. Read the message with `mutt` a popular command line mail client. Select the message with the arrow keys and type **Enter** to read the message; type **q** to exit.

## Removing a cron job

Use `crontab -r` to remove all cron jobs from your crontab file.

## Securing Cron

### Allow/Deny

You may not want users to create cron jobs as this can be a potential security risk. Open another terminal and as root add your user to `/etc/cron.deny` to prevent the user from running `cron`. Cron jobs already created will continue to run, but a denied user will not be able to add or delete a cron job.

Add your user name to `/etc/cron.deny` and then have that user try to run `crontab -r` the command will fail.

### PAM

PAM or Pluggable Authentication Modules can also secure `cron`. See the Red Hat documentation below for more information.

## Troubleshoot the Assignment

Typos are the main concern with this assignment. If you make a typo editing the times in the crontab file the `crontab` command will warn you. If your script isn't found or has an error. The cron daemon will email you.

## What to Submit

Submit a screenshot of the output of your cron job.

## Resources

- man 5 crontab
- man crontab
- [Scheduling Tasks with cron and atd](http://debian-handbook.info/browse/stable/sect.task-scheduling-cron-atd.html)
- [Automating System Tasks](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-Automating_System_Tasks.html)