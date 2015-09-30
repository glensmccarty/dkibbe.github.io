``` bash
#! /bin/bash

# Variables

PS3="Choose Rock, Paper, Scissors, or Quit by number. "

#Commands

select item in "Rock" "Paper" "Scissors" "Quit"
do
  if [[ $item = "Rock" ]]
  then echo "Paper beats Rock."
  break
  elif [[ $item = "Paper" ]]
  then echo "Scissors beats Paper."
  break
  elif [[ $item = "Scissors" ]]
  then echo "Rock beats Scissors."
  break
  elif [[ $item = "Quit" ]]
  then echo "Exit I will"
  exit
  fi
done

# END

```
