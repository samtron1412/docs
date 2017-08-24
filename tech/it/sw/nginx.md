[TOC]

# Overview
Nginx does not have any ability to process dynamic content natively. To handle PHP and other requests for dynamic content, Nginx must pass to an external processor for execution and wait for the rendered content to be sent back. The results can then be relayed to the client.


# [Configuration](https://www.linode.com/docs/websites/nginx/basic-nginx-configuration/)
All Nginx configuration files are located in the `/etc/nginx/` directory. The primary configuration file is `/etc/nginx/nginx.conf`.

Test nginx configuration file: `nginx -t`

## Templates
### Laravel
```
server {
    listen 80;
    server_name d.stavrovski.net www.d.stavrovski.net daniel.stavrovski.net;
    return 301 http://d.stavrovski.net$request_uri;

    access_log /var/log/nginx/d.stavrovski.net.log;
    error_log /var/log/nginx/d.stavrovski.net-error.log error;

    root /srv/www/d.stavrovski.net/public;
    index index.html index.php;

    ### ROOT DIRECTORY ###
    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    ### SECURITY ###
    error_page 403 =404;
    error_page 404 /404-not-found.html;

    location  /404-not-found.html {
        internal;
    }

    location ~* ^/uploads/.*.(html|htm|shtml|php)$ {
        types { }
        default_type text/plain;
    }

    location ~* ^/cache/.* {
        return 404;
    }

    #  location ~* admin {
    #      allow <YOUR_IP>;
    #      allow 127.0.0.1;
    #      deny all;
    #  }

    ### DISABLE LOGGING ###
    location = /robots.txt { access_log off; log_not_found off; }
    location = /favicon.ico { access_log off; log_not_found off; }

    ### CACHES ###
    location ~* \.(jpg|jpeg|gif|css|png|js|ico|html)$ { access_log off; expires max; }
    location ~* \.(woff|svg)$ { access_log off; log_not_found off; expires 30d; }
    location ~* \.(js)$ { access_log off; log_not_found off; expires 7d; }

    location /uploads/ {
        valid_referers none blocked d.stavrovski.net *.stavrovski.net;
        if ($invalid_referer) {
            return   403;
        }
    }

    fastcgi_buffers 256 16k;
    fastcgi_buffer_size 32k;
    fastcgi_connect_timeout 300;
    fastcgi_send_timeout 300;
    fastcgi_read_timeout 300;

    ### PHP BLOCK ###
    location ~ \.php?$ {
        fastcgi_keep_conn on;
        try_files $uri =404;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_intercept_errors on;
        fastcgi_split_path_info ^(.+\.php)(.*)$;
        fastcgi_hide_header X-Powered-By;
        # fastcgi_pass 127.0.0.1:9000;
        fastcgi_pass unix:/var/run/d.stavrovski.net.socket;
        # fastcgi_pass unix:/var/run/hhvm/hhvm.sock;
    }
}
```


## Starting, stopping, and reloading configuration
`nginx -s stop|quit|reload|reopen`

- stop: fast shutdown
- quit: graceful shutdown
- reload: reloading the configuration file
- reopen: reopening the log files

For example, to stop nginx processes with waiting for the worker processes to finish serving current requests, the following command can be executed: `nginx -s quit`

## Configuration File's Structure
nginx consists of modules which are controlled by directives specified in the configuration file.

Directives are divided into **simple directives** and **block directives**.

Simple directives: `<name> <parameters>;`

A block directive: `{ <name> <parameter> }`

A block directive can have other directives inside braces ({}), it is called a **context**.

The rest of a line after the `#` sign is considered a comment.

## Serving Static Resources
If there are several matching `location` blocks nginx selects the one with the **longest prefix**. The location block:

	location / {
	    root /data/www;
	}

above provides the shortest prefix, of length one, and so only if all other location blocks fail to provide a match, this block will be used.

## Setting Up FastCGI Proxying
	server {
	    location / {
	        fastcgi_pass  localhost:9000;
	        fastcgi_index  index.php;
	        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
          include        fastcgi_params;
	    }
	}

# Troubleshoot
## 502 Bad Gateway
Error log : `TIME [error] 22838#0: *7 connect() failed (111: Connection refused) while connecting to upstream, client: [my personal IP], server: [production server IP], request: "GET / HTTP/1.1", upstream: "fastcgi://127.0.0.1:9000", host: "[production server IP]"`

This error because php-fpm not allow clients from any IP accept localhost. So open file configuration of php-fpm, in Centos `/etc/php-fpm.d/www.conf`, find this line: `listen.allowed_clients 127.0.0.1` and comment it. It mean php-fpm will accept from any IP.