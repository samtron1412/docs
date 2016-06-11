[TOC]

# Overview



# Installation
## From source
- Install required dependencies
		yum install make gcc automake zlib-devel bison cmake libtool wget gcc-c++ unzip ncurses-devel openssl-devel pcre-devel libxml2-devel curl-devel gd-devel libxslt-devel apr-util-devel
- Get source: `https://archive.apache.org/dist/httpd/`
- Extract: `tar xzf <file>`
- Change dir
- [Configure](http://httpd.apache.org/docs/2.2/programs/configure.html)
	+ `/configure --enable-core --enable-ssl --with-mpm=worker --enable-proxy --enable-headers --enable-expires --enable-deflate --enable-filter --disable-dav --disable-negotiation --disable-cgid --disable-actions --disable-userdir --enable-so --enable-rewrite --with-included-apr --with-expat=builtin`
- `make && make install`
- `apachectl start`

## httpd service script
Create a script `/etc/init.d/httpd`

### Basic script

	#!/bin/bash
	#
	# Startup script for the Apache Web Server
	#
	# chkconfig: 345 85 15
	# description: Apache is a World Wide Web server.  It is used to serve \
	#           HTML files and CGI.
	# processname: httpd
	# pidfile: /usr/local/apache2/logs/httpd.pid
	# config: /usr/local/apache2/conf/httpd.conf

	# Source function library.
	. /etc/rc.d/init.d/functions

	# See how we were called.
	case "$1" in
	start)
	echo -n "Starting httpd: "
	daemon /usr/local/apache2/bin/httpd -DSSL
	echo
	touch /var/lock/subsys/httpd
	;;
	stop)
	echo -n "Shutting down http: "
	killproc httpd
	echo
	rm -f /var/lock/subsys/httpd
	rm -f /usr/local/apache2/logs/httpd.pid
	;;
	status)
	status httpd
	;;
	restart)
	$0 stop
	$0 start
	;;
	reload)
	echo -n "Reloading httpd: "
	killproc httpd -HUP
	echo
	;;
	*)
	echo "Usage: $0 {start|stop|restart|reload|status}"
	exit 1
	esac

	exit 0

