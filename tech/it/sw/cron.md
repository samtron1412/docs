[TOC]

# Overview

- How to use cron: https://opensource.com/article/17/11/how-use-cron-linux
- Editing with `crontab -e` since when you close the file it
  automatically restart the service for you
- Sample

```
# crontab -e
SHELL=/bin/bash
MAILTO=root@example.com
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin

# For details see man 4 crontabs

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed

# backup using the rsbu program to the internal 4TB HDD and then 4TB external
01 01 * * * /usr/local/bin/rsbu -vbd1 ; /usr/local/bin/rsbu -vbd2

# Set the hardware clock to keep it in sync with the more accurate system clock
03 05 * * * /sbin/hwclock --systohc

# Perform monthly updates on the first of the month
# 25 04 1 * * /usr/bin/dnf -y update
```

# Usage

- `<second> <minute> <hour> <day-of-month> <month> <day-of-week> <year(optional)>`
    + second: 0-59
    + minute: 0-59
    + hour: 0-23
    + day-of-month: 1-31
    + month: 0-11 or JAN-DEC
    + day-of-week: 1-7 or SUN-SAT
    + year (optional): empty or 1970-2099
- `*`: means any values (always)
- `?`: no specific value
    + It is allowed for the day-of-month and day-of-week fields
    + It is used instead of the asterisk `*` for leaving either
      day-of-month or day-of-week blank.
- Tool to describe or generate cron expression
    + https://www.freeformatter.com/cron-expression-generator-quartz.html
- Some other format of cron, people ignore certain fields
    + AWS CloudWatch cron: ignore the second part

# References

[wiki]: https://en.wikipedia.org/wiki/Cron
[gwiki]: https://wiki.gentoo.org/wiki/Cron
[awiki]: https://wiki.archlinux.org/index.php/Cron
[systemd-timer]: https://wiki.archlinux.org/index.php/Systemd/Timersing
