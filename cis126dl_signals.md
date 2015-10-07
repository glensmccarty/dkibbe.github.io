# Signals

## File Descriptors

`/proc/$$/fd/`

## Signals

## Program Termination

Let's create a run-away process

``` bash
$ cat /dev/zero >/dev/null
```

### Find the PID

Open a new terminal to run `ps` and find the PID.
``` bash
$ ps -ef | grep cat
```

### Kill the Process

Once you know the PID you can terminate the process SIGTERM.

``` bash
$ kill <PID>
```

## Trapping Signals

## Resources


> Written with [StackEdit](https://stackedit.io/).