### Advanced script

	#!/bin/bash
	#
	# httpd        Startup script for the Apache HTTP Server
	#
	# chkconfig: - 85 15
	# description: The Apache HTTP Server is an efficient and extensible  \
	#	       server implementing the current HTTP standards.
	# processname: httpd
	# config: /etc/httpd/conf/httpd.conf
	# config: /etc/sysconfig/httpd
	# pidfile: /var/run/httpd/httpd.pid
	#
	### BEGIN INIT INFO
	# Provides: httpd
	# Required-Start: $local_fs $remote_fs $network $named
	# Required-Stop: $local_fs $remote_fs $network
	# Should-Start: distcache
	# Short-Description: start and stop Apache HTTP Server
	# Description: The Apache HTTP Server is an extensible server
	#  implementing the current HTTP standards.
	### END INIT INFO

	# Source function library.
	. /etc/rc.d/init.d/functions

	if [ -f /etc/sysconfig/httpd ]; then
	        . /etc/sysconfig/httpd
	fi

	# Start httpd in the C locale by default.
	HTTPD_LANG=${HTTPD_LANG-"C"}

	# This will prevent initlog from swallowing up a pass-phrase prompt if
	# mod_ssl needs a pass-phrase from the user.
	INITLOG_ARGS=""

	# Set HTTPD=/usr/sbin/httpd.worker in /etc/sysconfig/httpd to use a server
	# with the thread-based "worker" MPM; BE WARNED that some modules may not
	# work correctly with a thread-based MPM; notably PHP will refuse to start.

	# Path to the apachectl script, server binary, and short-form for messages.
	apachectl=/usr/sbin/apachectl
	httpd=${HTTPD-/usr/sbin/httpd}
	prog=httpd
	pidfile=${PIDFILE-/var/run/httpd/httpd.pid}
	lockfile=${LOCKFILE-/var/lock/subsys/httpd}
	RETVAL=0
	STOP_TIMEOUT=${STOP_TIMEOUT-10}

	# The semantics of these two functions differ from the way apachectl does
	# things -- attempting to start while running is a failure, and shutdown
	# when not running is also a failure.  So we just do it the way init scripts
	# are expected to behave here.
	start() {
	        echo -n $"Starting $prog: "
	        LANG=$HTTPD_LANG daemon --pidfile=${pidfile} $httpd $OPTIONS
	        RETVAL=$?
	        echo
	        [ $RETVAL = 0 ] && touch ${lockfile}
	        return $RETVAL
	}

	# When stopping httpd, a delay (of default 10 second) is required
	# before SIGKILLing the httpd parent; this gives enough time for the
	# httpd parent to SIGKILL any errant children.
	stop() {
		echo -n $"Stopping $prog: "
		killproc -p ${pidfile} -d ${STOP_TIMEOUT} $httpd
		RETVAL=$?
		echo
		[ $RETVAL = 0 ] && rm -f ${lockfile} ${pidfile}
	}
	reload() {
	    echo -n $"Reloading $prog: "
	    if ! LANG=$HTTPD_LANG $httpd $OPTIONS -t >&/dev/null; then
	        RETVAL=6
	        echo $"not reloading due to configuration syntax error"
	        failure $"not reloading $httpd due to configuration syntax error"
	    else
	        # Force LSB behaviour from killproc
	        LSB=1 killproc -p ${pidfile} $httpd -HUP
	        RETVAL=$?
	        if [ $RETVAL -eq 7 ]; then
	            failure $"httpd shutdown"
	        fi
	    fi
	    echo
	}

	# See how we were called.
	case "$1" in
	  start)
		start
		;;
	  stop)
		stop
		;;
	  status)
	        status -p ${pidfile} $httpd
		RETVAL=$?
		;;
	  restart)
		stop
		start
		;;
	  condrestart|try-restart)
		if status -p ${pidfile} $httpd >&/dev/null; then
			stop
			start
		fi
		;;
	  force-reload|reload)
	        reload
		;;
	  graceful|help|configtest|fullstatus)
		$apachectl $@
		RETVAL=$?
		;;
	  *)
		echo $"Usage: $prog {start|stop|restart|condrestart|try-restart|force-reload|reload|status|fullstatus|graceful|help|configtest}"
		RETVAL=2
	esac

	exit $RETVAL


# Request life cycle
Think of it like this:

**DNS** is the *phone directory/yellow pages*. When someone wants to call your phone, they can look up your name and get your phone number and call that phone. DNS does the same but for computers - when someone wants to go to `www.example.com` they ask DNS for the IP address and then they can contact the computer that has that IP address. That is what **resolve** means. Resolving an IP address has nothing at all to do with Apache; it is strictly a DNS question.

The `ServerName` and `ServerAlias` is more like **a company's internal phone list**. Your webserver is the switchboard; it will accept all incoming connections to the server. Then the client/caller will tell them what name they're looking for, and it will look in the Apache configuration for how to handle that name.

If the name isn't listed as a ServerName/ServerAlias in the apache configuration, apache will always give them the **first VirtualHost listed**. Or, if there's **no VirtualHost at all, it will give the same content no matter what hostname is given in the request**.

ETA: So, step by step for a normal connection:

