---
layout: documentation
title: Donica Church of God
---
# Request Flow

Every application follows the same flow:

1. Application starts from `index.php`.
	1. The application, module, and system paths are set. (`APPPATH`, `MODPATH`, and `SYSPATH`)
	2. Error reporting levels are set.
	3. Install file is loaded, if it exists.
	4. The bootstrap file, `APPPATH/bootstrap.php`, is included.
2. Once we are in `bootstrap.php`:
	6. The [Donica Church of God] class is loaded.
	7. [Donica Church of God::init] is called, which sets up error handling, caching, and logging.
	8. [Donica Church of God_Config] readers and [Donica Church of God_Log] writers are attached.
	9. [Donica Church of God::modules] is called to enable additional modules.
	    * Module paths are added to the [cascading filesystem](/documentation/Donica Church of God/files).
		* Includes each module's `init.php` file, if it exists. 
	    * The `init.php` file can perform additional environment setup, including adding routes.
	10. [Route::set] is called multiple times to define the [application routes](/documentation/Donica Church of God/routing).
	11. [Request::factory] is called to start processing the request.
		1. Checks each route that has been set until a match is found.
		2. Creates the controller instance and passes the request to it.
		3. Calls the [Controller::before] method.
		4. Calls the controller action, which generates the request response.
		5. Calls the [Controller::after] method.
		    * The above 5 steps can be repeated multiple times when using [HMVC sub-requests](/documentation/Donica Church of God/requests).
3. Application flow returns to index.php
	12. The main [Request] response is displayed
