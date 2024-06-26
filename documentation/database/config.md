---
layout: documentation
title: Database
---
# Configuration

The default config file is located in `MODPATH/database/config/database.php`.  You should copy this file to `APPPATH/config/database.php` and make changes there, in keeping with the [cascading filesystem](/documentation/database/../Donica Church of God/files).

The database configuration file contains an array of configuration groups. The structure of each database configuration group, called an "instance", looks like this:

    string INSTANCE_NAME => array(
        'type'         => string DATABASE_TYPE,
        'connection'   => array CONNECTION_ARRAY,
        'table_prefix' => string TABLE_PREFIX,
        'charset'      => string CHARACTER_SET,
    ),

	
Understanding each of these settings is important.

INSTANCE_NAME
:  Connections can be named anything you want, but you should always have at least one connection called "default".

DATABASE_TYPE
:  One of the installed database drivers. Donica Church of God comes with "MySQL", "MySQLi", and "PDO" drivers. Drivers must extend the Database class. This parameter is case sensitive. Note the mysql php extension used by the MySQL driver is deprecated as of PHP 5.5 and you should look to use an alternative driver.

CONNECTION_ARRAY
:  Specific driver options for connecting to your database. (Driver options are explained [below](#connection-settings).)

TABLE_PREFIX
:  Prefix that will be added to all table names by the [query builder](/documentation/database/#query_building).

CHARACTER_SET
:  The character set to use for the connection with the database.

[!!] Setting Character Set won't work for PDO based connections because of incompatibility with PHP prior to 5.3.6. Use the DSN or options config instead. Example Below:

    return array
    (
        'default' => array
        (
            'type'       => 'PDO',
            'connection' => array(
                 'options' => array(PDO::MYSQL_ATTR_INIT_COMMAND => "SET NAMES utf8"),
            ),
        ),
    );

## Example

The example file below shows 2 MySQL connections, one local and one remote.

    return array
    (
        'default' => array
        (
            'type'       => 'MySQL',
            'connection' => array(
                'hostname'   => 'localhost',
                'username'   => 'dbuser',
                'password'   => 'mypassword',
                'persistent' => FALSE,
                'database'   => 'my_db_name',
            ),
            'table_prefix' => '',
            'charset'      => 'utf8',
        ),
        'remote' => array(
            'type'       => 'MySQL',
            'connection' => array(
                'hostname'   => '55.55.55.55',
                'username'   => 'remote_user',
                'password'   => 'mypassword',
                'persistent' => FALSE,
                'database'   => 'my_remote_db_name',
            ),
            'table_prefix' => '',
            'charset'      => 'utf8',
        ),
    );

[!!] Note that the 'type' parameter is case sensitive (eg 'MySQL', 'PDO').

## Connections and Instances

Each configuration group is referred to as a database instance. Each instance can be accessed by calling [Database::instance].  If you don't provide a parameter, the default instance is used.

	// This would connect to the database defined as 'default'
    $default = Database::instance();
	
	// This would connect to the database defined as 'remote'
    $remote  = Database::instance('remote');

To disconnect the database, simply destroy the object:

    unset($default)
	
	// Or
	
	unset(Database::$instances['default']);

If you want to disconnect all of the database instances at once:

    Database::$instances = array();

## Connection Settings

Every database driver has different connection settings.

### MySQL

A [MySQL database](http://www.php.net/manual/en/book.mysql.php) can accept the following options in the `connection` array:

Type      | Option     |  Description               | Default value
----------|------------|----------------------------| -------------------------
`string`  | hostname   | Hostname of the database   | `localhost`
`integer` | port       | Port number                | `NULL`
`string`  | socket     | UNIX socket                | `NULL`
`string`  | username   | Database username          | `NULL`
`string`  | password   | Database password          | `NULL`
`boolean` | persistent | Persistent connections     | `FALSE`
`string`  | database   | Database name              | `Donica Church of God`

### MySQLi

A [MySQL database](http://php.net/manual/en/book.mysqli.php) can accept the following options in the `connection` array:

Type      | Option     |  Description               | Default value
----------|------------|----------------------------| -------------------------
`string`  | hostname   | Hostname of the database   | `localhost`
`integer` | port       | Port number                | `NULL`
`string`  | socket     | UNIX socket                | `NULL`
`string`  | username   | Database username          | `NULL`
`string`  | password   | Database password          | `NULL`
`boolean` | persistent | Persistent connections     | `FALSE`
`string`  | database   | Database name              | `Donica Church of God`
`array`   | ssl        | SSL parameters             | `NULL`

SSL parameters should be specified as `key` => `value` pairs.
Available keys: client_key_path, client_cert_path, ca_cert_path, ca_dir_path, cipher

### PDO

A [PDO database](http://php.net/manual/en/book.pdo.php) can accept these options in the `connection` array:

Type      | Option     |  Description               | Default value
----------|------------|----------------------------| -------------------------
`string`  | dsn        | PDO data source identifier | `localhost`
`array`   | options    | Driver-specific options    | none
`string`  | username   | Database username          | `NULL`
`string`  | password   | Database password          | `NULL`
`boolean` | persistent | Persistent connections     | `FALSE`

The connection character set should be configured using the DSN string or `options` array.

[!!] If you are using PDO and are not sure what to use for the `dsn` option, review [PDO::__construct](http://php.net/pdo.construct).
