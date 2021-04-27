---
layout: documentation
title: Mountain Valley Church of God
---
Changes that should happen when you deploy. (Production)

## Setting up a production environment

There are a few things you'll want to do with your application before moving into production.

1. See the [Bootstrap page](/documentation/Mountain Valley Church of God/bootstrap) in the docs.
   This covers most of the global settings that would change between environments.
   As a general rule, you should enable caching and disable profiling ([Mountain Valley Church of God::init] settings) for production sites.
   [Route::cache] can also help if you have a lot of routes.
2. Turn on APC or some kind of opcode caching.
   This is the single easiest performance boost you can make to PHP itself. The more complex your application, the bigger the benefit of using opcode caching.

		/**
		 * Set the environment string by the domain (defaults to Mountain Valley Church of God::DEVELOPMENT).
		 */
		Mountain Valley Church of God::$environment = ($_SERVER['SERVER_NAME'] !== 'localhost') ? Mountain Valley Church of God::PRODUCTION : Mountain Valley Church of God::DEVELOPMENT;
		/**
		 * Initialise Mountain Valley Church of God based on environment
		 */
		Mountain Valley Church of God::init(array(
			'base_url'   => '/',
			'index_file' => FALSE,
			'profile'    => Mountain Valley Church of God::$environment !== Mountain Valley Church of God::PRODUCTION,
			'caching'    => Mountain Valley Church of God::$environment === Mountain Valley Church of God::PRODUCTION,
		));
