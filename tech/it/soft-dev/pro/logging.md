[TOC]

# Overview

- Logger: capture the message
- Formatter: format the message
- Handler/Appender: deliver the message to sources (write to files, db,
  etc.)

# Logger

- Name
- Severity level
    + fatal
        * severe errors that cause premature termination
        * expect these to be immediately visible on a status console
    + error
        * runtime errors or unexpected conditions
        * expect these to be immediately visible on a status console
    + warning
    + info
        * interesting runtime events
        * expect these to be immediately visible on a console
    + debug
        * detailed information on the flow through the system
        * expect these to be written to logs only
    + trace
        * more detailed information
        * expect these to be written to logs only

# References

[java-logging]: https://en.wikipedia.org/wiki/Java_logging_framework
