# System Activity Report (SAR)

## Introduction

"Learn how to correlate user complaints with the system activity reporter (SAR) and build a performance baseline for trending purposes using SAR logs. SAR is the perfect tool for systems administrators. It captures important system performance metrics at periodic intervals." -- IBM developerWorks

## Installation

	# yum install sysstat

## /etc/cron/d/sysstat

```
# Run system activity accounting tool every 10 minutes
*/10 * * * * root /usr/lib64/sa/sa1 1 1
# 0 * * * * root /usr/lib64/sa/sa1 600 6 &
# Generate a daily summary of process accounting at 23:53
53 23 * * * root /usr/lib64/sa/sa2 -A
```
## Displaying SAR stats

### Collecting data in log

	# /usr/lib64/sa/sa1

### Print out today's data

	# /usr/lib64/sa/sa2 -A

### Display basic data

	# LANG=C sar -q

### Disk Activity

	# sar 1 3

	# sar -P o

	# sar 1 10

	# sar -b
	
	# sar -n DEV

## Configure

	# alias sar='LANG=C sar'

### History

The default is to create data for 28 days.


## Resources

 - [Easy system monitoring with SAR](https://www.ibm.com/developerworks/aix/library/au-unix-perfmonsar.html)
 - [lide Share Presentation](http://www.slideshare.net/brendangregg/linux-performance-analysis-and-tools/34-sar_System_Activity_Reporter_Eg)
 - [SAR Examples](http://www.thegeekstuff.com/2011/03/sar-examples/)

							c


> Written with [StackEdit](https://stackedit.io/).