# Positional Parameters

## Introduction

Scripts can accept user input from the command line. This input is known as a **positional parameter.**

## Learning Objectives

  *When you have successfully completed this assignment you will be able to:*

  1. Explain the purpose of positional parameters.
  2. Use positional parameters in a script.
  3. Test for the absence of a positional parameter.

## Terms You Should Know

  + **#:** Variable that holds the number of positional variables
  + **@:** Variable that holds all the words of the positional parameters.
  + **0:** Variable that holds the name of the file.
  + **seq:**

## Positional Parameters (Variables)

### Examples

  **myscript.sh 1** has one positional parameter. The variable name is **1**.
  
  **myscript2.sh 1 2** has two positional parameters. Positional parameters are separated by spaces. The variable names are **1** and **2**.
   
  **myscript3.sh tux linux** also has 2 positional parameters. Positional parameters can be any length. The names are **tux** and **linux**.
  
  Positional parameters are given the variable names 1, 2, 3, 4, 5, 6, 7, 8, 9 in that order. You can have more that nine positional parameters but that is rare and they need to be handled differently.

## The # Variable

  The number of positional variables is stores in a variable - #. This script will display the number of positional variables given to a script.

	#!/usr/bin/env bash

	# Author: Tux
	# Purpose: To show number of positional parameters
	# Assignment: Positional Parameters.

	# Clear the screen before starting.
	clear

	if [[ "$#" -lt 1 ]]
        then
        echo "No parameters given to $0."
        else
        echo "$# parameters were given to $0."
	fi

	# END

  Make the script executable and run with any number of positional variables

## Using Positional Parameters in a Script

    #!/usr/bin/env bash
    
    # Author: Tux
    # Purpose: to show the use of positional parameters
    # Assignment: Positional Parameters.
    
    # Run a sequence using two values given.
    seq $1 $2
    
    # END
    
This script takes two positional parameters and passes them to the `seq` command.

    $ ./posiparam2.sh 1 5
    1
    2
    3
    4
    5

If no numbers are given the `seq` command will output an error message to stderr.

### Testing for Positional Parameters

This script adds an if statement to test for user input.

    #!/urs/bin/env bash
    
    # Author: Tux
    # Purpose: Test for proper user input.
    # Assignment: Positional Parameters.

    # Define variables
      BADPARAM=165

    # Check for input

      if [ $# != 2 ]
      then
	echo "Please enter two numbers"
	exit  $BADPARAM
      fi

    # Print the sequence
    
      seq $1 $2

    # END

## What to Submit
  
  Create a script that uses an if statement to print the first ten lines of a file to STDOUT. The file name is entered as a positional parameter. Script should test if the file exists and also test if no file is entered.

## Resources

 - [seq manpage](http://linux.die.net/man/1/seq)
 - [Greg's Bash Manual](http://mywiki.wooledge.org/BashGuide/Parameters)

Written with [StackEdit](https://stackedit.io/).
