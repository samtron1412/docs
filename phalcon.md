[TOC]

# Overview
Open source, full stack framework for PHP 5 written as a C-extension, optimized for high performance. A robust framework with all of its advantages. Fastest PHP framework.

[Documentation](http://docs.phalconphp.com/en/latest/index.html)

## How do traditional PHP framework work?
- Many files with classes and functions are read on every request made. Disk reading is expensive in terms of performance, especially when the file structure includes deep folders.
- Modern frameworks use lazyload (autoload) to increase performance (for load and execute only the code needed).
- Some of these classes contain methods that aren't used in every request but they're loaded always consuming memory.
- Continuous loading or interpreting is expensive and impacts performance.
- The framework code does not change very often, and yet an application needs to load and interpret it every time a request is made.

## How does a PHP C-extension work?
- C extension are loaded together with PHP one time on the web server's daemon start process.
- Classes and functions provided by the extension are ready to use for any application.
- The code isn't interpreted because is already compiled to a specific platform and processor.



# API
## Dispatcher
Dispatching is the process of taking **the request object, extracting the module name, controller name, action name, and optional parameters contained in it**, and then instantiating a controller and calling an action of that controller.

Phalcon\Mvc\Dispatcher is the component responsible for instantiating controllers and executing the required actions on them in an MVC application.

## Request
A wrapper for `$_GET, $_POST, ... of PHP`. Filter value for security._

## Cookie


## Query database
- Model wrapper, return object data: find()
- Create builder (PHQL), return object data: getQuery()->execute()
- Raw SQL, ResultSet()


# Tutorial
- [Phalcon Tutorials](https://github.com/phalcon/tutorial)

## Configure httpd.conf and .htaccess
**httpd.conf**

```
Alias /<alias>/ "/vagrant/projects/<alias>/public/"
<Directory "/vagrant/projects/<alias>/public">
    Options FollowSymLinks
    AllowOverride ALL
    Order allow,deny
    Allow from all
</Directory>
```

**.htaccess**

```
AddDefaultCharset UTF-8

<IfModule mod_rewrite.c>
    RewriteEngine On

    # If the directory with the specified name doesn't exist and
    RewriteCond %{REQUEST_FILENAME} !-d
    # the file with the specified name doesn't exist then
    RewriteCond %{REQUEST_FILENAME} !-f
    # apply this rewrite rule.
    RewriteRule ^(.*)$ /<alias>/index.php?_url=/$1 [QSA,L]
</IfModule>
```
**Note**: Remember add alias to `RewriteRule` to *index.php* at `.htaccess` file.

## Structure of /public/index.php
This file is main file of Phalcon, it will load all config and initialize environment. All request to application always receive by this file.

- Error reporting
	+ `error_reporting(E_ALL & ~E_NOTICE & ~E_DEPRECATED)`
- Composer autoload
	+ `require __DIR__.'/../vendor/autoload.php';`
- Read configuration file
	+ `$config = new Phalcon\Config\Adapter\Ini(__DIR__ . '/../app/config/config.ini');`
- Load constants is defined
	+ `include __DIR__ . '/../app/config/define.php';`
- Load database config:
	+ `include __DIR__ . '/../app/config/server.php';`
- Load logger config: use log4php
	+ `Logger::configure(__DIR__ . '/../app/config/log4.xml');`
- Autoloader, autoload classes:
	+ `include __DIR__ . "/../app/conf/loader.php";`
- Mobile check:
	+ `include __DIR__ . "/../app/conf/mobile.php";`
- Read services: important, dependencies injection
	+`include __DIR__ . "/../app/conf/services.php";`

### config.ini
```ini
debug = 1

[application]
controllersDir = /../controllers/
modelsDir      = /../models/
viewsDir       = /../app/views/
viewsSpDir     = /../app/viewssp/
pluginsDir     = /../plugins/
libsDir        = /../libs/
servicesDir    = /../services/
objectsDir     = /../objects/
baseUri        = /map_tool/

[metadata]
adapter = "Apc"
suffix = my-suffix
lifetime = 86400
```

### define.php
Define constants use in application functions.

	<?php
	define('CACHE_KEY_TOTAL_COUNT', 'net.webike.moto.motosearch_total_count');
	define('CACHE_KEY_MAKER_LIST', 'net.webike.moto.motosearch_maker_list');

	define('CACHE_KEY_MODEL', 'net.webike.moto.motosearch_model_%s');

### server.php
Create array store all database configurations. And define all constants use for configure server.

	<?php

	$databases = array();

	$databases['webikept_read']['host']     = '54.248.223.71';
	$databases['webikept_read']['username'] = 'webikept';
	$databases['webikept_read']['password'] = 'cbr900rr';
	$databases['webikept_read']['dbname']   = 'webikept';

	$databases['webikept_write']['host']     = '54.248.223.71:13306';
	$databases['webikept_write']['username'] = 'webikept';
	$databases['webikept_write']['password'] = 'cbr900rr';
	$databases['webikept_write']['dbname']   = 'webikept';

	$databases['dobar_read']['host']     = '54.248.223.71';
	$databases['dobar_read']['username'] = 'webike';
	$databases['dobar_read']['password'] = 'cbr900rr';
	$databases['dobar_read']['dbname']   = 'dobar';

	$databases['dobar_write']['host']     = '54.248.223.71';
	$databases['dobar_write']['username'] = 'webike';
	$databases['dobar_write']['password'] = 'cbr900rr';
	$databases['dobar_write']['dbname']   = 'dobar';

	$databases['wsd_read']['host']     = '54.248.223.71';
	$databases['wsd_read']['username'] = 'webike';
	$databases['wsd_read']['password'] = 'cbr900rr';
	$databases['wsd_read']['dbname']   = 'wsd_webikesh';

	$databases['wsd_write']['host']     = '54.248.223.71';
	$databases['wsd_write']['username'] = 'webike';
	$databases['wsd_write']['password'] = 'cbr900rr';
	$databases['wsd_write']['dbname']   = 'wsd_webikesh';

	define('SERVER_MEMCACHE', '192.168.33.15');
	define('SERVER_IMG', 'img.webike.net');

	define('SOLR_IP', '54.248.223.100');
	define('SOLR_PORT', '80');
	define('SOLR_PATH', '/solr/motobike/');

	define('SOLR_IP_MODEL', '54.248.223.100');
	define('SOLR_PORT_MODEL', '80');
	define('SOLR_PATH_MODEL', '/solr/motomodel/');

	define('COOKIE_DOMAIN', '192.168.33.15'); // local


	define('DOMAIN_IMAGE', '192.168.33.15');
	define('DOMAIN_PHOTO', 'img.webike.net');
	define('DOMAIN_MOTO', '192.168.33.15/moto');
	define('DOMAIN_MOBILE', 'm.webike.net');
	define('DOMAIN_BIZ', 'biz.webike.net');
	define('DOMAIN_WEBIKE', 'www.webike.net');
	define('DOMAIN_COMMUNITY', 'imp.webike.net');
	define('DOMAIN_SSL', '192.168.33.15');
	define('DOMAIN_LIFE', 'life.webike.net');
	define('DOMAIN_MENKYO', 'menkyo.webike.net');
	define('DOMAIN_DUCATI', 'ducati.webike.net');
	define('DOMAIN_EV', 'ev.webike.net');
	define('DOMAIN_COMPANY', 'www.rivercrane.com');
	define('DOMAIN_GLOBAL', 'japan.webike.net');
	define('DOMAIN_GLOBAL_ES', 'japan.webike.es');
	define('DOMAIN_GLOBAL_FR', 'japan.webike.fr');
	define('DOMAIN_GLOBAL_GE', 'japan.webike.ge');
	define('DOMAIN_GLOBAL_IT', 'www.japan-webike.it');
	define('DOMAIN_NEWS', 'news.webike.net');
	define('DOMAIN_NORICK', 'norick.webike.net');
	define('DOMAIN_CAMPAIGN', 'campaign.webike.net');
	define('DOMAIN_RANKING', 'ranking.webike.net');
	define('DOMAIN_DIR', 'dir.webike.net');
	define('DOMAIN_RENTAL', 'rental.webike.net');
	define('DOMAIN_HOKEN', 'hoken.webike.net');
	define('DOMAIN_SCHOOL', 'school.webike.net');
	define('DOMAIN_CAFE', 'cafe.webike.net');
	define('DOMAIN_KAITORI', 'kaitori.webike.net');
	define('DOMAIN_GALLERY',  'gallery.webike.net');

### Load log4php config from log4.xml
Use [log4php](https://logging.apache.org/log4php/)

### loader.php
	<?php

	$loader = new \Phalcon\Loader();

	/**
 	- We're a registering a set of directories taken from the configuration file
	 */
	$loader->registerDirs(
	  array(
	    __DIR__ . $config->application->controllersDir,
	    __DIR__ . $config->application->pluginsDir,
	    __DIR__ . $config->application->libsDir,
	    __DIR__ . $config->application->modelsDir,
	    __DIR__ . $config->application->servicesDir,
	    __DIR__ . $config->application->objectsDir,
	  )
	)->register();

### mobile.php
	<?php

	$spflag = false;
	if ($_GET[REQUEST_PARAM_SMART_PHONE]) {
	  if ($_GET[REQUEST_PARAM_SMART_PHONE] == 'pc') {
	    setcookie(COOKIE_NAME_SMART_PHONE, 'false', time() + (30 * (24*60*60)), '/',COOKIE_DOMAIN,false,false);
	  } else if ($_GET[REQUEST_PARAM_SMART_PHONE] == 'sp') {
	    setcookie(COOKIE_NAME_SMART_PHONE, 'true', time() + (30 * (24*60*60)), '/',COOKIE_DOMAIN,false,false);
	    $spflag = true;
	  }
	} else if ($_COOKIE[COOKIE_NAME_SMART_PHONE] == 'true') {
	  $spflag = true;
	} else {
	  // スマートフォン判定
	  $UA = $_SERVER['HTTP_USER_AGENT'];
	  if (ereg("iPhone|iPod|Android.*Mobile|Windows.*Phone", $UA)) {
	    $spflag = true;
	  }
	}

### services.php


## Troubleshooting
### Problems with IN(list) query syntax
- If you pass and String with bracket to `IN :param:` it will wrong syntax. In string of `param` will not contain bracket `()`
	+ e.g:
		// conditions of query
	  $conditions = "renkei_type = ?1 AND motorcycle_jyoukyo IN (?2)";

	  // parameters binding
	  $parameters = array(
	      1 => $renkeiType,
	      2 => '1,2,3,4,5,6'	//not use (1,2,3,4,5,6)
	  );

### ../public/index.php not found
May be your `.htaccess` or `httpd.conf` is wrong. Popular is you use `Alias` to redirect project but you forget add alias to `RewriteRule ^(.*)$ /<alias>/index.php?_url=/$1 [QSA,L]` at `.htaccess` file.

# Tools
## [Phalcon Developer Tool](https://github.com/phalcon/phalcon-devtools)
