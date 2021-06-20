[TOC]

# Overview

Something

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
