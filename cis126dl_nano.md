
# The Nano Text Editor

Nano is a simple command line editor and is the default editor used by Ubuntu.  While not nearly as powerful as Vi or Emacs it is a good choice for newbies. Even so, you will want to learn the basics of Vi or Vim since this is the standard edit used by system administrators.

Need screenshot here.

## Custom Nano Configuration

If `~/.nanorc` exists `nano` will read it and use the custom configuration it finds. There is already sample configuration file that you can use as a template.

1. Open `/usr/share/doc/nano/example/nanorc.sample.gz` in Gedit. Since it's a compressed file you can't use `vi` or `nano`.
2. Copy the file to your home directory as `.nanorc
3. Edit the file as needed.

## Resources

 - [Nano Users Manual](http://www.nano-editor.org/dist/v2.5/nano.html)
 - [Improved Syntax Highlighting](https://github.com/nanorc/nanorc)
