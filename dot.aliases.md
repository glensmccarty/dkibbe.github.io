```bash
#################################################################
# To list active aliases, run:                                  #
# alias                                                         #
#                                                               #
# To see names of all active functions, run:                    #
# declare -F                                                    #
#                                                               #
# To see the names and definitions of all active functions.     #
# declare -f                                                    #
#################################################################

# Backup to Blackbox
blackbox() {

  [ -d /run/media/dennisk/blackbox ]

  if [ $? = 0 ]; then
  rsync -aqz --delete --exclude .cache --exclude .mozilla --progress /home/dennisk /run/media/dennisk/blackbox/ 2>/dev/null
  sleep 5
  df -h /run/media/dennisk/blackbox
  else
    echo 'Did you mount the external drive?'
  fi 
}

# Use Ditaa to create a PNG.
ditaa() { java -jar ~/bin/ditaa.jar $1; }

# Simple way to make a backup of a file: backup [file]
backup() { cp "$1"{,.$(date +%Y%b%d)};}

# Generate passwords
alias genpasswd="strings /dev/urandom | grep -o '[[:alnum:]]' | head -n 30 | tr -d '\n'; echo"

alias du="du -ach | sort -h"

alias free="free -mt"

# List disk usage in human-readable units including filesystem type, and print a total at the bottom:
alias df="df -Tha --total"

alias ps="ps auxf"

alias df="df -Tha --total"

# Searches our process for an argument we'll pass:
alias psg="ps aux | grep -v grep | grep -i -e VSZ -e"

alias mkdir="mkdir -pv"

# Find files in current directory easily.
alias fhere="find . -iname "

# An alias to pipe our output to less for viewing large directory listings with the long format.
alias lsl="ls -lhFA | less"

# Clear the screen
alias c="clear"

# Download entirely a website: websiteget [URL]
alias websiteget="wget --random-wait -r -p -e robots=off -U mozilla"

# Show which applications are connecting to the network.
alias listen="lsof -P -i -n"

# These are for MST150SV
alias nyc1s="xfreerdp -f -u student 140.198.245.197:6092"
alias nyc2s="xfreerdp -f -u student 140.198.245.197:6093"
alias nyc1a='xfreerdp -f -u contoso\Administrator 140.198.245.197:6092'
alias nyc2a='xfreerdp -f -u contoso\Administrator 140.198.245.197:6093'
```


> Written with [StackEdit](https://stackedit.io/).