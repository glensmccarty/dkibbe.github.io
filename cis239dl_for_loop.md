# For Loops

## Introduction

Often you want to repeat an action on a list of files. A `for` loop will do this. For this assignment you will create a `for` loop that will use the `tr` command to convert upper case file names to lower case.

## Term You Should Know

 - `for`
 - `seq`
 - `{ }`
 - `touch`
 - Character classes

## For Loop

The syntax for the `for` loop looks like this:

	for i in <list>
	do
	<do something to $i>
	done

### Example

Type at the shell prompt:

	for i in cat dog mouse snake
	do
	echo "My favorite pet is my $i"
	done

## `seq` Command

You can also create the files using a `for` loop and the `{ }` command. *Note:* The `{ }` command replaces the `seq` command which is deprecated in the latest version of GNU/Bash.

	$ for i in {1..9}; do touch file"$i"; done

This will create a sequence from 1 (start) to 9 (end). Each instance of the variable **i** is replaced by the output of the `{ }` command. You specify a increment after the end number `{1..10..2}`. When typed on one line the semi-colon (**;**) replaces enter.

## Using echo to Test

This for loop will rename file1, file2, file3, etc. to FOO1, FOO2, FOO3, etc.

	$ for i in {1..9}; do mv file"$i" FOO"$i"; done

Placing the `echo` command in front of the `mv` command lets you test the command first.

	$ for i in {1..9}; do echo mv file"$i" FOO"$i"; done
	mv file1 FOO1
	mv file2 FOO2
	mv file3 FOO3

## What to Submit

Write a script that uses a `for` loop to remove (**rm**) the files you created. For 2 extra points use a `for` to remove only the odd numbered files leaving the even numbered files untouched. Submit the assignemnt using [Fedora pastebin](https://paste.fedoraproject.org/).

## Resources

 - [Bash Reference Manual (pattern matching)](https://www.gnu.org/software/bash/manual/bashref.html)
 - [Tests and Conditionals](http://mywiki.wooledge.org/BashGuide/TestsAndConditionals)

Written with [StackEdit](https://stackedit.io/).<!--se_discussion_list:{"MtCTdCfyDui2w1T7rhMObviJ":{"selectionStart":1417,"selectionEnd":1608,"commentList":[{"content":"for myvar in \"$(ls FILE[13579].txt)\";\n  do rm $myvar;\ndone"}],"discussionIndex":"MtCTdCfyDui2w1T7rhMObviJ"}}-->