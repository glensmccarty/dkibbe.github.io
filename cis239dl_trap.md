# Traps

In bash you can use the `trap` command to catch certain signals then run a command based on the trap.  This script will *trap* SIGINT and SIGTERM. SIGKILL is required to stop the process.

```bash
#!/usr/bin/env bash

# Author: Tux
# Script to demo trap

trap "echo 'You pressed CTL+C!'" INT
trap "echo 'You tries to kill me'" TERM

while true

do

sleep 60

done
```
## Resources

 - [How "Exit Traps" Can Make Your Bash Scripts Way More Robust And Reliable](http://redsymbol.net/articles/bash-exit-traps/)
 - [Bash Guide](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_12_02.html)

> Written with [StackEdit](https://stackedit.io/).