# Arrays

## Learning Objectives

*When you have successfully completed this assignment you will be able to:*

1. Explain why quoting is important. 
2. Create a simple array
3. List the indices of an array.
4. Add and remove elements from a array.
5. Create a script using an array.
6. Explain the need for proper quoting of arrays.
  
## Preparation

Make a new directory to work in.

``` bash
$ mkdir -p ~/temp/backup
$ cd temp
```
## Why use Arrays?

Arrays assure that your script will work properly regardless of input.
  
Try this:

``` bash
$ for i in {1..9}; do touch file\ -\ "${i}".txt; done
$ files="$(ls *.txt)"; cp $files backup/
```

The backup fails because **.txt* isn't expanded correctly due to the spaces in the file names.. Using an array solves the problem. This command create an array named *files* which contains all the *.txt* files in the directory

``` bash
$ files=(*.txt); cp "${files[@]}" backup/
```
	
## Terms You Should Know

+ **String**
+ **Array**
+ **Associative array**

## Preparation

Before we talk about arrays let's revisit a couple of topics.
  
## Strings

The term string refers to a sequence of characters which is treated as a single unit. The following command contains two strings, the command itself and an option. While not practical you could say that the entire command is a string.

``` bash
$ ls -l
```
Strings are limited to holding one element Take this alias for example. `ls -l` is treated as a single unit.

``` bash
$ alias lls='ls -l'
```

## Functions

Functions can contain more than one command and be use in scripts.

## Arrays

Arrays have the advantage that an array can hold more than one element. An array is a numbered list of strings: It maps integers to strings.

### Create an Array

Arrays can be created several ways. Here is the easiest. It creates an array *names* with 4 elements.

``` bash
$ names=(Bob Carol Ted Alice)
```

### What's in the Array?

You can display all the elements of an array this way.

``` bash
$ echo "${names[@]}"
Bob Carol Ted Alice
```

Or a single element by its position in the array. Note that the first element is **0**.

``` bash
$ echo "${names[0]}"
Bob
```

#### Adding to an Array

Fist let's see what positions are already taken in the array.

``` bash
$ echo "${!names[@]}"
0 1 2 3
```

Elements are assigned an index number starting with zero.

``` bash
$ names[5]="Big Bopper"
Big Bopper
```

It's OK to skip index numbers as we did here.

``` bash
	$ echo "${!names[@]}"
	0 1 2 3 5
	Bob Carol Ted Alice Big Bopper
```

#### Using an Array in a for Loop

``` bash
	for i in "${names[@]}"; do echo $i; done
	Bob
	Carol
	Ted
	Alice
	Big Bopper
```

Since index **4** was not assigned it is not printed.

#### Find the Length of an Element

The length of element **0** (Bob):

``` bash
$ echo "${#names[0]}"
	3
```

The length of element **5** (Big Bopper):
``` bash
$ echo "${#names[5]}"
10
```

## Unset an Array or Array Element

You can remove an element from the array with  the`unset` command.

``` bash
$ unset names[5]
$ for i in ${names[*]}; do echo $i; done
bob
carol
ted
alice
```

or unset all

``` bash
$ unset names # or unset names[@]
$ for i in ${names[*]}; do echo $i; done
(No output)
```

## Word Splitting
 
>  "Use more quotes!" Protect your strings and parameter expansions from [WordSplitting](http://mywiki.wooledge.org/WordSplitting). Word splitting will eat your babies if you don't quote things properly. -- Bash Guide

Let's demo that using a small script.

``` bash
#!/bin/sh
# args.sh
# Purpose: count the number of arguments given to the script.
printf "%d args:" $#
printf " <%s>" "$@"
echo
```

Make the script executable and run it with this example.

``` bash
$ ./args.sh hello world "how are you?"
3 args: <hello> <world> <how are you?>
```

This time without the quotes.

``` bash
$ ./args.sh hello world how are you?
5 args: <hello> <world> <how> <are> <you?>
```

The expansion is very different.

### Word Splitting Examples with an Arrays

Array not quoted.

``` bash
$ array=(testing testing "1 2 3")
$ ./args.sh ${array[@]}
5 args: <testing> <testing> <1> <2> <3>
```

Array quoted properly.

``` bash
$ array=(testing testing "1 2 3")
$ ./args.sh "${array[@]}"
3 args: <testing> <testing> <1 2 3>
```

## Associative Array

Associative Arrays are friendlier to work with since you replace the index with something more meaningful.

``` bash
$ declare -A FullNames
$ FullNames=( [MT]="Mark Twain" [TS]="Tom Sawyer" [HF]="Huckleberry Finn" )
$ echo "${FullNames[MT]}"
```

## What to Submit

Create a simple script that takes two positional parameters. The first parameter is the initials of a player on the 1939 New York Yankees and the second is the index of an array containing *home plate*, *first base*, *second base*, and *third base*. 

The script simply echoes to **stdout** " *player* is on *base*." Use an associative array named *player* to print the full name of the player and a regular array named *bases* to print which base the player is on. Make sure everything is properly quoted.

Submit your script at [Fedora Pastebin](https://paste.fedoraproject.org/).

Enter your name under *Your alias* and select Bash as the language.

![Fedora Pastebin](http://classfiles.dennisk.fastmail.net/fedora_pastebin-1.png)

Click *PASTE* and copy the shortened URL.

![Fedora Pastebin](http://classfiles.dennisk.fastmail.net/fedora_pastebin-2.png)

## Resources

+ [Bash word splitting](http://mywiki.wooledge.org/WordSplitting)
+ [Arrays](http://mywiki.wooledge.org/BashGuide/Arrays)
+ [Who's on First - Abbott & Costello](http://youtube.com/watch?v=kTcRRaXV-fg])
  
> Written with [StackEdit](https://stackedit.io/).