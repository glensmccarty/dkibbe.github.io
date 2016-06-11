# AWK, AWK ,AWK!

## Introduction

So, why the name? AWK is named after its inventors *Al Aho*, *Peter Weinberger* and *Brian Kernighan*, who first developed it at Bell Labs in the late 1970s. AWK is designed to perform simple data filtering and manipulation tasks in text files.

## Learning Objectives

*When you have successfully completed this assignment you will be able to:*

1. Be able to construct a simple AWK program.
2. Sort records using the `sort` command.

## Terms You Should Know

- **AWK**
- **nawk (new AWK)**
- **gawk (GNU AWK)**

## Preparation

1. AWK or Gawk should already be installed on any Linux distribution.
2. Create this sample text files:

twain.txt

  >Mark Twain
  Huckleberry "Huck" Finn
  Tom Sawyer
  Pap Finn
  Samuel Clements
  Becky Thatcher
  Joe Harper

## AWK

### Syntax

AWk programs start with `awk` followed by *options*, followed by a *pattern*, followed by one or more *actions* in curly brackets. Note that the action is surrounded by single quotes to prevent the shell from receiving special characters. An AWK program must have at least a pattern *or* an action and may have both.

AWK works with *records* and *fields* in text files. By default `awk` treats spaces and tabs as separators. If fields are separated by a different character `awk` can handle that to.

Both these examples will print the file twain.txt:

``` awk
$ awk '{print}' twain.txt
```

// $ awk '{print}' twain.txt

or

```awk
$ awk '{print $0}' twain.txt
```

Here a regular expression pattern is added to print only lines with *Finn*:

```awk
$ awk /Finn/'{print $0}' twain.txt
```

If the action is ommitted AWK filters on the entire file.
 
```awk 
$ awk /Finn/ twain.txt
```

### Fields and Records

AWK recognizes fields separated by white spaces and records separated by the new line character **\n**.

#### Fields

AWK recognizes fields separated by white spaces.

To print only the first field in our test file to stdout.

```awk
$ awk '{print $1}' twain.txt
```

To print both the first and second fields

```awk
$ awk '{print $1 $2}' twain.txt
```

AWK concatenated the two files together. Separating the fields with a comma will tell AWK to place a space between them in the output.

```awk
$ awk '{print $1, $2}' twain.txt
```
You can change the order of fields in the output.

```awk
$ awk '{print $2, $1}' twain.txt
```

An AWK program consists of a *pattern* followed by an *action*. The action is inside the curly braces. You can leave out one or the other but not both. This example prints all the records with 3 fields.

```awk
$ awk NF==3 twain.txt
```

This example will print the number of fields in each record.

```awk
$ awk '{print NF $0}' twain.txt
```

You can add comments and format the output like this:

```awk
$ awk '{print "Number of Fields:", NF, $0}' twain.txt
```

#### Records

Each line in a file is a record. Records are separated by the new line character **\n**.

This example adds a pattern to our previous AWK program. The **/Finn/** is a regular expression telling AWK to print only these records with *Finn* in the line.

```awk
$ awk /Finn/'{print $1, $2}' twain.txt
```
 
Actions can be combined so that only lines with *Finn* or *berry* are printed.

```awk
$ awk /Finn/'{print $0} /berry/{print $0}' twain.txt
```

And you can add a comment or anything else to the output. *Huckleberry "Huck" Finn* is printed twice since it matches both patterns.

```awk
$ awk /Finn/'{print "Search pattern is Finn:", $0} /berry/{print "Search patter is berry:", $0}' twain.txt
```

## Flags (Options)

You can add *flags* to modify AWK.

### AWK Program from File (-f)

AWK programs can be place in a text file. Open nano and type the following:

```awk
/Finn/{print "Search pattern is Finn:",  $0}
```

and run with the **-f** flag.

```awk
$ awk -f finn.awk twain.txt
```

Notice that the curly brackets do not need to be enclosed in single quotes when placed in a file.

### Change Field Separator (-F)

Copy *twain.txt* to *twain-commas.txt* and replace the spaces between fields with commas. 

```awk
$ awk '{print $2}' twain-commas.txt
```

The AWK program will fail because AWK is assuming space separators:

```awk
$ awk '{print}' twain-commas.txt
```

This will succeed:

```awk
$ awk -F, '{print}' twain-commas.txt
```

### Use a Variable (-v)

 You can use variables wit AWK. Here we'll create a Variable that will print some text.

```awk
$ awk -v adv="Characters created by Samuel Clements." '{print $0} {print adv}' twain.txt
```

You can use the output of a command as a variable.

```awk
$ awk -v DATE="$(date +%D)" '{print} {print "Current as of " DATE}' twain.txt
```

## BEGIN & END

In the previous examples AWK printed text after every line. Let's change that with BEGIN and END.

At the beginning of the file:

```awk
 $ awk -v adv="Characters created by Samuel Clements." '{print $0} BEGIN{print adv}' twain.txt
```
 
At the end of the file:

```awk
$ awk -v DATE="$(date +%D)" '{print} END{print "Current as of " DATE}' twain.txt
```

## What to Submit

Submit a one line AWK program (not in a text/script file) that will output the *login* and *GECOS* fields in */etc/passwd* for each account to STDOUT. Separate the fields with a *space* followed by a *dash* followed by a *space*. Remove any trailing commas from the GECOS field. The first line in the output should read "Accounts on xps13". Replace **xps13** with the actual hostname of the system you ran the script on. Sort the output by the login field.

Submit the assignment on [Fedora pastebin](https://paste.fedoraproject.org/).

*Hint: * Think outside the AWK. Pipe is your friend.

Sample output :

```
Accounts on xps13
avahi - Avahi mDNS daemon
backup - backup
bin - bin
colord - colord colour management 
daemon - daemon
dennisk - Dennis Kibbe
```

For 2 points extra arrange the commands so that the *Accounts on xps13* stays at the top of the output.

## Resources

- [Wikibooks: awk](https://en.wikibooks.org/wiki/Awk)
- [Awk by example](http://www.ibm.com/developerworks/library/l-awk1/index.html)
- [Introducing filters and regular expressions](http://www.ibm.com/developerworks/aix/tutorials/au-unixtips3/index.html)
- [POSIX Character Classes](http://www.regular-expressions.info/posixbrackets.html)

> Written with [StackEdit](https://stackedit.io/).<!--se_discussion_list:{"RD10yRKXY5dzthgnOuh9A1xh":{"selectionStart":5019,"selectionEnd":5033,"commentList":[{"content":"sort /etc/passwd | awk -v hn=$(hostname) -F\":\" '{ print $1,\"-\", $5 } BEGIN{print \"Accounts on\",hn}' | sed 's/,//g' | head -n2"},{"content":"sort /etc/passwd|awk -F: -v header=$(hostname) 'BEGIN {print \"Accounts on \" header} {print $1 \" - \" $5}'| sed 's/,//g'"},{"content":"sort -t: -k1 /etc/passwd | awk -v host=\"$(hostname)\" 'BEGIN {FS = \":\"; OFS = \" - \"; print \"Accounts on \" host} {print $1,$5}' | sed s/,*$//"}],"discussionIndex":"RD10yRKXY5dzthgnOuh9A1xh"}}-->