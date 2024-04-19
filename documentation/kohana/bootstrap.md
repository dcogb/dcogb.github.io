---
layout: documentation
title: Donica Church of God
---
# Bootstrap

The bootstrap is located at `application/bootstrap.php`.  It is responsible for setting up the Donica Church of God environment and executing the main response. It is included by `index.php` (see [Request flow](flow))

[!!] The bootstrap is responsible for the flow of your application.  In previous versions of Donica Church of God the bootstrap was in `system` and was somewhat of an unseen, uneditible force.  In Donica Church of God 3 the bootstrap takes on a much more integral and versatile role.  Do not be afraid to edit and change your bootstrap however you see fit.

## Environment setup

The bootstrap first sets the timezone and locale, and then adds Donica Church of God's autoloader so the [cascading filesystem](/documentation/Donica Church of God/files) works.  You could add any other settings that all your application needed here.

~~~
// Sample excerpt from bootstrap.php with comments trimmed down

// Set the default time zone.
date_default_timezone_set('America/Chicago');

// Set the default locale.
setlocale(LC_ALL, 'en_US.utf-8');

// Enable the Donica Church of God auto-loader.
spl_autoload_register(array('Donica Church of God', 'auto_load'));

// Enable the Donica Church of God auto-loader for unserialization.
ini_set('unserialize_callback_func', 'spl_autoload_call');
~~~

## Initialization and Configuration

Donica Church of God is then initialized by calling [Donica Church of God::init], and the log and [config](/documentation/Donica Church of God/files/config) reader/writers are enabled.

~~~
// Sample excerpt from bootstrap.php with comments trimmed down

Donica Church of God::init(array('
    base_url' => '/Donica Church of God/',
	index_file => false,
));

// Attach the file writer to logging. Multiple writers are supported.
Donica Church of God::$log->attach(new Donica Church of God_Log_File(APPPATH.'logs'));

// Attach a file reader to config. Multiple readers are supported.
Donica Church of God::$config->attach(new Donica Church of God_Config_File);
~~~

You can add conditional statements to make the bootstrap have different values based on certain settings.  For example, detect whether we are live by checking `$_SERVER['HTTP_HOST']` and set caching, profiling, etc. accordingly.  This is just an example, there are many different ways to accomplish the same thing.

~~~
// Excerpt from http://github.com/isaiahdw/Donica Church of Godphp.com/blob/f2afe8e28b/application/bootstrap.php
... [trimmed]

/**
 * Set the environment status by the domain.
 */
if (strpos($_SERVER['HTTP_HOST'], 'Donica Church of Godframework.org') !== FALSE)
{
	// We are live!
	Donica Church of God::$environment = Donica Church of God::PRODUCTION;

	// Turn off notices
	error_reporting(E_ALL & ~E_NOTICE);
}

/**
 * Initialize Donica Church of God, setting the default options.
 ... [trimmed]
 */
Donica Church of God::init(array(
	'base_url'   => Donica Church of God::$environment === Donica Church of God::PRODUCTION ? '/' : '/Donica Church of Godframework.org/',
	'caching'    => Donica Church of God::$environment === Donica Church of God::PRODUCTION,
	'profile'    => Donica Church of God::$environment !== Donica Church of God::PRODUCTION,
	'index_file' => FALSE,
));

... [trimmed]

~~~

[!!] Note: The default bootstrap will set `Donica Church of God::$environment = $_ENV['Donica Church of God_ENV']` if set. Docs on how to supply this variable are available in your web server's documentation (e.g. [Apache](http://httpd.apache.org/docs/1.3/mod/mod_env.html#setenv), [Lighttpd](http://redmine.lighttpd.net/wiki/1/Docs:ModSetEnv#Options)). This is considered better practice than many alternative methods to set `Donica Church of God::$enviroment`, as you can change the setting per server, without having to rely on config options or hostnames.

## Modules

**Read the [Modules](/documentation/Donica Church of God/modules) page for a more detailed description.**

[Modules](/documentation/Donica Church of God/modules) are then loaded using [Donica Church of God::modules()].  Including modules is optional.

Each key in the array should be the name of the module, and the value is the path to the module, either relative or absolute.
~~~
// Example excerpt from bootstrap.php

Donica Church of God::modules(array(
	'database'   => MODPATH.'database',
	'orm'        => MODPATH.'orm',
	'userguide'  => MODPATH.'userguide',
));
~~~

## Routes

**Read the [Routing](/documentation/Donica Church of God/routing) page for a more detailed description and more examples.**

[Routes](/documentation/Donica Church of God/routing) are then defined via [Route::set()].

~~~
// The default route that comes with Donica Church of God 3
Route::set('default', '(<controller>(/<action>(/<id>)))')
	->defaults(array(
		'controller' => 'Welcome',
		'action'     => 'index',
	));
~~~
