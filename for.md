```bash#! /bin/bash

# Purpose: Create a for loop that deletes files created previously

for myvar in "$(ls FILE[13579].txt)";
  do rm $myvar;
done

# END
```
