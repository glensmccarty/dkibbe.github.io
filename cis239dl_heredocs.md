# Here Documents

A here document contained in a script can be used to deliver information when the script is run similar to the `echo` command. Here is an example from Greg's Bash Guide:


	usage() {
	    cat <<EOF
		usage: foobar [-x] [-v] [-z] [file ...]
		A short explanation of the operation goes here.
		It might be a few lines long, but shouldn't be 	excessive.
		EOF
	}


The actual here document starts with `cat` and ends with **EOF**. The text between the End Of File markers is the text that is printed out. To make the here document easier to call in thwe script it has been wrapped in a function.

If the text of the here Doc is indented with Tabs. use the dash (**-**) option to remove them before printing.

	cat <<-EOF

## Feeding Data to a Command

Just as text is feed to the screen using `cat` data can be input to a command the same way.

	ftp -n << EOF
	open mirrors.xmission.com
	user anonymous nothinghere
	ascii
	cd gutenberg
	get GUTINDEX.01
	bye
	EOF

## What to Submit

Create a script containing a here document that prints the following information. 

	Today is Tuesday
	You are logged into a Linux system named xps13.
	Here is some info about the root partition:
	Filesystem      Size  Used Avail Use% Mounted on
	/dev/sda4        99G   26G   68G  28% /

In your script **Tuesday**, **Linux**, **xps13** and the last line (**/dev/sda4...**) should be replaced with the appropriate values from the system the script will be run on.

## Resources

 - [Heredocs and Herestrings](http://mywiki.wooledge.org/BashGuide/InputAndOutput#Heredocs_And_Herestrings)
 - [Introduction to text manipulation on UNIX-based systems](http://www.ibm.com/developerworks/aix/library/au-unixtext/)

> Written with [StackEdit](https://stackedit.io/).<!--se_discussion_list:{"IDHTZ2uVl5FJYtn7Z37y6brk":{"selectionStart":982,"selectionEnd":996,"commentList":[{"content":"cat << EOF\nToday is $(date +%A)\nYou are logged into a $(uname) system named $(hostname).\nHere is some info about the root partition:\nFilesystem      Size  Used Avail Use% Mounted on\n$(df -h | grep -E \\/$)\nHave a nice day!\nEOF"}],"discussionIndex":"IDHTZ2uVl5FJYtn7Z37y6brk"}}-->