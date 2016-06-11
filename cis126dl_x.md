## Overview

Linux is a module system.  Like Legos the components can be combined in different ways.  This includes the graphical user interface (GUI).

## Assignment Objectives

*When you have successfully completed this assignment you will be able to:*

- Explain the role of the X server.
- Start an application on the display.
- Describe the function of the window manager.

## Terms You Should Know

- **Desktop Environment** - Such as GNOME, KDE, XFCE, Enlightenment provide custom apps like a file manager, calculator, editor, graphical front ends for managing printers, keyboards, etc.

- **Window Manager** - Handles the placement and size of windows on the desktop and the window decorations.

- **X Window** - The GUI server Linux *Note:* X Window *not* X Windows

- **Virtual Terminal** - Non-graphical terminals accessible outside of the GUI.

- **GUI** - Graphic User Interface.

- **CLI** - Command Line Interface

- **GNOME** - The GNOME shell is one of the most popular desktop environments.

- **KDE** - KDE is a popular desktop environments.

## Preparation

Boot the Ubuntu Cd or a LiveUSB for this assignment.

## Virtual Terminals

Outside the glaring graphical facade of the desktop is the inky blackness that is the virtual terminal.  There are six *Ctrl+Alt+F1* to *Ctrl+Alt+F6* with *Ctrl+Alt+F7* returning you to the GUI.  Some distros swap *F7* and *F1* putting the GUI on *F1*.  If there is some program locking up the browser (Flash comes to mind) you can abandon the GUI and swiftly dispatch the offender from a virtual terminal.

1. Type *Ctrl+Alt+F1* to go to the first virtual terminal.
2. Log in with your user name and password.  Unlike the GUI the terminal does not show and character when you type your password.
3. Type `w` to list the users logged in.  You will see that you are logged in twice.
4. Type *Ctrl+Alt+F7* to return to the GUI.

## Starting Another Desktop

  Linux can have multiple desktops running at once.

1. Type *Ctrl+Alt+F1* to reach a virtual terminal.
2. Type `startx -- **:1` which will start a new desktop on *Ctrl+Alt+F8*.
3. Type *Ctrl+Alt+F7* to see your main desktop.
4. Type *Ctrl+Alt+F8* and you out.  You will be returned to the virtual terminal where you launched the desktop.
5. Try to start `mousepad`.  You can't because Mousepad is a graphical program
6. Start X (capital) `X :1&`.  The ampersand places the program in the background so you can start other programs from the prompt.
7. A new display starts on *Ctrl+Alt+F8*.  This is just the xorg graphical server -- **nothing but a black screen.
8. Type *Ctrl+Alt+F1* to return to the virtual terminal 1.
9. Start `mousepad` on display 1 `mousepad --display :1&`
10. Go to *Ctrl+Alt+F8*.  Mousepad is running but you can't move it around or resize it.
11. Start `xfce4-about` on display 1 `xfce4-about --display :1&`
12. About XFCE obstructs Mousepad and again you can't move it around or resize it.  You need a way to manage windows.

## Window Maker
  
Window Maker is a simple window manager that, well, manages windows.  Start it on display 1

	$ wmaker --display :1&

Now return to the desktop and you'll something much different.  You can access a menu by right clicking the desktop.

When you are finished close About XFCE but leave Mousepad open. Select *Session, Exit* from the Window Maker menu to close Window Maker.  Notice you can no longer move or resize Mousepad.  

## COMMENT Troubleshoot the Assignment

## What to Submit

Copy and paste these questions along with your answers into the submission text-box (not the comment box) to receive credit for this assignment.

1. What desktop environment is on your workstation?
2. Try starting a display :2 with Enlightenment.

## Resources

- [How to Coose the Best Linux Desktop for You](http://www.linux.com/learn/tutorials/783109-how-to-choose-the-best-linux-desktop-for-you/)
- [Window Maker](http://windowmaker.org)
- [Fluxbox](http://windowmaker.org)
- [Enlightenment](http://www.enlightenment.org)