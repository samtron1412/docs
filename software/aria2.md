[TOC]

# Overview
aria2 is a lightweight multi-protocol and multi-source command-line download utility.

The executable name for the aria2 package is `aria2c`. This legacy naming convention has been retained for backwards compatibility.

# Configuration
aria2 looks to `$XDG_CONFIG_HOME/aria2/aria2.conf` for a set of global configuration options by default.

This behavior can be modified with the `--conf-path` switch.

## Common options
`continue`: continue downloading a partially downloaded file if a corresponding control file exists.

`dir=.`: Store the downloaded file(s) in `.`

`file-allocation=none`: Do not pre-allocate disk space before downloading begins.

`max-connection-per-server=8`: Set a maximum of eight (8) connections to each server per file.

`min-split-size=5M`: Only split the file if the size is larger than 2*5MB = 10MB

`enable-http-pipelining=true`: Enable HTTP/1.1 pipelining to overcome network latency and to reduce network load.

`daemon=true`: Run as daemon

## Running options
`--checksum=sha-1=0192ba11326fe2298c8cb4de616f4d4140213838`

`--dry-run=true`: aria2 just checks whether the remote file is available and doesn't download data.

`--out=<file-name>`: The file name of the downloaded file. When the `--force-sequential` option is used, this option is ignored.

