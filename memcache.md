[TOC]

# Overview


# Tutorial
## Linux
- View stats of memcached: `$ memcached-tool localhost:11211 stats`
- Display all keys: `$ memcached-tool localhost:11211`
- Dump key and values to file: `$ memcached-tool localhost:11211 dump > file`
- Reset all memcached
	+ Restart service it will remove all items: `# service memcached restart`
	+ Flush all it just mark items as expired and not remove items
		* `$ telnet localhost 11211`
		* `flush all`
- Verify memcached is running:
	+ `pgrep memcached`
	+ `netstat -tulpn|grep :11211`


## Windows
### Config memcached service
To edit the memcached server configuration, open regedit and go to `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\memcached`, then find and edit the ImagePath

	"C:\memcached_win32\memcached.exe" -d runservice -m 256 -p 11210

Example running memcached with 256 M and on port 11210

Can change start parameters of service


	-p <num>      TCP port number to listen on (default: 11211)
	-U <num>      UDP port number to listen on (default: 11211, 0 is off)
	-s <file>     UNIX socket path to listen on (disables network support)
	-a <mask>     access mask for UNIX socket, in octal (default: 0700)
	-l <ip_addr>  interface to listen on (default: INADDR_ANY, all addresses)
	-s <file>     unix socket path to listen on (disables network support)
	-a <mask>     access mask for unix socket, in octal (default 0700)
	-l <ip_addr>  interface to listen on, default is INADDR_ANY
	-d start          tell memcached to start
	-d restart        tell running memcached to do a graceful restart
	-d stop|shutdown  tell running memcached to shutdown
	-d install        install memcached service
	-d uninstall      uninstall memcached service
	-r            maximize core file limit
	-u <username> assume identity of <username> (only when run as root)
	-m <num>      max memory to use for items in megabytes (default: 64 MB)
	-M            return error on memory exhausted (rather than removing items)
	-c <num>      max simultaneous connections (default: 1024)
	-k            lock down all paged memory.  Note that there is a
	              limit on how much memory you may lock.  Trying to
	              allocate more than that would fail, so be sure you
	              set the limit correctly for the user you started
	              the daemon with (not for -u <username> user;
	              under sh this is done with 'ulimit -S -l NUM_KB').
	-v            verbose (print errors/warnings while in event loop)
	-vv           very verbose (also print client commands/reponses)
	-vvv          extremely verbose (also print internal state transitions)
	-h            print this help and exit
	-i            print memcached and libevent license
	-P <file>     save PID in <file>, only used with -d option
	-f <factor>   chunk size growth factor (default: 1.25)
	-n <bytes>    minimum space allocated for key+value+flags (default: 48)
	-L            Try to use large memory pages (if available). Increasing
	              the memory page size could reduce the number of TLB misses
	              and improve the performance. In order to get large pages
	              from the OS, memcached will allocate the total item-cache
	              in one large chunk.
	-D <char>     Use <char> as the delimiter between key prefixes and IDs.
	              This is used for per-prefix stats reporting. The default is
	              ":" (colon). If this option is specified, stats collection
	              is turned on automatically; if not, then it may be turned on
	              by sending the "stats detail on" command to the server.
	-t <num>      number of threads to use (default: 4)
	-R            Maximum number of requests per event, limits the number of
	              requests process for a given connection to prevent
	              starvation (default: 20)
	-C            Disable use of CAS
	-b            Set the backlog queue limit (default: 1024)
	-B            Binding protocol - one of ascii, binary, or auto (default)
	-I            Override the size of each slab page. Adjusts max item size
	              (default: 1mb, min: 1k, max: 128m)


### List all keys
In the general case, there is no way to list all the keys that a memcached instance is storing. You can, however, list something like the first 1Meg of keys, which is usually enough during development. Here’s how:

Telnet to your server:

	telnet 127.0.0.1 11211

List the items, to get the slab ids:

	stats items
	STAT items:3:number 1
	STAT items:3:age 498
	STAT items:22:number 1
	STAT items:22:age 498
	END

The first number after ‘items’ is the slab id. Request a cache dump for each slab id, with a limit for the max number of keys to dump:

	stats cachedump 3 100
	ITEM views.decorators.cache.cache_header..cc7d9 [6 b; 1256056128 s]
	END

	stats cachedump 22 100
	ITEM views.decorators.cache.cache_page..8427e [7736 b; 1256056128 s]
	END
