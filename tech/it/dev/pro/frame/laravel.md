[TOC]

# Overview
MIT license, source code hosted on GitHub. Developer is Taylor Otwell. Initial release: June 2011.

## Features
- **Bunldes** provide a modular packaging system Laravel 3.x, Laravel 4.x uses [Composer](http://getcomposer.org/) as a dependency manager to add framework-agnostic and Laravel-specific PHP packages available from the [Packagist](https://packagist.org/) repository.
- **Eloquent ORM (object-relational mapping)** is an advanced PHP implementation of the *active record pattern*, providing at the same time internal methods for enforcing constraints to the relationships between database objects. Following the active record pattern, Eloquent ORM presents database *tables as classes*, with their object instances tied to single table rows. Laravel's *query builder* provides a more direct database access alternative to the Eloquent ORM.
- **Reverse routing**
- **Restful controllers**
- **Class auto loading** PHP classes; only the components which are actually used are loaded.
- **View composers** logical code units that can be executed when a view is loaded
- **IoC container**
- **Migrations** provide a version control system for database schema
- **Unit testing**
- **Automatic pagination**

## Technical
### Request life cycle



CLIENT -> `/public/index.php` -> `/bootstrap/autoload.php` -> `/vendor/autoload.php` -> `/vendor/composer/autoload_real.php` -> `/vendor/composer/ClassLoader.php` -> `/vendor/composer/include_paths.php` -> `/vendor/composer/autoload_namespaces.php` -> `/vendor/composer/autoload_psr4.php` -> `/vendor/composer/autoload_classmap.php` -> `/vendor/composer/autoload_files.php` -> `/bootstrap/start.php` -> `/bootstrap/paths.php` -> `/Illuminate/Foundation/start.php` -> `/app/start/global.php` -> `/app/filters.php` -> `/app/start/{$environment (local/production/test)}.php` -> `/app/routes.php` -> `/app/controllers` -> `/app/models` -> `/app/views` -> CLIENT

- CLIENT requests
- **BEGIN LOADING STEP** Starting point of web requests : `/public/index.php`
	+ Loads autoloader : `/bootstrap/autoload.php`
		* Loads vendor autoloaders : `/vendor/autoload.php`
			- /vendor/autoload_real.php
				+ /vendor/composer/ClassLoader.php
				+ /vendor/composer/include_paths.php
				+ /vendor/composer/autoload_namespaces.php
				+ /vendor/composer/autoload_psr4.php
				+ /vendor/composer/autoload_classmap.php
					* You can specify in `composer.json`
				+ /vendor/composer/autoload_files.php
					* You can specify in `composer.json`
		* Loads any optimized classes, compiled classes `/bootstrap/compiled.php`: inscrease performance
		* Initialize multibyte strings, handling of UTF-8 strings.
		* Register Laravel autoloader.
		* Load workbench stuff, if present
	+ Loads application bootstrap : `/bootstrap/start.php`
		* Creates the Laravel application : `Illuminate\Foundation\Application`
			- Binds request
			- Register base service providers: Exception, Routing, Event
			- Register base middlewares
		* Detect environment
		* Loads path settings : `/bootstrap/paths.php` **END LOADING STEP**
		* **BEGIN BOOTING STEP** Start Application : `/Illuminate/Foundation/start.php`
			- Check mcrypt extension
			- Bind the application in the container and configure: Facade, Environment Variables
			- Starts Exception handling
			- Sets timezone
			- Register Alias Loader
			- Enable HTTP method override
			- Load service providers
			- Register Booted start files : `/app/start/global.php`, `/app/start/{$env}.php`, `/app/routes.php`
			- Runs Application: `Illuminate\Foundation\Application->run`
				+ Build stacked HTTP kernel
				+ Handle middleware going down
				+ Boot service providers
				+ Calls booting callbacks
				+ Calls booted callbacks
			- Load application start script : `/app/start/global.php`
				+ ClassLoader
				+ Log file
				+ Errors handling
				+ Maintenance mode handler
				+ Loads filters : `/app/filters.php`
					* Authentication filters
					* Guest filters
					* CSRF filters
			- Loads environment start script : `/app/start/{environment}.php`
			- Loads routes : `/app/routes.php` **END BOOTING STEP**
- /app/controllers
- /app/models
- /app/views
- CLIENT view result


## Phylosophy and design

## Install
### [Composer](https://getcomposer.org/)
`composer global require "laravel/installer=~1.1"`

or `composer create-project laravel/laravel myapp`

Create previous version of Laravel: `composer create-project laravel/laravel=4.1.* myapp` or `composer create-project laravel/laravel myapp 4.1.*`

### [Homestead](http://laravel.com/docs/4.2/homestead)
**Laravel Homestead** is an official, pre-packaged Vargrant "box" that provides you a wonderful development environment without requiring you to install PHP, HHVM, a web server, and any other software on your local machine.

**Vargrant** provides a simple, elegant way to manage and provision Virtual Machines.

**Installation**
- Installing [VirtualBox](https://www.virtualbox.org/wiki/Downloads) & [Vargrant](http://www.vagrantup.com/downloads.html)
- Adding the Vargrant box: `vagrant box add laravel/homestead`
- Installing Homestead
	+ Via composer + PHP tool
		* `composer global require "laravel/homestead=~2.0"`
		* Make sure to place the `~/.composer/vendor/bin` directory in your PATH so the `homestead` executable is found when you run the `homestead` command in your terminal.
		* `homestead init`
		* `homestead edit`
	+ Via Git (No need install PHP at local)
		* `git clone https://github.com/laravel/homestead.git Homestead`
		* `bash init.sh`
		* The `Homestead.yaml` file will be placed in your `~/.homestead` directory.
- Set your SSH key
- Configure your shared folders
- Configure your nginx sites

**Daily Usage**
- Connecting via SSH
	+ Use password: vagrant - vagrant -> use sudo to change root password if need
	+ Use SSH private key spawn by vagrant
- Connecting to your database
	+ Use user: homestead - secret
	+ Use command to change root password: `UPDATE mysql.user SET Password='' WHERE User='root';FLUSH PRIVILEGES;`

Configure your homestead by edit file `Homestead.yaml`
- `sites`
- Adding `ports`:

```
ports:
	- send: 93000
		to: 9300
	- send: 7777
		to: 777
		protocol: udp
```

# User guide
## Version control
### Ignore

	/bootstrap/compiled.php
	/vendor
	composer.phar
	composer.lock  # Remove this one after you create a project
	.env.*.php
	.env.php
	.DS_Store
	Thumbs.db


	laravel:~/myapp$ svn propset svn:ignore vendor .
	laravel:~/myapp$ svn update
	laravel:~/myapp$ svn add a* b* c* C* p* r* s*
	laravel:~/myapp$ svn propset svn:ignore compiled.php bootstrap/
	laravel:~/myapp$ svn propset svn:ignore \* app/storage/cache/
	laravel:~/myapp$ svn propset svn:ignore \* app/storage/logs/
	laravel:~/myapp$ svn propset svn:ignore \* app/storage/meta/
	laravel:~/myapp$ svn propset svn:ignore \* app/storage/sessions/
	laravel:~/myapp$ svn propset svn:ignore \* app/storage/views/



## IoC container


## Facade


## Migration
**Migration**: a version control for database.

### Work flow
1. Configure Laravel to use migration
	- `app/config/database.php` change name of table will use to track migration status.
	- Install migration `php artisan migrate:install` it will create a table with name in the configuration and use it to track migration status.
2. Create a new migration (a version of table)
	- `php artisan migrate:make create_users` and then edit content of migration, up() and down() functions.
	- `php artisan migrate:make create_users --create --table=users` it will generate a basic structure for you.
3. Run migration `php artisan migrate`
4. Create new migration to modify this table, such as to add new columns
	- `php artisan migrate:make add_title_to_users`
	- Run migrate `php artisan migrate`

- Refresh : roll back all migrations and do it again
	+ `php artisan migrate:refresh`
- Rollback : roll back last migrate
	+ `php artisan migrate:rollback`
- Reset : roll back all migrate
	+ `php artisan migrate:reset`
- Run with different database: `php artisan migrate --database=mysql`
- View the real SQL will run when migrate, use to debug : `php artisan migrate --pretend`


### [Database seeding](https://web.archive.org/web/20141023114601/http://culttt.com/2013/12/16/seeding-laravel-4-database/)
Seed data is anything that must be loaded for an application to work properly.

Seed your database with test data using seed classes. All seed classes are stored in `app/database/seeds`. By default, a `DatabaseSeeder` class is defined for you. From this class, you call method to run other seed classes, allowing you to control the seeding order.

Example

```ruby
class DatabaseSeeder extends Seeder {

    public function run()
    {
        $this->call('UserTableSeeder');

        $this->command->info('User table seeded!');
    }

}

class UserTableSeeder extends Seeder {

    public function run()
    {
        DB::table('users')->delete();

        User::create(array('email' => 'foo@bar.com'));
    }

}
```

Run DatabaseSeeder class: `php artisan db:seed`

Run specific class: `php artisan db:seed --class=UserTableSeeder`

Seed after refesh migrations: `php artisan migrate:refesh --seed`

## Artisan CLI
Artisan is the name of the command-line interface included with Laravel. It provides a number of helpful commands for your use while developing your application. It is driven by the powerful Symfony Console component.

List all available commands: `php artisan list`

View the help screen for a command: `php artisan help <command>`

### Calling commands outside of CLI


### Scheduling artisan commands
`app/Console/Kernel.php`


## Unit test
Run test: `php vendor\phpunit\phpunit\phpunit` : run file phpunit.php at vendor

Configuration file: `phpunit.xml` at project folder.

### Mockery
Mocking object to test.

	$mockedObj = Mockery::mock('SomeClass')
	$mockedObj->shouldReceive('method name')
						->with('param1', 'param2', ...)
						->once();

Simple mock object

	public function testSimpleMocks()
	{
		$user = Mockery::mock(['getFullName' => 'Jeffrey Way']);
		$user->getFullName(); // Jeffrey Way
	}

Return values

	$mockedFile->shouldReceive('exists')
							->once()
							->andReturn(true);

	$mockedFile->shouldReceive('put')
							->never()

Expectations

	1 $mock->shouldReceive('method')->once();
	2 $mock->shouldReceive('method')->times(1);
	3 $mock->shouldReceive('method')->atLeast()->times(1);

	1 $mock->shouldReceive('get')->withAnyArgs()->once(); // the default
	2 $mock->shouldReceive('get')->with('foo.txt')->once();
	3 $mock->shouldReceive('put')->with('foo.txt', 'foo bar')->once();

	1 $mock->shouldReceive('get')->with(Mockery::type('string'))->once();

	1 $mockedFile->shouldReceive('put')
	2 ->with('/\.txt$/', Mockery::any())
	3 ->once();

	1 $mockedFile->shouldReceive('get')
	2 ->with(Mockery::anyOf('log.txt', 'cache.txt'))
	3 ->once();

Partial Mocks: only mock a method of class

	3 $mock = Mockery::mock('MyClass[getOption]');
	4 $mock->shouldReceive('getOption')
	5 ->once()
	6 ->andReturn(10000);

	1 $mock = Mockery::mock('MyClass[method1, method2]');

	3 $mock = Mockery::mock('MyClass')->makePartial();
	4 $mock->shouldReceive('getOption')
	5 ->once()
	6 ->andReturn(10000);

Hamcrest: a library use to write mockery and phpunit code easy




# Tips and Tricks
## Safely remove migration in Laravel 4
I accidentally created a migration with a **bad name** (command: `php artisan migrate:make`). I did not run (`php artisan migrate`) the migration, so I decided to remove it. My steps:

1. Manually delete the migration file under app/database/migrations/my_migration_file_name.php
2. Reset the composer autoload files: composer dump-autoload
3. Relax

If you did run the migration (`php artisan migrate`), you may do this:

a) Run `migrate:rollback` - it is the right way to undo the last migration (Thnx @Jakobud)

b) If `migrate:rollback` does not work, do it manually (I remember bugs with migrate:rollback in previous versions):

