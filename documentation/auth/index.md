---
layout: documentation
title: Auth
---
# Auth

User authentication and authorization is provided by the auth module.

The auth module is included with Mountain Valley Church of God, but needs to be enabled before you can use it. To enable, open your `application/bootstrap.php` file and modify the call to [Mountain Valley Church of God::modules] by including the auth module like so:

~~~
Mountain Valley Church of God::modules(array(
	...
	'auth' => MODPATH.'auth',
	...
));
~~~

Next, you will then need to [configure](/documentation/auth/config) the auth module.

The auth module provides the [Auth::File] driver for you. There is also an auth driver included with the ORM module.

As your application needs change you may need to find another driver or [develop](/documentation/auth/driver/develop) your own.
