# Tests and Conditionals

## Introduction

Tests and conditionals let you control the flow of your script.

## Learning Objectives


*When you have successfully completed this assignment you will be able to:*

1. Use the `test` command to test for a condition.
2. Use combine conditions.

## Terms You Should Know

+ **test**
+ **[ ]** or **[[ ]]:** Either will work but [[ ]] is preferred.
+ **-e**
+ **-d**
+ **-r**

## The Test Command

The `test` or `[[ ]]` command is used to test for a condition. If the condition is true an exit status of zero is returned.

    $ [[ 1 -lt 2 ]]
    $ echo $?
    0

If the condition is false an exit status of other than zero is returned.
  
    $ [[ 2 -lt 1 ]]
    $ echo $?
    1
    
## if/then/else

    $ if [[ -e Documents/ ]]; then echo "Directory exists."; else echo "Directory does not exist.";fi

### Combining Test Conditions

The **&&** is a logical AND. The **||** is a logical OR.

#### Logical AND

    $ if [[ -e file.txt ]] && [[ -w file.txt ]]; then echo "File exists and is writable by me."; else echo "File does not exist or is not writable.";fi

#### Logical OR

    $ if [[ -O file.txt ]] || [[ -G file.txt ]]; then echo "File exists and owned by me or my group."; else echo "File does not exist or is not owned by me or my group.";fi

#### Condition Not Met

Reverse a test with a bang **!** character.

    $ if ! [[ -e Docs/ ]]; then echo "Directory does not exist."; else echo "Directory does exist.";fi

#### Integer Test

You can test if a value is true or not.

    $ test 10 -gt 1
    $ echo "$?
    $ 0

or

    $ if [[ 10 -lt 1 ]];then clear;echo "10 is greater than 1.";else clear;echo "Condition is not true.";fi 

#### String Test

	 $ if
	 [[ $USER = dennisk ]]
	 then echo "Hi $USER"
	 else echo "Do I know you?"
	 fi

## What to Submit

Write a script that tests whether you can read `/etc/passwd` and `/etc/shadow`
  . Output to *stdout* the appropriate answer.
  
## Resources

+ [Greg's Bash Guide](http://mywiki.wooledge.org/BashGuide/TestsAndConditionals)
+ help test (from the terminal)

> Written with [StackEdit](https://stackedit.io/).
