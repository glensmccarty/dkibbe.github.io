
# Introduction

Sed is a **S**tream **ed**itor with these features:

1. Sed reads files line by line.
2. By default sed does not edit the original file but just outputs to STOUT.
3. Sed is used mostly for search and replace.

## Preparation

Create three text files putting each name, word or sentence on a separate line.

+ *twain.txt* - Mark Twain, Huckelberry finn, Pappy FINN, Becky Thatcher, Injun Joe, Tom Sawyer
+ *animals.txt* - cats, dogs, birds, fish, mice
+ linux.txt - Both Ubuntu and Mint are based on Debian., my website is at http://example.com/tux/.

## Syntax (substitution)

Sed is often used to search for patterns and replace them with something else.

### Example 1 

To replace cats with dogs.

	$ sed 's/cats/dogs/' animals.txt

+ **s** is for *substitution*
<!--+ **g** is for *global* (replace every instance)-->
+ **cats** is the term to be replaced
+ **dogs** replaces **cats**
+ *animals.txt* one or more files to search
+ The single quotes protect the shell from the forward slashes.

### Example 2

The **&** character is a shortcut standing for the item to be replaced.

	$ sed 's/cats/alley&/' animals.txt

### Example 3

The **-n** and **p** print only the pattern space.

	$ sed -n 's/Becky Thatcher/Ms. &/p' twain.txt 
	Ms. Becky Thatcher

### Example 4

You can give `sed` multiple scripts by separating them with the **;** (semi-colon) character.

	$ sed -n 's/Mark/Mike/p; s/Tom/Tim/p' twain.txt

### Example 4

The **I** (upper-case i) will apply the script to both upper and lower case.

	$ sed 's/finn/Finn/I' twain.txt

### Example 5

The replacement can contain the null string.

	$ sed 's/Finn //' twain.txt

## Syntax (deletion)

Sed can be used to delete lines containing text.

	$ sed '/Sawyer/d' twain.txt

## Escaping Metacharacters

If you want to use a metacharacter; that is a special character that `sed` uses it must be escaped with the **\\** (backslash). This fails since the **&** (ampersand) is a metacharacter.

	$ sed 's/and/&/' linux.txt

Escaping the **&** lets `sed` treat it as a regular character.

	$ sed 's/and/\&/' linux.txt

## Replacing the default separator

If you need to replace a string that contains the forward slash (**/**) multiple times you can replace the separator with another rather than escaping each instance.

	$ sed 's_http://example.com/tux/_http://tux.example.com_' linux.txt
	
##In-Place editing

By default `sed` does not edit the original file. This behavior can be changed with the **-i** option.

	$ sed -i 's/Mark/Mike/' twain.txt
	
## What to Submit

Write a `sed` script that will do the same as the `grep` command you wrote to remove unnecessary lines from */etc/login.defs. For full credit assume that comment lines may have one or more spaces before the **#** character.

## Resources
+ [Sed Manual](https://www.gnu.org/software/sed/manual/)
+ [Sed by Example](http://www.ibm.com/developerworks/library/l-sed1/)

> Written with [StackEdit](https://stackedit.io/).