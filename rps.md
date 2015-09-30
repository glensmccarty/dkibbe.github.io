```bash
#! /bin/bash

# Variables
handsign=""

# Commands

echo "Choose Rock, Paper, or Scissors:"

read handsign

case $handsign in

[rR]ock ) echo "Paper beats rock." ;; 

[sS]cissors ) echo "Rock beats scissors." ;;

[pP]aper ) echo "Scissors beats paper." ;;

* ) echo "What?" ;;

esac

# END
```
