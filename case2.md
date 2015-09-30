```bash
#!/bin/bash

HAND="rock"

case $HAND in
rock)
echo "Rock vs Rock - Tie"
;;
paper)
echo "Paper beats Rock"
;;
scissors)
echo "Rock beats Scissors"
;;
*)  echo "That doesn't count"
commands_to_execute_for_no_match
;;
esac
```
