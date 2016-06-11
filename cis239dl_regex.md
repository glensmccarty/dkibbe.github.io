# File Globbing and Regular Expressions

## Introduction

File globbing and regular expressions are powerful tools needed by every system administrator. With these tools you can quickly filter text files to find what you are looking for.

<!--## Learning Objectives

When you have successfully completed this assignment you will be able to:*

- Describe the use of common wild cards.
- Write a simple regular expression.
- Use `tr` to replace non-printing characters.-->

## Preparation

- To make the results stand out alias `grep` to `grep --color=auto` if it is not already.
- Create a temporary directory to work in `mkdir ~/temp` or work in `/tmp` which is usually cleared on reboot.

<!--Use the `cat` command to create a new file. Type **Ctrl+D** on a line by itself to end entry and save the file.

	$ cat >> twain.txt
	Mark Twain
	Samuel Clemens
	Huckleberry Finn
	"Huck" Finn
	Tom Sawyer
	Pappy Finn
	Ctrl+D
-->
Use `touch` to create some empty files.

	$ touch Exam exam{ple,ples,12}
	$ touch {a..z}.txt {0..9}.txt

## File Globbing (Wild Cards)

Wild cards can be used with common commands to match file names. While similar to regular expressions there are not the same. Regular expressions do not match file or directory names but strings.

Symbol|Description
---------|-------
?|Matches any single character
*|Matches any string, including the empty string.
[a,i,o]|Matches Ja, Ji or Jo.
[0-9]|Matches example0 to example9.
[a-z]|Matches examplea to examplez.
[A-Z]|Matches exampleA to exampleZ.

### Match All Characters

Match all files beginning with *exam* followed by any number of characters.

	$ touch Exam exam{ple,ples,12}

then:

    $ ls example*
    example examples example12

### Match Single Character

Match all files beginning with *example* followed by a single character.

    $ ls example?
    examples

### Character Classes

Square brackets match against any character enclosed in the brackets.

	$ ls [eE]xam*
	Exam  exam12  example  Example  examples

Or a range of characters

	$ ls [a-z].txt
	a.txt b.txt c.txt z.txt

### POSIX Character Classes

POSIX character classes let you match for example a-z and 0-9.

	$ ls [[:alnum:]].txt
	1.txt  2.txt  a.txt  b.txt
	
See **Resources** below for a complete list.

### Example 4 - Negation

Placing an exclamation mark or "bang" after the first bracket tells the shell not to match the character or characters in the bracket.

	$ ls [!E]xam*
	exam12  example  examples

### Match Special Character

To match a special character use the black slash to escape it.

File created with space character.

	$ touch file\ 1.txt file.txt

Tab completion lists both files.

	$ ls file
	file 1.txt  file.txt

Use the back slash to prevent the shell from interpreting the space as a special character.

	$ ls file\ 1.txt
	file 1.txt
    
## Regular Expressions (regex)

Regular expressions are strings of special characters that describe a pattern for searching. The following table show some of the characters special to regular expressions.

Symbol|Description
---|---
.|A period matches any single character once.
?|A question mark matches a single character zero or once.
*|Matches preceding character zero or more times.
+|Must match one or more times.
{n}|Matches n times exactly.
{n,}|Matches n times or more.
{n,m}|Matches at least n times but not more than m times.
^|Matches start of line.
$|Matches end of line.
\|Escapes special characters
?|Matches preceding character zero or one times.

### Matching a Literal Strings

Create a file named *twain.txt*

	$ cat > twain.txt
	Mark Twain
	Mark Twain, esq.
	Mr. Mark Twain
	Samuel Clemens
	Markus Twain
	mark twain
	Ctrl+D

The simplest regular expression is a literal string. The following matches each line with *Mark*.
  
    $ grep Mark twain.txt

### Case-insensitive Match

Note the `grep` is case sensitive. Filtering on *mark twain* returns nothing unless **-i** option is included.

	$ grep -i mark twain.txt
	mark twain

### 
  
The **-v** option reverses the search. This will return all the lines that do not have *Mark Twain*.
  
    $ grep -v Mark twain.txt

### Spaces

Use quotes to protect the shell from interpting the space.

	$ grep "Mark Twain" twain.txt

## Extended Regular Expressions

The `grep` command supports Extended Regular Expressions with the **-E** option. In this example `grep` will find **Mark** or **mark** but only at the start of a line.

	$ grep -E "^[M|m]ark" twain.txt

