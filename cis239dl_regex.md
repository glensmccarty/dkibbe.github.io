# File Globbing and Regular Expressions

## Introduction

File globing and regular expressions are powerful tools needed by  every system administrator.

## Learning Objectives

*When you have successfully completed this assignment you will be able to:*

- Describe the use of common wild cards.
- Write a simple regular expression.
- Use `sed` to modify text in a file.
- Use `tr` to replace non-printing characters.

## Preparation

- To make the results stand out alias `grep` to `grep --color=auto`.
- Create a temporary directory to work in `mkdir ~/temp`.
- Create a file to work with `"Mark Twain" "Huckleberry Finn" "Tom Sawyer" each on a separate line.

## File Globing (Wild Cards)

Wild cards can be used with common commands to match file names. While similar to regular expressions there are not the same. Regular expressions do not match file or directory names but strings.

<table border="1">
<th>Symbol</th><th>Description</th>
<tr><td>?</td><td>Matches any single character</td></tr>
<tr><td>*</td><td>Matches any string, including the empty string.</td></tr>
<tr><td>[a,i,o]</td><td>Matches Ja, Ji or Jo.</td></tr>
<tr><td>[0-9]</td><td>Matches example0 to example9.</td></tr>
<tr><td>[a-z]</td><td>Matches examplea to examplez.</td></tr>
<tr><td>[A-Z]</td><td>Matches exampleA to exampleZ.</td></tr>
</table>

### Example 1 

Match all files beginning with *exam* followed by any number of characters.

	$ touch exam example examples example12

then:

    $ ls example*
    exam example examples example12

### Example 2

Match all files beginning with *example* followed by a single character.

    $ ls example?
    examples
    
## Regular Expressions (regex)

Regular expressions are strings of special characters that describe a pattern for searching. The following table show some of the characters special to regular expressions.

<table border="1">
<th>Symbol</th><th>Description</th>
<tr><td>.</td><td>Matches any single character.</td></tr>
<tr><td>*</td><td>Matches preceding character zero or more times.</td></tr>
<tr><td>^</td><td>Matches start of line.</td></tr>
<tr><td>$</td><td>Matches end of line.</td></tr>
<tr><td>\</td><td>Represent special characters.</td></tr>
<!-- <tr><td>()</td><td>Groups regular expressions</td></tr> -->
<tr><td>?</td><td>Matches preceding character zero or one times</td></tr>
<!-- <tr><td>{n}</td><td>Matches the preceding character appearing 'n' times</td></tr>
<tr><td>{n,m}</td><td>Matches the preceding character appearing 'n' times but not more than 'm' times</td></tr>
<tr><td>{n,}</td><td>Matches the preceding character only when it appears 'n' times or more</td></tr>-->
</table>

### Literal Strings

The simplest regular expression is a literal string. The following matches each line with *Mark Twain* but only if on the same line.
  
    $ grep "Mark Twain" twain.txt
    
  <!--or if the quotes are left out both *Mark* and *Twain* separately.
  
    $ grep Mark Twain twain.txt-->
    
Note the `grep` is case sensitive. Filtering on *mark twain* returns nothing unless **-i** option is included.
  
The **-v** option reverses the search. This will return all the lines that do not have *Mark Twain*.
  
    $ grep -v "Mark Twain" twain.txt
    
### Special (Metacharacters)

#### The Period

The period returns a single character. Here *n* preceded by one character.

    $ grep ".n" twain.txt
    
  Or two *n*s followed by a single character.
  
    $ grep ".nn" twain.txt
    
### The Asterisk

An asterisk denotes zero or more characters.

    $ grep "n*" twain.txt

### Search for String at Start of Line

Filter lines that start with *Mark *Twain*

    $ grep ^"Mark Twain" twain.txt

### Search for a String at the End of Line

Filter lines that end with *Mark Twain*. This will fail if there is a space before the newline character.
  
    $ grep "Mark Twain"$ twain.txt
    
    $ cat -E twain.txt
    Space at end  Mark Twain $
    
<!--## Extended Regular Expressions

*** p\{2}

    grep -E p\{2} regex_sample

** "a+t"

    grep -E "a+t" regex_sample-->

## Brace Expansion

Here brace expansion is used to create files and bracket expansion is used to display them.

    $ for i in {0,1,2,3,4,5,6,7,8,9}; do touch file$i; done
    $ ls file[0-9]
    file0 file1 file2 file3 file4 file5 file6 file7 file8 file9

### Sequence

    {1..10}

    {a..bb}

    echo {a..z}

    $ touch file-{1..5}.txt

## Comma Separated List

{ aa,bb,cc,dd }

    $ echo {aaa,bbb,ccc,ddd}

## Logical OR

	$ grep -E '(a|b)' twain.txt

## Character Classes

Usage: grep [[:alnum:]]

<table border="1">
<tr><td>[:alnum:]</td><td>[:alpha:]</td><td>[:blank:]</td><td>[:cntrl:]</td></tr>
<tr><td>[:digit:]</td><td>[:graph:]</td><td>[:lower:]</td><td>[:print:]</td></tr>
<tr><td>[:punct:]</td><td>[:space:]</td><td>[:upper:]</td><td>[:xdigit:]</td></tr>
</table>

Modify *twain.txt* to quote 'Mark' "Twain". (note: both single and double quotes. Try `grep -E " twain.txt`. Which fails as the shell tries to interpret the quote.

