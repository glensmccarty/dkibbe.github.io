# Introduction

A **function** is a script within a script. Using functions in your scripts makes the script cleaner. A function can contain any commands you can place in a script.

# Terms and Concepts

- declare (-f, -F)
- function name()
- source (.)
- unset -f *function name*

# Create First Function

  #!/usr/bin/env bash

  # Date: Today
  # Author: Tux Penguin
  # Purpose: Demo functions

  function showdate() {
    date +%F
    }

    function showtime() {
      date +%r
    }

    function getname() {
      clear
      echo Please type your first and last name
      read firstname lastname
      echo $firstname $lastname, Nice to meet you
    }
    
    # END
    
<!--
    
    function twain() {
    
    for twain in $(ls marktwain*.ogg)
    do
      ogg123 $twain
    done
-->

# Source the Script

When a script is called directory Bash opens a subshell to run the script. Calling the script with the `source` command assures that the functions are available to the current shell and not a subshell.

![Diagram showing running a script in a shell vs. a subshell.][subshell]

You can demonstrate this by creating a simple script that echos a message to the console and then exits.

    #!/bin/bash
    
    echo Bye now
    
    exit
    
Run the script first with `source`.

    $ bash exit.sh
    Bye now
    
  then with `bash`
  
Since `source` runs the script in the same shell the `exit` command exits from the shell. Run from `bash` the script runs in a subshell than returns to the main shell.

    #END
# ~/.profile or ~/.bash_profile

To have functions available after login you can put the functions in ~/.bashrc or source a separate function library.

# What to Submit

Create simple Bash script containing a function.

# Order of Precedence

<table border="1">
<tr><td>Aliases</td></tr>
<tr><td>Keywords</td></tr>
<tr><td>Functions</td></tr>
<tr><td>Build-ins</td></tr>
<tr><td>Scripts & Programs</td></tr>
</table>

# Resources

- Chapter 3

<!-- Links ->

[subshell]: https://s3.amazonaws.com/CIS239DL/img/bash_subshell.png


> Written with [StackEdit](https://stackedit.io/).