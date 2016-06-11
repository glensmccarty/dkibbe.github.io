# Writing Your First Bash Shell Script

## Introduction

In this assignment you’ll create a very basic shell script. The only function of this script is to print “Hello World” to stdout. This assignment will introduce you to features that should be included in all the scripts that you write.

## Text Editors

Scripts can not have any formating and should not be written with a word processor. You should write your scripts on Linux using vi/vim, Nano or Emacs since you will want to test them. If you must use Windows use a program like [Notepad++](https://notepad-plus-plus.org/) which will end the lines correctly so the script will actually work on a Linux or Unix machine.

## Naming the Script

Name the script lower case, one word with a .sh extension. While not essential the .sh extension shows that this is a script and some text editors will use syntax highlighting to make the script easier to edit.

    # vi myscript.sh

## Parts of a Script

### Shebang line

This first line sets the environment for the script. In our case Bash. Usually you will see this shebang line in scripts you find on the Web..

    #!/bin/bash

A better choice is the following which makes the script more portable. Any POSIX compliant shell should run the script properly.

    #!/usr/bin/env bash

*Only one of the lines should be at the top of your script.*

### Comments

Include the following comment lines (comment lines start with the **#** character.) in all the scripts you write for this class.

- Purpose of the script
- Your Name
- What assignment the script is for.

*Example:*

    # Prints a "Hello World" message to the screen.
    # Tux Penguin
    # Assignment 1

### Variables

Next place any variables used in the script. Name your variables with lower case, CamelCase or, if upper case, make sure there is not an environmental variable with the same name. If variables are not used in the script you can skip this section

    # variables
    IPT=/usr/sbin/iptables
    pet=hamster
    MyVar=10

### Functions

If functions are used in the script put them next. Defining variables and functions at the top of the script help make the script more readable.

*Here is a simple example:*

``` bash
#!/usr/bin/env bash 

# Functions
usage() {
	echo "Usage: Please enter two
	parameters"
}

if [[ $# -ne 2 ]]
	then
		usage
		exit 1
fi
echo OK
```

Indentation can be used to make scripts more readable.

### Commands

Finally comes the commands that actually do the work. You can annotate these with a comment if you like.

    clear # Clears the screen.
    echo "Hello World" # printf works here too.

### End the Script

While not necessary it is nice to end the script with the following comment line.

    # END

### A Sample Script in Nano

![A sample first script](http://classfiles.dennisk.fastmail.net/hello_script.png)

### Run the Script

There are several ways to run your first script.

- Make the script executable and prepend the script with **./**.
- Run the script with the `bash` command.
- Use `source` to run the script.

### Debug the Assignment

If your script isn’t working the way you expect try adding this option to the `bash` command. It will give you useful debugging information.

    bash -xv myscript.sh

# What to Submit

Submit your script at [Fedora Pastebin](https://paste.fedoraproject.org/).

Enter your name under **Your alias** and select **Bash** as the language. Do not assign a password.

![Fedora pastebin](http://classfiles.dennisk.fastmail.net/fedora_pastebin-1.png)

Click **PASTE** and copy the shortened URL. You will submit the URL to complete the assignment.

[Fedora pastebin](http://classfiles.dennisk.fastmail.net/fedora_pastebin-2.png)

# Resources

- [Bash Shell Scripting - Wikibooks](https://en.wikibooks.org/wiki/Bash_Shell_Scripting "Bash Scripting")
- [Bash Reference Manual](https://www.gnu.org/software/bash/manual/bashref.html "Bash Reference Manual")
- [Linux Shell Scripting Tutorial](http://bash.cyberciti.biz/guide/Main_Page "Linux Shell Scripting Tutorial")
* [Google Shell Script Style Guide](https://google.github.io/styleguide/shell.xml)
* [POSIX](https://en.wikipedia.org/wiki/POSIX)
* [ShellCheck](http://www.shellcheck.net/)