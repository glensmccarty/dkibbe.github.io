# Case Statements

## Introduction

A case statement lets you express a series of if-then-else statements in a concise way. You can test a condition against the wildcard * for no matches.

*Points to remember:*

 - The case statement first expands the expression and tries to match it against each pattern.
 - When a match is found all of the associated statements are executed until the double semicolon **;;** is reached.
 - After the first match the case statement terminates with the exit status of the last command that was executed.
 - If there is no match the exit status is zero.

## Syntax

	case $VARIABLE in
	match_1)
	commands_to_execute
	;;
	match_2)
	commands_to_execute
	;;
	match_3)
	commands_to_execute
	;;
	*)  No match was found.
	commands_to_execute_for_no_match
	;;
	esac

## Example if, then, else

This example reads the value of the **LANG** environmental variable to determine the language to use. To set a "fake" **LANG** open a sub-shell by typing type `bash` then `LANG=de` for example.

	if [[ $LANG = en* ]]; then
	    echo 'Hello!'
	elif [[ $LANG = fr* ]]; then
	    echo 'Salut!'
	elif [[ $LANG = de* ]]; then
	    echo 'Guten Tag!'
	elif [[ $LANG = nl* ]]; then
	    echo 'Hallo!'
	elif [[ $LANG = it* ]]; then
	    echo 'Ciao!'
	elif [[ $LANG = es* ]]; then
	    echo 'Hola!'
	elif [[ $LANG = @(C|POSIX) ]]; then
	    echo 'hello world'
	else
	    echo 'I do not speak your language.'
	fi

## Example Case Statement

Set fake **LANG** first.

	case $LANG in
    en*) echo 'Hello!' ;;
    fr*) echo 'Salut!' ;;
    de*) echo 'Guten Tag!' ;;
    nl*) echo 'Hallo!' ;;
    it*) echo 'Ciao!' ;;
    es*) echo 'Hola!' ;;
    *)   echo 'I do not speak your language.' ;;
	esac

## What to Submit

Create a script containing a case statement that prints to stdout the appropriate statement when rock, paper or scissors is given. *Example:* If scissors is given then "Rock beats scissors" is the statement printed.

For 2 points extra credit use a wildcard set to accept the first letter upper or lower case (either **Rock** or **rock**).

# Resources

![Rock, paper, scissors](https://upload.wikimedia.org/wikipedia/commons/6/67/Rock-paper-scissors.svg)	

 - [The Case Statement](https://bash.cyberciti.biz/guide/The_case_statement)

> Written with [StackEdit](https://stackedit.io/).<!--se_discussion_list:{"hcEpDCg7vwewPJwJkZbILQCo":{"selectionStart":1725,"selectionEnd":1940,"commentList":[{"content":"echo \"paper rock scissors\"\necho \"What do you choose?\"\nread rps #rps=rock, paper, scissors\n#Computer chose rock\n\ncase $rps in\nrock) sleep 2s; echo \"Tie:  Rock, vs. Rock\" ;;\npaper) sleep 2s; echo \"You win:  Paper beats rock!\" ;;\nscissors) sleep 2s; echo \"Computer wins:  Rock beats scissors!\";;\n*) echo \"Pick again!\";;\nesac"}],"discussionIndex":"hcEpDCg7vwewPJwJkZbILQCo"}}-->