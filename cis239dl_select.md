<!-- <script src="https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js?lang=css&amp;skin=sunburst"></script> -->

# Select Menu

## Introduction

*select* lets you create simple menus.

## Assignment Objectives

*After successfully completing this assignment you will be able to:*

 1. Use *select* to create a menu
 2. Use PS3 to provide a custom prompt.

## Syntax

```bash
	select i in [list]
	do
		do something with $i
	done	
```

## Example

```bash
	select i in "German" "English" "Spanish" "Quit"
	  do
        if [[ "$i" = "German" ]]
        then echo "Guten Tag"
        break
        elif [[ "$i" = "English" ]]
        then echo "Hello"
        break
        elif [[ "$i" = "Spanish" ]]
        then echo "Holla"
        break
        elif [[ "$i" = "Quit" ]]
        then
        exit 
	fi
	done
```

## The PS3 Prompt

You can prompt using the PS3 prompt set before the select menu is run.

```bash
	PS3="Choose a language by number. "
	select
	...
	done
```

## What to Submit

Redo the "Rock, Paper, Scissors" assignment using a select menu. Use a custom PS3 prompt to make the menu selection more intuitive.

> Written with [StackEdit](https://stackedit.io/).