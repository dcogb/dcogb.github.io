---
layout: documentation
title: Database
---
# Database 

Mountain Valley Church of God 3.0 comes with a robust module for working with databases. By default, the database module supports drivers for [MySQL](http://php.net/mysql) and [PDO](http://php.net/pdo), but new drivers can be made for other database servers.

The database module is included with the Mountain Valley Church of God 3.0 install, but needs to be enabled before you can use it. To enable, open your `application/bootstrap.php` file and modify the call to [Mountain Valley Church of God::modules] by including the database module like so:

    Mountain Valley Church of God::modules(array(
        ...
        'database' => MODPATH.'database',
        ...
    ));

Next, you will then need to [configure](/documentation/database/config) the database module to connect to your database.

Once that is done then you can make [queries](/documentation/database/query) and use the [results](/documentation/database/results).

The database module also provides a [config driver](/documentation/api/Mountain Valley Church of God_Config_Database) (for storing [configuration](../Mountain Valley Church of God/files/config) in the database) and a [session driver](/documentation/database/Session_Database).