1. You type "http://www.example.com" into your browser.
2. Your computer asks its DNS resolver which IP address it should use when it wants to talk to www.example.com.
3. Your computer connects to that IP address, and says that it wants to talk to www.example.com (that's the Host:header in HTTP).
4. The webserver looks at its configuration to figure out what to do with a request for content from www.example.com. Any one of the following may happen:
- www.example.com is listed as a ServerName or ServerAlias for a VirtualHost - if so, then it will use the configuration for that VirtualHostto deliver the content.
- The server doesn't have any VirtualHosts at all - if so, then it will use the configuration in its httpd.conf to deliver the content.
- The server has VirtualHosts but www.example.com isn't listed in any of them - if so, the first Virtualhost in the list will be used to deliver the content.

# Configuration
## VirtualHost
The term Virtual Host refers to the practice of running more than one web site (such as **company1.example.com** and **company2.example.com**) on a single machine. Virtual hosts can be "IP-based", meaning that you have a different IP address for every web site, or "name-based", meaning that you have multiple names running on each IP address. The fact that they are running on the same physical server is not apparent to the end user.

[Examples](https://httpd.apache.org/docs/2.2/vhosts/examples.html)

```
<VirtualHost *:81>
    ServerAdmin tran.son@rivercrane.vn
    DocumentRoot "/vagrant/projects"
    ServerName projects.rivercrane.vn
    ServerAlias www.projects.rivercrane.vn
    ErrorLog "logs/projects.rivercrane.vn.com-error.log"
    CustomLog "logs/projects.rivercrane.vn-access.log" common
    RewriteEngine On

    # Inherit rewrite rule from basic host
    # RewriteOptions Inherit
</VirtualHost>

<Directory "/vagrant/projects">
    Options FollowSymLinks
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>
```

## .htaccess
### [Tips and Tricks](http://web.archive.org/web/20150602131726/http://www.askapache.com/htaccess/modrewrite-tips-tricks.html)

## Ubuntu
httpd version 1
`/etc/httpd/`
- conf : store httpd.conf file
- conf.d : store modules's config file, like subversion, it will load to config
- logs : access-log and error-log
- modules


httpd version 2
`/etc/apache2/`
- apache2.conf
- ports.conf
- mods-enabled
	+ *.load
	+ *.conf
- conf-enabled
	+ *.conf
- sites-enabled
	+ *.conf

## mod rewrite_rule
file rewrite_rule.conf (maybe have another name) contain all rewrite rule for apache server. It is included to httpd.conf.

### List of Mod_Rewrite Variables
	API_VERSION
	AUTH_TYPE
	CONTENT_LENGTH
	CONTENT_TYPE
	DOCUMENT_ROOT
	GATEWAY_INTERFACE
	IS_SUBREQ
	ORIG_PATH_INFO
	ORIG_PATH_TRANSLATED
	ORIG_SCRIPT_FILENAME
	ORIG_SCRIPT_NAME
	PATH
	PATH_INFO
	PHP_SELF
	QUERY_STRING
	REDIRECT_QUERY_STRING
	REDIRECT_REMOTE_USER
	REDIRECT_STATUS
	REDIRECT_URL
	REMOTE_ADDR
	REMOTE_HOST
	REMOTE_IDENT
	REMOTE_PORT
	REMOTE_USER
	REQUEST_FILENAME
	REQUEST_METHOD
	REQUEST_TIME
	REQUEST_URI
	SCRIPT_FILENAME
	SCRIPT_GROUP
	SCRIPT_NAME
	SCRIPT_URI
	SCRIPT_URL
	SCRIPT_USER
	SERVER_ADDR
	SERVER_ADMIN
	SERVER_NAME
	SERVER_PORT
	SERVER_PROTOCOL
	SERVER_SIGNATURE
	SERVER_SOFTWARE
	THE_REQUEST
	TIME
	TIME_DAY
	TIME_HOUR
	TIME_MIN
	TIME_MON
	TIME_SEC
	TIME_WDAY
	TIME_YEAR
	TZ
	UNIQUE_ID

#### HTTP Variables

	HTTP_ACCEPT
	HTTP_ACCEPT_CHARSET
	HTTP_ACCEPT_ENCODING
	HTTP_ACCEPT_LANGUAGE
	HTTP_CACHE_CONTROL
	HTTP_CONNECTION
	HTTP_COOKIE
	HTTP_FORWARDED
	HTTP_HOST
	HTTP_KEEP_ALIVE
	HTTP_PROXY_CONNECTION
	HTTP_REFERER
	HTTP_USER_AGENT

#### SSL Variables

	HTTPS
	SSL_CIPHER
	SSL_CIPHER_ALGKEYSIZE
	SSL_CIPHER_EXPORT
	SSL_CIPHER_USEKEYSIZE
	SSL_CLIENT_VERIFY
	SSL_PROTOCOL
	SSL_SERVER_A_KEY
	SSL_SERVER_A_SIG
	SSL_SERVER_CERT
	SSL_SERVER_I_DN
	SSL_SERVER_I_DN_C
	SSL_SERVER_I_DN_CN
	SSL_SERVER_I_DN_L
	SSL_SERVER_I_DN_O
	SSL_SERVER_I_DN_OU
	SSL_SERVER_I_DN_ST
	SSL_SERVER_M_SERIAL
	SSL_SERVER_M_VERSION
	SSL_SERVER_S_DN
	SSL_SERVER_S_DN_CN
	SSL_SERVER_S_DN_O
	SSL_SERVER_S_DN_OU
	SSL_SERVER_V_END
	SSL_SERVER_V_START
	SSL_SESSION_ID
	SSL_VERSION_INTERFACE
	SSL_VERSION_LIBRARY

### RewriteRule ^ - [L]

	RewriteCond %{REQUEST_FILENAME} -f [OR]
	RewriteCond %{REQUEST_FILENAME} -d
	RewriteRule ^ - [L]


- `^` is a somewhat unorthodox way of saying "match anything", just as you say
- `-` means "take no action"
- `[L]` means "last rule" i.e. stop processing RewriteRules after this point

I assume there are other rules following this one, because this combination of RewriteCond/RewriteRule says that if the current request is for an existing file or directory, mod_rewrite should ignore any subsequent RewriteRules.

### Internal Redirect Loop Protection
	RewriteCond %{ENV:REDIRECT_STATUS} 200
	RewriteRule ^ - [L]

## modules
- List all modules: `httpd -M` or `apachectl -M`
- httpd load modules follow two ways: `static` and `shared`
	+ `static`: the module willbe compiled into the Apache binary itself and will be loaded every time Apache is started.
	+ `shared`: the module will be compiled as dynamic shared library and you can choose whether you want to load it or not by `LoadModule` directive on `httpd.conf`.
	+ Apache may be faster with static modules but in order to remove or update an module you have to recompile the whole code.

### Multi-Processing Modules (mpm)
core module apache use to handle request, it depend on operating system. **It specify when compiled time.**

compiled with config: `./configure --with-mpm=<module_name>`

**Type of mpm**
- **Prefork**: non-threaded, spawn processes to handle request, compatible with everything, work with each request amd the rest wait on queue.
- **mpm_winnt**: optimized for Windows NT.
- **Worker**: threaded, concurrency, should use only at apache 2.2, apache 2.4
- **Event**: like Worker module, except hands request down to child threads only when a request has actually been made. only use at apache 2.4


# Tutorial
## How to setup multiple PHP versions on Apache
- [link1](http://blog.servergrove.com/2011/08/22/how-to-setup-multiple-php-versions-on-apache/)
- [link2](http://mossiso.com/2009/09/02/multiple-php-instances-with-one-apache.html)

# Troubleshoot
Check config syntax: `apachectl configtext`

## [(13) Permission Denied](https://wiki.apache.org/httpd/13PermissionDenied)
- **AH00132**: file permissions deny server access
- **AH00035**: access denied because search permissions are missing on a component of the paths

Set permission 755 for DocumentRoot up to root.

`chmod 755 home/webike/www`



## How to Fix “Starting httpd: httpd: apr_sockaddr_info_get() failed” and "httpd: Could not reliably determine the server's fully qualified domain name, using 1x.x.x.x for ServerName x.x.x.x is a public ip server !"
- Edit `/etc/hosts`: **127.0.0.1 vagrant.centos.global <domain name>**
- Edit `httpd.conf`: **ServerName www.vagrant.centos.global:80**
- Restart httpd service
