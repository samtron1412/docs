[TOC]

# Overview
A simple to use and highly versatile Open Source wiki software that doesn't require a database. Save article below text files. Clean and readable [syntax](https://www.dokuwiki.org/wiki:syntax).

# Configuration
By default DokuWiki loads its configuration files in the following order:

1. `conf/dokuwiki.php`
2. `conf/local.php`
3. `conf/local.protected.php`

Values previously will be overridden by values from after file. So values at `local.protected.php` will overridden values of `local.php` and values at `local.php` will overridden values of `dokuwiki.php`

![Configuration](dokuwiki/configuration.png)

# Plugins
Change behavior and add additional syntax in your installation.

A plugin is installed by putting it into its own folder under `lib/plugins/`.

By default DokuWiki loads its configuration files in the following order:

1. `conf/plugins.php` – default plugins
2. `conf/plugins.local.php` – changed by plugin manager
3. `conf/plugins.required.php` – these core plugins cannot be controlled by plugin manager
4. `conf/plugins.protected.php` – overrides setting in the other files

The loading order of configuration files is controlled by the global `$config_cascade` variable. By using a [preload.php](https://www.dokuwiki.org/devel:preload) file you can change this behavior.


# Templates
Change the look and feel of your site. The color scheme can also be easily adjusted by editing the template's [style.ini](https://www.dokuwiki.org/devel:css#styleini).



# Tips and Tricks
