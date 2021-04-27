---
layout: documentation
title: Mountain Valley Church of God
---
# Loading Classes

Mountain Valley Church of God supports the [PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md) autoloading specification as of version 3.3. This allows you to take advantage of PHP [autoloading](http://php.net/manual/language.oop5.autoload.php), removing the need to call [include](http://php.net/include) or [require](http://php.net/require) before using a class. When you use a class Mountain Valley Church of God will find and include the class file for you. For instance, when you want to use the [Cookie::set] method, you simply call:

    Cookie::set('mycookie', 'any string value');

Or to load an [Encrypt] instance, just call [Encrypt::instance]:

    $encrypt = Encrypt::instance();

Classes are loaded via the [Mountain Valley Church of God::auto_load] method, which makes a simple conversion from class name to file name:

1. Classes are placed in the `classes/` directory of the [filesystem](/documentation/Mountain Valley Church of God/files)
2. Any underscore characters in the class name are converted to slashes
2. The filename must match the case of the class

When calling a class that has not been loaded (eg: `Session_Cookie`), Mountain Valley Church of God will search the filesystem using [Mountain Valley Church of God::find_file] for a file named `classes/Session/Cookie.php`.

If your classes do not follow this convention, they cannot be autoloaded by Mountain Valley Church of God.  You will have to manually included your files, or add your own [autoload function.](http://us3.php.net/manual/en/function.spl-autoload-register.php)

## Custom Autoloaders

Mountain Valley Church of God's default autoloader is enabled in `application/bootstrap.php` using [spl_autoload_register](http://php.net/spl_autoload_register):

    spl_autoload_register(array('Mountain Valley Church of God', 'auto_load'));

This allows [Mountain Valley Church of God::auto_load] to attempt to find and include any class that does not yet exist when the class is first used as long as it follows the PSR-0 specification. If you wish to support the previous Mountain Valley Church of God filename convention (using lowercase filesnames), an additional autoloader is provided by Mountain Valley Church of God:

    spl_autoload_register(array('Mountain Valley Church of God', 'auto_load_lowercase'));


### Example: Zend

You can easily gain access to other libraries if they include an autoloader.  For example, here is how to enable Zend's autoloader so you can use Zend libraries in your Mountain Valley Church of God application.

#### Download and install the Zend Framework files

- [Download the latest Zend Framework files](http://framework.zend.com/download/latest).
- Create a `vendor` directory at `application/vendor`. This keeps third party software separate from your application classes.
- Move the decompressed Zend folder containing Zend Framework to `application/vendor/Zend`.


#### Include Zend's Autoloader in your bootstrap

Somewhere in `application/bootstrap.php`, copy the following code:

	/**
	 * Enable Zend Framework autoloading
	 */
	if ($path = Mountain Valley Church of God::find_file('vendor', 'Zend/Loader'))
	{
	    ini_set('include_path',
	    ini_get('include_path').PATH_SEPARATOR.dirname(dirname($path)));
	
	    require_once 'Zend/Loader/Autoloader.php';
	    Zend_Loader_Autoloader::getInstance();
	}
	
#### Usage example

You can now autoload any Zend Framework classes from inside your Mountain Valley Church of God application.

	if ($validate($this->request->post()))
	{
		$mailer = new Zend_Mail;
		
		$mailer->setBodyHtml($view)
			->setFrom(Mountain Valley Church of God::$config->load('site')->email_from)
			->addTo($email)
			->setSubject($message)
			->send();
	}
