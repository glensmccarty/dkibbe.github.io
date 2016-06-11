# Chopping Strings

![Man with Axe](http://classfiles.dennisk.fastmail.net/chop.png)

Sometimes you need to remove part of a string. For example a phone number:

```bash
$ myphone="123-456-7890"
$ echo $myphone
123-456-7890
```
## Chop from the Start of a String

This chops all characters *before* the first dash. Note the curly braces not parenthesis. This example matches the *shortest* string starting from the beginning of the string.

```bash
$ echo ${myphone#*-}
456-7890
```
To chop all the characters before the second dash use this. This matches the *longest* string from the beginning.

```bash
$ echo ${myphone##*-}
7890
```
You can remember that **#** and **##**chop from the start of the string since **#** is *before* the **$** which denotes variables.

## Chop from the End of a String

The percent character is used to chop from the end of a string matching the first dash. 

```bash
$ echo ${myphone%-*}
123-456
```
To match the second dash from the end.

```bash
$ echo ${myphone%%-*}
123
```
An way to remember which character to use is to note that **$** represents the expression itself and to chop from the start of the string you use **#** and **##** and to chop from the end of the string **%** and **%%**.

## Greedy vs. Non-Greedy

Both **##** and **%%** are known as *greedy* matches since they match the longest string. While *#* and *%* are *non-greedy*.

## Chopping Directories

Linux provides two commands for parsing a directory string.

### basename

```bash
$ basename /usr/share/doc/bash/changelog.Debian.gz 
changelog.Debian.gz
```

You can specify the suffix to remove as well.

```bash
$ basename /usr/share/doc/bash/changelog.Debian.gz .Debian.gz
changelog
```

### dirname

`dirname` returns the last directory in the string

```bash
$ dirname /usr/share/doc/bash/changelog.Debian.gz
/usr/share/doc/bash
```

and

```bash
$ dirname /usr/share/doc/
/usr/share
```

## Command Substitution

### basename

```bash
$ mybase=$(basename /usr/share/doc/bash/copyright)
copyright
```

### dirname

```bash
$ mydir=$(dirname /usr/share/doc/bash/copyright)
/usr/share/doc/bash
```

## What to Submit

123-456-7890 x123

Write a script that will return only the **10** digit phone number stripping the extension or strip both the Area Code and extension returning a **7** digit number. The script should accept two positional parameters. The first being a phone number formatted as above and the second being either **e** to strip the Area Code or **ae** to strip the Area Code and extension.

Submit the assignment on [Fedora pastebin](http://fpastebin.net).

<!--For extra credit please each part in a function and call it with ??-->

# Resources

 - [Chopping Strings Like a Pro](http://www.ibm.com/developerworks/library/l-bash/index.html)

> Written with [StackEdit](https://stackedit.io/).<!--se_discussion_list:{"RLFFpPTvpOzvVy2lub81MIQ4":{"selectionStart":2117,"selectionEnd":2131,"commentList":[{"content":"#!/usr/bin/env bash\n# Assignment: Chopping Strings\n# Name: Jeremiah Summers\n# As Simple as I can get (with the exception of functions)\n \n#Vars\nphone_num=\"$1\"\n \n#functions\nfunction strip_area\n{\n    echo \"${phone_num#*-}\"\n}\n \nfunction strip_ext\n{\n    no_area=\"${phone_num#*-}\"\n    echo \"${no_area%x*}\"\n}\n \n#Begin\n \nif [[ \"$2\" == \"a\" ]]; then\n  strip_area\nelif [[ \"$2\" == \"ae\" ]]; then\n  strip_ext\nelse\n  echo \"Wrong Parameters used\"\n  echo \"Remember to quote number and ext\"\n  echo \"ex. $0 \\\"480-878-1764 x123\\\" [a or ae]\"\nfi\n \n#end"}],"discussionIndex":"RLFFpPTvpOzvVy2lub81MIQ4"},"PJQ3nrkWDBly0Rb0B9Vx7i0l":{"selectionStart":2117,"selectionEnd":2131,"commentList":[{"content":"#!/usr/bin/env bash\n \n# AUTHOR: Shane Sexton\n# CHOPPING STRINGS\n# This script takes two positional parameters, a quoted phone number\n# and either \"a\", \"e\", or \"ae\" to tell the function whether to strip\n# the area code, extension, or area code and extension. It also vali-\n# dates the input\n \n \n## FUNCTIONS ##\n \nstrip_area_code(){\n  echo ${1#*-}         # Return everything past first hyphen from right\n}\n \nstrip_extension(){\n  echo ${1%' '*}       # Return everything before first space from left\n}\n \nstrip_both(){\n  phone_number=\"${1%' x'*}\"  # Strip extension first\n  echo ${phone_number#*-}    # Strip area code and return number\n}\n \nvalidate_input(){\n \n# If no first parameter, bug user and exit\n  if [[ -z \"$1\" ]]; then      \n    printf \"Please enter a phone number.\\n\"\n    exit 1\n  fi\n \n# If second parameter is incorrect, bug user and exit\n  if ! [[ (\"$2\" == \"a\") || (\"$2\" == \"e\") || (\"$2\" == \"ae\") ]]; then\n    printf \"Please enter a, e, or ae after the phone number.\\n\"\n    exit 1\n  fi\n}\n \n## BODY ##\n \nvalidate_input \"$1\" \"$2\" # validate inputs\n \ncase $2 in               # modify phone number based on 2nd parameter\n \"a\") strip_area_code \"$1\" ;;  \n \"e\") strip_extension \"$1\" ;;\n \"ae\") strip_both $1 ;;\nesac\n \n## END ##"}],"discussionIndex":"PJQ3nrkWDBly0Rb0B9Vx7i0l"},"U4ViLDFS0LHFff9gRaB37yFj":{"selectionStart":2117,"selectionEnd":2131,"commentList":[{"content":"#!/usr/bin/env bash\n \n#Lining Lin\n#Return a part of 10 digit phone number as requested\n#Chopping Strings\n \n#Variables\nphone=$1\nphone1=${phone#*-}\nphone2=${phone1%x*}\n \n#Print format as requested\n \necho \"The input phone number is $1.\"\n \ncase $2 in\ne*) echo $phone1 ;;\nae*) echo $phone2 ;;\n*) echo \"Invalid input\" ;;\nesac\n \n#END"},{"content":"#!/bin/bash\n#author: Dieu Dang\n#assignment: chopping strings\n \n myphone=$1\n+ myphone='123-456-7890 x123'\n if [ $2 = \"e\" ]\n then\n echo ${myphone%\\ *}\n elif [ $2 = \"ae\" ]\n then\n num1=${myphone%x*}\n num=${num1#*-}\n echo $num1\n fi\n+ '[' e = e ']'\n+ echo 123-456-7890\n123-456-7890\n  \n  #done"}],"discussionIndex":"U4ViLDFS0LHFff9gRaB37yFj"}}-->