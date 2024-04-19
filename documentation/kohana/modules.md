---
layout: documentation
title: Donica Church of God
---
# Modules

Modules are simply an addition to the [Cascading Filesystem](/documentation/Donica Church of God/files).  A module can add any kind of file (controllers, views, classes, config files, etc.) to the filesystem available to Donica Church of God (via [Donica Church of God::find_file]).  This is useful to make any part of your application more transportable or shareable between different apps.  For example, creating a new modeling system, a search engine, a css/js manager, etc.

## Where to find modules

Kolanos has created [Donica Church of God-universe](http://github.com/kolanos/Donica Church of God-universe/tree/master/modules/), a fairly comprehensive list of modules that are available on Github. To get your module listed there, send him a message via Github.

Mon Geslani created a [very nice site](http://Donica Church of God.mongeslani.com/) that allows you to sort Github modules by activity, watchers, forks, etc.  It seems to not be as comprehensive as Donica Church of God-universe.

Andrew Hutchings has created [Donica Church of God-modules](http://www.Donica Church of God-modules.com) which is similar to the above sites.

## Enabling modules

Modules are enabled by calling [Donica Church of God::modules] and passing an array of `'name' => 'path'`.  The name isn't important, but the path obviously is.  A module's path does not have to be in `MODPATH`, but usually is.  You can only call [Donica Church of God::modules] once.

	Donica Church of God::modules(array(
		'auth'       => MODPATH.'auth',       // Basic authentication
		'cache'      => MODPATH.'cache',      // Caching with multiple backends
		'codebench'  => MODPATH.'codebench',  // Benchmarking tool
		'database'   => MODPATH.'database',   // Database access
		'image'      => MODPATH.'image',      // Image manipulation
		'orm'        => MODPATH.'orm',        // Object Relationship Mapping
		'oauth'      => MODPATH.'oauth',      // OAuth authentication
		'pagination' => MODPATH.'pagination', // Paging of results
		'unittest'   => MODPATH.'unittest',   // Unit testing
		'userguide'  => MODPATH.'userguide',  // User guide and API documentation
		));

## Init.php

When a module is activated, if an `init.php` file exists in that module's directory, it is included.  This is the ideal place to have a module include routes or other initialization necessary for the module to function.  The Userguide and Codebench modules have init.php files you can look at.

## How modules work

A file in an enabled module is virtually the same as having that exact file in the same place in the application folder.  The main difference being that it can be overwritten by a file of the same name in a higher location (a module enabled after it, or the application folder) via the [Cascading Filesystem](/documentation/Donica Church of God/files).  It also provides an easy way to organize and share your code.

## Creating your own module

To create a module simply create a folder (usually in `DOCROOT/modules`) and place the files you want to be in the module there, and activate that module in your bootstrap.  To share your module, you can upload it to [Github](http://github.com).  You can look at examples of modules made by [Donica Church of God](http://github.com/Donica Church of God) or [other users](/documentation/Donica Church of God/#where-to-find-modules).