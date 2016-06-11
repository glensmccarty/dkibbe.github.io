# sed (stream editor)

`sed` is a stream editor for filtering and transforming text and supports regular expressions. By default `sed` outputs to STDOUT and does not alter the original file.

## Preparation

Create a file to work on.

	$ cat > twain.txt
	Mark Twain
	Mr. Mark Twain
	Samuel Clemens
	mark twain

Create asecond file.

	$ cat > linux.txt
	http://example.com/tux/
	
Type **Ctrl+D** on a line by itself to end the file.

### Substitution

    $ sed 's/Mark/Mary/' twain.txt

Sed is case sensitive so *mark twain* isn't changed. The single quotes are necessary to protect the shell from forward slashes. If you only want to see the lines changed use the **-n** and **p** options.

	sed -n 's/mark twain/Tom Sawyer/p' twain.txt
	
### Multiple Substitutions

Sed statements are separated by a semicolon so you can use more than one substitution.

	$ sed 's/Mark/Samuel/ ; s/Mr./Ms./' twain.txt

### Deletion

The **d** instruction tells `sed` to delete the line rather than make a substitution.

    $ sed '/Mark/d' twain.txt

### Sed Scripts

Sed scripts can be placed in a file. One script per line with no quotes.

	$ cat > sed.txt
	s/Mark/Samuel/
	/Mr. /d
	
Type **Ctrl+D** on a line by itself to end the file.

### Edit In Place

Sed can edit the original file with the **-i** option.

	$ sed -i 's/mark twain/Tom Sawyer/' twain.txt

And make a backup if a suffix is given.

	$ sed -i.bak 's/mark twain/Tom Sawyer/' twain.txt

### Write to a File

The **w** instruction writes changes to the named file. The **-n** option suppresses output to the command line.

	 $ sed -n 's/Mark/Tom/w twain.new' twain.txt

### Display Pattern

Here `sed` just displays the pattern "PASS" at the start of a line.

	$ sed -n '/^PASS/p' /etc/login.defs

### Replace the Default Separator

If you need to replace a string that contains the forward slash (**/**) multiple times you can replace the separator with another rather than escaping each instance.

Instead of:

	$ sed 's/http:\/\/example.com\/tux\//http:\/\/tux.example.com/' linux.txt

You can substitute another character for the separator.

	$ sed 's_http://example.com/tux/_http://tux.example.com_' linux.txt

## Resources

- [GNU sed Users' Manual](https://www.gnu.org/software/sed/manual/)
- [Sed by Example](http://www.ibm.com/developerworks/library/l-sed1/)
- [Introducing filters and regular expressions](http://www.ibm.com/developerworks/aix/tutorials/au-unixtips3/index.html)
- [POSIX Character Classes](http://www.regular-expressions.info/posixbrackets.html)

> Written with [StackEdit](https://stackedit.io/).