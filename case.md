```bash
#!/bin/bash

# Created 09/16/2015
# *******

# Set variables

object=""
objFlag="BAD"

until [ "$objFlag" == "GOOD" ]; do
   echo -n "Pick rock, paper or scissors: "
   read object
   objFlag="GOOD"

# Convert input to lower case.
   object=${object,,}

   case $object in 
      rock)     echo "Paper beats Rock."     ;;
      paper)    echo "Scissors beats Paper." ;;
      scissors) echo "Rock beats Scissors."  ;;
      *)        echo "Invalid input."        ; objFlag="BAD" ;;
   esac
done

# END
```
