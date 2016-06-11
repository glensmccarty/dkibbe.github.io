# Using script to Record a Bash Session

The `script` command records the commands you type in the shell. You play the session back with the `scriptreplay` command.

## Recording the Session

	$ script --timing=<name_of_timing_file>
	Script started, file is typescript
	
This will record all commands in the `typescript` file.

Type `exit` to stop and end the recording session.

	$ exit
	Script done, file is typescript

The default record file is `typescript` but you use a different file name to keep a collection of scripts.

	$ script --timing=myscript.timing myscript
	Script started, file is myscript

## Playback

The `scriptreplay` command will replay the commands in real time if a timing file was used.

	$ scriptreplay -t <name_of_timing_file>

If you used a custom name be sure to include it:

	$ scriptreplay myscript.timing myscript

You can use `less `to view the typescript file.

	$ less -r typescript

## Resources

 - script manpage
 - scriptreplay manpage

> Written with [StackEdit](https://stackedit.io/).