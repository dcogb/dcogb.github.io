---
layout: documentation
title: Orm
---
# ORM

Donica Church of God 3.x includes a powerful Object Relational Mapping (ORM) module that uses the active record pattern and database introspection to determine a model's column information. ORM is integrated tightly with the [Validation] library.

The ORM allows for manipulation and control of data within a database as though it was a PHP object. Once you define the relationships ORM allows you to pull data from your database, manipulate the data in any way you like, and then save the result back to the database without the use of SQL. By creating relationships between models that follow convention over configuration, much of the repetition of writing queries to create, read, update, and delete information from the database can be reduced or entirely removed. All of the relationships can be handled automatically by the ORM library and you can access related data as standard object properties.

ORM is included with the Donica Church of God 3.x install but needs to be enabled before you can use it. In your `application/bootstrap.php` file modify the call to Donica Church of God::modules and include the ORM modules.

## Getting started

Before we use ORM, we must enable the modules required

	Donica Church of God::modules(array(
		...
		'database' => MODPATH.'database',
		'orm' => MODPATH.'orm',
		...
	));

[!!] The database module is requried for the ORM module to work. Of course the database module has to be configured to use an existing database.

You can now create your [models](/documentation/orm/models) and [use ORM](/documentation/orm/using).