1. Manually delete the migration file under `app/database/migrations/my_migration_file_name.php`
2. Reset the composer autoload files: `composer dump-autoload`
3. Modify your database: Remove the last entry from the migrations table

## Logging SQL queries
- Should use [barryvdh/laravel-debugbar]( barryvdh/laravel-debugbar): [github repo](https://github.com/barryvdh/laravel-debugbar), [docs](http://phpdebugbar.com/docs/)
- Use script below, add to `/app/start/local.php`: read comment section to know how it work.

```php
/*
 | 1. Before you start with this create a file in your logs folder (eg : 'query.log') and grant laravel write access to it.
 | 2. Place the snippet in your '/app/start/local.php' file. (or routes.php or anywhere...)
 | 3. Access artisan from your console and type this -
 |    $ php artisan tail --path="app/storage/logs/query.log" (better use full path)
*/

$path = storage_path().'/logs/query.log';

if (!File::exists($path)) {
    File::put($path, "Query Log".PHP_EOL);
}

App::before(function($request) use($path) {
    $start = PHP_EOL.'=| '.$request->method().' '.$request->path().' |='.PHP_EOL;
    File::append($path, $start);
});

Event::listen('illuminate.query', function($sql, $bindings, $time) use($path) {
    // Uncomment this if you want to include bindings to queries
    $sql = str_replace(array('%', '?'), array('%%', '%s'), $sql);
    $sql = vsprintf($sql, $bindings);
    $time_now = (new DateTime)->format('Y-m-d H:i:s');;
    $log = $time_now.' | '.$sql.' | '.$time.'ms'.PHP_EOL;
    File::append($path, $log);
});
```


## Optimize application
`php artisan optimize --force`

Clear compiled classes: `php artisan clear-compiled`

# Troubleshoot
## Eloquent __construct() injection
When you write a function __construct() in an Eloquent class and you use Eloquent function like *<class>::find()* it will cause an error when new an instance for function *finc*.

`$instance = new static;`

It loss arguments you inject to class so it will cause an error. [link](http://forumsarchive.laravel.io/viewtopic.php?pid=47124#p47124)

## Table use to authentication must have collumn created_at, updated_at
When use convention to authentication in Laravel, table must have two column with named: **created_at, updated_at**

**Note**: convention of Laravel.
