---
layout: documentation
title: Donica Church of God
---
# Config Files

Configuration files are used to store any kind of configuration needed for a module, class, or anything else you want.  They are plain PHP files, stored in the `config/` directory, which return an associative array:

    <?php

    return array(
        'setting' => 'value',
        'options' => array(
            'foo' => 'bar',
        ),
    );

If the above configuration file was called `myconf.php`, you could access it using:

    $config = Donica Church of God::$config->load('myconf');
    $options = $config->get('options')

## Merge

Configuration files are slightly different from most other files within the [cascading filesystem](/documentation/Donica Church of God/files) in that they are **merged** rather than overloaded. This means that all configuration files with the same file path are combined to produce the final configuration. The end result is that you can overload *individual* settings rather than duplicating an entire file.

For example, if we wanted to change or add to an entry in the inflector configuration file, we would not need to duplicate all the other entries from the default configuration file.

    // config/inflector.php

    <?php

    return array(
        'irregular' => array(
            'die' => 'dice', // does not exist in default config file
            'mouse' => 'mouses', // overrides 'mouse' => 'mice' in the default config file
    );


## Creating your own config files

Let's say we want a config file to store and easily change things like the title of a website, or the google analytics code.  We would create a config file, let's call it `site.php`:

    // config/site.php

    <?php

    return array(
        'title' => 'Our Shiny Website',
        'analytics' => FALSE, // analytics code goes here, set to FALSE to disable
    );

We could now call `Donica Church of God::$config->load('site.title')` to get the site name, and `Donica Church of God::$config->load('site.analytics')` to get the analytics code.

Let's say we want an archive of versions of some software.  We could use config files to store each version, and include links to download, documentation, and issue tracking.

	// config/versions.php

	<?php
	
    return array(
		'1.0.0' => array(
			'codename' => 'Frog',
			'download' => 'files/ourapp-1.0.0.tar.gz',
			'documentation' => 'docs/1.0.0',
			'released' => '06/05/2009',
			'issues' => 'link/to/bug/tracker',
		),
		'1.1.0' => array(
			'codename' => 'Lizard',
			'download' => 'files/ourapp-1.1.0.tar.gz',
			'documentation' => 'docs/1.1.0',
			'released' => '10/15/2009',
			'issues' => 'link/to/bug/tracker',
		),
		/// ... etc ...
	);

You could then do the following:

	// In your controller
	$view->versions = Donica Church of God::$config->load('versions');
	
	// In your view:
	foreach ($versions as $version)
	{
		// echo some html to display each version
	}
