# Killing a Run Away Process

Sometimes a process can get out of hand and drain system resources. It's important to identify a run away process and terminate it. In this assignment you will start a process to drive up CPU usage and than use various command line tool to identify and terminate the run away process.

## Commands and Terms You Should Know

Process
: A computer program in action

&
: An Ampersand following a command put the command in the background.

jobs
: List jobs running in the background.

fg
: Bring a backgrounded job to the foreground.

PID
: Process ID

ps
: Displays static information about processes.

ptree
: Displays a hierarchical view of processes.

top
: Provides a dynamic real-time view of a running system.

htop
: An interactive process view that allows scrolling.

init
: init is the parent of all processes on the system.

nice
: Run a program with modified scheduling priority.

renice
: Alter priority of a running process.

kill
: Terminate a running process.

signal
: Linux supports standard signals (SIGTERM, SIGKILL). See Resources below.

## Preparation

This lab can be done on any virtual machine.

## Process States

As a process executes it changes state according to its circumstances. Linux processes have the following states:

Running
: The process is either running (it is the current process in the system) or it is ready to run (it is waiting to be assigned to one of the system's CPUs).

Waiting
: The process is waiting for an event or for a resource. Linux differentiates between two types of waiting process; interruptible and uninterruptible. Interruptible waiting processes can be interrupted by signals whereas uninterruptible waiting processes are waiting directly on hardware conditions and cannot be interrupted under any circumstances.

Stopped
: The process has been stopped, usually by receiving a signal. A process that is being debugged can be in a stopped state. 

Zombie
: This is a halted process whose parent died before it finished. A zombie process will be taken over by `init` and terminated.

## A CPU Hog

To simulate a runaway process redirect */dev/zero* which outputs an endless stream of zeros to */dev/null* which is a black hole. 

		$ cat /dev/zero >/dev/null

### Monitor the process

Open a new terminal and run the `top` command to see that the script is hogging CPU cycles.

![top](https://wm.sdf.org/gallery/albums/userpics/10081/top-cpuhog.jpg)

## Die, Process, Die!

## Getting the Correct PID

The first step to killing a run away process is to identify the Process ID. Use the `ps` command to identify the PID. *The PID number will be unique to your system.*

![ps][]

### "He's dead, Jim

The `kill` command is used to terminate processes.

		$ kill pid_number

After running the command you should see the process disappear from the `top`.

### SIGTERM
	
The `kill` command sends the *SIGTERM 15* signal to the process asking it to terminate and clear up any temporary files.

### SIGKILL

You can also send the more powerful *SIGKILL 9* signal which kills the process if it doesn't respond to  SIGTERM.

		$ kill -9 pid_number

Use *SIGKILL* only as a last resort since it can leave temporary behind.

## Nice and Renice

The priority of a process can be changed with these commands. Only the root or superuser raise the prioity of a process.



## Background

Placing a process in the background is useful.

## Zombies!

Download this [small C program][zombie] to create zombie processes.

Make the program executable and run it from the command line.

		$ chmod +x zombies
		$ ./zomie

Use the techniques you used above to find and remove the zombie process.

## What to Submit

Submit a screenshot of the */dev/zero > /dev/null* process running in `top`.

## Resources

+ man init
+ man 7 signal
+ man ps
+ [The Linux Kernel][The Linux Kernel]
+ [An Overview of Linux Processes][An Overview of Linux Processes]
+ [A small C program to create zombie processes][zombie]
+ [White Zombie (1932)][White Zombie]

[top]: https://wm.sdf.org/gallery/albums/userpics/10081/top-cpuhog.jpg "cpuhog script running in top"
[ps]: https://wm.sdf.org/gallery/albums/userpics/10081/ps-cpuhog.jpg "cpuhog script running in ps"
[The Linux Kernel]: http://www.tldp.org/LDP/tlk/kernel/processes.html "The Linux Kernel"
[An Overview of Linux Processes]: https://www.ibm.com/developerworks/community/blogs/58e72888-6340-46ac-b488-d31aa4058e9c/entry/an_overview_of_linux_processes21?lang=en "An Overview of Linux Processes"
[zombie]: http://dennisk.freeshell.org/zombie "A program to create zombies"
[White Zombie]: https://www.youtube.com/watch?v=g3JGItKPT8g "White Zombie (1932)"



