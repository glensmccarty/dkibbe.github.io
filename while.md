```bash
#!/bin/bash

NUM=21
MAX=20

while [ "$NUM" -gt "$MAX" ]
do
echo $NUM
let "NUM += 1"

done
```