It's possible to escape the quote.

	grep -E \" twain.txt
or use a character set to capure all the punctuation.

	grep -E [[:punct:]] twain.txt

## sed

`sed` is a stream editor for filtering and transforming text and supports regular expressions. Try these examples. By default `sed` outputs to STDOUT and does not alter the original file.

    sed s/apple/orange/ regex_sample

    sed s/^apple/orange/ regex_sample

## tr

The `tr` command can replace non-printing characters.

This example will replace the new line character with a space putting all words on one line. 

    tr '\n' ' ' < regex_sample

This example will replace all lower case letters with upper case letters.

    tr '[:lower:]' '[:upper:]' < regex_sample

<!--## Debug the Assignment-->

## XKCD

![XFCD Cartoon on regular expressions][xkcd]

## What to Submit

Create a regular expression that will remove all unnecessary lines from */etc/login.defs*.


## Resources

  + man regex
  + man glob
  + [IBM DevelopersWorks][ibm]
  + [Wikibooks: Regular Expressions][regex]
  + [Wikibooks: grep][grep]  
  + [Wikibooks: sed][sed]
  <!--+ [Wikibooks: awk][awk]
  + [Awk by example][awk1]-->
  +[Introducing filters and regular expressions][grepsedawk]
  
<!-- Links

This is [an example](http://example.com/ "Title") inline link.
This is [an example][id] reference-style link.
[id]: http://example.com/  "Optional Title Here"
![alt text](/path/img.jpg "Title")
![alt text][id]
-->

[ibm]: http://www.ibm.com/developerworks/aix/library/au-speakingunix9/ "Speaking UNIX, Part 9: Regular expressions"
[sed]: https://en.wikibooks.org/wiki/Sed "Wikibooks: sed"
[regex]: https://en.wikibooks.org/wiki/Regular_Expressions "Wikibooks: Regular Expressions"
[grep]: https://en.wikibooks.org/wiki/Grep "Wikibooks: grep"
[awk]: https://en.wikibooks.org/wiki/Awk "Wikibooks: awk"
[awk1]: http://www.ibm.com/developerworks/library/l-awk1/index.html "Awk by example"
[grepsedawk]: http://www.ibm.com/developerworks/aix/tutorials/au-unixtips3/index.html
[xkcd]: https://sslimgs.xkcd.com/comics/regular_expressions.png "XFCD Cartoon on regular expressions"

## Creative Commons License

[![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)](http://creativecommons.org/licenses/by-sa/3.0/)  
This work is licensed under a [Creative Commons Attribution-ShareAlike 3.0 Unported License](http://creativecommons.org/licenses/by-sa/3.0/).