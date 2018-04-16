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

# Different practices for logging

## Verbose mode for the limitation to the production environment

- Selling code to bank, hospital, and others.

DEBUG Level

Any parameters passed into the method
Any row counts from result sets I retrieve
Any datarows that may contain suspicious data when being passed down to the method
Any "generated" file paths, connection strings, or other values that could get mungled up when being "pieced together" by the environment.
INFO Level

The start and end of the method
The start and end of any major loops
The start of any major case/switch statements
ERROR Level

Handled exceptions
Invalid login attempts (if security is an issue)
Bad data that I have intercepted forreporting
FATAL Level

Unhandled exceptions.

# References

[java-logging]: https://en.wikipedia.org/wiki/Java_logging_framework