### Special (Metacharacters)

#### The Period

The period matches a single character. Here *n* preceded by one character.

    $ grep ".n" twain.txt
    
  Or *ar* followed by a single character.
  
    $ grep "ar." twain.txt
    
### The Asterisk

An asterisk denotes zero or more characters.

    $ grep -E "n*" twain.txt

### Search for String at Start of Line

Filter lines that start with *Mark *Twain*

    $ grep "^Mark Twain" twain.txt

### Search for Non-Printing Characters

Filter lines that end with *Mark Twain*. This will fail if there is a space before the newline character.
  
    $ grep "Mark Twain$" twain.txt
    
If there are spaces, tabs or unusual characters in the file the **-A** option to `cat` will show that.

Open the *twain.txt* file in Nano and add spaces at the end of a line and tabs between words. The **$** charachter shows the end of the line.

      $ cat -A twain.txt
      Mark Twain^I$
      Mr. Mark Twain  $
      mark twain$

### DOS files

Use `unix2dos` to convert the file to DOS line endings then use `cat -A` command above to display them.	 
    
<!--## Brace Expansion

Here brace expansion is used to create files and bracket expansion is used to display them.

    $ for i in {0,1,2,3,4,5,6,7,8,9}; do touch file$i; done
    $ ls file[0-9]
    file0 file1 file2 file3 file4 file5 file6 file7 file8 file9

### Sequence

    $ echo {a..z}

    $ touch file-{1..5}.txt

## Comma Separated List

    $ echo {aaa,bbb,ccc,ddd}
    -->

## Logical OR

	$ grep -E '(Mark|mark)' twain.txt

## POSIX Character Classes

Usage: grep [[:alnum:]]

*This is only a partial list.*

Class|Description
---------|-------
[:alnum:]|letters and numbers
[:alpha:]|letters
[:digit:]|numbers
[:lower:]|lower case
[:punct:]|punctuation
[:upper:]|upper case

<!--No submission is needed.No dify *twain.txt* to quote 'Mark' "Twain". (note: both single and double quotes. Try `grep -E " twain.txt`. Which fails as the shell tries to interpret the quote.

It's possible to escape the quote.

	$ grep -E \" twain.txt
or use a character set to capure all the punctuation.

	$ grep -E [[:punct:]] twain.txt-->

<!--## sed

`sed` is a stream editor for filtering and transforming text and supports regular expressions. Try these examples. By default `sed` outputs to STDOUT and does not alter the original file.

    $ sed s/apple/orange/ regex_sample

    $ sed s/^apple/orange/ regex_sample
-->

<!--## tr

The `tr` command can replace non-printing characters.

This example will replace the new line character with a space putting all words on one line. 

    $ tr '\n' ' ' < regex_sample

This example will replace all lower case letters with upper case letters.

    $ tr '[:lower:]' '[:upper:]' < regex_sample-->

## What to Submit

<!--
grep -E -v '(^#|^$)' /etc/login.defs
-->

Use the `grep` command to display only the essential lines in the `/etc/login.defs` file. Blank lines and lines starting with the comment character **#** should not be displayed. Submit a screenshot of the *complete* command you used.

## Resources

- [IBM DevelopersWorks][regex-1]
- [Wikibooks: Regular Expressions][regex-2]
- [Wikibooks: grep][regex-3]  
- [Bash Extended Globbing][regex-4]
- [POSIX Character Classes][regex-5]
- [regex(7) - Linux man page][regex-6]
- [glob(7) - Linux man page][regex-7]

[regex-1]: http://www.ibm.com/developerworks/aix/library/au-speakingunix9/ "IBM DevelopersWorks"
[regex-2]: https://en.wikibooks.org/wiki/Regular_Expressions "Wikibooks: Regular Expressions"
[regex-3]: https://en.wikibooks.org/wiki/Grep "Wikibooks: grep"
[regex-4]: http://www.linuxjournal.com/content/bash-extended-globbing "Bash Extended Globbing"
[regex-5]: http://www.regular-expressions.info/posixbrackets.html "POSIX Character Classes"
[regex-6]: http://linux.die.net/man/7/regex "regex(7) - Linux man page"
[regex-7]: http://linux.die.net/man/7/glob "glob(7) - Linux man page"

> Written with [StackEdit](https://stackedit.io/).